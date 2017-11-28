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
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a><span data-ttu-id="3cb67-103">Inschakelen van Azure Diagnostics in Azure-Cloudservices</span><span class="sxs-lookup"><span data-stu-id="3cb67-103">Enabling Azure Diagnostics in Azure Cloud Services</span></span>
<span data-ttu-id="3cb67-104">Zie [overzicht van Azure Diagnostics](../azure-diagnostics.md) voor de achtergrond op Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="3cb67-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a><span data-ttu-id="3cb67-105">Hoe diagnostische gegevens in een Werkrol tooEnable</span><span class="sxs-lookup"><span data-stu-id="3cb67-105">How tooEnable Diagnostics in a Worker Role</span></span>
<span data-ttu-id="3cb67-106">Dit scenario beschrijft hoe een Azure-werkrol die telemetrie gegevens met verzendt tooimplement Hallo EventSource .NET-klasse.</span><span class="sxs-lookup"><span data-stu-id="3cb67-106">This walkthrough describes how tooimplement an Azure worker role that emits telemetry data using hello .NET EventSource class.</span></span> <span data-ttu-id="3cb67-107">Azure Diagnostics is gebruikte toocollect hello telemetriegegevens en opslaan in een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="3cb67-107">Azure Diagnostics is used toocollect hello telemetry data and store it in an Azure storage account.</span></span> <span data-ttu-id="3cb67-108">Bij het maken van een werkrol kunt Visual Studio automatisch de Diagnostics 1.0 als onderdeel van de oplossing Hallo in Azure SDK voor .NET 2.4 en eerdere versies.</span><span class="sxs-lookup"><span data-stu-id="3cb67-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of hello solution in Azure SDKs for .NET 2.4 and earlier.</span></span> <span data-ttu-id="3cb67-109">Hallo beschrijven volgende instructies Hallo-proces voor het Hallo-werkrol, Hallo oplossing Diagnostics 1.0 uitschakelen en het implementeren van diagnostische gegevens 1.2 of 1.3 tooyour werkrol maken.</span><span class="sxs-lookup"><span data-stu-id="3cb67-109">hello following instructions describe hello process for creating hello worker role, disabling Diagnostics 1.0 from hello solution, and deploying Diagnostics 1.2 or 1.3 tooyour worker role.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3cb67-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3cb67-110">Prerequisites</span></span>
<span data-ttu-id="3cb67-111">In dit artikel wordt ervan uitgegaan dat u hebt een Azure-abonnement en gebruik van Visual Studio Hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="3cb67-111">This article assumes you have an Azure subscription and are using Visual Studio with hello Azure SDK.</span></span> <span data-ttu-id="3cb67-112">Als u niet een Azure-abonnement hebt, kunt u zich aanmeldt voor Hallo [gratis proefversie][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="3cb67-112">If you do not have an Azure subscription, you can sign up for hello [Free Trial][Free Trial].</span></span> <span data-ttu-id="3cb67-113">Zorg ervoor dat te[installeren en configureren van Azure PowerShell versie 0.8.7 of hoger][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="3cb67-113">Make sure too[Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-worker-role"></a><span data-ttu-id="3cb67-114">Stap 1: Een Werkrol maken</span><span class="sxs-lookup"><span data-stu-id="3cb67-114">Step 1: Create a Worker Role</span></span>
1. <span data-ttu-id="3cb67-115">Start **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="3cb67-115">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="3cb67-116">Maak een **Azure Cloud Service** project uit Hallo **Cloud** sjabloon die gericht is op .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="3cb67-116">Create an **Azure Cloud Service** project from hello **Cloud** template that targets .NET Framework 4.5.</span></span>  <span data-ttu-id="3cb67-117">Naam Hallo 'WadExample' project en klik op Ok.</span><span class="sxs-lookup"><span data-stu-id="3cb67-117">Name hello project "WadExample" and click Ok.</span></span>
3. <span data-ttu-id="3cb67-118">Selecteer **Werkrol** en klik op Ok.</span><span class="sxs-lookup"><span data-stu-id="3cb67-118">Select **Worker Role** and click Ok.</span></span> <span data-ttu-id="3cb67-119">Hallo-project wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3cb67-119">hello project will be created.</span></span>
4. <span data-ttu-id="3cb67-120">In **Solution Explorer**, dubbelklikt u op Hallo **WorkerRole1** eigenschappenbestand.</span><span class="sxs-lookup"><span data-stu-id="3cb67-120">In **Solution Explorer**, double-click hello **WorkerRole1** properties file.</span></span>
5. <span data-ttu-id="3cb67-121">In Hallo **configuratie** tabblad un selectievakje **diagnostische gegevens inschakelen** toodisable Diagnostics 1.0 (Azure SDK 2.4 en eerder).</span><span class="sxs-lookup"><span data-stu-id="3cb67-121">In hello **Configuration** tab, un-check **Enable Diagnostics** toodisable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span></span>
6. <span data-ttu-id="3cb67-122">Uw tooverify oplossing bouwen die u hebt geen fouten.</span><span class="sxs-lookup"><span data-stu-id="3cb67-122">Build your solution tooverify that you have no errors.</span></span>

### <a name="step-2-instrument-your-code"></a><span data-ttu-id="3cb67-123">Stap 2: Uw code softwareontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="3cb67-123">Step 2: Instrument your code</span></span>
<span data-ttu-id="3cb67-124">Hallo-inhoud van WorkerRole.cs vervangen door Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="3cb67-124">Replace hello contents of WorkerRole.cs with hello following code.</span></span> <span data-ttu-id="3cb67-125">klasse SampleEventSourceWriter, zijn overgenomen van Hallo Hallo [EventSource klasse][EventSource Class], implementeert vier logboekregistratiemethoden: **SendEnums**, **MessageMethod** , **SetOther** en **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="3cb67-125">hello class SampleEventSourceWriter, inherited from hello [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="3cb67-126">eerste parameter toohello Hallo **WriteEvent** methode Hallo-ID voor de betreffende gebeurtenis Hallo definieert.</span><span class="sxs-lookup"><span data-stu-id="3cb67-126">hello first parameter toohello **WriteEvent** method defines hello ID for hello respective event.</span></span> <span data-ttu-id="3cb67-127">Hallo Run-methode implementeert een oneindige lus die elk Hallo logboekregistratiemethoden die worden geïmplementeerd in Hallo aanroept **SampleEventSourceWriter** klasse elke 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="3cb67-127">hello Run method implements an infinite loop that calls each of hello logging methods implemented in hello **SampleEventSourceWriter** class every 10 seconds.</span></span>

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


### <a name="step-3-deploy-your-worker-role"></a><span data-ttu-id="3cb67-128">Stap 3: Uw Werkrol implementeren</span><span class="sxs-lookup"><span data-stu-id="3cb67-128">Step 3: Deploy your Worker Role</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. <span data-ttu-id="3cb67-129">Uw rol worker tooAzure uit vanuit Visual Studio implementeren door het selecteren van Hallo **WadExample** -project in Solution Explorer Hallo vervolgens **publiceren** van Hallo **bouwen** menu.</span><span class="sxs-lookup"><span data-stu-id="3cb67-129">Deploy your worker role tooAzure from within Visual Studio by selecting hello **WadExample** project in hello Solution Explorer then **Publish** from hello **Build** menu.</span></span>
2. <span data-ttu-id="3cb67-130">Kies uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="3cb67-130">Choose your subscription.</span></span>
3. <span data-ttu-id="3cb67-131">In Hallo **Microsoft Azure Publish Settings** dialoogvenster Selecteer **nieuwe maken...** .</span><span class="sxs-lookup"><span data-stu-id="3cb67-131">In hello **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span></span>
4. <span data-ttu-id="3cb67-132">In Hallo **Cloudservice maken en Storage-Account** dialoogvenster, voer een **naam** (bijvoorbeeld ' WadExample') en selecteer een regio of affiniteitsgroep.</span><span class="sxs-lookup"><span data-stu-id="3cb67-132">In hello **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span></span>
5. <span data-ttu-id="3cb67-133">Set Hallo **omgeving** te**fasering**.</span><span class="sxs-lookup"><span data-stu-id="3cb67-133">Set hello **Environment** too**Staging**.</span></span>
6. <span data-ttu-id="3cb67-134">Wijzigen van een andere **instellingen** als in de betreffende en klikt u op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="3cb67-134">Modify any other **Settings** as appropriate and click **Publish**.</span></span>
7. <span data-ttu-id="3cb67-135">Wanneer implementatie is voltooid, controleert u of in hello Azure-portal uw cloudservice is in een **met** status.</span><span class="sxs-lookup"><span data-stu-id="3cb67-135">After deployment has completed, verify in hello Azure portal that your cloud service is in a **Running** state.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a><span data-ttu-id="3cb67-136">Stap 4: Maken van uw configuratiebestand diagnostische gegevens en Hallo uitbreiding installeren</span><span class="sxs-lookup"><span data-stu-id="3cb67-136">Step 4: Create your Diagnostics configuration file and install hello extension</span></span>
1. <span data-ttu-id="3cb67-137">Hallo openbare configuratie bestand schemadefinitie downloaden door het uitvoeren van Hallo volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="3cb67-137">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. <span data-ttu-id="3cb67-138">Toevoegen van een XML-bestand tooyour **WorkerRole1** project door met de rechtermuisknop op Hallo **WorkerRole1** project en selecteer **toevoegen** -> **Nieuw Item...**</span><span class="sxs-lookup"><span data-stu-id="3cb67-138">Add an XML file tooyour **WorkerRole1** project by right-clicking on hello **WorkerRole1** project and select **Add** -> **New Item…**</span></span><span data-ttu-id="3cb67-139"> -> **Visual C# items** -> **gegevens** -> **XML-bestand**.</span><span class="sxs-lookup"><span data-stu-id="3cb67-139"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="3cb67-140">Hallo bestandsnaam 'WadExample.xml'.</span><span class="sxs-lookup"><span data-stu-id="3cb67-140">Name hello file "WadExample.xml".</span></span>

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. <span data-ttu-id="3cb67-142">Hallo WadConfig.xsd koppelen aan Hallo-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="3cb67-142">Associate hello WadConfig.xsd with hello configuration file.</span></span> <span data-ttu-id="3cb67-143">Zorg ervoor dat Hallo WadExample.xml editorvenster Hallo actieve venster.</span><span class="sxs-lookup"><span data-stu-id="3cb67-143">Make sure hello WadExample.xml editor window is hello active window.</span></span> <span data-ttu-id="3cb67-144">Druk op **F4** tooopen hello **eigenschappen** venster.</span><span class="sxs-lookup"><span data-stu-id="3cb67-144">Press **F4** tooopen hello **Properties** window.</span></span> <span data-ttu-id="3cb67-145">Klik op Hallo **schema's** eigenschap in Hallo **eigenschappen** venster.</span><span class="sxs-lookup"><span data-stu-id="3cb67-145">Click hello **Schemas** property in hello **Properties** window.</span></span> <span data-ttu-id="3cb67-146">Klik op Hallo **...**</span><span class="sxs-lookup"><span data-stu-id="3cb67-146">Click hello **…**</span></span> <span data-ttu-id="3cb67-147">in Hallo **schema's** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="3cb67-147">in hello **Schemas** property.</span></span> <span data-ttu-id="3cb67-148">Klik op Hallo **toevoegen...**</span><span class="sxs-lookup"><span data-stu-id="3cb67-148">Click hello **Add…**</span></span> <span data-ttu-id="3cb67-149">knop en navigeer toohello locatie waar u Hallo XSD-bestand en selecteer Hallo bestand WadConfig.xsd opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3cb67-149">button and navigate toohello location where you saved hello XSD file and select hello file WadConfig.xsd.</span></span> <span data-ttu-id="3cb67-150">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3cb67-150">Click **OK**.</span></span>

4. <span data-ttu-id="3cb67-151">Hallo-inhoud van Hallo WadExample.xml configuratiebestand vervangen Hello na XML en sla het Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="3cb67-151">Replace hello contents of hello WadExample.xml configuration file with hello following XML and save hello file.</span></span> <span data-ttu-id="3cb67-152">Dit configuratiebestand definieert een aantal prestaties tellers toocollect: één voor CPU-gebruik en één voor geheugengebruik.</span><span class="sxs-lookup"><span data-stu-id="3cb67-152">This configuration file defines a couple performance counters toocollect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="3cb67-153">Vervolgens definieert Hallo configuratie Hallo vier gebeurtenissen toohello methoden in Hallo SampleEventSourceWriter klasse overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="3cb67-153">Then hello configuration defines hello four events corresponding toohello methods in hello SampleEventSourceWriter class.</span></span>

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

### <a name="step-5-install-diagnostics-on-your-worker-role"></a><span data-ttu-id="3cb67-154">Stap 5: Diagnostische gegevens op uw Werkrol installeren</span><span class="sxs-lookup"><span data-stu-id="3cb67-154">Step 5: Install Diagnostics on your Worker Role</span></span>
<span data-ttu-id="3cb67-155">Hallo PowerShell-cmdlets voor het beheren van diagnostische gegevens op een web- of worker-rol zijn: Set-AzureServiceDiagnosticsExtension en Get-AzureServiceDiagnosticsExtension verwijderen AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="3cb67-155">hello PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span></span>

1. <span data-ttu-id="3cb67-156">Open Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3cb67-156">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="3cb67-157">Hallo script tooinstall diagnostische gegevens niet uitvoeren op uw werkrol (Vervang *StorageAccountKey* met Hallo-toegangssleutel voor uw opslagaccount wadexample en *config_path* met Hallo pad toohello *WadExample.xml* bestand):</span><span class="sxs-lookup"><span data-stu-id="3cb67-157">Execute hello script tooinstall Diagnostics on your worker role (replace *StorageAccountKey* with hello storage account key for your wadexample storage account and *config_path* with hello path toohello *WadExample.xml* file):</span></span>

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="3cb67-158">Stap 6: Bekijk de telemetrische gegevens</span><span class="sxs-lookup"><span data-stu-id="3cb67-158">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="3cb67-159">In Visual Studio Hallo **Server Explorer**, navigeer toohello wadexample storage-account.</span><span class="sxs-lookup"><span data-stu-id="3cb67-159">In hello Visual Studio **Server Explorer**, navigate toohello wadexample storage account.</span></span> <span data-ttu-id="3cb67-160">Nadat het Hallo-cloudservice is ongeveer vijf (5) minuten uitgevoerd, ziet u Hallo tabellen **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** en **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="3cb67-160">After hello cloud service has been running about five (5) minutes, you should see hello tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="3cb67-161">Dubbelklik op een Hallo tabellen tooview Hallo telemetrie die is verzameld.</span><span class="sxs-lookup"><span data-stu-id="3cb67-161">Double-click one of hello tables tooview hello telemetry that has been collected.</span></span>

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="3cb67-163">Schema van het configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="3cb67-163">Configuration File Schema</span></span>
<span data-ttu-id="3cb67-164">Hallo Diagnostics configuratiebestand definieert waarden die gebruikt tooinitialize diagnostische configuratie-instellingen zijn wanneer Hallo diagnostics agent wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="3cb67-164">hello Diagnostics configuration file defines values that are used tooinitialize diagnostic configuration settings when hello diagnostics agent starts.</span></span> <span data-ttu-id="3cb67-165">Zie Hallo [nieuwste schemaverwijzing](https://msdn.microsoft.com/library/azure/mt634524.aspx) voor geldige waarden en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="3cb67-165">See hello [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3cb67-166">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="3cb67-166">Troubleshooting</span></span>
<span data-ttu-id="3cb67-167">Als u problemen ondervindt, raadpleegt u [probleemoplossing Azure Diagnostics](../azure-diagnostics-troubleshooting.md) voor meer informatie over bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="3cb67-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cb67-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3cb67-168">Next Steps</span></span>
<span data-ttu-id="3cb67-169">[Een overzicht van verwante Azure virtuele machines diagnostische artikelen](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange Hallo gegevens verzamelt, oplossen van problemen of meer informatie over diagnostische gegevens over het algemeen.</span><span class="sxs-lookup"><span data-stu-id="3cb67-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange hello data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
