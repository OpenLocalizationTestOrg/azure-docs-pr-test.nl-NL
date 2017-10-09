---
title: aaaAzure Diagnostics 1.2 configuratieschema | Microsoft Docs
description: ALLEEN relevant als u van Azure SDK 2.5 met Azure Virtual Machines, virtuele-Machineschaalsets, Service Fabric of Cloud Services gebruikmaakt.
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
ms.openlocfilehash: 31559317b696556a64b51b58800b176ade9a4679
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-12-configuration-schema"></a>Azure Diagnostics 1.2 configuratieschema
> [!NOTE]
> Azure Diagnostics is Hallo onderdeel dat wordt gebruikt toocollect prestatiemeteritems en andere statistieken van Azure Virtual Machines, virtuele-Machineschaalsets, Service Fabric en Cloud-Services.  Deze pagina is alleen relevant als u een van deze services.
>

Azure Diagnostics wordt gebruikt met andere Microsoft-producten voor diagnostische gegevens zoals Azure Monitor, Application Insights en Log Analytics.

Dit schema definieert Hallo mogelijke waarden kunt u tooinitialize diagnostische configuratie-instellingen wanneer Hallo diagnostische monitor wordt gestart.  


 Hallo openbare configuratie bestand schemadefinitie downloaden door het uitvoeren van Hallo volgende PowerShell-opdracht:  

```PowerShell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

 Zie voor meer informatie over het gebruik van Azure Diagnostics [diagnostische gegevens inschakelen in Azure Cloud Services](http://azure.microsoft.com/documentation/articles/cloud-services-dotnet-diagnostics/).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Voorbeeld van een configuratiebestand voor Hallo diagnostische gegevens  
 Hallo volgende voorbeeld ziet u een configuratiebestand typische diagnostische gegevens:  

```xml
<?xml version="1.0" encoding="utf-8"?>  
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">  
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
        <EtwEventSourceProviderConfiguration provider="MyProviderClass" scheduledTransferPeriod="PT5M">  
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
      <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
        <CrashDumpConfiguration processName="mynewprocess.exe" />  
        <CrashDumpConfiguration processName="badapp.exe"/>  
      </CrashDumps>  
    </DiagnosticMonitorConfiguration>  
  </WadCfg>  
</PublicConfig>  

```  

## <a name="diagnostics-configuration-namespace"></a>Diagnostische configuratie Namespace  
 Hallo XML-naamruimte voor Hallo diagnostics-configuratiebestand is:  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="publicconfig-element"></a>PublicConfig Element  
 Element op het hoogste niveau van Hallo diagnostics-configuratiebestand. Hallo beschrijft volgende tabel Hallo elementen van Hallo-configuratiebestand.  

|Elementnaam|Beschrijving|  
|------------------|-----------------|  
|**WadCfg**|Vereist. Configuratie-instellingen voor Hallo telemetrie gegevens toobe verzameld.|  
|**StorageAccount**|Hallo-naam van hello Azure Storage-account toostore Hallo gegevens in. Dit kan ook worden opgegeven als parameter bij het uitvoeren van de cmdlet Set-AzureServiceDiagnosticsExtension Hallo.|  
|**LocalResourceDirectory**|Hallo-map op Hallo virtuele machine toobe gebruikt door Hallo Monitoring Agent toostore gebeurtenisgegevens. Als dat niet is ingesteld, Hallo standaarddirectory wordt gebruikt:<br /><br /> Voor een functie Worker/webservice:`C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> Voor een virtuele Machine:`C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Vereiste kenmerken zijn:<br /><br /> -                      **pad** - hello directory op Hallo system toobe die wordt gebruikt door Azure Diagnostics.<br /><br /> -                      **expandEnvironment** -Hiermee wordt bepaald of omgevingsvariabelen in de padnaam Hallo worden uitgevouwen.|  

## <a name="wadcfg-element"></a>WadCFG Element  
Hiermee definieert u configuratie-instellingen voor Hallo telemetrie gegevens toobe verzameld. Hallo volgende tabel beschrijft de onderliggende elementen:  

|Elementnaam|Beschrijving|  
|------------------|-----------------|  
|**DiagnosticMonitorConfiguration**|Vereist. Optionele kenmerken zijn:<br /><br /> -                     **overallQuotaInMB** -maximale hoeveelheid lokale schijfruimte die kan worden gebruikt door Hallo Hallo verschillende soorten diagnostische gegevens verzameld door Azure Diagnostics. de standaardinstelling Hallo is 5120MB.<br /><br /> -                     **useProxyServer** -Configureer Azure Diagnostics toouse Hallo proxyserverinstellingen zoals in de instellingen van Internet Explorer.|  
|**CrashDumps**|Verzameling van crashdumps inschakelen. Optionele kenmerken zijn:<br /><br /> -                     **containerName** -Hallo-naam van blob-container in uw Azure Storage-account toobe hello toostore crashdumps gebruikt.<br /><br /> -                     **crashDumpType** -configureert Azure Diagnostics toocollect Mini of volledige crash dumpbestanden.<br /><br /> -                     **directoryQuotaPercentage**-Hiermee configureert u Hallo percentage **overallQuotaInMB** toobe gereserveerd voor crashdumps op Hallo VM.|  
|**DiagnosticInfrastructureLogs**|Inschakelen van verzamelen van logboeken die worden gegenereerd door Azure Diagnostics. Hallo infrastructuur diagnostische logboeken zijn handig voor het oplossen van Hallo diagnostics systeem zelf. Optionele kenmerken zijn:<br /><br /> -                     **scheduledTransferLogLevelFilter** -configureert Hallo minimale ernstniveau Hallo-logboeken die worden verzameld.<br /><br /> -                     **scheduledTransferPeriod** -hello-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond. Hallo-waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**Mappen**|Hiermee Hallo verzameling Hallo inhoud van een map, IIS kan de logboeken voor het aanvragen van toegang en/of de IIS-logboeken. Het optionele kenmerk:<br /><br /> **scheduledTransferPeriod** -hello-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond. Hallo-waarde is een [XML "Duur van het gegevenstype."](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**EtwProviders**|Hiermee configureert u de verzameling van ETW-gebeurtenissen van EventSource en/of ETW Manifest op basis van providers.|  
|**Metrische gegevens**|Dit element kunt u toogenerate een prestaties teller tabel die is geoptimaliseerd voor snelle query's. Elk prestatiemeteritem dat is gedefinieerd in Hallo **PerformanceCounters** element in Hallo metrische gegevens tabel in de toevoeging toohello prestatiemeteritem is opgeslagen. Vereist kenmerk:<br /><br /> **resourceId** -dit is de resource-ID Hallo Hallo virtuele Machine die u om Azure Diagnostics implementeert. Hallo ophalen **resourceID** van Hallo [Azure-portal](https://portal.azure.com). Selecteer **Bladeren** -> **resourcegroepen** -> **< naam\>**. Klik op Hallo **eigenschappen** tegel en Hallo-waarde van de Hallo kopiëren **ID** veld.|  
|**PerformanceCounters**|Hiermee bepaalt u Hallo van prestatiemeteritems. Het optionele kenmerk:<br /><br /> **scheduledTransferPeriod** -hello-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond. De waarde is een [XML 'Duur gegevenstype'.](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**WindowsEventLog**|Hallo-verzameling van het Windows-gebeurtenislogboeken kunt. Het optionele kenmerk:<br /><br /> **scheduledTransferPeriod** -hello-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond. De waarde is een [XML 'Duur gegevenstype'.](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  

## <a name="crashdumps-element"></a>CrashDumps Element  
 Verzameling van crashdumps kunt. Hallo volgende tabel beschrijft de onderliggende elementen:  

|Elementnaam|Beschrijving|  
|------------------|-----------------|  
|**CrashDumpConfiguration**|Vereist. Vereist kenmerk:<br /><br /> **Procesnaam** - hello naam van het gewenste Azure Diagnostics toocollect een crashdump voor Hallo-proces.|  
|**crashDumpType**|Azure Diagnostics toocollect mini of volledige crashdumps configureert.|  
|**directoryQuotaPercentage**|Hiermee configureert u Hallo percentage **overallQuotaInMB** toobe gereserveerd voor crashdumps op Hallo VM.|  

## <a name="directories-element"></a>Mappen Element  
 Hiermee Hallo verzameling Hallo inhoud van een map, IIS kan de logboeken voor het aanvragen van toegang en/of de IIS-logboeken. Hallo volgende tabel beschrijft de onderliggende elementen:  

|Elementnaam|Beschrijving|  
|------------------|-----------------|  
|**Gegevensbronnen**|Een lijst met mappen toomonitor.|  
|**FailedRequestLogs**|Dit element in configuratie Hallo inclusief kunt verzamelen van logboeken over mislukte aanvragen tooan ISS-site of toepassing. U moet ook de traceringsopties onder inschakelen **system. WebServer** in **Web.config**.|  
|**IISLogs**|Dit element in configuratie Hallo inclusief kunt Hallo-verzameling van IIS-logboeken:<br /><br /> **containerName** -Hallo-naam van blob-container in uw Azure Storage-account toobe hello toostore Hallo IIS-logboeken gebruikt.|  

## <a name="datasources-element"></a>Gegevensbronnen Element  
 Een lijst met mappen toomonitor. Hallo volgende tabel beschrijft de onderliggende elementen:  

|Elementnaam|Beschrijving|  
|------------------|-----------------|  
|**DirectoryConfiguration**|Vereist. Vereist kenmerk:<br /><br /> **containerName** -Hallo-naam van Hallo blob-container in uw Azure Storage-account toobe gebruikt toostore Hallo-logboekbestanden.|  

## <a name="directoryconfiguration-element"></a>DirectoryConfiguration Element  
 **DirectoryConfiguration** omvat mogelijk een Hallo **Absolute** of **LocalResource** element, maar niet beide. Hallo volgende tabel beschrijft de onderliggende elementen:  

|Elementnaam|Beschrijving|  
|------------------|-----------------|  
|**Absolute**|Hallo absoluut pad toohello directory toomonitor. Hallo na kenmerken zijn vereist:<br /><br /> -                     **Pad** -Hallo absoluut pad toohello directory toomonitor.<br /><br /> -                      **expandEnvironment** -configureert u of omgevingsvariabelen in pad worden uitgevouwen.|  
|**LocalResource**|Hallo pad relatief tooa lokale resource toomonitor. Vereiste kenmerken zijn:<br /><br /> -                     **Naam** -Hallo lokale resource die Hallo directory toomonitor bevat<br /><br /> -                     **relativePath** -pad relatief tooName met Hallo directory toomonitor Hallo|  

## <a name="etwproviders-element"></a>EtwProviders Element  
 Hiermee configureert u de verzameling van ETW-gebeurtenissen van EventSource en/of ETW Manifest op basis van providers. Hallo volgende tabel beschrijft de onderliggende elementen:  

|Elementnaam|Beschrijving|  
|------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Hiermee configureert u de verzameling van gebeurtenissen die worden gegenereerd op basis van [EventSource klasse](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Vereist kenmerk:<br /><br /> **provider** -Hallo klassenaam van Hallo EventSource gebeurtenis.<br /><br /> Optionele kenmerken zijn:<br /><br /> -                     **scheduledTransferLogLevelFilter** -Hallo minimale ernst niveau tootransfer tooyour storage-account.<br /><br /> -                     **scheduledTransferPeriod** -hello-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond. De waarde is een [duur van het gegevenstype XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  
|**EtwManifestProviderConfiguration**|Vereist kenmerk:<br /><br /> **provider** -GUID van het Hallo-gebeurtenisprovider Hallo<br /><br /> Optionele kenmerken zijn:<br /><br /> - **scheduledTransferLogLevelFilter** -Hallo minimale ernst niveau tootransfer tooyour storage-account.<br /><br /> -                     **scheduledTransferPeriod** -hello-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond. De waarde is een [duur van het gegevenstype XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="etweventsourceproviderconfiguration-element"></a>EtwEventSourceProviderConfiguration Element  
 Hiermee configureert u de verzameling van gebeurtenissen die worden gegenereerd op basis van [EventSource klasse](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Hallo volgende tabel beschrijft de onderliggende elementen:  

|Elementnaam|Beschrijving|  
|------------------|-----------------|  
|**DefaultEvents**|Het optionele kenmerk:<br /><br /> **eventDestination** - hello naam van het Hallo tabel toostore Hallo gebeurtenissen in|  
|**Gebeurtenis**|Vereist kenmerk:<br /><br /> **id** -Hallo Hallo-gebeurtenis-id.<br /><br /> Het optionele kenmerk:<br /><br /> **eventDestination** - hello naam van het Hallo tabel toostore Hallo gebeurtenissen in|  

## <a name="etwmanifestproviderconfiguration-element"></a>EtwManifestProviderConfiguration Element  
 Hallo volgende tabel beschrijft de onderliggende elementen:  

|Elementnaam|Beschrijving|  
|------------------|-----------------|  
|**DefaultEvents**|Het optionele kenmerk:<br /><br /> **eventDestination** - hello naam van het Hallo tabel toostore Hallo gebeurtenissen in|  
|**Gebeurtenis**|Vereist kenmerk:<br /><br /> **id** -Hallo Hallo-gebeurtenis-id.<br /><br /> Het optionele kenmerk:<br /><br /> **eventDestination** - hello naam van het Hallo tabel toostore Hallo gebeurtenissen in|  

## <a name="metrics-element"></a>Element van de metrische gegevens  
 Hiermee kunt u toogenerate een prestaties teller tabel die is geoptimaliseerd voor snelle query's. Hallo volgende tabel beschrijft de onderliggende elementen:  

|Elementnaam|Beschrijving|  
|------------------|-----------------|  
|**MetricAggregation**|Vereist kenmerk:<br /><br /> **scheduledTransferPeriod** -hello-interval tussen geplande overdrachten toostorage toohello dichtstbijzijnde minuut afgerond. De waarde is een [duur van het gegevenstype XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="performancecounters-element"></a>PerformanceCounters Element  
 Hiermee bepaalt u Hallo van prestatiemeteritems. Hallo volgende tabel beschrijft de onderliggende elementen:  

|Elementnaam|Beschrijving|  
|------------------|-----------------|  
|**PerformanceCounterConfiguration**|Hallo na kenmerken zijn vereist:<br /><br /> -                     **counterSpecifier** - hello naam van het prestatiemeteritem Hallo. Bijvoorbeeld `\Processor(_Total)\% Processor Time`. een lijst met prestatiemeteritems op uw host Hallo-opdracht uitvoeren tooget `typeperf`.<br /><br /> -                     **sampleRate** -hoe vaak hello teller moet actieve.<br /><br /> Het optionele kenmerk:<br /><br /> **eenheid** -eenheid Hallo van Hallo teller.|  

## <a name="performancecounterconfiguration-element"></a>PerformanceCounterConfiguration Element  
 Hallo volgende tabel beschrijft de onderliggende elementen:  

|Elementnaam|Beschrijving|  
|------------------|-----------------|  
|**aantekening**|Vereist kenmerk:<br /><br /> **displayName** -Hallo weergavenaam voor de teller Hallo<br /><br /> Het optionele kenmerk:<br /><br /> **landinstelling** -landinstelling toouse Hallo Hallo tellernaam om weer te geven|  

## <a name="windowseventlog-element"></a>WindowsEventLog Element  
 Hallo volgende tabel beschrijft de onderliggende elementen:  

|Elementnaam|Beschrijving|  
|------------------|-----------------|  
|**Gegevensbron**|Hallo Windows-gebeurtenislogboeken toocollect. Vereist kenmerk:<br /><br /> **naam** -Hallo XPath-query met een beschrijving van Hallo windows gebeurtenissen toobe verzameld. Bijvoorbeeld:<br /><br /> `Application!*[System[(Level >= 3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level >= 3]]`<br /><br /> toocollect alle gebeurtenissen opgeven ' * '.|
