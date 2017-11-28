---
title: aaaDeploy Docker-container-cluster in Azure | Microsoft Docs
description: Een oplossing voor Kubernetes, DC/OS of Docker Swarm in Azure Container Service implementeren met behulp van hello Azure-portal of een Resource Manager-sjabloon.
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure, dcos, swarm, kubernetes, azure container service, acs
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 26e3a7d0af9d71acd8b5c85fd667fcf7d84cef66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-portal"></a><span data-ttu-id="0575a-104">Implementeert een Docker-container die als host fungeert voor oplossing met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="0575a-104">Deploy a Docker container hosting solution using hello Azure portal</span></span>



<span data-ttu-id="0575a-105">Azure Container Service biedt een snelle implementatie van populaire open-sourceoplossingen voor containerclustering en -orchestration.</span><span class="sxs-lookup"><span data-stu-id="0575a-105">Azure Container Service provides rapid deployment of popular open-source container clustering and orchestration solutions.</span></span> <span data-ttu-id="0575a-106">Dit document begeleidt u bij een Azure Container Service-cluster implementeren met behulp van hello Azure-portal of een snelstartsjabloon met de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0575a-106">This document walks you through deploying an Azure Container Service cluster by using hello Azure portal or an Azure Resource Manager quickstart template.</span></span> 

<span data-ttu-id="0575a-107">U kunt ook een Azure Container Service-cluster implementeren met behulp van Hallo [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) of hello Azure Container Service API's.</span><span class="sxs-lookup"><span data-stu-id="0575a-107">You can also deploy an Azure Container Service cluster by using hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) or hello Azure Container Service APIs.</span></span>

<span data-ttu-id="0575a-108">Zie [Kennismaking met Azure Container Service](../container-service-intro.md) voor achtergrondinformatie.</span><span class="sxs-lookup"><span data-stu-id="0575a-108">For background, see [Azure Container Service introduction](../container-service-intro.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0575a-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0575a-109">Prerequisites</span></span>

* <span data-ttu-id="0575a-110">**Azure-abonnement**: als u nog geen abonnement hebt, kunt u zich registreren voor een [gratis proefversie](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="0575a-110">**Azure subscription**: If you don't have one, sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> <span data-ttu-id="0575a-111">Voor een groter cluster kunt u een Betalen per gebruik-abonnement of andere aanschafopties overwegen.</span><span class="sxs-lookup"><span data-stu-id="0575a-111">For a larger cluster, consider a pay-as-you go subscription or other purchase options.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0575a-112">Het gebruik van uw Azure-abonnement en [resourcequota toe](../../azure-subscription-service-limits.md), zoals kernen quota, Hallo grootte van Hallo cluster die u implementeert kunt beperken.</span><span class="sxs-lookup"><span data-stu-id="0575a-112">Your Azure subscription usage and [resource quotas](../../azure-subscription-service-limits.md), such as cores quotas, can limit hello size of hello cluster you deploy.</span></span> <span data-ttu-id="0575a-113">toorequest een verhoging van het quotum, open een [online klant ondersteuningsaanvraag](../../azure-supportability/how-to-create-azure-support-request.md) zonder kosten.</span><span class="sxs-lookup"><span data-stu-id="0575a-113">toorequest a quota increase, open an [online customer support request](../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
    >

* <span data-ttu-id="0575a-114">**Openbare SSH-RSA-sleutel**: bij het implementeren via het Hallo-portal of een van de Azure-snelstartsjablonen hello, moet u tooprovide Hallo openbare sleutel voor verificatie met een Azure Container Service virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="0575a-114">**SSH RSA public key**: When deploying through hello portal or one of hello Azure quickstart templates, you need tooprovide hello public key for authentication against Azure Container Service virtual machines.</span></span> <span data-ttu-id="0575a-115">toocreate Secure Shell (SSH) RSA-sleutels, Zie Hallo [OS X- en Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) of [Windows](../../virtual-machines/linux/ssh-from-windows.md) richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="0575a-115">toocreate Secure Shell (SSH) RSA keys, see hello [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md) guidance.</span></span> 

* <span data-ttu-id="0575a-116">**Service-principal client-ID en geheim** (alleen Kubernetes): Zie voor meer informatie over en richtlijnen toocreate een Azure Active Directory-service-principal, [over service-principal voor een cluster Kubernetes hello](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="0575a-116">**Service principal client ID and secret** (Kubernetes only): For more information and guidance toocreate an Azure Active Directory service principal, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>



## <a name="create-a-cluster-by-using-hello-azure-portal"></a><span data-ttu-id="0575a-117">Maken van een cluster met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="0575a-117">Create a cluster by using hello Azure portal</span></span>
1. <span data-ttu-id="0575a-118">Aanmelden toohello Azure-portal, selecteer **nieuw**, en zoek hello Azure Marketplace voor **Azure Container Service**.</span><span class="sxs-lookup"><span data-stu-id="0575a-118">Sign in toohello Azure portal, select **New**, and search hello Azure Marketplace for **Azure Container Service**.</span></span>

    ![Azure Container Service in Marketplace](./media/container-service-deployment/acs-portal1.png)  <br />

2. <span data-ttu-id="0575a-120">Klik op **Azure Container Service** en klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0575a-120">Click **Azure Container Service**, and click **Create**.</span></span>

3. <span data-ttu-id="0575a-121">Op Hallo **basisbeginselen** blade Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="0575a-121">On hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="0575a-122">**Orchestrator**: Selecteer een van de Hallo container orchestrators toodeploy op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0575a-122">**Orchestrator**: Select one of hello container orchestrators toodeploy on hello cluster.</span></span>
        * <span data-ttu-id="0575a-123">**DC/OS**: implementeert een DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="0575a-123">**DC/OS**: Deploys a DC/OS cluster.</span></span>
        * <span data-ttu-id="0575a-124">**Swarm**: implementeert een Docker Swarm-cluster.</span><span class="sxs-lookup"><span data-stu-id="0575a-124">**Swarm**: Deploys a Docker Swarm cluster.</span></span>
        * <span data-ttu-id="0575a-125">**Kubernetes**: implementeert een Kubernetes-cluster.</span><span class="sxs-lookup"><span data-stu-id="0575a-125">**Kubernetes**: Deploys a Kubernetes cluster.</span></span>
    * <span data-ttu-id="0575a-126">**Subscription**: selecteer een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0575a-126">**Subscription**: Select an Azure subscription.</span></span>
    * <span data-ttu-id="0575a-127">**Resourcegroep**: Hallo-naam van een nieuwe resourcegroep voor Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="0575a-127">**Resource group**: Enter hello name of a new resource group for hello deployment.</span></span>
    * <span data-ttu-id="0575a-128">**Locatie**: Selecteer een Azure-regio voor hello Azure Container Service-implementatie.</span><span class="sxs-lookup"><span data-stu-id="0575a-128">**Location**: Select an Azure region for hello Azure Container Service deployment.</span></span> <span data-ttu-id="0575a-129">Raadpleeg voor beschikbaarheid, [Beschikbare producten per regio](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="0575a-129">For availability, check [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
    
    ![Basisinstellingen](./media/container-service-deployment/acs-portal3.png)  <br />
    
    <span data-ttu-id="0575a-131">Klik op **OK** wanneer u bent klaar tooproceed.</span><span class="sxs-lookup"><span data-stu-id="0575a-131">Click **OK** when you're ready tooproceed.</span></span>

4. <span data-ttu-id="0575a-132">Op Hallo **de hoofdsleutel van de configuratie** blade Voer Hallo-instellingen voor Linux-hoofdknooppunt Hallo of knooppunten in het Hallo-cluster (sommige instellingen zijn specifiek tooeach orchestrator) te volgen:</span><span class="sxs-lookup"><span data-stu-id="0575a-132">On hello **Master configuration** blade, enter hello following settings for hello Linux master node or nodes in hello cluster (some settings are specific tooeach orchestrator):</span></span>

    * <span data-ttu-id="0575a-133">**Basispagina-DNS-naam**: Hallo voorvoegsel gebruikt toocreate een unieke volledig gekwalificeerde domeinnaam (FQDN) voor Hallo master.</span><span class="sxs-lookup"><span data-stu-id="0575a-133">**Master DNS name**: hello prefix used toocreate a unique fully qualified domain name (FQDN) for hello master.</span></span> <span data-ttu-id="0575a-134">Hallo master FQDN-naam van het formulier Hallo is *voorvoegsel*beheergegevens*locatie*. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="0575a-134">hello master FQDN is of hello form *prefix*mgmt.*location*.cloudapp.azure.com.</span></span>
    * <span data-ttu-id="0575a-135">**Gebruikersnaam**: Hallo gebruikersnaam op voor een account op elk Hallo Linux virtuele machines in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0575a-135">**User name**: hello user name for an account on each of hello Linux virtual machines in hello cluster.</span></span>
    * <span data-ttu-id="0575a-136">**Openbare SSH-RSA-sleutel**: Hallo openbare sleutel toobe gebruikt voor verificatie met een virtuele Linux-machines Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0575a-136">**SSH RSA public key**: Add hello public key toobe used for authentication against hello Linux virtual machines.</span></span> <span data-ttu-id="0575a-137">Het is belangrijk dat deze sleutel geen regeleinden bevat en het Hallo omvat `ssh-rsa` voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="0575a-137">It is important that this key contains no line breaks, and it includes hello `ssh-rsa` prefix.</span></span> <span data-ttu-id="0575a-138">Hallo `username@domain` postfix is optioneel.</span><span class="sxs-lookup"><span data-stu-id="0575a-138">hello `username@domain` postfix is optional.</span></span> <span data-ttu-id="0575a-139">Hallo sleutel moet er ongeveer als volgende Hallo: **ssh-rsa AAAAB3Nz... <>...... UcyupgH azureuser@linuxvm** .</span><span class="sxs-lookup"><span data-stu-id="0575a-139">hello key should look something like hello following: **ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**.</span></span> 
    * <span data-ttu-id="0575a-140">**Service-principal**: als u Hallo Kubernetes orchestrator hebt geselecteerd, voert u een Azure Active Directory **Service-principal client-ID** (ook wel Hallo appId) en **geheim voor Service-principal client** (wachtwoord).</span><span class="sxs-lookup"><span data-stu-id="0575a-140">**Service principal**: If you selected hello Kubernetes orchestrator, enter an Azure Active Directory **Service principal client ID** (also called hello appId) and **Service principal client secret** (password).</span></span> <span data-ttu-id="0575a-141">Zie voor meer informatie [over service-principal voor een cluster Kubernetes hello](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="0575a-141">For more information, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>
    * <span data-ttu-id="0575a-142">**De hoofdsleutel van de count**: Hallo aantal masters in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0575a-142">**Master count**: hello number of masters in hello cluster.</span></span>
    * <span data-ttu-id="0575a-143">**VM diagnostics**: voor sommige orchestrators, kunt u VM diagnostics op Hallo masters inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0575a-143">**VM diagnostics**: For some orchestrators, you can enable VM diagnostics on hello masters.</span></span>

    ![Master configuration](./media/container-service-deployment/acs-portal4.png)  <br />

    <span data-ttu-id="0575a-145">Klik op **OK** wanneer u bent klaar tooproceed.</span><span class="sxs-lookup"><span data-stu-id="0575a-145">Click **OK** when you're ready tooproceed.</span></span>

5. <span data-ttu-id="0575a-146">Op Hallo **agentconfiguratie** blade Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="0575a-146">On hello **Agent configuration** blade, enter hello following information:</span></span>

    * <span data-ttu-id="0575a-147">**Aantal agents**: voor Docker Swarm en Kubernetes, is deze waarde Hallo kunt u het oorspronkelijke aantal agents in de agentschaalset Hallo.</span><span class="sxs-lookup"><span data-stu-id="0575a-147">**Agent count**: For Docker Swarm and Kubernetes, this value is hello initial number of agents in hello agent scale set.</span></span> <span data-ttu-id="0575a-148">Voor DC/OS is het oorspronkelijke aantal agents in een persoonlijke schaalset Hallo.</span><span class="sxs-lookup"><span data-stu-id="0575a-148">For DC/OS, it is hello initial number of agents in a private scale set.</span></span> <span data-ttu-id="0575a-149">Bovendien wordt een openbare schaalset gemaakt voor DC/OS, die een vooraf bepaald aantal agents bevat.</span><span class="sxs-lookup"><span data-stu-id="0575a-149">Additionally, a public scale set is created for DC/OS, which contains a predetermined number of agents.</span></span> <span data-ttu-id="0575a-150">Hallo is aantal agents in deze openbare schaalsets bepaald door het aantal masters in het cluster Hallo Hallo: één openbare agent voor een model en twee openbare agents voor drie of 5 masters.</span><span class="sxs-lookup"><span data-stu-id="0575a-150">hello number of agents in this public scale set is determined by hello number of masters in hello cluster: one public agent for one master, and two public agents for three or five masters.</span></span>
    * <span data-ttu-id="0575a-151">**De grootte van de virtuele machine agent**: Hallo grootte van Hallo agent virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="0575a-151">**Agent virtual machine size**: hello size of hello agent virtual machines.</span></span>
    * <span data-ttu-id="0575a-152">**Besturingssysteem**: deze instelling is momenteel alleen beschikbaar als u Hallo Kubernetes orchestrator geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="0575a-152">**Operating system**: This setting is currently available only if you selected hello Kubernetes orchestrator.</span></span> <span data-ttu-id="0575a-153">Kies een Linux-distributie of een toorun van het besturingssysteem Windows Server op Hallo agents.</span><span class="sxs-lookup"><span data-stu-id="0575a-153">Choose either a Linux distribution or a Windows Server operating system toorun on hello agents.</span></span> <span data-ttu-id="0575a-154">Op basis van deze instelling wordt bepaald of op het cluster Linux- of Windows-container-apps kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0575a-154">This setting determines whether your cluster can run Linux or Windows container apps.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="0575a-155">Ondersteuning voor Windows-containers bevindt zich voor Kubernetes-clusters nog in de preview-fase.</span><span class="sxs-lookup"><span data-stu-id="0575a-155">Windows container support is in preview for Kubernetes clusters.</span></span> <span data-ttu-id="0575a-156">Op DC/OS- en Swarm-clusters worden momenteel alleen Linux-agents ondersteund in Azure-Container Service.</span><span class="sxs-lookup"><span data-stu-id="0575a-156">On DC/OS and Swarm clusters, only Linux agents are currently supported in Azure Container Service.</span></span>

    * <span data-ttu-id="0575a-157">**Agentreferenties**: als u de Windows-besturingssysteem Hallo hebt geselecteerd, voert u een beheerder **gebruikersnaam** en **wachtwoord** voor Hallo agent virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="0575a-157">**Agent credentials**: If you selected hello Windows operating system, enter an administrator **User name** and **Password** for hello agent VMs.</span></span> 

    ![Agent configuration](./media/container-service-deployment/acs-portal5.png)  <br />

    <span data-ttu-id="0575a-159">Klik op **OK** wanneer u bent klaar tooproceed.</span><span class="sxs-lookup"><span data-stu-id="0575a-159">Click **OK** when you're ready tooproceed.</span></span>

6. <span data-ttu-id="0575a-160">Klik op **OK** nadat de servicevalidatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="0575a-160">After service validation finishes, click **OK**.</span></span>

    ![Validatie](./media/container-service-deployment/acs-portal6.png)  <br />

7. <span data-ttu-id="0575a-162">Hallo rwaarden.</span><span class="sxs-lookup"><span data-stu-id="0575a-162">Review hello terms.</span></span> <span data-ttu-id="0575a-163">implementatieproces toostart hello, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="0575a-163">toostart hello deployment process, click **Create**.</span></span>

    <span data-ttu-id="0575a-164">Als u toopin Hallo implementatie toohello Azure-portal hebt gekozen, ziet u de implementatiestatus Hallo.</span><span class="sxs-lookup"><span data-stu-id="0575a-164">If you've elected toopin hello deployment toohello Azure portal, you can see hello deployment status.</span></span>

    ![Implementatiestatus](./media/container-service-deployment/acs-portal8.png)  <br />

<span data-ttu-id="0575a-166">Hallo implementatie duurt enkele minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="0575a-166">hello deployment takes several minutes toocomplete.</span></span> <span data-ttu-id="0575a-167">Hello Azure Container Service-cluster is klaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="0575a-167">Then, hello Azure Container Service cluster is ready for use.</span></span>


## <a name="create-a-cluster-by-using-a-quickstart-template"></a><span data-ttu-id="0575a-168">Een cluster maken met het snelstartsjabloon</span><span class="sxs-lookup"><span data-stu-id="0575a-168">Create a cluster by using a quickstart template</span></span>
<span data-ttu-id="0575a-169">Azure-snelstartsjablonen zijn beschikbaar toodeploy een cluster in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="0575a-169">Azure quickstart templates are available toodeploy a cluster in Azure Container Service.</span></span> <span data-ttu-id="0575a-170">Hallo opgegeven Quick Start-sjablonen kunnen worden gewijzigd tooinclude extra of geavanceerde configuratie van Azure.</span><span class="sxs-lookup"><span data-stu-id="0575a-170">hello provided quickstart templates can be modified tooinclude additional or advanced Azure configuration.</span></span> <span data-ttu-id="0575a-171">een Azure Container Service-cluster met behulp van een sjabloon voor de Azure quickstart toocreate, moet u een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0575a-171">toocreate an Azure Container Service cluster by using an Azure quickstart template, you need an Azure subscription.</span></span> <span data-ttu-id="0575a-172">Als u er geen hebt, kunt u zich [registreren voor een gratis proefversie](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="0575a-172">If you don't have one, then sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> 

<span data-ttu-id="0575a-173">Volg deze stappen toodeploy een cluster met een sjabloon en Azure CLI 2.0 Hallo (Zie [installatie en configuratie-instructies](/cli/azure/install-az-cli2)).</span><span class="sxs-lookup"><span data-stu-id="0575a-173">Follow these steps toodeploy a cluster using a template and hello Azure CLI 2.0 (see [installation and setup instructions](/cli/azure/install-az-cli2)).</span></span>

> [!NOTE] 
> <span data-ttu-id="0575a-174">Als u van een Windows-systeem gebruikmaakt, kunt u dezelfde stappen toodeploy een sjabloon met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0575a-174">If you're on a Windows system, you can use similar steps toodeploy a template using Azure PowerShell.</span></span> <span data-ttu-id="0575a-175">De stappen worden verderop in dit gedeelte beschreven.</span><span class="sxs-lookup"><span data-stu-id="0575a-175">See steps later in this section.</span></span> <span data-ttu-id="0575a-176">U kunt ook een sjabloon via Hallo implementeren [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) of andere methoden.</span><span class="sxs-lookup"><span data-stu-id="0575a-176">You can also deploy a template through hello [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) or other methods.</span></span>

1. <span data-ttu-id="0575a-177">toodeploy een DC/OS, Docker Swarm of Kubernetes-cluster, selecteer een van Hallo beschikbaar Quick Start-sjablonen in GitHub.</span><span class="sxs-lookup"><span data-stu-id="0575a-177">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="0575a-178">Hierna volgt een gedeeltelijke lijst.</span><span class="sxs-lookup"><span data-stu-id="0575a-178">A partial list follows.</span></span> <span data-ttu-id="0575a-179">Hello DC/OS- en Swarm-sjablonen zijn hetzelfde, behalve de standaardselectie voor orchestrator Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="0575a-179">hello DC/OS and Swarm templates are hello same, except for hello default orchestrator selection.</span></span>

    * [<span data-ttu-id="0575a-180">DC/OS-sjabloon</span><span class="sxs-lookup"><span data-stu-id="0575a-180">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="0575a-181">Swarm-sjabloon</span><span class="sxs-lookup"><span data-stu-id="0575a-181">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="0575a-182">Kubernetes-sjabloon</span><span class="sxs-lookup"><span data-stu-id="0575a-182">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="0575a-183">Meld u bij tooyour Azure-account (`az login`), en zorg ervoor dat hello Azure CLI is verbonden tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0575a-183">Log in tooyour Azure account (`az login`), and make sure that hello Azure CLI is connected tooyour Azure subscription.</span></span> <span data-ttu-id="0575a-184">Hallo standaardabonnement kunt u met behulp van de volgende opdracht Hallo zien:</span><span class="sxs-lookup"><span data-stu-id="0575a-184">You can see hello default subscription by using hello following command:</span></span>

    ```azurecli
    az account show
    ```
    
    <span data-ttu-id="0575a-185">Als u meer dan één abonnement en de noodzaak tooset op een andere standaard-abonnement hebt, voert u `az account set --subscription` en Hallo abonnements-ID of naam opgeven.</span><span class="sxs-lookup"><span data-stu-id="0575a-185">If you have more than one subscription and need tooset a different default subscription, run `az account set --subscription` and specify hello subscription ID or name.</span></span>

3. <span data-ttu-id="0575a-186">Een aanbevolen procedure is om een nieuwe resourcegroep voor Hallo-implementatie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0575a-186">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="0575a-187">een resourcegroep toocreate gebruiken Hallo `az group create` opdracht een naam van een resourcegroep en locatie opgeven:</span><span class="sxs-lookup"><span data-stu-id="0575a-187">toocreate a resource group, use hello `az group create` command specify a resource group name and location:</span></span> 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. <span data-ttu-id="0575a-188">Maak een JSON-bestand met Hallo vereiste sjabloon parameters.</span><span class="sxs-lookup"><span data-stu-id="0575a-188">Create a JSON file containing hello required template parameters.</span></span> <span data-ttu-id="0575a-189">Download Hallo parameterbestand met de naam `azuredeploy.parameters.json` die wordt meegestuurd met hello Azure Container Service-sjabloon `azuredeploy.json` in GitHub.</span><span class="sxs-lookup"><span data-stu-id="0575a-189">Download hello parameters file named `azuredeploy.parameters.json` that accompanies hello Azure Container Service template `azuredeploy.json` in GitHub.</span></span> <span data-ttu-id="0575a-190">Voer de vereiste parameterwaarden voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="0575a-190">Enter required parameter values for your cluster.</span></span> 

    <span data-ttu-id="0575a-191">Bijvoorbeeld: toouse hello [DC/OS-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), parameterwaarden worden doorgegeven voor `dnsNamePrefix` en `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="0575a-191">For example, toouse hello [DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), supply parameter values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="0575a-192">Zie de beschrijvingen van Hallo in `azuredeploy.json` en opties voor andere parameters.</span><span class="sxs-lookup"><span data-stu-id="0575a-192">See hello descriptions in `azuredeploy.json` and options for other parameters.</span></span>  
 

5. <span data-ttu-id="0575a-193">Een Container Service-cluster maken bestand door te geven Hallo implementatie parameters Hello volgende opdracht, waarbij:</span><span class="sxs-lookup"><span data-stu-id="0575a-193">Create a Container Service cluster by passing hello deployment parameters file with hello following command, where:</span></span>

    * <span data-ttu-id="0575a-194">**RESOURCE_GROUP** Hallo-naam van resourcegroep Hallo die u hebt gemaakt in de vorige stap Hallo is.</span><span class="sxs-lookup"><span data-stu-id="0575a-194">**RESOURCE_GROUP** is hello name of hello resource group that you created in hello previous step.</span></span>
    * <span data-ttu-id="0575a-195">**DEPLOYMENT_NAME** (optioneel) Dit is een naam toohello-implementatie.</span><span class="sxs-lookup"><span data-stu-id="0575a-195">**DEPLOYMENT_NAME** (optional) is a name you give toohello deployment.</span></span>
    * <span data-ttu-id="0575a-196">**TEMPLATE_URI** Hallo-locatie van het implementatiebestand Hallo `azuredeploy.json`.</span><span class="sxs-lookup"><span data-stu-id="0575a-196">**TEMPLATE_URI** is hello location of hello deployment file `azuredeploy.json`.</span></span> <span data-ttu-id="0575a-197">Deze URI moet Hallo Raw-bestand niet de toohello van een wijzer GitHub UI.</span><span class="sxs-lookup"><span data-stu-id="0575a-197">This URI must be hello Raw file, not a pointer toohello GitHub UI.</span></span> <span data-ttu-id="0575a-198">toofind deze URI, selecteer Hallo `azuredeploy.json` bestand in GitHub en op Hallo **Raw** knop.</span><span class="sxs-lookup"><span data-stu-id="0575a-198">toofind this URI, select hello `azuredeploy.json` file in GitHub, and click hello **Raw** button.</span></span>  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    <span data-ttu-id="0575a-199">U kunt ook parameters opgeven als een tekenreeks JSON-indeling op Hallo-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="0575a-199">You can also provide parameters as a JSON-formatted string on hello command line.</span></span> <span data-ttu-id="0575a-200">U kunt een opdracht vergelijkbare toohello volgt:</span><span class="sxs-lookup"><span data-stu-id="0575a-200">Use a command similar toohello following:</span></span>

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > <span data-ttu-id="0575a-201">Hallo implementatie duurt enkele minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="0575a-201">hello deployment takes several minutes toocomplete.</span></span>
    > 

### <a name="equivalent-powershell-commands"></a><span data-ttu-id="0575a-202">Vergelijkbare PowerShell-opdrachten</span><span class="sxs-lookup"><span data-stu-id="0575a-202">Equivalent PowerShell commands</span></span>
<span data-ttu-id="0575a-203">U kunt een Azure Container Service-clustersjabloon ook implementeren met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0575a-203">You can also deploy an Azure Container Service cluster template with PowerShell.</span></span> <span data-ttu-id="0575a-204">Dit document is gebaseerd op Hallo versie 1.0 [Azure PowerShell-module](https://azure.microsoft.com/blog/azps-1-0/).</span><span class="sxs-lookup"><span data-stu-id="0575a-204">This document is based on hello version 1.0 [Azure PowerShell module](https://azure.microsoft.com/blog/azps-1-0/).</span></span>

1. <span data-ttu-id="0575a-205">toodeploy een DC/OS, Docker Swarm of Kubernetes-cluster, selecteer een van Hallo beschikbaar Quick Start-sjablonen in GitHub.</span><span class="sxs-lookup"><span data-stu-id="0575a-205">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="0575a-206">Hierna volgt een gedeeltelijke lijst.</span><span class="sxs-lookup"><span data-stu-id="0575a-206">A partial list follows.</span></span> <span data-ttu-id="0575a-207">Opmerking dat hello DC/OS- en Swarm-sjablonen zijn Hallo dezelfde zijn, met uitzondering van de standaardselectie voor orchestrator Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="0575a-207">Note that hello DC/OS and Swarm templates are hello same, with hello exception of hello default orchestrator selection.</span></span>

    * [<span data-ttu-id="0575a-208">DC/OS-sjabloon</span><span class="sxs-lookup"><span data-stu-id="0575a-208">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="0575a-209">Swarm-sjabloon</span><span class="sxs-lookup"><span data-stu-id="0575a-209">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="0575a-210">Kubernetes-sjabloon</span><span class="sxs-lookup"><span data-stu-id="0575a-210">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="0575a-211">Controleer of uw PowerShell-sessie in tooAzure is ondertekend voordat het maken van een cluster in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0575a-211">Before creating a cluster in your Azure subscription, verify that your PowerShell session has been signed in tooAzure.</span></span> <span data-ttu-id="0575a-212">U kunt dit doen met Hallo `Get-AzureRMSubscription` opdracht:</span><span class="sxs-lookup"><span data-stu-id="0575a-212">You can do this with hello `Get-AzureRMSubscription` command:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="0575a-213">Als u toosign in tooAzure moet, gebruikt u Hallo `Login-AzureRMAccount` opdracht:</span><span class="sxs-lookup"><span data-stu-id="0575a-213">If you need toosign in tooAzure, use hello `Login-AzureRMAccount` command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

4. <span data-ttu-id="0575a-214">Een aanbevolen procedure is om een nieuwe resourcegroep voor Hallo-implementatie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0575a-214">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="0575a-215">een resourcegroep toocreate gebruiken Hallo `New-AzureRmResourceGroup` opdracht in en geef een naam en doel-regio voor de groep voor resource:</span><span class="sxs-lookup"><span data-stu-id="0575a-215">toocreate a resource group, use hello `New-AzureRmResourceGroup` command, and specify a resource group name and destination region:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. <span data-ttu-id="0575a-216">Nadat u een resourcegroep hebt gemaakt, kunt u uw cluster maken met de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="0575a-216">After you create a resource group, you can create your cluster with hello following command.</span></span> <span data-ttu-id="0575a-217">Hallo-URI van Hallo gewenste sjabloon wordt opgegeven met de Hallo `-TemplateUri` parameter.</span><span class="sxs-lookup"><span data-stu-id="0575a-217">hello URI of hello desired template is specified with hello `-TemplateUri` parameter.</span></span> <span data-ttu-id="0575a-218">Wanneer u deze opdracht uitvoert, vraagt PowerShell u de parameterwaarden voor de implementatie op te geven.</span><span class="sxs-lookup"><span data-stu-id="0575a-218">When you run this command, PowerShell prompts you for deployment parameter values.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a><span data-ttu-id="0575a-219">Sjabloonparameters opgeven</span><span class="sxs-lookup"><span data-stu-id="0575a-219">Provide template parameters</span></span>
<span data-ttu-id="0575a-220">Als u bekend met PowerShell bent, weet u dat u door de beschikbare parameters voor een cmdlet Hallo bladeren kunt met een minteken (-) te typen en vervolgens op Hallo TAB-toets te drukken.</span><span class="sxs-lookup"><span data-stu-id="0575a-220">If you're familiar with PowerShell, you know that you can cycle through hello available parameters for a cmdlet by typing a minus sign (-) and then pressing hello TAB key.</span></span> <span data-ttu-id="0575a-221">Dezelfde functionaliteit werkt ook met parameters die u in de sjabloon definieert.</span><span class="sxs-lookup"><span data-stu-id="0575a-221">This same functionality also works with parameters that you define in your template.</span></span> <span data-ttu-id="0575a-222">Zodra u de sjabloonnaam Hallo typt, Hallo-cmdlet haalt Hallo sjabloon parseert Hallo parameters en Hallo sjabloon parameters toohello opdracht dynamisch worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0575a-222">As soon as you type hello template name, hello cmdlet fetches hello template, parses hello parameters, and adds hello template parameters toohello command dynamically.</span></span> <span data-ttu-id="0575a-223">Dit maakt het eenvoudig toospecify Hallo sjabloonparameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="0575a-223">This makes it easy toospecify hello template parameter values.</span></span> <span data-ttu-id="0575a-224">En als u een waarde van de vereiste parameter bent vergeten, vraagt PowerShell u om Hallo-waarde.</span><span class="sxs-lookup"><span data-stu-id="0575a-224">And, if you forget a required parameter value, PowerShell prompts you for hello value.</span></span>

<span data-ttu-id="0575a-225">Hier volgt de volledige opdracht Hallo met parameters die zijn opgenomen.</span><span class="sxs-lookup"><span data-stu-id="0575a-225">Here is hello full command, with parameters included.</span></span> <span data-ttu-id="0575a-226">Geef uw eigen waarden voor Hallo namen van Hallo resources.</span><span class="sxs-lookup"><span data-stu-id="0575a-226">Provide your own values for hello names of hello resources.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a><span data-ttu-id="0575a-227">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0575a-227">Next steps</span></span>
<span data-ttu-id="0575a-228">Nu u een werkend cluster hebt, kunt u deze documenten lezen voor meer informatie over verbinding en beheer:</span><span class="sxs-lookup"><span data-stu-id="0575a-228">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="0575a-229">Verbinding maken met tooan Azure Container Service-cluster</span><span class="sxs-lookup"><span data-stu-id="0575a-229">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="0575a-230">Werken met de Azure Container Service en DC/OS</span><span class="sxs-lookup"><span data-stu-id="0575a-230">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="0575a-231">Werken met de Azure Container Service en Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="0575a-231">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="0575a-232">Werken met de Azure Container Service en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0575a-232">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)
