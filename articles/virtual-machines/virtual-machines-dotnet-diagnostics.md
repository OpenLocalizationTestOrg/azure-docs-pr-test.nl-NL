---
title: aaaHow toouse Azure diagnostics in virtuele Machines | Microsoft Docs
description: Met behulp van Azure diagnostics toogather-gegevens van virtuele Machines van Azure voor foutopsporing, prestaties, bewaking, analyse van het netwerkverkeer en meer meten.
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
ms.openlocfilehash: 54cdfd30d7bbbb71af449826e90234faf5ecdf44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a>Diagnostische gegevens in Azure Virtual Machines inschakelen
Zie [overzicht van Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) voor de achtergrond op Azure Diagnostics.

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a>Hoe tooEnable diagnostische gegevens in een virtuele Machine
Deze doorloop wordt beschreven hoe tooremotely Diagnostics tooan virtuele machine van Azure installeren vanaf een ontwikkelcomputer. U leert ook hoe een toepassing die wordt uitgevoerd op deze virtuele machine van Azure en verzendt telemetrie gegevens met tooimplement .NET Hallo [EventSource klasse][EventSource Class]. Azure Diagnostics is gebruikte toocollect Hallo Telemetrie en opslaan in een Azure storage-account.

### <a name="pre-requisites"></a>Vereisten
Deze doorloop wordt ervan uitgegaan dat u hebt een Azure-abonnement en Visual Studio 2017 Hello Azure SDK. Als u niet een Azure-abonnement hebt, kunt u zich aanmeldt voor Hallo [gratis proefversie][Free Trial]. Zorg ervoor dat te[installeren en configureren van Azure PowerShell versie 0.8.7 of hoger][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-virtual-machine"></a>Stap 1: Een virtuele Machine maken
1. Start Visual Studio 2017 op uw ontwikkelcomputer.
2. In Visual Studio Hallo **Server Explorer** Vouw **Azure**, met de rechtermuisknop op **virtuele Machines** Selecteer **virtuele Machine maken**.
3. Selecteer uw Azure-abonnement in Hallo **Kies een abonnement** dialoogvenster en klik op **volgende**.
4. Selecteer **Windows Server 2012 R2 Datacenter, juni 2017** in Hallo **selecteert u de installatiekopie van een virtuele Machine** dialoogvenster en klik op **volgende**.
5. In Hallo **basisinstellingen van de virtuele Machine**, stel de naam van de virtuele machine Hallo te 'wadexample'. Stel uw gebruikersnaam en wachtwoord en klik op **volgende**.
6. In Hallo **Cloud Service-instellingen** dialoogvenster Maak een nieuwe cloudservice met de naam 'wadexampleVM'. Maken van een nieuw opslagaccount met de naam 'wadexample' en klik op **volgende**.
7. Klik op **Create**.

### <a name="step-2-create-your-application"></a>Stap 2: Uw toepassing maken
1. Start Visual Studio 2017 op uw ontwikkelcomputer.
2. Maak een nieuwe Visual C#-consoletoepassing die gericht is op .NET Framework 4.5. Naam Hallo project 'WadExampleVM'.

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. Hallo inhoud van Program.cs met de volgende code Hallo vervangen. Hallo klasse **SampleEventSourceWriter** implementeert vier logboekregistratiemethoden: **SendEnums**, **MessageMethod**, **SetOther** en  **HighFreq**. Hallo eerste parameter toohello WriteEvent-methode definieert Hallo-ID voor de betreffende gebeurtenis Hallo. Hallo Run-methode implementeert een oneindige lus die elk Hallo logboekregistratiemethoden die worden geïmplementeerd in Hallo aanroept **SampleEventSourceWriter** klasse elke 10 seconden.

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums tooint for efficient logging.
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

             // Emit several events every time we go through hello loop
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
4. Hallo-bestand opslaan en selecteer **Build Solution** van Hallo **bouwen** menu toobuild uw code.

### <a name="step-3-deploy-your-application"></a>Stap 3: Uw toepassing implementeren
1. Met de rechtermuisknop op Hallo **WadExampleVM** project in **Solution Explorer** en kies **map in Verkenner openen**.
2. Navigeer toohello *bin\Debug* map en kopieer alle Hallo-bestanden (WadExampleVM.*)
3. In **Server Explorer** met de rechtermuisknop op Hallo virtuele machine en kies **verbinding maken met behulp van extern bureaublad**.
4. Eenmaal zijn verbonden toohello VM maakt u een map met de naam WadExampleVM en plak de toepassingsbestanden van uw in Hallo map.
5. Hallo toepassing WadExampleVM.exe starten. Hier ziet u een lege consolevenster.

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a>Stap 4: Maken van uw configuratie van diagnostische en Hallo uitbreiding installeren
1. Hallo openbare configuratie bestand schema definitie tooyour ontwikkelingscomputer door het uitvoeren van de volgende PowerShell-opdracht Hallo downloaden:

     (Get-AzureServiceAvailableExtension - Extensienaam 'PaaSDiagnostics' - ProviderNamespace 'Microsoft.Azure.Diagnostics'). PublicConfigurationSchema | Out-File-codering utf8 - FilePath 'WadConfig.xsd'
2. Open een nieuw XML-bestand in Visual Studio, hetzij in een project dat u al hebt geopend of in een Visual Studio-instantie met geen openstaande projecten. Selecteer in Visual Studio **toevoegen** -> **Nieuw Item...** -> **Visual C# items** -> **gegevens** -> **XML-bestand**. Bestand met de Hallo 'WadExample.xml'
3. Hallo WadConfig.xsd koppelen aan Hallo-configuratiebestand. Zorg ervoor dat Hallo WadExample.xml editorvenster Hallo actieve venster. Druk op **F4** tooopen hello **eigenschappen** venster. Klik op Hallo **schema's** eigenschap in Hallo **eigenschappen** venster. Klik op Hallo **...** in Hallo **schema's** eigenschap. Klik op Hallo **toevoegen...** knop en navigeer toohello locatie waar u Hallo XSD-bestand en selecteer Hallo bestand WadConfig.xsd opgeslagen. Klik op **OK**.
4. Hallo-inhoud van Hallo WadExample.xml configuratiebestand vervangen Hello na XML en sla het Hallo-bestand. Dit configuratiebestand definieert een aantal prestaties tellers toocollect: één voor CPU-gebruik en één voor geheugengebruik. Vervolgens definieert Hallo configuratie Hallo vier gebeurtenissen toohello methoden in Hallo SampleEventSourceWriter klasse overeenkomt.

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
Hallo PowerShell-cmdlets voor het beheren van diagnostische gegevens op een virtuele machine zijn: Set-AzureVMDiagnosticsExtension en Get-AzureVMDiagnosticsExtension verwijderen AzureVMDiagnosticsExtension.

1. Open op uw computer developer Azure PowerShell.
2. Hallo script tooremotely installeren diagnostische gegevens niet uitvoeren op uw virtuele machine (vervangen `<user>` door uw gebruikersnaam van de directory. Vervang `<StorageAccountKey>` met Hallo-toegangssleutel voor uw opslagaccount wadexamplevm):
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
In Visual Studio Hallo **Server Explorer** navigeren toohello wadexample storage-account. Na het Hallo-virtuele machine actief is geweest ongeveer 5 minuten ziet u Hallo tabellen **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** en **WADSetOtherTable**. Dubbelklik op een van de Hallo tabellen tooview Hallo telemetrie die is verzameld.

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a>Schema van het configuratiebestand
Hallo Diagnostics configuratiebestand definieert waarden die gebruikt tooinitialize diagnostische configuratie-instellingen zijn wanneer Hallo diagnostics agent wordt gestart. Zie Hallo [nieuwste schemaverwijzing](https://msdn.microsoft.com/library/azure/mt634524.aspx) voor geldige waarden en voorbeelden.

## <a name="troubleshooting"></a>Problemen oplossen
Zie [probleemoplossing Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
[Zie een lijst met virtuele machine verwante artikelen van Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange Hallo gegevens verzamelt, oplossen van problemen of meer informatie over diagnostische gegevens over het algemeen.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
