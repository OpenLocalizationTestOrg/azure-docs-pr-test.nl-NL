---
title: aaaConfigure Azure Diagnostics toosend gegevens tooApplication Insights | Microsoft Docs
description: Hello Azure Diagnostics openbare configuratie toosend gegevens tooApplication Insights bijwerken.
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 7c36f29da8fdc12fa58c17458348a311b900b0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a>Cloud-Service, virtuele Machine of Service Fabric diagnostische gegevens tooApplication Insights verzenden
Cloudservices, virtuele Machines, virtuele-Machineschaalsets en Service Fabric alle hello Azure Diagnostics extensie toocollect gegevens gebruikt.  Azure diagnostics verzendt gegevens tooAzure Storage-tabellen.  U kunt echter ook alle pipe of een subset van Hallo tooother gegevenslocaties met behulp van Azure Diagnostics extensie 1.5 of hoger.

Dit artikel wordt beschreven hoe toosend gegevens van Azure Diagnostics extensie tooApplication Insights Hallo.

## <a name="diagnostics-configuration-explained"></a>Configuratie van diagnostische uitgelegd
Hello Azure diagnostics extensie 1.5 geïntroduceerd put zijn extra locaties waar u diagnostische gegevens kunt verzenden.

Van de voorbeeldconfiguratie van een sink voor Application Insights:

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- Hallo **Sink** *naam* kenmerk is een tekenreekswaarde die een unieke identificatie van Hallo sink.

- Hallo **ApplicationInsights** element geeft instrumentatiesleutel Hallo Application insights-resource waar hello Azure diagnostics-gegevens worden verzonden.
    - Als u een bestaande Application Insights-resource niet hebt, raadpleegt u [Maak een nieuwe Application Insights-resource](../application-insights/app-insights-create-new-resource.md) voor meer informatie over het maken van een bron en het Hallo-instrumentatiesleutel ophalen.
    - Als u een Cloudservice met de Azure SDK 2.8 of hoger ontwikkelt, wordt deze instrumentatiesleutel automatisch ingevuld. Hallo-waarde is gebaseerd op Hallo **APPINSIGHTS_INSTRUMENTATIONKEY** service van configuratie-instelling wanneer verpakking Hallo Cloud Services-project. Zie [gebruik Application Insights met Azure Diagnostics tootroubleshoot Cloudservice problemen](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).

- Hallo **kanalen** element bevat een of meer **kanaal** elementen.
    - Hallo *naam* kenmerk unieke toothat kanaal verwijst.
    - Hallo *loglevel* kenmerk kunt u het Hallo-registratieniveau dat kanaal Hallo kunt opgeven. Hallo beschikbaar logboekniveaus in volgorde van de meeste tooleast gegevens zijn:
        - Uitgebreide
        - Informatie
        - Waarschuwing
        - Fout
        - Kritieke

Een kanaal fungeert als een filter, en kunt u tooselect specifieke logboek niveaus toosend toohello doel sink. U kan bijvoorbeeld uitgebreide logboeken verzamelen en ze toostorage verzenden, maar alleen fouten toohello sink verzenden.

Hallo volgende afbeelding ziet u deze relatie.

![De openbare configuratie voor diagnostische gegevens](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

Hallo volgende afbeelding wordt samengevat configuratiewaarden Hallo en hoe ze werken. U kunt meerdere put opnemen in de configuratie op verschillende niveaus in de hiërarchie Hallo Hallo. Hallo sink op het hoogste niveau Hallo fungeert als een algemene instelling en hello een opgegeven op afzonderlijke Hallo element fungeert als een onderdrukking toothat globale instelling.

![Diagnostische gegevens Sinks configuratie met Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a>Volledige sink configuratievoorbeeld
Hier volgt een compleet voorbeeld van de openbare configuratie Hallo-bestand
1. alle fouten tooApplication Insights verzendt (opgegeven op Hallo **DiagnosticMonitorConfiguration** knooppunt)
2. verzendt ook uitgebreide niveau logboeken voor Hallo toepassingslogboeken (opgegeven op Hallo **logboeken** knooppunt).

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent toothis channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent toothis channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent toothis channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
                    "sampleRate": "PT3M"
                }
            ]
        },
        "WindowsEventLog": {
            "scheduledTransferPeriod": "PT1M",
            "DataSource": [
                {
                    "name": "Application!*"
                }
            ]
        },
        "Logs": {
            "scheduledTransferPeriod": "PT1M",
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent toothis channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
Hallo volgende regels hebben in de vorige configuratie hello, Hallo betekenis te volgen:

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a>Alle Hallo-gegevens worden verzameld door Azure diagnostics verzenden

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a>Alleen fout logboeken toohello Application Insights sink verzenden

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a>Uitgebreide toepassingslogboeken tooApplication Insights verzenden

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a>Beperkingen

- **Kanalen zich alleen aanmelden type niet prestatiemeteritems als.** Als u een kanaal met een element van de teller prestaties opgeeft, wordt dit genegeerd.
- **Hallo logboekniveau voor een kanaal kan Hallo logboekniveau voor wat wordt er door Azure diagnostics wordt verzameld niet overschrijden.** U kan bijvoorbeeld fouten toepassingslogboek in Logboeken-element Hallo verzamelen en probeer toosend uitgebreide logboeken toohello toepassing inzicht sink. Hallo *scheduledTransferLogLevelFilter* kenmerk moet altijd gelijk verzamelen of meer logboeken dan Hallo Hiermee meldt u zich probeert toosend tooa sink.
- **U kunt geen blob-gegevens verzameld door Azure diagnostics extensie tooApplication Insights verzenden.** Bijvoorbeeld, iets opgegeven onder Hallo *mappen* knooppunt. TooApplication Insights wordt verzonden door voor crashdumps Hallo werkelijke crashdump tooblob opslag wordt verzonden en alleen een melding dat crashdump Hallo is gegenereerd.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[uw Azure diagnostics-gegevens weergeven](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.
* Gebruik [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello Azure diagnostics-extensie voor uw toepassing.
* Gebruik [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello Azure diagnostics-extensie voor uw toepassing
