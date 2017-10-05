---
title: Het gebruik van Azure diagnostics in virtuele Machines | Microsoft Docs
description: Met behulp van Azure diagnostics voor het verzamelen van gegevens van virtuele Machines van Azure voor foutopsporing, prestaties, bewaking, analyse van het netwerkverkeer en meer meten.
services: virtual-machines
documentationcenter: .net
author: davidmu1
manager: 
editor: 
ms.assetid: dfaabc7a-23e7-4af0-8369-f504d2915b3d
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2016
ms.author: davidmu
ms.openlocfilehash: 8ff6b9825212359617b748aba1c78ed789b130dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a>Diagnostische gegevens in Azure Virtual Machines inschakelen
Zie [overzicht van Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) voor de achtergrond op Azure Diagnostics.

## <a name="how-to-enable-diagnostics-in-a-virtual-machine"></a>Diagnostische gegevens in een virtuele Machine inschakelen
Deze doorloop wordt beschreven hoe extern diagnostische gegevens naar een virtuele machine van Azure installeren vanaf een ontwikkelingscomputer. U leert ook hoe voor het implementeren van een toepassing die wordt uitgevoerd op deze virtuele machine van Azure en verzendt met behulp van de .NET-telemetriegegevens [EventSource klasse][EventSource Class]. Azure Diagnostics wordt gebruikt voor het verzamelen van de Telemetrie en opslaan in een Azure storage-account.

### <a name="pre-requisites"></a>Vereisten
Deze doorloop wordt ervan uitgegaan dat u hebt een Azure-abonnement en Visual Studio 2017 gebruikt met de Azure SDK. Als u niet een Azure-abonnement hebt, kunt u zich aanmelden voor de [gratis proefversie][Free Trial]. Zorg ervoor dat u [installeren en configureren van Azure PowerShell versie 0.8.7 of hoger][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-virtual-machine"></a>Stap 1: Een virtuele Machine maken
1. Start Visual Studio 2017 op uw ontwikkelcomputer.
2. In de Visual Studio **Server Explorer** Vouw **Azure**, met de rechtermuisknop op **virtuele Machines** Selecteer **virtuele Machine maken**.
3. Selecteer uw Azure-abonnement in de **Kies een abonnement** dialoogvenster en klik op **volgende**.
4. Selecteer **Windows Server 2012 R2 Datacenter, juni 2017** in de **selecteert u de installatiekopie van een virtuele Machine** dialoogvenster en klik op **volgende**.
5. In de **basisinstellingen van de virtuele Machine**, de naam van virtuele machine 'wadexample' ingesteld. Stel uw gebruikersnaam en wachtwoord en klik op **volgende**.
6. In de **Cloud Service-instellingen** dialoogvenster Maak een nieuwe cloudservice met de naam 'wadexampleVM'. Maken van een nieuw opslagaccount met de naam 'wadexample' en klik op **volgende**.
7. Klik op **Create**.

### <a name="step-2-create-your-application"></a>Stap 2: Uw toepassing maken
1. Start Visual Studio 2017 op uw ontwikkelcomputer.
2. Maak een nieuwe Visual C#-consoletoepassing die gericht is op .NET Framework 4.5. Noem het project 'WadExampleVM'.

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. Vervang de inhoud van Program.cs met de volgende code. De klasse **SampleEventSourceWriter** implementeert vier logboekregistratiemethoden: **SendEnums**, **MessageMethod**, **SetOther** en **HighFreq**. De eerste parameter voor de WriteEvent-methode definieert de ID voor de betreffende gebeurtenis. De methode Run implementeert een oneindige lus die voor elk van de logboekregistratiemethoden geïmplementeerd aanroept in de **SampleEventSourceWriter** klasse elke 10 seconden.

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums to int for efficient logging.
         public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
         public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
         public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }
       }

       enum MyColor {
         Red,
         Blue,
         Green
       }

       [Flags]
       enum MyFlags {
         Flag1 = 1,
         Flag2 = 2,
         Flag3 = 4
       }

       class Program
       {
         static void Main(string[] args) {
         Trace.TraceInformation("My application entry point called");

         int value = 0;

         while (true) {
             Thread.Sleep(10000);
             Trace.TraceInformation("Working");

             // Emit several events every time we go through the loop
             for (int i = 0; i < 6; i++) {
                 SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
             }

             for (int i = 0; i < 3; i++) {
                 SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                 SampleEventSourceWriter.Log.SetOther(true, 123456789);
             }

             if (value == int.MaxValue) value = 0;
             SampleEventSourceWriter.Log.HighFreq(value++);
         }

        }
      }
     }
     ```
4. Sla het bestand en selecteer **Build Solution** van de **bouwen** menu voor het bouwen van uw code.

### <a name="step-3-deploy-your-application"></a>Stap 3: Uw toepassing implementeren
1. Met de rechtermuisknop op de **WadExampleVM** project in **Solution Explorer** en kies **map in Verkenner openen**.
2. Navigeer naar de *bin\Debug* map en kopieer alle bestanden (WadExampleVM.*)
3. In **Server Explorer** met de rechtermuisknop op de virtuele machine en kies **verbinding maken met behulp van extern bureaublad**.
4. Maak een map met de naam WadExampleVM en uw toepassing naar de map bestanden plakken eenmaal zijn verbonden met de virtuele machine.
5. Start de toepassing WadExampleVM.exe. Hier ziet u een lege consolevenster.

### <a name="step-4-create-your-diagnostics-configuration-and-install-the-extension"></a>Stap 4: De configuratie van diagnostische gegevens maakt en de uitbreiding te installeren
1. De schemadefinitie van de openbare configuratie voor bestand naar uw ontwikkelcomputer downloaden door het uitvoeren van de volgende PowerShell-opdracht:

     (Get-AzureServiceAvailableExtension - Extensienaam 'PaaSDiagnostics' - ProviderNamespace 'Microsoft.Azure.Diagnostics'). PublicConfigurationSchema | Out-File-codering utf8 - FilePath 'WadConfig.xsd'
2. Open een nieuw XML-bestand in Visual Studio, hetzij in een project dat u al hebt geopend of in een Visual Studio-instantie met geen openstaande projecten. Selecteer in Visual Studio **toevoegen** -> **Nieuw Item...** -> **Visual C# items** -> **gegevens** -> **XML-bestand**. Noem het bestand 'WadExample.xml'
3. De WadConfig.xsd koppelen aan het configuratiebestand. Zorg ervoor dat de editor voor WadExample.xml het actieve venster. Druk op **F4** openen de **eigenschappen** venster. Klik op de **schema's** eigenschap in de **eigenschappen** venster. Klik op de **...** in de **schema's** eigenschap. Klik op de knop **Toevoegen...** knop en navigeer naar de locatie waar u het XSD-bestand hebt opgeslagen en selecteert u het bestand WadConfig.xsd. Klik op **OK**.
4. De inhoud van het configuratiebestand WadExample.xml vervangen door de volgende XML en sla het bestand. Dit configuratiebestand definieert een aantal prestatiemeteritems voor het verzamelen van: één voor CPU-gebruik en één voor geheugengebruik. De configuratie definieert de vier gebeurtenissen die overeenkomt met de methoden in de klasse SampleEventSourceWriter.

```
        <?xml version="1.0" encoding="utf-8"?>
        <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
              <WadCfg>
                <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
                  <PerformanceCounters scheduledTransferPeriod="PT1M">
                    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
                    <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
                      </PerformanceCounters>
                      <EtwProviders>
                        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
                              <Event id="1" eventDestination="EnumsTable"/>
                              <Event id="2" eventDestination="MessageTable"/>
                              <Event id="3" eventDestination="SetOtherTable"/>
                              <Event id="4" eventDestination="HighFreqTable"/>
                              <DefaultEvents eventDestination="DefaultTable" />
                        </EtwEventSourceProviderConfiguration>
                      </EtwProviders>
                </DiagnosticMonitorConfiguration>
              </WadCfg>
        </PublicConfig>
```

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a>Stap 5: Extern installeren diagnostische gegevens op uw virtuele Machine van Azure
De PowerShell-cmdlets voor het beheren van diagnostische gegevens op een virtuele machine zijn: Set-AzureVMDiagnosticsExtension en Get-AzureVMDiagnosticsExtension verwijderen AzureVMDiagnosticsExtension.

1. Open op uw computer developer Azure PowerShell.
2. Voer het script op afstand te installeren diagnostische gegevens op de virtuele machine (vervangen `<user>` door uw gebruikersnaam van de directory. Vervang `<StorageAccountKey>` door de sleutel van het opslagaccount voor uw opslagaccount wadexamplevm):
```
     $storage_name = "wadexamplevm"
     $key = "<StorageAccountKey>"
     $config_path="c:\users\<user>\documents\visual studio 2017\Projects\WadExampleVM\WadExampleVM\WadExample.xml"
     $service_name="wadexamplevm"
     $vm_name="WadExample"
     $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
     $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name
     $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.*" -VM $VM1 -StorageContext $storageContext
     $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM
```
### <a name="step-6-look-at-your-telemetry-data"></a>Stap 6: Bekijk de telemetrische gegevens
In de Visual Studio **Server Explorer** gaat u naar het opslagaccount wadexample. Nadat de virtuele machine actief is geweest ongeveer 5 minuten ziet u de tabellen **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** en **WADSetOtherTable**. Dubbelklik op een van de tabellen om weer te geven van de telemetrie die is verzameld.

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a>Schema van het configuratiebestand
Het configuratiebestand van de diagnostische gegevens definieert waarden die worden gebruikt voor het initialiseren van diagnostische configuratie-instellingen wanneer de diagnostics-agent wordt gestart. Zie de [nieuwste schemaverwijzing](https://msdn.microsoft.com/library/azure/mt634524.aspx) voor geldige waarden en voorbeelden.

## <a name="troubleshooting"></a>Problemen oplossen
Zie [probleemoplossing Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
[Zie een lijst met virtuele machine verwante artikelen van Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) wijzigen van de gegevens die u verzamelt, oplossen van problemen of meer informatie over diagnostische gegevens over het algemeen.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
