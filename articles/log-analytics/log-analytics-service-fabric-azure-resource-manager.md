---
title: Service Fabric-toepassingen met behulp van logboekanalyse aaaAssess hello Azure-portal | Microsoft Docs
description: U kunt Hallo Service Fabric oplossing gebruiken in hello Azure portal tooassess Hallo risico en status van uw Service Fabric-toepassingen met logboekanalyse micro-services, knooppunten en clusters.
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a><span data-ttu-id="dc34d-103">Evalueer Service Fabric-toepassingen en micro-services met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="dc34d-103">Assess Service Fabric applications and micro-services with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dc34d-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dc34d-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="dc34d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc34d-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Service Fabric symbool](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="dc34d-107">Dit artikel wordt beschreven hoe toouse Hallo Service Fabric-oplossing in logboekanalyse toohelp identificeren en oplossen van problemen in uw Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="dc34d-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="dc34d-108">Hallo Service Fabric-oplossing gebruikt Azure Diagnostics-gegevens van uw virtuele machines van Service Fabric door het verzamelen van deze gegevens uit uw af van de Azure-tabellen.</span><span class="sxs-lookup"><span data-stu-id="dc34d-108">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="dc34d-109">Log Analytics leest vervolgens de Service Fabric framework gebeurtenissen, met inbegrip van **betrouwbare servicegebeurtenissen**, **Actor gebeurtenissen**, **operationele gebeurtenissen**, en **aangepaste ETW-gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="dc34d-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="dc34d-110">Dashboard van de oplossing hello bent u problemen die aandacht vereisen kunnen tooview en relevante gebeurtenissen in uw omgeving Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="dc34d-110">With hello solution dashboard, you are able tooview notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="dc34d-111">tooget gestart met Hallo-oplossing, moet u tooconnect uw Service Fabric-werkruimte voor logboekanalyse cluster tooa.</span><span class="sxs-lookup"><span data-stu-id="dc34d-111">tooget started with hello solution, you need tooconnect your Service Fabric cluster tooa Log Analytics workspace.</span></span> <span data-ttu-id="dc34d-112">Hier volgen drie scenario's tooconsider:</span><span class="sxs-lookup"><span data-stu-id="dc34d-112">Here are three scenarios tooconsider:</span></span>

1. <span data-ttu-id="dc34d-113">Als u uw Service Fabric-cluster niet hebt geïmplementeerd, gebruikt u de stappen Hallo in ***implementeren van een werkruimte voor logboekanalyse tooa Service Fabric-Cluster aangesloten*** toodeploy een nieuw cluster en hebt geconfigureerd tooreport tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="dc34d-113">If you have not deployed your Service Fabric cluster, use hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace*** toodeploy a new cluster and have it configured tooreport tooLog Analytics.</span></span>
2. <span data-ttu-id="dc34d-114">Als u toocollect prestatiemeteritems uit uw hosts toouse andere OMS-oplossingen zoals beveiliging op uw Service Fabric-Cluster moet, stappen Hallo in ***implementeren van een werkruimte voor logboekanalyse tooa Service Fabric-Cluster verbonden met het VM-extensie geïnstalleerd.***</span><span class="sxs-lookup"><span data-stu-id="dc34d-114">If you need toocollect performance counters from your hosts toouse other OMS solutions such as Security on your Service Fabric Cluster, follow hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="dc34d-115">Als u al uw Service Fabric-cluster hebt geïmplementeerd en tooconnect wilt het tooLog Analytics, Hallo stappen in ***toevoegen van een bestaande opslag account tooLog Analytics.***</span><span class="sxs-lookup"><span data-stu-id="dc34d-115">If you have already deployed your Service Fabric cluster and want tooconnect it tooLog Analytics, follow hello steps in ***Adding an existing storage account tooLog Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a><span data-ttu-id="dc34d-116">Implementeer een werkruimte voor logboekanalyse tooa Service Fabric-Cluster is verbonden.</span><span class="sxs-lookup"><span data-stu-id="dc34d-116">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace.</span></span>
<span data-ttu-id="dc34d-117">Deze sjabloon Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="dc34d-117">This template does hello following:</span></span>

1. <span data-ttu-id="dc34d-118">Een Azure Service Fabric-werkruimte voor logboekanalyse cluster al verbonden tooa implementeert.</span><span class="sxs-lookup"><span data-stu-id="dc34d-118">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="dc34d-119">U hebt een nieuwe werkruimte Hallo optie toocreate tijdens het Hallo-sjabloon of invoer Hallo-naam van een bestaande werkruimte voor logboekanalyse implementeren.</span><span class="sxs-lookup"><span data-stu-id="dc34d-119">You have hello option toocreate a new workspace while deploying hello template, or input hello name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="dc34d-120">Werkruimte voor logboekanalyse van Hallo diagnostische storage account toohello toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="dc34d-120">Adds hello diagnostic storage account toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="dc34d-121">Hiermee schakelt u Hallo Service Fabric-oplossing in de werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="dc34d-121">Enables hello Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="dc34d-122">[![TooAzure implementeren](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="dc34d-122">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="dc34d-123">Als u hebt geselecteerd wordt Hallo hierboven op de knop implementeren, hello Azure portal wordt geopend met de parameters voor u tooedit.</span><span class="sxs-lookup"><span data-stu-id="dc34d-123">Once you select hello deploy button above, hello Azure portal opens with parameters for you tooedit.</span></span> <span data-ttu-id="dc34d-124">Worden toocreate ervoor een nieuwe resourcegroep als invoer van de naam van een nieuwe Log Analytics-werkruimte:</span><span class="sxs-lookup"><span data-stu-id="dc34d-124">Be sure toocreate a new resource group if you input a new Log Analytics workspace name:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="dc34d-127">Accepteer de juridische voorwaarden Hallo en klik op **maken** toostart Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="dc34d-127">Accept hello legal terms and click **Create** toostart hello deployment.</span></span> <span data-ttu-id="dc34d-128">Zodra het Hallo-implementatie is voltooid, moet u nieuwe werkruimte Hallo en cluster gemaakt zien en Hallo WADServiceFabric * gebeurtenissen, WADWindowsEventLogs en WADETWEvent tabellen die zijn toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="dc34d-128">Once hello deployment is completed, you should see hello new workspace and cluster created, and hello WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="dc34d-130">Implementeer een werkruimte voor logboekanalyse tooa Service Fabric-Cluster verbonden met VM-extensie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="dc34d-130">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="dc34d-131">Deze sjabloon Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="dc34d-131">This template does hello following:</span></span>

1. <span data-ttu-id="dc34d-132">Een Azure Service Fabric-werkruimte voor logboekanalyse cluster al verbonden tooa implementeert.</span><span class="sxs-lookup"><span data-stu-id="dc34d-132">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="dc34d-133">U kunt een nieuwe werkruimte maken of een bestaande gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dc34d-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="dc34d-134">Werkruimte voor logboekanalyse van Hallo diagnostische storage accounts toohello toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="dc34d-134">Adds hello diagnostic storage accounts toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="dc34d-135">Hiermee schakelt u Hallo Service Fabric-oplossing in de werkruimte voor logboekanalyse Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc34d-135">Enables hello Service Fabric solution in hello Log Analytics workspace.</span></span>
4. <span data-ttu-id="dc34d-136">Hallo MMA agentextensie installeert in elke virtuele-machineschaalset ingesteld in het Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="dc34d-136">Installs hello MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="dc34d-137">Hallo MMA agent is geïnstalleerd, bent u maatstaven voor prestaties kunnen tooview over uw knooppunten.</span><span class="sxs-lookup"><span data-stu-id="dc34d-137">With hello MMA agent installed, you are able tooview performance metrics about your nodes.</span></span>

<span data-ttu-id="dc34d-138">[![TooAzure implementeren](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="dc34d-138">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="dc34d-139">Hieronder worden dezelfde stappen hierboven benodigde parameters op invoer Hallo Hallo en ere van een implementatie.</span><span class="sxs-lookup"><span data-stu-id="dc34d-139">Following hello same steps above, input hello necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="dc34d-140">Weer ziet u de nieuwe werkruimte hello, cluster en af tabellen alle gemaakte:</span><span class="sxs-lookup"><span data-stu-id="dc34d-140">Once again you should see hello new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="dc34d-142">Weergeven van prestatiegegevens</span><span class="sxs-lookup"><span data-stu-id="dc34d-142">Viewing Performance Data</span></span>

<span data-ttu-id="dc34d-143">tooview prestatiegegevens van de knooppunten:</span><span class="sxs-lookup"><span data-stu-id="dc34d-143">tooview Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="dc34d-144">Start Hallo werkruimte voor logboekanalyse van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="dc34d-144">Launch hello Log Analytics workspace from hello Azure portal.</span></span>
  <span data-ttu-id="dc34d-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="dc34d-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="dc34d-146">TooSettings gaat op Hallo linkerdeelvenster en selecteer gegevens >> Windows-prestatiemeteritems >> 'hello toevoegen geselecteerd prestatiemeteritems': ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="dc34d-146">Go tooSettings on hello left pane, and select Data >> Windows Performance Counters >> "Add hello selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="dc34d-147">In logboek zoeken, gebruikt u Hallo toodelve query's in de belangrijkste metrische gegevens over uw knooppunten te volgen:</span><span class="sxs-lookup"><span data-stu-id="dc34d-147">In Log Search, use hello following queries toodelve into key metrics about your nodes:</span></span>

    <span data-ttu-id="dc34d-148">a.</span><span class="sxs-lookup"><span data-stu-id="dc34d-148">a.</span></span> <span data-ttu-id="dc34d-149">Vergelijken gemiddelde CPU-gebruik op alle knooppunten in Hallo laatste één uur toosee welke knooppunten hebben problemen met het Hallo en met welke tijdsinterval een knooppunt dat opnieuw moest een piek:</span><span class="sxs-lookup"><span data-stu-id="dc34d-149">Compare hello average CPU Utilization across all your nodes in hello last one hour toosee which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="dc34d-151">b.</span><span class="sxs-lookup"><span data-stu-id="dc34d-151">b.</span></span> <span data-ttu-id="dc34d-152">Vergelijkbare lijndiagrammen voor het beschikbare geheugen op elk knooppunt in deze query weergeven:</span><span class="sxs-lookup"><span data-stu-id="dc34d-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="dc34d-153">een lijst met alle knooppunten, waarbij Hallo exacte gemiddelde waarde voor beschikbare megabytes (MB) voor elk knooppunt tooview Gebruik deze query:</span><span class="sxs-lookup"><span data-stu-id="dc34d-153">tooview a listing of all your nodes, showing hello exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="dc34d-155">c.</span><span class="sxs-lookup"><span data-stu-id="dc34d-155">c.</span></span> <span data-ttu-id="dc34d-156">In geval van Hallo gewenste toodrill omlaag in een specifiek knooppunt door in elk uur gemiddelde hello, minimum, maximum en 75 percentiel CPU-gebruik, je kunt toodo dit door met behulp van deze query (vervangen veld Computer):</span><span class="sxs-lookup"><span data-stu-id="dc34d-156">In hello case that you want toodrill down into a specific node by examining hello hourly average, minimum, maximum and 75-percentile CPU usage, you're able toodo this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="dc34d-158">Meer informatie lezen over maatstaven voor prestaties in logboekanalyse op Hallo [Operations Management Suite-blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span><span class="sxs-lookup"><span data-stu-id="dc34d-158">Read more information about performance metrics in Log Analytics at hello [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-toolog-analytics"></a><span data-ttu-id="dc34d-159">Toevoegen van een bestaande opslag account tooLog Analytics</span><span class="sxs-lookup"><span data-stu-id="dc34d-159">Adding an existing storage account tooLog Analytics</span></span>

<span data-ttu-id="dc34d-160">Deze sjabloon wordt gewoon de bestaande opslag accounts tooa nieuwe of bestaande werkruimte voor logboekanalyse toevoegen</span><span class="sxs-lookup"><span data-stu-id="dc34d-160">This template simply adds your existing storage accounts tooa new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="dc34d-161">[![TooAzure implementeren](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="dc34d-161">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="dc34d-162">Als u met een bestaande werkruimte voor logboekanalyse werkt, selecteert u bij het selecteren van een resourcegroep 'Bestaande gebruiken' en zoek naar de resourcegroep Hallo met Hallo Log Analytics-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="dc34d-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for hello resource group containing hello Log Analytics workspace.</span></span> <span data-ttu-id="dc34d-163">Maak een nieuwe één als anders.</span><span class="sxs-lookup"><span data-stu-id="dc34d-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="dc34d-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="dc34d-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="dc34d-165">Nadat u deze sjabloon is geïmplementeerd, kunt u zich kunt toosee Hallo storage account verbonden tooyour logboekanalyse werkruimte.</span><span class="sxs-lookup"><span data-stu-id="dc34d-165">After this template has been deployed, you will be able toosee hello storage account connected tooyour Log Analytics workspace.</span></span> <span data-ttu-id="dc34d-166">In dit exemplaar toegevoegd ik een meer storage account toohello Exchange werkruimte ik die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="dc34d-166">In this instance, I added one more storage account toohello Exchange workspace I created above.</span></span>
<span data-ttu-id="dc34d-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="dc34d-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="dc34d-168">Service Fabric-gebeurtenissen weergeven</span><span class="sxs-lookup"><span data-stu-id="dc34d-168">View Service Fabric events</span></span>

<span data-ttu-id="dc34d-169">Eenmaal Hallo implementaties zijn voltooid en Hallo Service Fabric-oplossing in uw werkruimte is ingeschakeld, selecteert u Hallo **Service Fabric** -tegel in Hallo logboekanalyse portal toolaunch Hallo Service Fabric dashboard.</span><span class="sxs-lookup"><span data-stu-id="dc34d-169">Once hello deployments are completed and hello Service Fabric solution has been enabled in your workspace, select hello **Service Fabric** tile in hello Log Analytics portal toolaunch hello Service Fabric dashboard.</span></span> <span data-ttu-id="dc34d-170">Hallo dashboard bevat Hallo kolommen in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc34d-170">hello dashboard includes hello columns in hello following table.</span></span> <span data-ttu-id="dc34d-171">Elke kolom bevat Hallo bovenste 10 gebeurtenissen door het aantal die overeenkomt met dat van de kolom criteria voor Hallo tijdbereik opgegeven.</span><span class="sxs-lookup"><span data-stu-id="dc34d-171">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="dc34d-172">U kunt een zoekopdracht logboek waarmee de volledige lijst Hallo door te klikken op uitvoeren **alle** onderin Hallo rechts van elke kolom, of door te klikken op de kolomkop Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc34d-172">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="dc34d-173">**Service Fabric-gebeurtenis**</span><span class="sxs-lookup"><span data-stu-id="dc34d-173">**Service Fabric event**</span></span> | <span data-ttu-id="dc34d-174">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="dc34d-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="dc34d-175">Problemen die aandacht vereisen</span><span class="sxs-lookup"><span data-stu-id="dc34d-175">Notable Issues</span></span> |<span data-ttu-id="dc34d-176">Een weergave van de problemen zoals RunAsyncFailures RunAsynCancellations en keuzelijsten knooppunt.</span><span class="sxs-lookup"><span data-stu-id="dc34d-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="dc34d-177">Operationele gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="dc34d-177">Operational Events</span></span> |<span data-ttu-id="dc34d-178">Operationele gebeurtenissen zoals upgrade van de toepassing en implementaties aandacht vereisen.</span><span class="sxs-lookup"><span data-stu-id="dc34d-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="dc34d-179">Gebeurtenissen van betrouwbare Service</span><span class="sxs-lookup"><span data-stu-id="dc34d-179">Reliable Service Events</span></span> |<span data-ttu-id="dc34d-180">Opmerkelijke betrouwbare servicegebeurtenissen dergelijke Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="dc34d-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="dc34d-181">Actor-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="dc34d-181">Actor Events</span></span> |<span data-ttu-id="dc34d-182">Opmerkelijke actor-gebeurtenissen die worden gegenereerd door uw micro-services, zoals uitzonderingen worden veroorzaakt door een actormethode, actor-activeringen en deactivations, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="dc34d-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="dc34d-183">Toepassingsgebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="dc34d-183">Application Events</span></span> |<span data-ttu-id="dc34d-184">Alle aangepaste ETW-gebeurtenissen die worden gegenereerd door uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="dc34d-184">All custom ETW events generated by your applications.</span></span> |

![Service Fabric-dashboard](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric-dashboard](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="dc34d-187">Hallo volgende tabel bevat de methoden van de collectie en andere informatie over hoe gegevens worden verzameld voor Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="dc34d-187">hello following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="dc34d-188">Platform</span><span class="sxs-lookup"><span data-stu-id="dc34d-188">platform</span></span> | <span data-ttu-id="dc34d-189">Directe Agent</span><span class="sxs-lookup"><span data-stu-id="dc34d-189">Direct Agent</span></span> | <span data-ttu-id="dc34d-190">Operations Manager-agent</span><span class="sxs-lookup"><span data-stu-id="dc34d-190">Operations Manager agent</span></span> | <span data-ttu-id="dc34d-191">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="dc34d-191">Azure Storage</span></span> | <span data-ttu-id="dc34d-192">Operations Manager is vereist?</span><span class="sxs-lookup"><span data-stu-id="dc34d-192">Operations Manager required?</span></span> | <span data-ttu-id="dc34d-193">Operations Manager-agent gegevens verzonden via de beheergroep</span><span class="sxs-lookup"><span data-stu-id="dc34d-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="dc34d-194">Frequentie van de verzameling</span><span class="sxs-lookup"><span data-stu-id="dc34d-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="dc34d-195">Windows</span><span class="sxs-lookup"><span data-stu-id="dc34d-195">Windows</span></span> |  |  | <span data-ttu-id="dc34d-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="dc34d-196">&#8226;</span></span> |  |  |<span data-ttu-id="dc34d-197">10 minuten</span><span class="sxs-lookup"><span data-stu-id="dc34d-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="dc34d-198">U kunt Hallo bereik van deze gebeurtenissen in Service Fabric-oplossing Hallo wijzigen door te klikken op **gegevens op basis van de afgelopen 7 dagen** Hallo boven aan het Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="dc34d-198">You can change hello scope of these events in hello Service Fabric solution by clicking **Data based on last 7 days** at hello top of hello dashboard.</span></span> <span data-ttu-id="dc34d-199">U kunt ook gebeurtenissen gegenereerd binnen Hallo afgelopen zeven dagen een dag of zes uur weergeven.</span><span class="sxs-lookup"><span data-stu-id="dc34d-199">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="dc34d-200">U kunt ook selecteren **aangepaste** toospecify een aangepast datumbereik.</span><span class="sxs-lookup"><span data-stu-id="dc34d-200">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="dc34d-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dc34d-201">Next steps</span></span>

* <span data-ttu-id="dc34d-202">Gebruik [logboek van zoekopdrachten in logboekanalyse](log-analytics-log-searches.md) tooview gedetailleerde gegevens voor Service Fabric-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dc34d-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
