---
title: aaaAzure Diagnostics 1.0 configuratieschema | Microsoft Docs
description: Dit is alleen relevant als u van Azure SDK 2.4 gebruikmaakt en onder met Azure Virtual Machines, virtuele-Machineschaalsets, Service Fabric of Cloud Services.
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
ms.openlocfilehash: bdd2b26217d6ea28f19e651ab429e7e7401ff57b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a>Het Schema van Azure Diagnostics 1.0
> [!NOTE]
> Azure Diagnostics is Hallo onderdeel dat wordt gebruikt toocollect prestatiemeteritems en andere statistieken van Azure Virtual Machines, virtuele-Machineschaalsets, Service Fabric en Cloud-Services.  Deze pagina is alleen relevant als u een van deze services.
>

Azure Diagnostics wordt gebruikt met andere Microsoft-producten voor diagnostische gegevens zoals Azure Monitor, Application Insights en Log Analytics.

Hello Azure Diagnostics-configuratiebestand definieert waarden die gebruikt tooinitialize Hallo diagnostische Monitor worden. Dit bestand is gebruikte tooinitialize diagnostische configuratie-instellingen wanneer Hallo diagnostics wordt gestart bewaken.  

 Hello Azure Diagnostics-configuratiebestand in het schema is standaard geïnstalleerd toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory. Vervang `<version>` met versie geïnstalleerd Hallo Hallo [Azure SDK](http://www.windowsazure.com/develop/downloads/).  

> [!NOTE]
>  Hallo diagnostics-configuratiebestand wordt meestal gebruikt met starten van de taken waarvoor de diagnostische gegevens toobe die eerder in het opstartproces Hallo worden verzameld. Zie voor meer informatie over het gebruik van Azure Diagnostics [Logboekregistratiegegevens verzamelen met behulp van Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Voorbeeld van een configuratiebestand voor Hallo diagnostische gegevens  
 Hallo volgende voorbeeld ziet u een configuratiebestand typische diagnostische gegevens:  

```xml  
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"  
      configurationChangePollInterval="PT1M"  
      overallQuotaInMB="4096">  
   <DiagnosticInfrastructureLogs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  
   <Logs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  

   <Directories bufferQuotaInMB="1024"   
      scheduledTransferPeriod="PT1M">  

      <!-- These three elements specify hello special directories   
           that are set up for hello log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories hello DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative tooa local   
                 resource defined in hello service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- hello counter specifier is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- hello event log name is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a>DiagnosticsConfiguration Namespace  
 Hallo XML-naamruimte voor Hallo diagnostics-configuratiebestand is:  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a>Schema-elementen  
 Hallo diagnostics configuratiebestand bevat Hallo volgende elementen.


## <a name="diagnosticmonitorconfiguration-element"></a>DiagnosticMonitorConfiguration Element  
op het hoogste niveau element Hallo van Hallo diagnostics-configuratiebestand.  

Kenmerken:

|Kenmerk  |Type   |Vereist| Standaard | Beschrijving|  
|-----------|-------|--------|---------|------------|  
|**configurationChangePollInterval**|Duur|Optioneel | PT1M| Hiermee geeft u hello-interval op welke diagnostische monitor Hallo polls voor diagnostische configuratiewijzigingen.|  
|**overallQuotaInMB**|unsignedInt|Optioneel| 4000 MB. Als u een waarde opgeeft, deze mag niet groter zijn dan deze hoeveelheid |Hallo totale hoeveelheid system bestandsopslag voor alle logboekregistratie buffers toegewezen.|  

## <a name="diagnosticinfrastructurelogs-element"></a>DiagnosticInfrastructureLogs Element  
Hallo configuratie buffer voor Hallo-logboeken die worden gegenereerd door Hallo onderliggende diagnostics infrastructuur.

Bovenliggend Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).  

Kenmerken:

|Kenmerk|Type|Beschrijving|  
|---------|----|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Optioneel. Hallo maximum hoeveelheid system bestandsopslag die beschikbaar is voor Hallo opgegeven gegevens.<br /><br /> Hallo standaardwaarde is 0.|  
|**scheduledTransferLogLevelFilter**|Tekenreeks|Optioneel. Hiermee geeft u een minimale ernstniveau Hallo voor logboekvermeldingen die worden overgedragen. de standaardwaarde Hallo is **Undefined**. Andere mogelijke waarden zijn **uitgebreid**, **informatie**, **waarschuwing**, **fout**, en **Kritiek**.|  
|**scheduledTransferPeriod**|Duur|Optioneel. Hiermee geeft u hello-interval tussen de geplande overdrachten van gegevens, afgerond toohello dichtstbijzijnde minuut.<br /><br /> Hallo standaardwaarde is PT0S.|  

## <a name="logs-element"></a>Logboeken Element  
 Definieert Hallo buffer configuratie voor basic-Azure Logboeken.

 Bovenliggend element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).  

Kenmerken:  

|Kenmerk|Type|Beschrijving|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Optioneel. Hallo maximum hoeveelheid system bestandsopslag die beschikbaar is voor Hallo opgegeven gegevens.<br /><br /> Hallo standaardwaarde is 0.|  
|**scheduledTransferLogLevelFilter**|Tekenreeks|Optioneel. Hiermee geeft u een minimale ernstniveau Hallo voor logboekvermeldingen die worden overgedragen. de standaardwaarde Hallo is **Undefined**. Andere mogelijke waarden zijn **uitgebreid**, **informatie**, **waarschuwing**, **fout**, en **Kritiek**.|  
|**scheduledTransferPeriod**|Duur|Optioneel. Hiermee geeft u hello-interval tussen de geplande overdrachten van gegevens, afgerond toohello dichtstbijzijnde minuut.<br /><br /> Hallo standaardwaarde is PT0S.|  

## <a name="directories-element"></a>Mappen Element  
Hallo configuratie buffer voor logboeken op basis van bestanden die u kunt definiëren.

Bovenliggend element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).  


Kenmerken:  

|Kenmerk|Type|Beschrijving|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Optioneel. Hallo maximum hoeveelheid system bestandsopslag die beschikbaar is voor Hallo opgegeven gegevens.<br /><br /> Hallo standaardwaarde is 0.|  
|**scheduledTransferPeriod**|Duur|Optioneel. Hiermee geeft u hello-interval tussen de geplande overdrachten van gegevens, afgerond toohello dichtstbijzijnde minuut.<br /><br /> Hallo standaardwaarde is PT0S.|  

## <a name="crashdumps-element"></a>CrashDumps Element  
 Hallo crash dumpbestanden directory definieert.

 Bovenliggend Element: [mappen Element](#Directories).  

Kenmerken:  

|Kenmerk|Type|Beschrijving|  
|---------------|----------|-----------------|  
|**container**|Tekenreeks|Hallo-naam van Hallo container waar Hallo inhoud van Hallo map toobe is overgedragen.|  
|**directoryQuotaInMB**|unsignedInt|Optioneel. Hiermee geeft u Hallo maximale grootte van de directory Hallo in megabytes.<br /><br /> Hallo standaardwaarde is 0.|  

## <a name="failedrequestlogs-element"></a>FailedRequestLogs Element  
 Definieert de logboekmap Hallo-mislukte aanvragen.

 Bovenliggende Element [mappen Element](#Directories).  

Kenmerken:  

|Kenmerk|Type|Beschrijving|  
|---------------|----------|-----------------|  
|**container**|Tekenreeks|Hallo-naam van Hallo container waar Hallo inhoud van Hallo map toobe is overgedragen.|  
|**directoryQuotaInMB**|unsignedInt|Optioneel. Hiermee geeft u Hallo maximale grootte van de directory Hallo in megabytes.<br /><br /> Hallo standaardwaarde is 0.|  

##  <a name="iislogs-element"></a>IISLogs Element  
 Hallo IIS logboekmap definieert.

 Bovenliggende Element [mappen Element](#Directories).  

Kenmerken:  

|Kenmerk|Type|Beschrijving|  
|---------------|----------|-----------------|  
|**container**|Tekenreeks|Hallo-naam van Hallo container waar Hallo inhoud van Hallo map toobe is overgedragen.|  
|**directoryQuotaInMB**|unsignedInt|Optioneel. Hiermee geeft u Hallo maximale grootte van de directory Hallo in megabytes.<br /><br /> Hallo standaardwaarde is 0.|  

## <a name="datasources-element"></a>Gegevensbronnen Element  
 Hiermee definieert u nul of meer extra logboekback-mappen.

 Bovenliggend Element: [mappen Element](#Directories).

## <a name="directoryconfiguration-element"></a>DirectoryConfiguration Element  
 Hallo-map van logboekbestand bestanden toomonitor definieert.

 Bovenliggend Element: [gegevensbronnen Element](#DataSources).

Kenmerken:

|Kenmerk|Type|Beschrijving|  
|---------------|----------|-----------------|  
|**container**|Tekenreeks|Hallo-naam van Hallo container waar Hallo inhoud van Hallo map toobe is overgedragen.|  
|**directoryQuotaInMB**|unsignedInt|Optioneel. Hiermee geeft u Hallo maximale grootte van de directory Hallo in megabytes.<br /><br /> Hallo standaardwaarde is 0.|  

## <a name="absolute-element"></a>Absolute Element  
 Hiermee definieert u een absoluut pad van Hallo directory toomonitor met optionele omgeving uitbreiding.

 Bovenliggend Element: [DirectoryConfiguration Element](#DirectoryConfiguration).  

Kenmerken:  

|Kenmerk|Type|Beschrijving|  
|---------------|----------|-----------------|  
|**pad**|Tekenreeks|Vereist. Hallo absoluut pad toohello directory toomonitor.|  
|**expandEnvironment**|Booleaanse waarde|Vereist. Als instellen te**true**, omgevingsvariabelen in Hallo pad worden uitgevouwen.|  

## <a name="localresource-element"></a>LocalResource Element  
 Hiermee definieert u een pad relatief tooa lokale bron gedefinieerd in de servicedefinitie Hallo.

 Bovenliggend Element: [DirectoryConfiguration Element](#DirectoryConfiguration).  

Kenmerken:  

|Kenmerk|Type|Beschrijving|  
|---------------|----------|-----------------|  
|**naam**|Tekenreeks|Vereist. Hallo-naam van Hallo lokale resource die Hallo directory toomonitor bevat.|  
|**relativePath**|Tekenreeks|Vereist. Hallo pad relatief toohello lokale resource toomonitor.|  

## <a name="performancecounters-element"></a>PerformanceCounters Element  
 Hallo pad toohello prestaties teller toocollect definieert.

 Bovenliggend Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).


 Kenmerken:  

|Kenmerk|Type|Beschrijving|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Optioneel. Hallo maximum hoeveelheid system bestandsopslag die beschikbaar is voor Hallo opgegeven gegevens.<br /><br /> Hallo standaardwaarde is 0.|  
|**scheduledTransferPeriod**|Duur|Optioneel. Hiermee geeft u hello-interval tussen de geplande overdrachten van gegevens, afgerond toohello dichtstbijzijnde minuut.<br /><br /> Hallo standaardwaarde is PT0S.|  

## <a name="performancecounterconfiguration-element"></a>PerformanceCounterConfiguration Element  
 Hallo prestaties teller toocollect definieert.

 Bovenliggend Element: [PerformanceCounters Element](#PerformanceCounters).  

 Kenmerken:  

|Kenmerk|Type|Beschrijving|  
|---------------|----------|-----------------|  
|**counterSpecifier**|Tekenreeks|Vereist. Hallo pad toohello prestaties teller toocollect.|  
|**sampleRate**|Duur|Vereist. Hallo snelheid welke Hallo prestatiemeteritem moet worden verzameld.|  

## <a name="windowseventlog-element"></a>WindowsEventLog Element  
 Hallo gebeurtenislogboeken toomonitor definieert.

 Bovenliggend Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).

  Kenmerken:

|Kenmerk|Type|Beschrijving|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Optioneel. Hallo maximum hoeveelheid system bestandsopslag die beschikbaar is voor Hallo opgegeven gegevens.<br /><br /> Hallo standaardwaarde is 0.|  
|**scheduledTransferLogLevelFilter**|Tekenreeks|Optioneel. Hiermee geeft u een minimale ernstniveau Hallo voor logboekvermeldingen die worden overgedragen. de standaardwaarde Hallo is **Undefined**. Andere mogelijke waarden zijn **uitgebreid**, **informatie**, **waarschuwing**, **fout**, en **Kritiek**.|  
|**scheduledTransferPeriod**|Duur|Optioneel. Hiermee geeft u hello-interval tussen de geplande overdrachten van gegevens, afgerond toohello dichtstbijzijnde minuut.<br /><br /> Hallo standaardwaarde is PT0S.|  

## <a name="datasource-element"></a>DataSource-Element  
 Hallo gebeurtenislogboek toomonitor definieert.

 Bovenliggend Element: [WindowsEventLog Element](#windowsEventLog).  

 Kenmerken:

|Kenmerk|Type|Beschrijving|  
|---------------|----------|-----------------|  
|**naam**|Tekenreeks|Vereist. Een XPath-expressie Hallo logboek toocollect opgeven.|  
