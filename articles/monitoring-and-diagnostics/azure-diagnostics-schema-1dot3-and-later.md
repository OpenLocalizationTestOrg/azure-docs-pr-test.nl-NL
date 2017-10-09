---
title: aaaAzure Diagnostics 1.3 en hoger configuratieschema uitbreiding | Microsoft Docs
description: Schemaversie 1.3 en hoger Azure diagnostische gegevens verzonden als onderdeel van Hallo Microsoft Azure SDK 2,4 en hoger.
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: robb
ms.openlocfilehash: bd15d3a79ea818fcb3235854717e58d5da36518e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a>Azure Diagnostics 1.3 en hoger configuratieschema
> [!NOTE]
> Hello Azure Diagnostics-extensie is Hallo onderdeel gebruikt toocollect prestatiemeteritems en andere statistieken van:
> - Azure Virtual Machines 
> - Schaalsets voor virtuele machines
> - Service Fabric 
> - Cloudservices 
> - Netwerkbeveiligingsgroepen
> 
> Deze pagina is alleen relevant als u een van deze services.

Deze pagina is ongeldig voor versies 1.3 en nieuwere (Azure SDK 2,4 en hoger). Nieuwere configuratiesecties zijn opmerkingen tooshow in welke versie ze zijn toegevoegd.  

Hallo-configuratiebestand hier beschreven is gebruikte tooset diagnostische configuratie-instellingen wanneer Hallo diagnostics wordt gestart bewaken.  

Hallo-uitbreiding wordt gebruikt in combinatie met andere Microsoft-producten voor diagnostische gegevens zoals Azure Monitor, Application Insights en Log Analytics.



Hallo openbare configuratie bestand schemadefinitie downloaden door het uitvoeren van Hallo volgende PowerShell-opdracht:  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

Zie voor meer informatie over het gebruik van Azure Diagnostics [Azure-extensie voor diagnostische gegevens](azure-diagnostics.md).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Voorbeeld van een configuratiebestand voor Hallo diagnostische gegevens  
 Hallo volgende voorbeeld ziet u een configuratiebestand typische diagnostische gegevens:  

```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DiagnosticsConfiguration  xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">   
  <PublicConfig>  
    <WadCfg>  
      <DiagnosticMonitorConfiguration overallQuotaInMB="10000">  

        <PerformanceCounters scheduledTransferPeriod="PT1M">  
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />  
        </PerformanceCounters>  

        <Directories scheduledTransferPeriod="PT5M">  
          <IISLogs containerName="iislogs" />  
          <FailedRequestLogs containerName="iisfailed" />  

          <DataSources>  
            <DirectoryConfiguration containerName="mynewprocess">  
              <Absolute path="C:\MyNewProcess" expandEnvironment="false" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="badapp">  
              <Absolute path="%SYSTEMDRIVE%\BadApp" expandEnvironment="true" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="goodapp">  
              <LocalResource name="Skippy" relativePath="..\PeanutButter"/>  
            </DirectoryConfiguration>  
          </DataSources>  

        </Directories>  

        <EtwProviders>  
          <EtwEventSourceProviderConfiguration   
                       provider="MyProviderClass"   
                       scheduledTransferPeriod="PT5M">  
            <Event id="0"/>  
            <Event id="1" eventDestination="errorTable"/>  
            <DefaultEvents />  
          </EtwEventSourceProviderConfiguration>  
          <EtwManifestProviderConfiguration provider="5974b00b-84c2-44bc-9e58-3a2451b4e3ad" scheduledTransferLogLevelFilter="Information" scheduledTransferPeriod="PT2M">  
            <Event id="0"/>  
            <DefaultEvents eventDestination="defaultTable"/>  
          </EtwManifestProviderConfiguration>  
        </EtwProviders>  

        <WindowsEventLog scheduledTransferPeriod="PT5M">  
          <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>  
          <DataSource name="System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]" />  
          <DataSource name="System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]" />  
        </WindowsEventLog>  

        <Logs  bufferQuotaInMB="1024"   
             scheduledTransferPeriod="PT1M"   
             scheduledTransferLogLevelFilter="Verbose"   
             sinks="ApplicationInsights.AppLogs"/>  <!-- sinks attribute added in 1.5 -->  

        <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
          <CrashDumpConfiguration processName="mynewprocess.exe" />  
          <CrashDumpConfiguration processName="badapp.exe"/>  
        </CrashDumps>  

        <DockerSources> <!-- Added in 1.9 --> 
          <Stats enabled="true" sampleRate="PT1M" scheduledTransferPeriod="PT1M" />
        </DockerSources>

      </DiagnosticMonitorConfiguration>  

      <SinksConfig>   <!-- Added in 1.5 -->  
        <Sink name="ApplicationInsights">   
          <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>   
          <Channels>   
            <Channel logLevel="Error" name="Errors"  />   
            <Channel logLevel="Verbose" name="AppLogs"  />   
          </Channels>   
        </Sink>   
        <Sink name="EventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryEventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryStorageAccount"> <!-- Added in 1.7 -->
          <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" />
        </Sink>
   </SinksConfig>

  </WadCfg>  

  <StorageAccount>diagstorageaccount</StorageAccount>
  <StorageType>TableAndBlob</StorageType> <!-- Added in 1.8 -->  
  </PublicConfig>  

  <PrivateConfig>  <!-- Added in 1.3 -->  
    <StorageAccount name="" key="" endpoint="" sasToken="{sas token}"  />  <!-- sasToken in Private config added in 1.8.1 -->  
    <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
   
    <SecondaryStorageAccounts>
       <StorageAccount name="secondarydiagstorageaccount" key="{base64 encoded key}" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
   
    <SecondaryEventHubs>
       <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
    </SecondaryEventHubs>

  </PrivateConfig>  
  <IsEnabled>true</IsEnabled>  
</DiagnosticsConfiguration>  

```  

JSON-equivalent van Hallo vorige XML-configuratiebestand. 

Hallo PublicConfig en PrivateConfig worden gescheiden omdat in de meeste gevallen voor json-gebruik, de als verschillende variabelen worden doorgegeven. Deze gevallen zijn onder andere Resource Manager-sjablonen, virtuele-machineschaalset PowerShell en Visual Studio. 

```json
"PublicConfig" {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 10000,
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT1M",
                        "unit": "percent"
                    }
                ]
            },
            "Directories": {
                "scheduledTransferPeriod": "PT5M",
                "IISLogs": {
                    "containerName": "iislogs"
                },
                "FailedRequestLogs": {
                    "containerName": "iisfailed"
                },
                "DataSources": [
                    {
                        "containerName": "mynewprocess",
                        "Absolute": {
                            "path": "C:\\MyNewProcess",
                            "expandEnvironment": false
                        }
                    },
                    {
                        "containerName": "badapp",
                        "Absolute": {
                            "path": "%SYSTEMDRIVE%\\BadApp",
                            "expandEnvironment": true
                        }
                    },
                    {
                        "containerName": "goodapp",
                        "LocalResource": {
                            "relativePath": "..\\PeanutButter",
                            "name": "Skippy"
                        }
                    }
                ]
            },
            "EtwProviders": {
                "sinks": "",
                "EtwEventSourceProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT5M",
                        "provider": "MyProviderClass",
                        "Event": [
                            {
                                "id": 0
                            },
                            {
                                "id": 1,
                                "eventDestination": "errorTable"
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ],
                "EtwManifestProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT2M",
                        "scheduledTransferLogLevelFilter": "Information",
                        "provider": "5974b00b-84c2-44bc-9e58-3a2451b4e3ad",
                        "Event": [
                            {
                                "id": 0
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT5M",
                "DataSource": [
                    {
                        "name": "System!*[System[Provider[@Name='Microsoft Antimalware']]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Verbose",
                "sinks": "ApplicationInsights.AppLogs"
            },
            "CrashDumps": {
                "directoryQuotaPercentage": 30,
                "dumpType": "Mini",
                "containerName": "wad-crashdumps",
                "CrashDumpConfiguration": [
                    {
                        "processName": "mynewprocess.exe"
                    },
                    {
                        "processName": "badapp.exe"
                    }
                ]
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
                                "name": "Errors"
                            },
                            {
                                "logLevel": "Verbose",
                                "name": "AppLogs"
                            }
                        ]
                    }
                },
                {
                    "name": "EventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryEventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryStorageAccount",
                    "StorageAccount": {
                        "name": "secondarydiagstorageaccount",
                        "endpoint": "https://core.windows.net"
                    }
                }
            ]
        }
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```json
"PrivateConfig" {
    "storageAccountName": "diagstorageaccount",
    "storageAccountKey": "{base64 encoded key}",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "EventHub": {
        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    },
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "key": "{base64 encoded key}",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    },
    "SecondaryEventHubs": {
        "EventHub": [
            {
                "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                "SharedAccessKeyName": "SendRule",
                "SharedAccessKey": "{base64 encoded key}"
            }
        ]
    }
}

```

## <a name="reading-this-page"></a>Deze pagina lezen  
 Hallo zijn labels te volgen ongeveer in volgorde van Hallo voorgaande voorbeeld.  Als u niet een volledige beschrijving waar u verwacht ziet, zoekpagina Hallo voor Hallo element of kenmerk.  

## <a name="common-attribute-types"></a>Algemene kenmerktypen  
 **scheduledTransferPeriod** kenmerk wordt weergegeven in verschillende elementen. Is het Hallo-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond. Hallo-waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp)


## <a name="diagnosticsconfiguration-element"></a>DiagnosticsConfiguration Element  
 *Structuur: Root - DiagnosticsConfiguration*

In versie 1.3 toegevoegd.  

op het hoogste niveau element Hallo van Hallo diagnostics-configuratiebestand.  

**Kenmerk** xmlns - Hallo XML-naamruimte voor Hallo diagnostics-configuratiebestand is:  
http://schemas.Microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  


|Onderliggende elementen|Beschrijving|  
|--------------------|-----------------|  
|**PublicConfig**|Vereist. Zie de beschrijving ergens anders op deze pagina.|  
|**PrivateConfig**|Optioneel. Zie de beschrijving ergens anders op deze pagina.|  
|**IsEnabled**|Booleaanse waarde. Zie de beschrijving ergens anders op deze pagina.|  

## <a name="publicconfig-element"></a>PublicConfig Element  
 *Structuur: Basis - DiagnosticsConfiguration - PublicConfig*

 Beschrijft de configuratie van de openbare diagnostische Hallo.  

|Onderliggende elementen|Beschrijving|  
|--------------------|-----------------|  
|**WadCfg**|Vereist. Zie de beschrijving ergens anders op deze pagina.|  
|**StorageAccount**|Hallo-naam van hello Azure Storage-account toostore Hallo gegevens in. Kan ook worden opgegeven als parameter bij het uitvoeren van de cmdlet Set-AzureServiceDiagnosticsExtension Hallo.|  
|**StorageType**|Kan *tabel*, *Blob*, of *TableAndBlob*. De tabel is standaard. Wanneer TableAndBlob is gekozen, diagnostische gegevens worden geschreven tweemaal--eenmaal tooeach type.|  
|**LocalResourceDirectory**|Hallo-map op Hallo virtuele machine waar hello Monitoring Agent gebeurtenisgegevens opslaat. Als dat niet wordt is ingesteld, Hallo standaarddirectory gebruikt:<br /><br /> Voor een functie Worker/webservice:`C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> Voor een virtuele Machine:`C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Vereiste kenmerken zijn:<br /><br /> - **pad** - hello directory op Hallo system toobe die wordt gebruikt door Azure Diagnostics.<br /><br /> - **expandEnvironment** -Hiermee wordt bepaald of omgevingsvariabelen in de padnaam Hallo worden uitgevouwen.|  

## <a name="wadcfg-element"></a>WadCFG Element  
 *Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG-*
 
 Identificeert en configureert u Hallo telemetrie gegevens toobe verzameld.  


## <a name="diagnosticmonitorconfiguration-element"></a>DiagnosticMonitorConfiguration Element 
 *Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*

 Vereist 

|Kenmerken|Beschrijving|  
|----------------|-----------------|  
| **overallQuotaInMB** | maximale hoeveelheid lokale schijfruimte die kan worden gebruikt door Hallo Hallo verschillende soorten diagnostische gegevens verzameld door Azure Diagnostics. de standaardinstelling Hallo is 5120 MB.<br />
|**useProxyServer** | Azure Diagnostics toouse Hallo proxyserverinstellingen configureren zoals in de instellingen van Internet Explorer.|  

<br /> <br />

|Onderliggende elementen|Beschrijving|  
|--------------------|-----------------|  
|**CrashDumps**|Zie de beschrijving ergens anders op deze pagina.|  
|**DiagnosticInfrastructureLogs**|Inschakelen van verzamelen van logboeken die worden gegenereerd door Azure Diagnostics. Hallo infrastructuur diagnostische logboeken zijn handig voor het oplossen van Hallo diagnostics systeem zelf. Optionele kenmerken zijn:<br /><br /> - **scheduledTransferLogLevelFilter** -configureert Hallo minimale ernstniveau Hallo-logboeken die worden verzameld.<br /><br /> - **scheduledTransferPeriod** -hello-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond. Hallo-waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**Mappen**|Zie de beschrijving ergens anders op deze pagina.|  
|**EtwProviders**|Zie de beschrijving ergens anders op deze pagina.|  
|**Metrische gegevens**|Zie de beschrijving ergens anders op deze pagina.|  
|**PerformanceCounters**|Zie de beschrijving ergens anders op deze pagina.|  
|**WindowsEventLog**|Zie de beschrijving ergens anders op deze pagina.| 
|**DockerSources**|Zie de beschrijving ergens anders op deze pagina. | 



## <a name="crashdumps-element"></a>CrashDumps Element  
 *Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps-*
 
 Hallo-verzameling van crashdumps inschakelen.  

|Kenmerken|Beschrijving|  
|----------------|-----------------|  
|**containerName**|Optioneel. Hallo-naam van de blob-container in uw Azure Storage-account toobe hello toostore crashdumps gebruikt.|  
|**crashDumpType**|Optioneel.  Azure Diagnostics toocollect mini of volledige crashdumps configureert.|  
|**directoryQuotaPercentage**|Optioneel.  Hiermee configureert u Hallo percentage **overallQuotaInMB** toobe gereserveerd voor crashdumps op Hallo VM.|  

|Onderliggende elementen|Beschrijving|  
|--------------------|-----------------|  
|**CrashDumpConfiguration**|Vereist. Hiermee definieert u configuratiewaarden voor elk proces.<br /><br /> Hallo na kenmerk is ook vereist:<br /><br /> **Procesnaam** - hello naam van het gewenste Azure Diagnostics toocollect een crashdump voor Hallo-proces.|  

## <a name="directories-element"></a>Mappen Element 
 *Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - mappen*

 Hiermee Hallo verzameling Hallo inhoud van een map, IIS kan de logboeken voor het aanvragen van toegang en/of de IIS-logboeken.  

 Optionele **scheduledTransferPeriod** kenmerk. Zie eerder uitleg.  

|Onderliggende elementen|Beschrijving|  
|--------------------|-----------------|  
|**IISLogs**|Dit element in configuratie Hallo inclusief kunt Hallo-verzameling van IIS-logboeken:<br /><br /> **containerName** -Hallo-naam van blob-container in uw Azure Storage-account toobe hello toostore Hallo IIS-logboeken gebruikt.|   
|**FailedRequestLogs**|Dit element in configuratie Hallo inclusief kunt verzamelen van logboeken over mislukte aanvragen tooan ISS-site of toepassing. U moet ook de traceringsopties onder inschakelen **system. WebServer** in **Web.config**.|  
|**Gegevensbronnen**|Een lijst met mappen toomonitor.| 




## <a name="datasources-element"></a>Gegevensbronnen Element  
 *Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - mappen - gegevensbronnen*

 Een lijst met mappen toomonitor.  

|Onderliggende elementen|Beschrijving|  
|--------------------|-----------------|  
|**DirectoryConfiguration**|Vereist. Vereist kenmerk:<br /><br /> **containerName** - hello naam van het Hallo blob-container in uw Azure Storage-account dat toobe toostore Hallo logboekbestanden gebruikt.|  





## <a name="directoryconfiguration-element"></a>DirectoryConfiguration Element  
 *Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - mappen - gegevensbronnen - DirectoryConfiguration-*

 Beide hello, omvat mogelijk **Absolute** of **LocalResource** element, maar niet beide.  

|Onderliggende elementen|Beschrijving|  
|--------------------|-----------------|  
|**Absolute**|Hallo absoluut pad toohello directory toomonitor. Hallo na kenmerken zijn vereist:<br /><br /> - **Pad** -Hallo absoluut pad toohello directory toomonitor.<br /><br /> - **expandEnvironment** -configureert u of omgevingsvariabelen in pad worden uitgevouwen.|  
|**LocalResource**|Hallo pad relatief tooa lokale resource toomonitor. Vereiste kenmerken zijn:<br /><br /> - **Naam** -Hallo lokale resource die Hallo directory toomonitor bevat<br /><br /> - **relativePath** -pad relatief tooName met Hallo directory toomonitor Hallo|  



## <a name="etwproviders-element"></a>EtwProviders Element  
 *Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders-*

 Hiermee configureert u de verzameling van ETW-gebeurtenissen van EventSource en/of ETW Manifest op basis van providers.  

|Onderliggende elementen|Beschrijving|  
|--------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Hiermee configureert u de verzameling van gebeurtenissen die worden gegenereerd op basis van [EventSource klasse](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Vereist kenmerk:<br /><br /> **provider** -Hallo klassenaam van Hallo EventSource gebeurtenis.<br /><br /> Optionele kenmerken zijn:<br /><br /> - **scheduledTransferLogLevelFilter** -Hallo minimale ernst niveau tootransfer tooyour storage-account.<br /><br /> - **scheduledTransferPeriod** -hello-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond. Hallo-waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**EtwManifestProviderConfiguration**|Vereist kenmerk:<br /><br /> **provider** -GUID van het Hallo-gebeurtenisprovider Hallo<br /><br /> Optionele kenmerken zijn:<br /><br /> - **scheduledTransferLogLevelFilter** -Hallo minimale ernst niveau tootransfer tooyour storage-account.<br /><br /> - **scheduledTransferPeriod** -hello-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond. Hallo-waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="etweventsourceproviderconfiguration-element"></a>EtwEventSourceProviderConfiguration Element  
 *Structuur: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwEventSourceProviderConfiguration*

 Hiermee configureert u de verzameling van gebeurtenissen die worden gegenereerd op basis van [EventSource klasse](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).  

|Onderliggende elementen|Beschrijving|  
|--------------------|-----------------|  
|**DefaultEvents**|Het optionele kenmerk:<br/><br/> **eventDestination** - hello naam van het Hallo tabel toostore Hallo gebeurtenissen in|  
|**Gebeurtenis**|Vereist kenmerk:<br /><br /> **id** -Hallo Hallo-gebeurtenis-id.<br /><br /> Het optionele kenmerk:<br /><br /> **eventDestination** - hello naam van het Hallo tabel toostore Hallo gebeurtenissen in|  



## <a name="etwmanifestproviderconfiguration-element"></a>EtwManifestProviderConfiguration Element  
 *Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*

|Onderliggende elementen|Beschrijving|  
|--------------------|-----------------|  
|**DefaultEvents**|Het optionele kenmerk:<br /><br /> **eventDestination** - hello naam van het Hallo tabel toostore Hallo gebeurtenissen in|  
|**Gebeurtenis**|Vereist kenmerk:<br /><br /> **id** -Hallo Hallo-gebeurtenis-id.<br /><br /> Het optionele kenmerk:<br /><br /> **eventDestination** - hello naam van het Hallo tabel toostore Hallo gebeurtenissen in|  



## <a name="metrics-element"></a>Element van de metrische gegevens  
 *Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - metrische gegevens*

 Hiermee kunt u toogenerate een prestaties teller tabel die is geoptimaliseerd voor snelle query's. Elk prestatiemeteritem dat is gedefinieerd in Hallo **PerformanceCounters** element in Hallo metrische gegevens tabel in de toevoeging toohello prestatiemeteritem is opgeslagen.  

 Hallo **resourceId** kenmerk is vereist.  Hallo resource-ID van de virtuele Machine die u om Azure Diagnostics implementeert Hallo. Hallo ophalen **resourceID** van Hallo [Azure-portal](https://portal.azure.com). Selecteer **Bladeren** -> **resourcegroepen** -> **< naam\>**. Klik op Hallo **eigenschappen** tegel en Hallo-waarde van de Hallo kopiëren **ID** veld.  

|Onderliggende elementen|Beschrijving|  
|--------------------|-----------------|  
|**MetricAggregation**|Vereist kenmerk:<br /><br /> **scheduledTransferPeriod** -hello-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond. Hallo-waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="performancecounters-element"></a>PerformanceCounters Element  
 *Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters-*

 Hiermee bepaalt u Hallo van prestatiemeteritems.  

 Het optionele kenmerk:  

 Optionele **scheduledTransferPeriod** kenmerk. Zie eerder uitleg.

|Onderliggend Element|Beschrijving|  
|-------------------|-----------------|  
|**PerformanceCounterConfiguration**|Hallo na kenmerken zijn vereist:<br /><br /> - **counterSpecifier** - hello naam van het prestatiemeteritem Hallo. Bijvoorbeeld `\Processor(_Total)\% Processor Time`. tooget een lijst van de prestaties van prestatiemeteritems op uw host, voert u de opdracht Hallo `typeperf`.<br /><br /> - **sampleRate** -hoe vaak hello teller moet actieve.<br /><br /> Het optionele kenmerk:<br /><br /> **eenheid** -eenheid Hallo van Hallo teller.|  




## <a name="windowseventlog-element"></a>WindowsEventLog Element
 *Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog-*
 
 Hallo-verzameling van het Windows-gebeurtenislogboeken kunt.  

 Optionele **scheduledTransferPeriod** kenmerk. Zie eerder uitleg.  

|Onderliggend Element|Beschrijving|  
|-------------------|-----------------|  
|**Gegevensbron**|Hallo Windows-gebeurtenislogboeken toocollect. Vereist kenmerk:<br /><br /> **naam** -Hallo XPath-query met een beschrijving van Hallo windows gebeurtenissen toobe verzameld. Bijvoorbeeld:<br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> toocollect alle gebeurtenissen opgeven ' * '|  




## <a name="logs-element"></a>Logboeken Element  
 *Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logboeken*

 Aanwezig zijn op versie 1.0 en 1.1. 1.2 ontbreken. Terug in 1.3 toegevoegd.  

 Definieert Hallo buffer configuratie voor basic-Azure Logboeken.  

|Kenmerk|Type|Beschrijving|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|**unsignedInt**|Optioneel. Hallo maximum hoeveelheid system bestandsopslag die beschikbaar is voor Hallo opgegeven gegevens.<br /><br /> Hallo standaardwaarde is 0.|  
|**scheduledTransferLogLevelFilterr**|**tekenreeks**|Optioneel. Hiermee geeft u een minimale ernstniveau Hallo voor logboekvermeldingen die worden overgedragen. de standaardwaarde Hallo is **Undefined**, die alle logboeken overdraagt. Andere mogelijke waarden (in volgorde van de meeste tooleast gegevens) zijn **uitgebreid**, **informatie**, **waarschuwing**, **fout**, en **Kritieke**.|  
|**scheduledTransferPeriod**|**duur**|Optioneel. Hiermee geeft u hello-interval tussen de geplande overdrachten van gegevens, afgerond toohello dichtstbijzijnde minuut.<br /><br /> Hallo standaardwaarde is PT0S.|  
|**sinks** toegevoegd in 1.5|**tekenreeks**|Optioneel. Punten tooa sink locatie tooalso diagnostische gegevens verzenden. Bijvoorbeeld, Application Insights.|  

## <a name="dockersources"></a>DockerSources
 *Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources-*

 In 1,9 toegevoegd.

|Elementnaam|Beschrijving|  
|------------------|-----------------|  
|**Statistieken**|Geeft Hallo systeem toocollect statistieken voor Docker-containers|  

## <a name="sinksconfig-element"></a>SinksConfig Element  
 *Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*

 Een lijst met locaties toosend diagnostische gegevens tooand Hallo-configuratie die is gekoppeld aan deze locaties.  

|Elementnaam|Beschrijving|  
|------------------|-----------------|  
|**Sink**|Zie de beschrijving ergens anders op deze pagina.|  

## <a name="sink-element"></a>Sink-Element
 *Structuur: De hoofd - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink-*

 In versie 1.5 toegevoegd.  

 Locaties toosend diagnostische gegevens naar definieert. Bijvoorbeeld: hello Application Insights-service.  

|Kenmerk|Type|Beschrijving|  
|---------------|----------|-----------------|  
|**naam**|Tekenreeks|Een Hallo van tekenreeks identificerende sinkname.|  

|Element|Type|Beschrijving|  
|-------------|----------|-----------------|  
|**Application Insights**|Tekenreeks|Alleen bij het verzenden van gegevens tooApplication Insights gebruikt. Hallo Instrumentatiesleutel voor een actieve Application Insights-account dat u toegang tot hebt bevatten.|  
|**Kanalen**|Tekenreeks|Één voor elke extra filteren die u stream|  

## <a name="channels-element"></a>Kanalen Element  
 *Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - kanalen*

 In versie 1.5 toegevoegd.  

 Hiermee definieert u filters voor stromen van logboekgegevens een sink te doorlopen.  

|Element|Type|Beschrijving|  
|-------------|----------|-----------------|  
|**Kanaal**|Tekenreeks|Zie de beschrijving ergens anders op deze pagina.|  

## <a name="channel-element"></a>Kanaal-Element
 *Structuur: Basis - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - kanalen - kanaal*

 In versie 1.5 toegevoegd.  

 Locaties toosend diagnostische gegevens naar definieert. Bijvoorbeeld: hello Application Insights-service.  

|Kenmerken|Type|Beschrijving|  
|----------------|----------|-----------------|  
|**logLevel**|**tekenreeks**|Hiermee geeft u een minimale ernstniveau Hallo voor logboekvermeldingen die worden overgedragen. de standaardwaarde Hallo is **Undefined**, die alle logboeken overdraagt. Andere mogelijke waarden (in volgorde van de meeste tooleast gegevens) zijn **uitgebreid**, **informatie**, **waarschuwing**, **fout**, en **Kritieke**.|  
|**naam**|**tekenreeks**|Een unieke naam van Hallo kanaal toorefer naar|  


## <a name="privateconfig-element"></a>PrivateConfig Element 
 *Structuur: Basis - DiagnosticsConfiguration - PrivateConfig*

 In versie 1.3 toegevoegd.  

 Optioneel  

 Slaat de details van persoonlijke Hallo van Hallo storage-account (naam, sleutel en -eindpunt). Deze informatie toohello virtuele machine wordt verzonden, maar kan niet worden opgehaald uit.  

|Onderliggende elementen|Beschrijving|  
|--------------------|-----------------|  
|**StorageAccount**|Hallo storage account toouse. Hallo na kenmerken zijn vereist<br /><br /> - **naam** - hello naam van het Hallo-opslagaccount.<br /><br /> - **sleutel** - hello sleutel toohello storage-account.<br /><br /> - **eindpunt** -Hallo eindpunt tooaccess Hallo storage-account. <br /><br /> -**sasToken** (1.8.1)-kunt u een SAS-token in plaats van de sleutel van een opslagaccount in de persoonlijke configuratie Hallo toegevoegd. Indien opgegeven, wordt de opslagaccountsleutel Hallo genegeerd. <br />Vereisten voor Hallo SAS-Token: <br />-Ondersteunt alleen account SAS-token <br />- *b*, *t* servicetypen zijn vereist. <br /> - *een*, *c*, *u*, *w* machtigingen zijn vereist. <br /> - *c*, *o* brontypen die zijn vereist. <br /> -Ondersteunt alleen Hallo HTTPS-protocol <br /> -Starten en het verlooptijdstip moet geldig zijn.|  


## <a name="isenabled-element"></a>IsEnabled Element  
 *Structuur: Basis - DiagnosticsConfiguration - IsEnabled*

 Booleaanse waarde. Gebruik `true` tooenable Hallo diagnostics of `false` toodisable Hallo diagnostische gegevens.
