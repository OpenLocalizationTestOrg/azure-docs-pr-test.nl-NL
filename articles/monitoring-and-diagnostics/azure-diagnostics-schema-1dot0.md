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
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="facce-103">Het Schema van Azure Diagnostics 1.0</span><span class="sxs-lookup"><span data-stu-id="facce-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="facce-104">Azure Diagnostics is Hallo onderdeel dat wordt gebruikt toocollect prestatiemeteritems en andere statistieken van Azure Virtual Machines, virtuele-Machineschaalsets, Service Fabric en Cloud-Services.</span><span class="sxs-lookup"><span data-stu-id="facce-104">Azure Diagnostics is hello component used toocollect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="facce-105">Deze pagina is alleen relevant als u een van deze services.</span><span class="sxs-lookup"><span data-stu-id="facce-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="facce-106">Azure Diagnostics wordt gebruikt met andere Microsoft-producten voor diagnostische gegevens zoals Azure Monitor, Application Insights en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="facce-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="facce-107">Hello Azure Diagnostics-configuratiebestand definieert waarden die gebruikt tooinitialize Hallo diagnostische Monitor worden.</span><span class="sxs-lookup"><span data-stu-id="facce-107">hello Azure Diagnostics configuration file defines values that are used tooinitialize hello Diagnostics Monitor.</span></span> <span data-ttu-id="facce-108">Dit bestand is gebruikte tooinitialize diagnostische configuratie-instellingen wanneer Hallo diagnostics wordt gestart bewaken.</span><span class="sxs-lookup"><span data-stu-id="facce-108">This file is used tooinitialize diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

 <span data-ttu-id="facce-109">Hello Azure Diagnostics-configuratiebestand in het schema is standaard geïnstalleerd toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span><span class="sxs-lookup"><span data-stu-id="facce-109">By default, hello Azure Diagnostics configuration schema file is installed toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="facce-110">Vervang `<version>` met versie geïnstalleerd Hallo Hallo [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="facce-110">Replace `<version>` with hello installed version of hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="facce-111">Hallo diagnostics-configuratiebestand wordt meestal gebruikt met starten van de taken waarvoor de diagnostische gegevens toobe die eerder in het opstartproces Hallo worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="facce-111">hello diagnostics configuration file is typically used with startup tasks that require diagnostic data toobe collected earlier in hello startup process.</span></span> <span data-ttu-id="facce-112">Zie voor meer informatie over het gebruik van Azure Diagnostics [Logboekregistratiegegevens verzamelen met behulp van Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span><span class="sxs-lookup"><span data-stu-id="facce-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="facce-113">Voorbeeld van een configuratiebestand voor Hallo diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="facce-113">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="facce-114">Hallo volgende voorbeeld ziet u een configuratiebestand typische diagnostische gegevens:</span><span class="sxs-lookup"><span data-stu-id="facce-114">hello following example shows a typical diagnostics configuration file:</span></span>  

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

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="facce-115">DiagnosticsConfiguration Namespace</span><span class="sxs-lookup"><span data-stu-id="facce-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="facce-116">Hallo XML-naamruimte voor Hallo diagnostics-configuratiebestand is:</span><span class="sxs-lookup"><span data-stu-id="facce-116">hello XML namespace for hello diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="facce-117">Schema-elementen</span><span class="sxs-lookup"><span data-stu-id="facce-117">Schema Elements</span></span>  
 <span data-ttu-id="facce-118">Hallo diagnostics configuratiebestand bevat Hallo volgende elementen.</span><span class="sxs-lookup"><span data-stu-id="facce-118">hello diagnostics configuration file includes hello following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="facce-119">DiagnosticMonitorConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="facce-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="facce-120">op het hoogste niveau element Hallo van Hallo diagnostics-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="facce-120">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="facce-121">Kenmerken:</span><span class="sxs-lookup"><span data-stu-id="facce-121">Attributes:</span></span>

|<span data-ttu-id="facce-122">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="facce-122">Attribute</span></span>  |<span data-ttu-id="facce-123">Type</span><span class="sxs-lookup"><span data-stu-id="facce-123">Type</span></span>   |<span data-ttu-id="facce-124">Vereist</span><span class="sxs-lookup"><span data-stu-id="facce-124">Required</span></span>| <span data-ttu-id="facce-125">Standaard</span><span class="sxs-lookup"><span data-stu-id="facce-125">Default</span></span> | <span data-ttu-id="facce-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="facce-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="facce-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="facce-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="facce-128">Duur</span><span class="sxs-lookup"><span data-stu-id="facce-128">duration</span></span>|<span data-ttu-id="facce-129">Optioneel</span><span class="sxs-lookup"><span data-stu-id="facce-129">Optional</span></span> | <span data-ttu-id="facce-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="facce-130">PT1M</span></span>| <span data-ttu-id="facce-131">Hiermee geeft u hello-interval op welke diagnostische monitor Hallo polls voor diagnostische configuratiewijzigingen.</span><span class="sxs-lookup"><span data-stu-id="facce-131">Specifies hello interval at which hello diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="facce-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="facce-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="facce-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="facce-133">unsignedInt</span></span>|<span data-ttu-id="facce-134">Optioneel</span><span class="sxs-lookup"><span data-stu-id="facce-134">Optional</span></span>| <span data-ttu-id="facce-135">4000 MB.</span><span class="sxs-lookup"><span data-stu-id="facce-135">4000 MB.</span></span> <span data-ttu-id="facce-136">Als u een waarde opgeeft, deze mag niet groter zijn dan deze hoeveelheid</span><span class="sxs-lookup"><span data-stu-id="facce-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="facce-137">Hallo totale hoeveelheid system bestandsopslag voor alle logboekregistratie buffers toegewezen.</span><span class="sxs-lookup"><span data-stu-id="facce-137">hello total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="facce-138">DiagnosticInfrastructureLogs Element</span><span class="sxs-lookup"><span data-stu-id="facce-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="facce-139">Hallo configuratie buffer voor Hallo-logboeken die worden gegenereerd door Hallo onderliggende diagnostics infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="facce-139">Defines hello buffer configuration for hello logs that are generated by hello underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="facce-140">Bovenliggend Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="facce-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="facce-141">Kenmerken:</span><span class="sxs-lookup"><span data-stu-id="facce-141">Attributes:</span></span>

|<span data-ttu-id="facce-142">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="facce-142">Attribute</span></span>|<span data-ttu-id="facce-143">Type</span><span class="sxs-lookup"><span data-stu-id="facce-143">Type</span></span>|<span data-ttu-id="facce-144">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="facce-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="facce-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="facce-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="facce-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="facce-146">unsignedInt</span></span>|<span data-ttu-id="facce-147">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-147">Optional.</span></span> <span data-ttu-id="facce-148">Hallo maximum hoeveelheid system bestandsopslag die beschikbaar is voor Hallo opgegeven gegevens.</span><span class="sxs-lookup"><span data-stu-id="facce-148">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="facce-149">Hallo standaardwaarde is 0.</span><span class="sxs-lookup"><span data-stu-id="facce-149">hello default is 0.</span></span>|  
|<span data-ttu-id="facce-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="facce-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="facce-151">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="facce-151">string</span></span>|<span data-ttu-id="facce-152">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-152">Optional.</span></span> <span data-ttu-id="facce-153">Hiermee geeft u een minimale ernstniveau Hallo voor logboekvermeldingen die worden overgedragen.</span><span class="sxs-lookup"><span data-stu-id="facce-153">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="facce-154">de standaardwaarde Hallo is **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="facce-154">hello default value is **Undefined**.</span></span> <span data-ttu-id="facce-155">Andere mogelijke waarden zijn **uitgebreid**, **informatie**, **waarschuwing**, **fout**, en **Kritiek**.</span><span class="sxs-lookup"><span data-stu-id="facce-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="facce-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="facce-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="facce-157">Duur</span><span class="sxs-lookup"><span data-stu-id="facce-157">duration</span></span>|<span data-ttu-id="facce-158">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-158">Optional.</span></span> <span data-ttu-id="facce-159">Hiermee geeft u hello-interval tussen de geplande overdrachten van gegevens, afgerond toohello dichtstbijzijnde minuut.</span><span class="sxs-lookup"><span data-stu-id="facce-159">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="facce-160">Hallo standaardwaarde is PT0S.</span><span class="sxs-lookup"><span data-stu-id="facce-160">hello default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="facce-161">Logboeken Element</span><span class="sxs-lookup"><span data-stu-id="facce-161">Logs Element</span></span>  
 <span data-ttu-id="facce-162">Definieert Hallo buffer configuratie voor basic-Azure Logboeken.</span><span class="sxs-lookup"><span data-stu-id="facce-162">Defines hello buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="facce-163">Bovenliggend element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="facce-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="facce-164">Kenmerken:</span><span class="sxs-lookup"><span data-stu-id="facce-164">Attributes:</span></span>  

|<span data-ttu-id="facce-165">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="facce-165">Attribute</span></span>|<span data-ttu-id="facce-166">Type</span><span class="sxs-lookup"><span data-stu-id="facce-166">Type</span></span>|<span data-ttu-id="facce-167">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="facce-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="facce-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="facce-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="facce-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="facce-169">unsignedInt</span></span>|<span data-ttu-id="facce-170">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-170">Optional.</span></span> <span data-ttu-id="facce-171">Hallo maximum hoeveelheid system bestandsopslag die beschikbaar is voor Hallo opgegeven gegevens.</span><span class="sxs-lookup"><span data-stu-id="facce-171">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="facce-172">Hallo standaardwaarde is 0.</span><span class="sxs-lookup"><span data-stu-id="facce-172">hello default is 0.</span></span>|  
|<span data-ttu-id="facce-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="facce-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="facce-174">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="facce-174">string</span></span>|<span data-ttu-id="facce-175">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-175">Optional.</span></span> <span data-ttu-id="facce-176">Hiermee geeft u een minimale ernstniveau Hallo voor logboekvermeldingen die worden overgedragen.</span><span class="sxs-lookup"><span data-stu-id="facce-176">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="facce-177">de standaardwaarde Hallo is **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="facce-177">hello default value is **Undefined**.</span></span> <span data-ttu-id="facce-178">Andere mogelijke waarden zijn **uitgebreid**, **informatie**, **waarschuwing**, **fout**, en **Kritiek**.</span><span class="sxs-lookup"><span data-stu-id="facce-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="facce-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="facce-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="facce-180">Duur</span><span class="sxs-lookup"><span data-stu-id="facce-180">duration</span></span>|<span data-ttu-id="facce-181">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-181">Optional.</span></span> <span data-ttu-id="facce-182">Hiermee geeft u hello-interval tussen de geplande overdrachten van gegevens, afgerond toohello dichtstbijzijnde minuut.</span><span class="sxs-lookup"><span data-stu-id="facce-182">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="facce-183">Hallo standaardwaarde is PT0S.</span><span class="sxs-lookup"><span data-stu-id="facce-183">hello default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="facce-184">Mappen Element</span><span class="sxs-lookup"><span data-stu-id="facce-184">Directories Element</span></span>  
<span data-ttu-id="facce-185">Hallo configuratie buffer voor logboeken op basis van bestanden die u kunt definiëren.</span><span class="sxs-lookup"><span data-stu-id="facce-185">Defines hello buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="facce-186">Bovenliggend element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="facce-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="facce-187">Kenmerken:</span><span class="sxs-lookup"><span data-stu-id="facce-187">Attributes:</span></span>  

|<span data-ttu-id="facce-188">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="facce-188">Attribute</span></span>|<span data-ttu-id="facce-189">Type</span><span class="sxs-lookup"><span data-stu-id="facce-189">Type</span></span>|<span data-ttu-id="facce-190">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="facce-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="facce-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="facce-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="facce-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="facce-192">unsignedInt</span></span>|<span data-ttu-id="facce-193">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-193">Optional.</span></span> <span data-ttu-id="facce-194">Hallo maximum hoeveelheid system bestandsopslag die beschikbaar is voor Hallo opgegeven gegevens.</span><span class="sxs-lookup"><span data-stu-id="facce-194">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="facce-195">Hallo standaardwaarde is 0.</span><span class="sxs-lookup"><span data-stu-id="facce-195">hello default is 0.</span></span>|  
|<span data-ttu-id="facce-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="facce-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="facce-197">Duur</span><span class="sxs-lookup"><span data-stu-id="facce-197">duration</span></span>|<span data-ttu-id="facce-198">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-198">Optional.</span></span> <span data-ttu-id="facce-199">Hiermee geeft u hello-interval tussen de geplande overdrachten van gegevens, afgerond toohello dichtstbijzijnde minuut.</span><span class="sxs-lookup"><span data-stu-id="facce-199">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="facce-200">Hallo standaardwaarde is PT0S.</span><span class="sxs-lookup"><span data-stu-id="facce-200">hello default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="facce-201">CrashDumps Element</span><span class="sxs-lookup"><span data-stu-id="facce-201">CrashDumps Element</span></span>  
 <span data-ttu-id="facce-202">Hallo crash dumpbestanden directory definieert.</span><span class="sxs-lookup"><span data-stu-id="facce-202">Defines hello crash dumps directory.</span></span>

 <span data-ttu-id="facce-203">Bovenliggend Element: [mappen Element](#Directories).</span><span class="sxs-lookup"><span data-stu-id="facce-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="facce-204">Kenmerken:</span><span class="sxs-lookup"><span data-stu-id="facce-204">Attributes:</span></span>  

|<span data-ttu-id="facce-205">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="facce-205">Attribute</span></span>|<span data-ttu-id="facce-206">Type</span><span class="sxs-lookup"><span data-stu-id="facce-206">Type</span></span>|<span data-ttu-id="facce-207">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="facce-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="facce-208">**container**</span><span class="sxs-lookup"><span data-stu-id="facce-208">**container**</span></span>|<span data-ttu-id="facce-209">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="facce-209">string</span></span>|<span data-ttu-id="facce-210">Hallo-naam van Hallo container waar Hallo inhoud van Hallo map toobe is overgedragen.</span><span class="sxs-lookup"><span data-stu-id="facce-210">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="facce-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="facce-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="facce-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="facce-212">unsignedInt</span></span>|<span data-ttu-id="facce-213">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-213">Optional.</span></span> <span data-ttu-id="facce-214">Hiermee geeft u Hallo maximale grootte van de directory Hallo in megabytes.</span><span class="sxs-lookup"><span data-stu-id="facce-214">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="facce-215">Hallo standaardwaarde is 0.</span><span class="sxs-lookup"><span data-stu-id="facce-215">hello default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="facce-216">FailedRequestLogs Element</span><span class="sxs-lookup"><span data-stu-id="facce-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="facce-217">Definieert de logboekmap Hallo-mislukte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="facce-217">Defines hello failed request log directory.</span></span>

 <span data-ttu-id="facce-218">Bovenliggende Element [mappen Element](#Directories).</span><span class="sxs-lookup"><span data-stu-id="facce-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="facce-219">Kenmerken:</span><span class="sxs-lookup"><span data-stu-id="facce-219">Attributes:</span></span>  

|<span data-ttu-id="facce-220">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="facce-220">Attribute</span></span>|<span data-ttu-id="facce-221">Type</span><span class="sxs-lookup"><span data-stu-id="facce-221">Type</span></span>|<span data-ttu-id="facce-222">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="facce-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="facce-223">**container**</span><span class="sxs-lookup"><span data-stu-id="facce-223">**container**</span></span>|<span data-ttu-id="facce-224">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="facce-224">string</span></span>|<span data-ttu-id="facce-225">Hallo-naam van Hallo container waar Hallo inhoud van Hallo map toobe is overgedragen.</span><span class="sxs-lookup"><span data-stu-id="facce-225">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="facce-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="facce-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="facce-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="facce-227">unsignedInt</span></span>|<span data-ttu-id="facce-228">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-228">Optional.</span></span> <span data-ttu-id="facce-229">Hiermee geeft u Hallo maximale grootte van de directory Hallo in megabytes.</span><span class="sxs-lookup"><span data-stu-id="facce-229">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="facce-230">Hallo standaardwaarde is 0.</span><span class="sxs-lookup"><span data-stu-id="facce-230">hello default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="facce-231">IISLogs Element</span><span class="sxs-lookup"><span data-stu-id="facce-231">IISLogs Element</span></span>  
 <span data-ttu-id="facce-232">Hallo IIS logboekmap definieert.</span><span class="sxs-lookup"><span data-stu-id="facce-232">Defines hello IIS log directory.</span></span>

 <span data-ttu-id="facce-233">Bovenliggende Element [mappen Element](#Directories).</span><span class="sxs-lookup"><span data-stu-id="facce-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="facce-234">Kenmerken:</span><span class="sxs-lookup"><span data-stu-id="facce-234">Attributes:</span></span>  

|<span data-ttu-id="facce-235">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="facce-235">Attribute</span></span>|<span data-ttu-id="facce-236">Type</span><span class="sxs-lookup"><span data-stu-id="facce-236">Type</span></span>|<span data-ttu-id="facce-237">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="facce-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="facce-238">**container**</span><span class="sxs-lookup"><span data-stu-id="facce-238">**container**</span></span>|<span data-ttu-id="facce-239">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="facce-239">string</span></span>|<span data-ttu-id="facce-240">Hallo-naam van Hallo container waar Hallo inhoud van Hallo map toobe is overgedragen.</span><span class="sxs-lookup"><span data-stu-id="facce-240">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="facce-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="facce-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="facce-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="facce-242">unsignedInt</span></span>|<span data-ttu-id="facce-243">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-243">Optional.</span></span> <span data-ttu-id="facce-244">Hiermee geeft u Hallo maximale grootte van de directory Hallo in megabytes.</span><span class="sxs-lookup"><span data-stu-id="facce-244">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="facce-245">Hallo standaardwaarde is 0.</span><span class="sxs-lookup"><span data-stu-id="facce-245">hello default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="facce-246">Gegevensbronnen Element</span><span class="sxs-lookup"><span data-stu-id="facce-246">DataSources Element</span></span>  
 <span data-ttu-id="facce-247">Hiermee definieert u nul of meer extra logboekback-mappen.</span><span class="sxs-lookup"><span data-stu-id="facce-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="facce-248">Bovenliggend Element: [mappen Element](#Directories).</span><span class="sxs-lookup"><span data-stu-id="facce-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="facce-249">DirectoryConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="facce-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="facce-250">Hallo-map van logboekbestand bestanden toomonitor definieert.</span><span class="sxs-lookup"><span data-stu-id="facce-250">Defines hello directory of log files toomonitor.</span></span>

 <span data-ttu-id="facce-251">Bovenliggend Element: [gegevensbronnen Element](#DataSources).</span><span class="sxs-lookup"><span data-stu-id="facce-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="facce-252">Kenmerken:</span><span class="sxs-lookup"><span data-stu-id="facce-252">Attributes:</span></span>

|<span data-ttu-id="facce-253">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="facce-253">Attribute</span></span>|<span data-ttu-id="facce-254">Type</span><span class="sxs-lookup"><span data-stu-id="facce-254">Type</span></span>|<span data-ttu-id="facce-255">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="facce-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="facce-256">**container**</span><span class="sxs-lookup"><span data-stu-id="facce-256">**container**</span></span>|<span data-ttu-id="facce-257">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="facce-257">string</span></span>|<span data-ttu-id="facce-258">Hallo-naam van Hallo container waar Hallo inhoud van Hallo map toobe is overgedragen.</span><span class="sxs-lookup"><span data-stu-id="facce-258">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="facce-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="facce-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="facce-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="facce-260">unsignedInt</span></span>|<span data-ttu-id="facce-261">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-261">Optional.</span></span> <span data-ttu-id="facce-262">Hiermee geeft u Hallo maximale grootte van de directory Hallo in megabytes.</span><span class="sxs-lookup"><span data-stu-id="facce-262">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="facce-263">Hallo standaardwaarde is 0.</span><span class="sxs-lookup"><span data-stu-id="facce-263">hello default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="facce-264">Absolute Element</span><span class="sxs-lookup"><span data-stu-id="facce-264">Absolute Element</span></span>  
 <span data-ttu-id="facce-265">Hiermee definieert u een absoluut pad van Hallo directory toomonitor met optionele omgeving uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="facce-265">Defines an absolute path of hello directory toomonitor with optional environment expansion.</span></span>

 <span data-ttu-id="facce-266">Bovenliggend Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="facce-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="facce-267">Kenmerken:</span><span class="sxs-lookup"><span data-stu-id="facce-267">Attributes:</span></span>  

|<span data-ttu-id="facce-268">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="facce-268">Attribute</span></span>|<span data-ttu-id="facce-269">Type</span><span class="sxs-lookup"><span data-stu-id="facce-269">Type</span></span>|<span data-ttu-id="facce-270">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="facce-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="facce-271">**pad**</span><span class="sxs-lookup"><span data-stu-id="facce-271">**path**</span></span>|<span data-ttu-id="facce-272">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="facce-272">string</span></span>|<span data-ttu-id="facce-273">Vereist.</span><span class="sxs-lookup"><span data-stu-id="facce-273">Required.</span></span> <span data-ttu-id="facce-274">Hallo absoluut pad toohello directory toomonitor.</span><span class="sxs-lookup"><span data-stu-id="facce-274">hello absolute path toohello directory toomonitor.</span></span>|  
|<span data-ttu-id="facce-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="facce-275">**expandEnvironment**</span></span>|<span data-ttu-id="facce-276">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="facce-276">boolean</span></span>|<span data-ttu-id="facce-277">Vereist.</span><span class="sxs-lookup"><span data-stu-id="facce-277">Required.</span></span> <span data-ttu-id="facce-278">Als instellen te**true**, omgevingsvariabelen in Hallo pad worden uitgevouwen.</span><span class="sxs-lookup"><span data-stu-id="facce-278">If set too**true**, environment variables in hello path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="facce-279">LocalResource Element</span><span class="sxs-lookup"><span data-stu-id="facce-279">LocalResource Element</span></span>  
 <span data-ttu-id="facce-280">Hiermee definieert u een pad relatief tooa lokale bron gedefinieerd in de servicedefinitie Hallo.</span><span class="sxs-lookup"><span data-stu-id="facce-280">Defines a path relative tooa local resource defined in hello service definition.</span></span>

 <span data-ttu-id="facce-281">Bovenliggend Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="facce-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="facce-282">Kenmerken:</span><span class="sxs-lookup"><span data-stu-id="facce-282">Attributes:</span></span>  

|<span data-ttu-id="facce-283">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="facce-283">Attribute</span></span>|<span data-ttu-id="facce-284">Type</span><span class="sxs-lookup"><span data-stu-id="facce-284">Type</span></span>|<span data-ttu-id="facce-285">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="facce-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="facce-286">**naam**</span><span class="sxs-lookup"><span data-stu-id="facce-286">**name**</span></span>|<span data-ttu-id="facce-287">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="facce-287">string</span></span>|<span data-ttu-id="facce-288">Vereist.</span><span class="sxs-lookup"><span data-stu-id="facce-288">Required.</span></span> <span data-ttu-id="facce-289">Hallo-naam van Hallo lokale resource die Hallo directory toomonitor bevat.</span><span class="sxs-lookup"><span data-stu-id="facce-289">hello name of hello local resource that contains hello directory toomonitor.</span></span>|  
|<span data-ttu-id="facce-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="facce-290">**relativePath**</span></span>|<span data-ttu-id="facce-291">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="facce-291">string</span></span>|<span data-ttu-id="facce-292">Vereist.</span><span class="sxs-lookup"><span data-stu-id="facce-292">Required.</span></span> <span data-ttu-id="facce-293">Hallo pad relatief toohello lokale resource toomonitor.</span><span class="sxs-lookup"><span data-stu-id="facce-293">hello path relative toohello local resource toomonitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="facce-294">PerformanceCounters Element</span><span class="sxs-lookup"><span data-stu-id="facce-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="facce-295">Hallo pad toohello prestaties teller toocollect definieert.</span><span class="sxs-lookup"><span data-stu-id="facce-295">Defines hello path toohello performance counter toocollect.</span></span>

 <span data-ttu-id="facce-296">Bovenliggend Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="facce-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="facce-297">Kenmerken:</span><span class="sxs-lookup"><span data-stu-id="facce-297">Attributes:</span></span>  

|<span data-ttu-id="facce-298">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="facce-298">Attribute</span></span>|<span data-ttu-id="facce-299">Type</span><span class="sxs-lookup"><span data-stu-id="facce-299">Type</span></span>|<span data-ttu-id="facce-300">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="facce-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="facce-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="facce-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="facce-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="facce-302">unsignedInt</span></span>|<span data-ttu-id="facce-303">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-303">Optional.</span></span> <span data-ttu-id="facce-304">Hallo maximum hoeveelheid system bestandsopslag die beschikbaar is voor Hallo opgegeven gegevens.</span><span class="sxs-lookup"><span data-stu-id="facce-304">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="facce-305">Hallo standaardwaarde is 0.</span><span class="sxs-lookup"><span data-stu-id="facce-305">hello default is 0.</span></span>|  
|<span data-ttu-id="facce-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="facce-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="facce-307">Duur</span><span class="sxs-lookup"><span data-stu-id="facce-307">duration</span></span>|<span data-ttu-id="facce-308">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-308">Optional.</span></span> <span data-ttu-id="facce-309">Hiermee geeft u hello-interval tussen de geplande overdrachten van gegevens, afgerond toohello dichtstbijzijnde minuut.</span><span class="sxs-lookup"><span data-stu-id="facce-309">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="facce-310">Hallo standaardwaarde is PT0S.</span><span class="sxs-lookup"><span data-stu-id="facce-310">hello default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="facce-311">PerformanceCounterConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="facce-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="facce-312">Hallo prestaties teller toocollect definieert.</span><span class="sxs-lookup"><span data-stu-id="facce-312">Defines hello performance counter toocollect.</span></span>

 <span data-ttu-id="facce-313">Bovenliggend Element: [PerformanceCounters Element](#PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="facce-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="facce-314">Kenmerken:</span><span class="sxs-lookup"><span data-stu-id="facce-314">Attributes:</span></span>  

|<span data-ttu-id="facce-315">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="facce-315">Attribute</span></span>|<span data-ttu-id="facce-316">Type</span><span class="sxs-lookup"><span data-stu-id="facce-316">Type</span></span>|<span data-ttu-id="facce-317">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="facce-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="facce-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="facce-318">**counterSpecifier**</span></span>|<span data-ttu-id="facce-319">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="facce-319">string</span></span>|<span data-ttu-id="facce-320">Vereist.</span><span class="sxs-lookup"><span data-stu-id="facce-320">Required.</span></span> <span data-ttu-id="facce-321">Hallo pad toohello prestaties teller toocollect.</span><span class="sxs-lookup"><span data-stu-id="facce-321">hello path toohello performance counter toocollect.</span></span>|  
|<span data-ttu-id="facce-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="facce-322">**sampleRate**</span></span>|<span data-ttu-id="facce-323">Duur</span><span class="sxs-lookup"><span data-stu-id="facce-323">duration</span></span>|<span data-ttu-id="facce-324">Vereist.</span><span class="sxs-lookup"><span data-stu-id="facce-324">Required.</span></span> <span data-ttu-id="facce-325">Hallo snelheid welke Hallo prestatiemeteritem moet worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="facce-325">hello rate at which hello performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="facce-326">WindowsEventLog Element</span><span class="sxs-lookup"><span data-stu-id="facce-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="facce-327">Hallo gebeurtenislogboeken toomonitor definieert.</span><span class="sxs-lookup"><span data-stu-id="facce-327">Defines hello event logs toomonitor.</span></span>

 <span data-ttu-id="facce-328">Bovenliggend Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="facce-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="facce-329">Kenmerken:</span><span class="sxs-lookup"><span data-stu-id="facce-329">Attributes:</span></span>

|<span data-ttu-id="facce-330">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="facce-330">Attribute</span></span>|<span data-ttu-id="facce-331">Type</span><span class="sxs-lookup"><span data-stu-id="facce-331">Type</span></span>|<span data-ttu-id="facce-332">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="facce-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="facce-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="facce-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="facce-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="facce-334">unsignedInt</span></span>|<span data-ttu-id="facce-335">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-335">Optional.</span></span> <span data-ttu-id="facce-336">Hallo maximum hoeveelheid system bestandsopslag die beschikbaar is voor Hallo opgegeven gegevens.</span><span class="sxs-lookup"><span data-stu-id="facce-336">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="facce-337">Hallo standaardwaarde is 0.</span><span class="sxs-lookup"><span data-stu-id="facce-337">hello default is 0.</span></span>|  
|<span data-ttu-id="facce-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="facce-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="facce-339">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="facce-339">string</span></span>|<span data-ttu-id="facce-340">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-340">Optional.</span></span> <span data-ttu-id="facce-341">Hiermee geeft u een minimale ernstniveau Hallo voor logboekvermeldingen die worden overgedragen.</span><span class="sxs-lookup"><span data-stu-id="facce-341">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="facce-342">de standaardwaarde Hallo is **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="facce-342">hello default value is **Undefined**.</span></span> <span data-ttu-id="facce-343">Andere mogelijke waarden zijn **uitgebreid**, **informatie**, **waarschuwing**, **fout**, en **Kritiek**.</span><span class="sxs-lookup"><span data-stu-id="facce-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="facce-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="facce-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="facce-345">Duur</span><span class="sxs-lookup"><span data-stu-id="facce-345">duration</span></span>|<span data-ttu-id="facce-346">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="facce-346">Optional.</span></span> <span data-ttu-id="facce-347">Hiermee geeft u hello-interval tussen de geplande overdrachten van gegevens, afgerond toohello dichtstbijzijnde minuut.</span><span class="sxs-lookup"><span data-stu-id="facce-347">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="facce-348">Hallo standaardwaarde is PT0S.</span><span class="sxs-lookup"><span data-stu-id="facce-348">hello default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="facce-349">DataSource-Element</span><span class="sxs-lookup"><span data-stu-id="facce-349">DataSource Element</span></span>  
 <span data-ttu-id="facce-350">Hallo gebeurtenislogboek toomonitor definieert.</span><span class="sxs-lookup"><span data-stu-id="facce-350">Defines hello event log toomonitor.</span></span>

 <span data-ttu-id="facce-351">Bovenliggend Element: [WindowsEventLog Element](#windowsEventLog).</span><span class="sxs-lookup"><span data-stu-id="facce-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="facce-352">Kenmerken:</span><span class="sxs-lookup"><span data-stu-id="facce-352">Attributes:</span></span>

|<span data-ttu-id="facce-353">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="facce-353">Attribute</span></span>|<span data-ttu-id="facce-354">Type</span><span class="sxs-lookup"><span data-stu-id="facce-354">Type</span></span>|<span data-ttu-id="facce-355">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="facce-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="facce-356">**naam**</span><span class="sxs-lookup"><span data-stu-id="facce-356">**name**</span></span>|<span data-ttu-id="facce-357">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="facce-357">string</span></span>|<span data-ttu-id="facce-358">Vereist.</span><span class="sxs-lookup"><span data-stu-id="facce-358">Required.</span></span> <span data-ttu-id="facce-359">Een XPath-expressie Hallo logboek toocollect opgeven.</span><span class="sxs-lookup"><span data-stu-id="facce-359">An XPath expression specifying hello log toocollect.</span></span>|  
