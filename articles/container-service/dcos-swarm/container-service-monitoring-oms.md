---
title: aaaMonitor Azure DC/OS-cluster - Operations Management | Microsoft Docs
description: Een Azure Container Service DC/OS-cluster met de Microsoft Operations Management Suite bewaken.
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="a5797-103">Monitor voor een Azure Container Service DC/OS-cluster met Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="a5797-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="a5797-104">Microsoft Operations Management Suite (OMS) is een cloudoplossing voor IT-beheer van Microsoft waarmee u uw on-premises en cloudinfrastructuur kunt beheren en beveiligen.</span><span class="sxs-lookup"><span data-stu-id="a5797-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="a5797-105">Container oplossing is een oplossing in OMS Log Analytics, waardoor u inventaris weergeven Hallo-container, prestaties en logboeken op één locatie.</span><span class="sxs-lookup"><span data-stu-id="a5797-105">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="a5797-106">U kunt controleren, containers oplossen door bekijkt hello Logboeken in de centrale locatie en veel ruis veroorzaken verbruikt overtollige container op een host vinden.</span><span class="sxs-lookup"><span data-stu-id="a5797-106">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="a5797-107">Raadpleeg voor meer informatie over de oplossing Container toothe [Container oplossing Log Analytics](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="a5797-107">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-hello-dcos-universe"></a><span data-ttu-id="a5797-108">Instellen van OMS uit Hallo DC/OS universe</span><span class="sxs-lookup"><span data-stu-id="a5797-108">Setting up OMS from hello DC/OS universe</span></span>


<span data-ttu-id="a5797-109">In dit artikel wordt ervan uitgegaan dat u een DC/OS hebt ingesteld en eenvoudige web containertoepassingen op Hallo cluster hebt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a5797-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on hello cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="a5797-110">Vereiste</span><span class="sxs-lookup"><span data-stu-id="a5797-110">Pre-requisite</span></span>
- <span data-ttu-id="a5797-111">[Microsoft Azure-abonnement](https://azure.microsoft.com/free/) -u kunt dit gratis ophalen.</span><span class="sxs-lookup"><span data-stu-id="a5797-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="a5797-112">Setup van Microsoft OMS-werkruimte - Zie 'Stap 3' hieronder</span><span class="sxs-lookup"><span data-stu-id="a5797-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="a5797-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a5797-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="a5797-114">Hallo DC/OS-dashboard, klik op Universe en zoek naar OMS zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a5797-114">In hello DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="a5797-115">Klik op **Install**.</span><span class="sxs-lookup"><span data-stu-id="a5797-115">Click **Install**.</span></span> <span data-ttu-id="a5797-116">U ziet een pop up met Hallo OMS versie-informatie en een **pakket installeren** of **installatie in de geavanceerde** knop.</span><span class="sxs-lookup"><span data-stu-id="a5797-116">You will see a pop up with hello OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="a5797-117">Wanneer u klikt op **installatie in de geavanceerde**, die leidt u toohello **OMS specifieke configuratie-eigenschappen** pagina.</span><span class="sxs-lookup"><span data-stu-id="a5797-117">When you click **Advanced Installation**, which leads you toohello **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="a5797-118">Hier wordt u gevraagd tooenter hello `wsid` (Hallo OMS-werkruimte-ID) en `wskey` (Hallo OMS primaire sleutel voor Hallo werkruimte-id).</span><span class="sxs-lookup"><span data-stu-id="a5797-118">Here, you will be asked tooenter hello `wsid` (hello OMS workspace ID) and `wskey` (hello OMS primary key for hello workspace id).</span></span> <span data-ttu-id="a5797-119">beide tooget `wsid` en `wskey` u toocreate moet een OMS-account bij <https://mms.microsoft.com>. Volg Hallo stappen toocreate een account.</span><span class="sxs-lookup"><span data-stu-id="a5797-119">tooget both `wsid` and `wskey` you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="a5797-120">Wanneer u klaar bent met het Hallo-account maken, moet u tooobtain uw `wsid` en `wskey` door te klikken op **instellingen**, klikt u vervolgens **verbonden bronnen**, en vervolgens **Linux-Servers** , zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a5797-120">Once you are done creating hello account, you need tooobtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="a5797-121">Hallo nummer u OMS exemplaren selecteren dat u wilt en klik op de knop 'Bekijken en installeren' Hallo.</span><span class="sxs-lookup"><span data-stu-id="a5797-121">Select hello number you OMS instances that you want and click hello ‘Review and Install’ button.</span></span> <span data-ttu-id="a5797-122">Meestal zult u toohave Hallo aantal OMS exemplaren gelijk toohello van de virtuele machine hebt u in uw cluster agent.</span><span class="sxs-lookup"><span data-stu-id="a5797-122">Typically, you will want toohave hello number of OMS instances equal toohello number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="a5797-123">OMS-Agent voor Linux is geïnstalleerd als afzonderlijke containers op elke VM die deze wil toocollect informatie voor de controle en logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="a5797-123">OMS Agent for Linux is installs as individual containers on each VM that it wants toocollect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="a5797-124">Instellen van een eenvoudige OMS-dashboard</span><span class="sxs-lookup"><span data-stu-id="a5797-124">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="a5797-125">Zodra u Hallo OMS-Agent voor Linux op Hallo virtuele machines hebt geïnstalleerd, wordt in het volgende stap tooset up Hallo OMS dashboard is.</span><span class="sxs-lookup"><span data-stu-id="a5797-125">Once you have installed hello OMS Agent for Linux on hello VMs, next step is tooset up hello OMS dashboard.</span></span> <span data-ttu-id="a5797-126">Er zijn van twee manieren toodo dit: OMS-Portal of Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="a5797-126">There are two ways toodo this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="a5797-127">OMS-Portal</span><span class="sxs-lookup"><span data-stu-id="a5797-127">OMS Portal</span></span> 

<span data-ttu-id="a5797-128">Meld u bij toohello OMS-portal (<https://mms.microsoft.com>) en ga toohello **oplossing galerie**.</span><span class="sxs-lookup"><span data-stu-id="a5797-128">Log in toohello OMS portal (<https://mms.microsoft.com>) and go toohello **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="a5797-129">Wanneer u naar Hallo **oplossing galerie**, selecteer **Containers**.</span><span class="sxs-lookup"><span data-stu-id="a5797-129">Once you are in hello **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="a5797-130">Wanneer u Hallo Container oplossing hebt geselecteerd, worden er Hallo tegel op Hallo OMS overzicht dashboardpagina.</span><span class="sxs-lookup"><span data-stu-id="a5797-130">Once you’ve selected hello Container Solution, you will see hello tile on hello OMS Overview Dashboard page.</span></span> <span data-ttu-id="a5797-131">Nadat de containergegevens Hallo ingenomen is geïndexeerd, ziet u Hallo tegel ingevuld met informatie over de oplossing weergeven tegels.</span><span class="sxs-lookup"><span data-stu-id="a5797-131">Once hello ingested container data is indexed, you will see hello tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="a5797-132">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a5797-132">Azure Portal</span></span> 

<span data-ttu-id="a5797-133">Aanmelding tooAzure portal op <https://portal.microsoft.com/>.</span><span class="sxs-lookup"><span data-stu-id="a5797-133">Login tooAzure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="a5797-134">Ga naar **Marketplace**, selecteer **bewaking + management** en klik op **alle Zie**.</span><span class="sxs-lookup"><span data-stu-id="a5797-134">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="a5797-135">Typ vervolgens `containers` in de zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="a5797-135">Then Type `containers` in search.</span></span> <span data-ttu-id="a5797-136">U ziet in de zoekresultaten Hallo ' containers'.</span><span class="sxs-lookup"><span data-stu-id="a5797-136">You will see "containers" in hello search results.</span></span> <span data-ttu-id="a5797-137">Selecteer **Containers** en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="a5797-137">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="a5797-138">Nadat u op **maken**, wordt u gevraagt voor uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="a5797-138">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="a5797-139">Selecteer uw werkruimte of als u geen abonnement hebt, maakt u een nieuwe werkruimte.</span><span class="sxs-lookup"><span data-stu-id="a5797-139">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="a5797-140">Nadat u uw werkruimte hebt geselecteerd, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="a5797-140">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="a5797-141">Raadpleeg voor meer informatie over Hallo OMS Container oplossing toothe [Container oplossing Log Analytics](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="a5797-141">For more information about hello OMS Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a><span data-ttu-id="a5797-142">Hoe tooscale OMS-Agent met ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="a5797-142">How tooscale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="a5797-143">Als u toohave geïnstalleerd OMS-agent niet genoeg Hallo werkelijke infrastructuurmanifest moet of u VMSS zijn schaalt door meer VM toe te voegen, kunt u doen door te schalen Hallo `msoms` service.</span><span class="sxs-lookup"><span data-stu-id="a5797-143">In case you need toohave installed OMS agent short of hello actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling hello `msoms` service.</span></span>

<span data-ttu-id="a5797-144">Ga tooMarathon of Hallo Services voor DC/OS-gebruikersinterface tabblad en het aantal knooppunten opschalen.</span><span class="sxs-lookup"><span data-stu-id="a5797-144">You can either go tooMarathon or hello DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="a5797-145">Hiermee implementeert u tooother knooppunten die nog niet zijn geïmplementeerd op Hallo OMS-agent.</span><span class="sxs-lookup"><span data-stu-id="a5797-145">This will deploy tooother nodes which have not yet deployed hello OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="a5797-146">MS OMS verwijderen</span><span class="sxs-lookup"><span data-stu-id="a5797-146">Uninstall MS OMS</span></span>

<span data-ttu-id="a5797-147">toouninstall MS OMS Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a5797-147">toouninstall MS OMS enter hello following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="a5797-148">Laat ons weten.</span><span class="sxs-lookup"><span data-stu-id="a5797-148">Let us know!!!</span></span>
<span data-ttu-id="a5797-149">Wat werkt?</span><span class="sxs-lookup"><span data-stu-id="a5797-149">What works?</span></span> <span data-ttu-id="a5797-150">Wat ontbreekt?</span><span class="sxs-lookup"><span data-stu-id="a5797-150">What is missing?</span></span> <span data-ttu-id="a5797-151">Wat kan er anders moet u voor deze toobe nuttig voor u?</span><span class="sxs-lookup"><span data-stu-id="a5797-151">What else do you need for this toobe useful for you?</span></span> <span data-ttu-id="a5797-152">Laat ons weten op <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span><span class="sxs-lookup"><span data-stu-id="a5797-152">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5797-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a5797-153">Next steps</span></span>

 <span data-ttu-id="a5797-154">Nu dat u hebt ingesteld OMS toomonitor uw containers[uw dashboard container zien](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="a5797-154">Now that you have set up OMS toomonitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
