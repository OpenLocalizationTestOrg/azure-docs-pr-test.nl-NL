---
title: aaaHow toouse met Cloudservices Azure diagnostics (.NET) | Microsoft Docs
description: Met behulp van Azure diagnostics toogather cloud gegevens van Azure Services voor foutopsporing, prestaties, bewaking, analyse van het netwerkverkeer en meer meten.
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: robb
ms.openlocfilehash: 1525eac1e85955d8f05aa21a9805e0a80d0e4bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a>Inschakelen van Azure Diagnostics in Azure-Cloudservices
Zie [overzicht van Azure Diagnostics](../azure-diagnostics.md) voor de achtergrond op Azure Diagnostics.

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a>Hoe diagnostische gegevens in een Werkrol tooEnable
Dit scenario beschrijft hoe een Azure-werkrol die telemetrie gegevens met verzendt tooimplement Hallo EventSource .NET-klasse. Azure Diagnostics is gebruikte toocollect hello telemetriegegevens en opslaan in een Azure storage-account. Bij het maken van een werkrol kunt Visual Studio automatisch de Diagnostics 1.0 als onderdeel van de oplossing Hallo in Azure SDK voor .NET 2.4 en eerdere versies. Hallo beschrijven volgende instructies Hallo-proces voor het Hallo-werkrol, Hallo oplossing Diagnostics 1.0 uitschakelen en het implementeren van diagnostische gegevens 1.2 of 1.3 tooyour werkrol maken.

### <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u hebt een Azure-abonnement en gebruik van Visual Studio Hello Azure SDK. Als u niet een Azure-abonnement hebt, kunt u zich aanmeldt voor Hallo [gratis proefversie][Free Trial]. Zorg ervoor dat te[installeren en configureren van Azure PowerShell versie 0.8.7 of hoger][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-worker-role"></a>Stap 1: Een Werkrol maken
1. Start **Visual Studio**.
2. Maak een **Azure Cloud Service** project uit Hallo **Cloud** sjabloon die gericht is op .NET Framework 4.5.  Naam Hallo 'WadExample' project en klik op Ok.
3. Selecteer **Werkrol** en klik op Ok. Hallo-project wordt gemaakt.
4. In **Solution Explorer**, dubbelklikt u op Hallo **WorkerRole1** eigenschappenbestand.
5. In Hallo **configuratie** tabblad un selectievakje **diagnostische gegevens inschakelen** toodisable Diagnostics 1.0 (Azure SDK 2.4 en eerder).
6. Uw tooverify oplossing bouwen die u hebt geen fouten.

### <a name="step-2-instrument-your-code"></a>Stap 2: Uw code softwareontwikkelaars
Hallo-inhoud van WorkerRole.cs vervangen door Hallo code te volgen. klasse SampleEventSourceWriter, zijn overgenomen van Hallo Hallo [EventSource klasse][EventSource Class], implementeert vier logboekregistratiemethoden: **SendEnums**, **MessageMethod** , **SetOther** en **HighFreq**. eerste parameter toohello Hallo **WriteEvent** methode Hallo-ID voor de betreffende gebeurtenis Hallo definieert. Hallo Run-methode implementeert een oneindige lus die elk Hallo logboekregistratiemethoden die worden geïmplementeerd in Hallo aanroept **SampleEventSourceWriter** klasse elke 10 seconden.

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums tooint for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through hello loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set hello maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a>Stap 3: Uw Werkrol implementeren

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. Uw rol worker tooAzure uit vanuit Visual Studio implementeren door het selecteren van Hallo **WadExample** -project in Solution Explorer Hallo vervolgens **publiceren** van Hallo **bouwen** menu.
2. Kies uw abonnement.
3. In Hallo **Microsoft Azure Publish Settings** dialoogvenster Selecteer **nieuwe maken...** .
4. In Hallo **Cloudservice maken en Storage-Account** dialoogvenster, voer een **naam** (bijvoorbeeld ' WadExample') en selecteer een regio of affiniteitsgroep.
5. Set Hallo **omgeving** te**fasering**.
6. Wijzigen van een andere **instellingen** als in de betreffende en klikt u op **publiceren**.
7. Wanneer implementatie is voltooid, controleert u of in hello Azure-portal uw cloudservice is in een **met** status.

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a>Stap 4: Maken van uw configuratiebestand diagnostische gegevens en Hallo uitbreiding installeren
1. Hallo openbare configuratie bestand schemadefinitie downloaden door het uitvoeren van Hallo volgende PowerShell-opdracht:

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. Toevoegen van een XML-bestand tooyour **WorkerRole1** project door met de rechtermuisknop op Hallo **WorkerRole1** project en selecteer **toevoegen** -> **Nieuw Item...** -> **Visual C# items** -> **gegevens** -> **XML-bestand**. Hallo bestandsnaam 'WadExample.xml'.

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. Hallo WadConfig.xsd koppelen aan Hallo-configuratiebestand. Zorg ervoor dat Hallo WadExample.xml editorvenster Hallo actieve venster. Druk op **F4** tooopen hello **eigenschappen** venster. Klik op Hallo **schema's** eigenschap in Hallo **eigenschappen** venster. Klik op Hallo **...** in Hallo **schema's** eigenschap. Klik op Hallo **toevoegen...** knop en navigeer toohello locatie waar u Hallo XSD-bestand en selecteer Hallo bestand WadConfig.xsd opgeslagen. Klik op **OK**.

4. Hallo-inhoud van Hallo WadExample.xml configuratiebestand vervangen Hello na XML en sla het Hallo-bestand. Dit configuratiebestand definieert een aantal prestaties tellers toocollect: één voor CPU-gebruik en één voor geheugengebruik. Vervolgens definieert Hallo configuratie Hallo vier gebeurtenissen toohello methoden in Hallo SampleEventSourceWriter klasse overeenkomt.

```xml
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

### <a name="step-5-install-diagnostics-on-your-worker-role"></a>Stap 5: Diagnostische gegevens op uw Werkrol installeren
Hallo PowerShell-cmdlets voor het beheren van diagnostische gegevens op een web- of worker-rol zijn: Set-AzureServiceDiagnosticsExtension en Get-AzureServiceDiagnosticsExtension verwijderen AzureServiceDiagnosticsExtension.

1. Open Azure PowerShell.
2. Hallo script tooinstall diagnostische gegevens niet uitvoeren op uw werkrol (Vervang *StorageAccountKey* met Hallo-toegangssleutel voor uw opslagaccount wadexample en *config_path* met Hallo pad toohello *WadExample.xml* bestand):

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a>Stap 6: Bekijk de telemetrische gegevens
In Visual Studio Hallo **Server Explorer**, navigeer toohello wadexample storage-account. Nadat het Hallo-cloudservice is ongeveer vijf (5) minuten uitgevoerd, ziet u Hallo tabellen **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** en **WADSetOtherTable**. Dubbelklik op een Hallo tabellen tooview Hallo telemetrie die is verzameld.

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a>Schema van het configuratiebestand
Hallo Diagnostics configuratiebestand definieert waarden die gebruikt tooinitialize diagnostische configuratie-instellingen zijn wanneer Hallo diagnostics agent wordt gestart. Zie Hallo [nieuwste schemaverwijzing](https://msdn.microsoft.com/library/azure/mt634524.aspx) voor geldige waarden en voorbeelden.

## <a name="troubleshooting"></a>Problemen oplossen
Als u problemen ondervindt, raadpleegt u [probleemoplossing Azure Diagnostics](../azure-diagnostics-troubleshooting.md) voor meer informatie over bekende problemen.

## <a name="next-steps"></a>Volgende stappen
[Een overzicht van verwante Azure virtuele machines diagnostische artikelen](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange Hallo gegevens verzamelt, oplossen van problemen of meer informatie over diagnostische gegevens over het algemeen.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
