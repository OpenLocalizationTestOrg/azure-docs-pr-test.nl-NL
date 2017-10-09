---
title: Service Fabric aaaAzure met API Management snel aan de slag | Microsoft Docs
description: Deze handleiding wordt getoond hoe tooquickly aan de slag met Azure API Management en Service Fabric.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="f0db7-103">Service Fabric met Azure API Management snel starten</span><span class="sxs-lookup"><span data-stu-id="f0db7-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="f0db7-104">Deze handleiding laat zien u hoe tooset Azure API Management met Service Fabric-up maken van en het configureren van uw eerste API bewerking toosend verkeer tooback-end-services in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f0db7-104">This guide shows you how tooset up Azure API Management with Service Fabric and configure your first API operation toosend traffic tooback-end services in Service Fabric.</span></span> <span data-ttu-id="f0db7-105">toolearn meer informatie over Azure API Management-scenario's met Service Fabric Zie Hallo [overzicht](service-fabric-api-management-overview.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="f0db7-105">toolearn more about Azure API Management scenarios with Service Fabric, see hello [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a><span data-ttu-id="f0db7-106">API Management en Service Fabric tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="f0db7-106">Deploy API Management and Service Fabric tooAzure</span></span>

<span data-ttu-id="f0db7-107">de eerste stap Hallo is toodeploy API Management en een tooAzure Service Fabric-cluster in een gedeelde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="f0db7-107">hello first step is toodeploy API Management and a Service Fabric cluster tooAzure in a shared Virtual Network.</span></span> <span data-ttu-id="f0db7-108">Hiermee kunt API Management toocommunicate rechtstreeks met Service Fabric zodat deze kan direct tooany back-end-service in Service Fabric detectie-service, service partitie resolutie en voorwaarts verkeer uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f0db7-108">This allows API Management toocommunicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly tooany backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="f0db7-109">Topologie</span><span class="sxs-lookup"><span data-stu-id="f0db7-109">Topology</span></span>

<span data-ttu-id="f0db7-110">Deze handleiding implementeert Hallo volgende topologie tooAzure waarin API Management en Service Fabric zijn in de subnetten van Hallo hetzelfde virtuele netwerk:</span><span class="sxs-lookup"><span data-stu-id="f0db7-110">This guide deploys hello following topology tooAzure in which API Management and Service Fabric are in subnets of hello same Virtual Network:</span></span>

 ![Een bijschrift][sf-apim-topology-overview]

<span data-ttu-id="f0db7-112">tooget aan de slag wilt, zijn Resource Manager-sjablonen beschikbaar voor elke stap van de implementatie:</span><span class="sxs-lookup"><span data-stu-id="f0db7-112">tooget started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="f0db7-113">Netwerktopologie:</span><span class="sxs-lookup"><span data-stu-id="f0db7-113">Network topology:</span></span>
    - <span data-ttu-id="f0db7-114">[Network.JSON][network-arm]</span><span class="sxs-lookup"><span data-stu-id="f0db7-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="f0db7-115">[Network.parameters.JSON][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="f0db7-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="f0db7-116">Service Fabric-cluster:</span><span class="sxs-lookup"><span data-stu-id="f0db7-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="f0db7-117">[cluster.JSON][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="f0db7-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="f0db7-118">[cluster.parameters.JSON][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="f0db7-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="f0db7-119">API Management:</span><span class="sxs-lookup"><span data-stu-id="f0db7-119">API Management:</span></span>
    - <span data-ttu-id="f0db7-120">[APIM.JSON][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="f0db7-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="f0db7-121">[APIM.parameters.JSON][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="f0db7-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-tooazure-and-select-your-subscription"></a><span data-ttu-id="f0db7-122">TooAzure aanmelden en uw abonnement te selecteren</span><span class="sxs-lookup"><span data-stu-id="f0db7-122">Sign in tooAzure and select your subscription</span></span>

<span data-ttu-id="f0db7-123">Maakt gebruik van deze handleiding [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="f0db7-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="f0db7-124">Wanneer u een nieuwe PowerShell-sessie start, meld u aan tooyour Azure-account en uw abonnement te selecteren voordat u Azure-opdrachten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f0db7-124">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="f0db7-125">Meld u aan tooyour Azure-account:</span><span class="sxs-lookup"><span data-stu-id="f0db7-125">Sign in tooyour Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="f0db7-126">Selecteer uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="f0db7-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="f0db7-127">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="f0db7-127">Create a resource group</span></span>

<span data-ttu-id="f0db7-128">Maak een nieuwe resourcegroep voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="f0db7-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="f0db7-129">Geef deze een naam en een locatie.</span><span class="sxs-lookup"><span data-stu-id="f0db7-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a><span data-ttu-id="f0db7-130">Hallo netwerktopologie implementeren</span><span class="sxs-lookup"><span data-stu-id="f0db7-130">Deploy hello network topology</span></span>

<span data-ttu-id="f0db7-131">de eerste stap Hallo is tooset up Hallo netwerk topologie toowhich API Management en Hallo Service Fabric-cluster wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f0db7-131">hello first step is tooset up hello network topology toowhich API Management and hello Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="f0db7-132">Hallo [network.json] [ network-arm] Resource Manager-sjabloon is geconfigureerd toocreate een virtueel netwerk (VNET) met twee subnetten en twee Netwerkbeveiligingsgroep groepen (NSG).</span><span class="sxs-lookup"><span data-stu-id="f0db7-132">hello [network.json][network-arm] Resource Manager template is configured toocreate a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="f0db7-133">Hallo [network.parameters.json] [ network-parameters-arm] parameterbestand Hallo namen bevat van Hallo subnetten en nsg's die API Management en Service Fabric om te worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f0db7-133">hello [network.parameters.json][network-parameters-arm] parameters file contains hello names of hello subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="f0db7-134">Voor deze handleiding hoeft Hallo parameterwaarden niet toobe gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="f0db7-134">For this guide, hello parameter values do not need toobe changed.</span></span> <span data-ttu-id="f0db7-135">Hallo API Management en Service Fabric-Resource Manager-sjablonen gebruiken deze waarden, zodat als ze hier zijn gewijzigd, moet u wijzigen in de andere Resource Manager-sjablonen dienovereenkomstig Hallo.</span><span class="sxs-lookup"><span data-stu-id="f0db7-135">hello API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in hello other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="f0db7-136">Download Hallo Resource Manager-sjabloon en de parameters-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0db7-136">Download hello following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="f0db7-137">[Network.JSON][network-arm]</span><span class="sxs-lookup"><span data-stu-id="f0db7-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="f0db7-138">[Network.parameters.JSON][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="f0db7-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="f0db7-139">Gebruik Hallo volgende PowerShell-opdracht toodeploy Hallo Resource Manager-sjabloon en de parameter bestanden voor Hallo netwerk instellen:</span><span class="sxs-lookup"><span data-stu-id="f0db7-139">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for hello network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a><span data-ttu-id="f0db7-140">Hallo Service Fabric-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="f0db7-140">Deploy hello Service Fabric cluster</span></span>

<span data-ttu-id="f0db7-141">Zodra de netwerkbronnen Hallo hebt implementeren, Hallo volgende stap is een Service Fabric-cluster toohello VNET in Hallo subnet toodeploy en NSG voor Hallo Service Fabric-cluster is aangewezen.</span><span class="sxs-lookup"><span data-stu-id="f0db7-141">Once hello network resources have finished deploying, hello next step is toodeploy a Service Fabric cluster toohello VNET in hello subnet and NSG designated for hello Service Fabric cluster.</span></span> <span data-ttu-id="f0db7-142">Hallo Service Fabric-Resource Manager-sjabloon is voor deze zelfstudie vooraf geconfigureerde toouse Hallo namen van Hallo VNET, subnet en NSG die u hebt ingesteld in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="f0db7-142">For this tutorial, hello Service Fabric Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

<span data-ttu-id="f0db7-143">Hallo Service Fabric-cluster Resource Manager-sjabloon is geconfigureerd toocreate een beveiligde cluster met Certificaatbeveiliging.</span><span class="sxs-lookup"><span data-stu-id="f0db7-143">hello Service Fabric cluster Resource Manager template is configured toocreate a secure cluster with certificate security.</span></span> <span data-ttu-id="f0db7-144">Hallo-certificaat is gebruikte toosecure knooppunt naar communicatie voor uw cluster en toomanage gebruiker toegang tooyour Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="f0db7-144">hello certificate is used toosecure node-to-node communication for your cluster and toomanage user access tooyour Service Fabric cluster.</span></span> <span data-ttu-id="f0db7-145">Dit certificaat tooaccess Hallo Service Fabric Naming Service API Management gebruikt voor servicedetectie.</span><span class="sxs-lookup"><span data-stu-id="f0db7-145">API Management uses this certificate tooaccess  hello Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="f0db7-146">Deze stap is vereist dat u een certificaat in de Sleutelkluis voor clusterbeveiliging.</span><span class="sxs-lookup"><span data-stu-id="f0db7-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="f0db7-147">Zie voor meer informatie over het instellen van een beveiligde cluster met Sleutelkluis [in deze handleiding over het maken van een cluster in Azure Resource Manager gebruiken](service-fabric-cluster-creation-via-arm.md)</span><span class="sxs-lookup"><span data-stu-id="f0db7-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="f0db7-148">U kunt Azure Active Directory-verificatie in toevoeging toohello certificaat gebruikt voor toegang tot cluster toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f0db7-148">You may add Azure Active Directory authentication in addition toohello certificate used for cluster access.</span></span> <span data-ttu-id="f0db7-149">Azure Active Directory is de aanbevolen manier toomanage gebruiker toegang tooyour Service Fabric-cluster hello, maar is niet nodig toocomplete in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f0db7-149">Azure Active Directory is hello recommended way toomanage user access tooyour Service Fabric cluster, but is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="f0db7-150">Een certificaat is vereist in beide gevallen voor cluster knooppunt naar beveiliging en Azure API Management-verificatie op dit moment biedt geen ondersteuning voor verificatie met Azure Active Directory voor een Service Fabric-back-end.</span><span class="sxs-lookup"><span data-stu-id="f0db7-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="f0db7-151">Download Hallo Resource Manager-sjabloon en de parameters-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0db7-151">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="f0db7-152">[cluster.JSON][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="f0db7-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="f0db7-153">[cluster.parameters.JSON][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="f0db7-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="f0db7-154">Vul Hallo leeg parameters in Hallo `cluster.parameters.json` bestand voor uw implementatie, met inbegrip van Hallo [Sleutelkluis informatie](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) voor uw cluster-certificaat.</span><span class="sxs-lookup"><span data-stu-id="f0db7-154">Fill in hello empty parameters in hello `cluster.parameters.json` file for your deployment, including hello [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="f0db7-155">Hallo volgende PowerShell-opdracht toodeploy Hallo Resource Manager-sjabloon en de parameter bestanden toocreate Hallo Service Fabric-cluster gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f0db7-155">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files toocreate hello Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="f0db7-156">Implementeren van API Management</span><span class="sxs-lookup"><span data-stu-id="f0db7-156">Deploy API Management</span></span>

<span data-ttu-id="f0db7-157">Ten slotte implementeren API Management toohello VNET in Hallo subnet en NSG die is aangewezen voor API Management.</span><span class="sxs-lookup"><span data-stu-id="f0db7-157">Finally, deploy API Management toohello VNET in hello subnet and NSG designated for API Management.</span></span> <span data-ttu-id="f0db7-158">U hoeft niet toowait voor Hallo Service Fabric-cluster implementatie toofinish voordat u implementeert API Management.</span><span class="sxs-lookup"><span data-stu-id="f0db7-158">You do not need toowait for hello Service Fabric cluster deployment toofinish before deploying API Management.</span></span> 

<span data-ttu-id="f0db7-159">Hallo API Management-Resource Manager-sjabloon is voor deze zelfstudie vooraf geconfigureerde toouse Hallo namen van Hallo VNET, subnet en NSG die u hebt ingesteld in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="f0db7-159">For this tutorial, hello API Management Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

 1. <span data-ttu-id="f0db7-160">Download Hallo Resource Manager-sjabloon en de parameters-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0db7-160">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="f0db7-161">[APIM.JSON][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="f0db7-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="f0db7-162">[APIM.parameters.JSON][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="f0db7-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="f0db7-163">Vul Hallo leeg parameters in Hallo `apim.parameters.json` voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="f0db7-163">Fill in hello empty parameters in hello `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="f0db7-164">Hallo volgende PowerShell-opdracht toodeploy Hallo Resource Manager-sjabloon en de parameter bestanden voor API Management gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f0db7-164">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="f0db7-165">API Management configureren</span><span class="sxs-lookup"><span data-stu-id="f0db7-165">Configure API Management</span></span>

<span data-ttu-id="f0db7-166">Zodra uw API Management en Service Fabric-cluster worden geïmplementeerd, kunt u een Service Fabric-back-end kunt configureren in API Management.</span><span class="sxs-lookup"><span data-stu-id="f0db7-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="f0db7-167">Hiermee kunt u toocreate een back-end-service-beleid waarmee verkeer tooyour Service Fabric-cluster worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="f0db7-167">This allows you toocreate a backend service policy that sends traffic tooyour Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="f0db7-168">Beveiliging van API Management</span><span class="sxs-lookup"><span data-stu-id="f0db7-168">API Management Security</span></span>

<span data-ttu-id="f0db7-169">tooconfigure hello Service Fabric-back-end, moet u eerst tooconfigure API Management-beveiligingsinstellingen.</span><span class="sxs-lookup"><span data-stu-id="f0db7-169">tooconfigure hello Service Fabric backend, you first need tooconfigure API Management security settings.</span></span> <span data-ttu-id="f0db7-170">tooconfigure beveiligingsinstellingen, gaat u tooyour API Management-service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f0db7-170">tooconfigure security settings, go tooyour API Management service in hello Azure portal.</span></span>

#### <a name="enable-hello-api-management-rest-api"></a><span data-ttu-id="f0db7-171">Hallo API Management REST API inschakelen</span><span class="sxs-lookup"><span data-stu-id="f0db7-171">Enable hello API Management REST API</span></span>

<span data-ttu-id="f0db7-172">Hallo API Management REST API is momenteel Hallo alleen manier tooconfigure een back-endservice.</span><span class="sxs-lookup"><span data-stu-id="f0db7-172">hello API Management REST API is currently hello only way tooconfigure a backend service.</span></span> <span data-ttu-id="f0db7-173">de eerste stap Hallo tooenable Hallo API Management REST API is en beveilig deze.</span><span class="sxs-lookup"><span data-stu-id="f0db7-173">hello first step is tooenable hello API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="f0db7-174">Selecteer in de Hallo API Management-service, **Management-API - voorbeeld** onder **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="f0db7-174">In hello API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="f0db7-175">Controleer de Hallo **API Management REST API inschakelen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="f0db7-175">Check hello **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="f0db7-176">Hallo Management API URL Opmerking: dit is Hallo URL gebruiken we later tooset up Hallo Service Fabric-back-end</span><span class="sxs-lookup"><span data-stu-id="f0db7-176">Note hello Management API URL - this is hello URL we'll use later tooset up hello Service Fabric backend</span></span>
 4. <span data-ttu-id="f0db7-177">Genereren een **toegangstoken** als u een vervaldatum en een sleutel selecteert, klikt u vervolgens op Hallo **genereren** knop naar de onderkant Hallo van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="f0db7-177">Generate an **access Token** by selecting an expiry date and a key, then click hello **Generate** button toward hello bottom of hello page.</span></span>
 5. <span data-ttu-id="f0db7-178">Kopiëren Hallo **toegangstoken** en sla deze - kun je in Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="f0db7-178">Copy hello **access token** and save it - we'll use this in hello following steps.</span></span> <span data-ttu-id="f0db7-179">Houd er rekening mee dat deze verschilt van Hallo primaire en secundaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="f0db7-179">Note this is different from hello primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="f0db7-180">Een Service Fabric-client-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="f0db7-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="f0db7-181">API Management moet verifiëren met uw Service Fabric-cluster voor detectie van de service met behulp van een clientcertificaat dat toegang tooyour cluster heeft.</span><span class="sxs-lookup"><span data-stu-id="f0db7-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access tooyour cluster.</span></span> <span data-ttu-id="f0db7-182">Ter vereenvoudiging Hallo deze zelfstudie maakt gebruik van uw cluster hetzelfde certificaat bij het maken van de Service Fabric-cluster hello, die standaard gebruikte tooaccess kan worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f0db7-182">For simplicity, this tutorial uses hello same certificate specified when creating hello Service Fabric cluster, which by default can be used tooaccess your cluster.</span></span>

 1. <span data-ttu-id="f0db7-183">Selecteer in de Hallo API Management-service, **clientcertificaten - PREVIEW** onder **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="f0db7-183">In hello API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="f0db7-184">Klik op Hallo **+ toevoegen** knop</span><span class="sxs-lookup"><span data-stu-id="f0db7-184">Click hello **+ Add** button</span></span>
 2. <span data-ttu-id="f0db7-185">Selecteer Hallo persoonlijke sleutelbestand (.pfx) van Hallo cluster certificaat dat u hebt opgegeven bij het maken van uw Service Fabric-cluster, een naam geven en Hallo-wachtwoord voor persoonlijke sleutel bevatten.</span><span class="sxs-lookup"><span data-stu-id="f0db7-185">Select hello private key file (.pfx) of hello cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide hello private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="f0db7-186">Deze zelfstudie wordt Hallo hetzelfde certificaat voor verificatie en cluster knooppunt naar de clientbeveiligingssessie.</span><span class="sxs-lookup"><span data-stu-id="f0db7-186">This tutorial uses hello same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="f0db7-187">U kunt een afzonderlijke clientcertificaat hebt u een geconfigureerde tooaccess Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="f0db7-187">You may use a separate client certificate if you have one configured tooaccess your Service Fabric cluster.</span></span>

### <a name="configure-hello-backend"></a><span data-ttu-id="f0db7-188">Hallo back-end configureren</span><span class="sxs-lookup"><span data-stu-id="f0db7-188">Configure hello backend</span></span>

<span data-ttu-id="f0db7-189">Nu dat API Management-beveiliging is geconfigureerd, kunt u Hallo Service Fabric-back-end kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="f0db7-189">Now that API Management security is configured, you can configure hello Service Fabric backend.</span></span> <span data-ttu-id="f0db7-190">Hallo Service Fabric-cluster is voor Service Fabric-back-ends, Hallo backend, in plaats van een specifieke Service Fabric-service.</span><span class="sxs-lookup"><span data-stu-id="f0db7-190">For Service Fabric backends, hello Service Fabric cluster is hello backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="f0db7-191">Hiermee wordt een enkele beleidsregel tooroute toomore dan één service in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f0db7-191">This allows a single policy tooroute toomore than one service in hello cluster.</span></span>

<span data-ttu-id="f0db7-192">Deze stap is vereist Hallo-toegangstoken die u eerder hebt gegenereerd en vingerafdruk voor uw cluster-certificaat dat u hebt geüpload tooAPI Management in de vorige stap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="f0db7-192">This step requires hello access token you generated earlier and hello thumbprint for your cluster certificate you uploaded tooAPI Management in hello previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="f0db7-193">Als u een afzonderlijke clientcertificaat in de vorige stap Hallo voor API Management gebruikt, moet u de vingerafdruk van het Hallo voor Hallo clientcertificaat in toevoeging toohello cluster certificaatvingerafdruk in deze stap.</span><span class="sxs-lookup"><span data-stu-id="f0db7-193">If you used a separate client certificate in hello previous step for API Management, you need hello thumbprint for hello client certificate in addition toohello cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="f0db7-194">Verzenden Hallo HTTP PUT-aanvraag toohello API Management-API-URL die u eerder hebt genoteerd bij het inschakelen van Hallo API Management REST API tooconfigure Hallo Service Fabric back-endservice te volgen.</span><span class="sxs-lookup"><span data-stu-id="f0db7-194">Send hello following HTTP PUT request toohello API Management API URL you noted earlier when enabling hello API Management REST API tooconfigure hello Service Fabric backend service.</span></span> <span data-ttu-id="f0db7-195">U ziet een `HTTP 201 Created` antwoord als Hallo-opdracht is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="f0db7-195">You should see an `HTTP 201 Created` response when hello command succeeds.</span></span> <span data-ttu-id="f0db7-196">Zie voor meer informatie over elk veld Hallo API Management [back-end voor API-naslagdocumentatie](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span><span class="sxs-lookup"><span data-stu-id="f0db7-196">For more information on each field, see hello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="f0db7-197">HTTP-opdracht en URL:</span><span class="sxs-lookup"><span data-stu-id="f0db7-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="f0db7-198">Headers voor aanvraag:</span><span class="sxs-lookup"><span data-stu-id="f0db7-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="f0db7-199">Hoofdtekst van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="f0db7-199">Request body:</span></span>
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

<span data-ttu-id="f0db7-200">Hallo **url** parameter hier is een volledig gekwalificeerde servicenaam van een service in het cluster die alle aanvragen zijn doorgestuurd tooby standaard als er geen servicenaam is opgegeven in een back-end-beleid.</span><span class="sxs-lookup"><span data-stu-id="f0db7-200">hello **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed tooby default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="f0db7-201">U kunt de naam van een valse service, zoals "fabric: / valse/service ' als u niet van plan toohave een fallback-service bent.</span><span class="sxs-lookup"><span data-stu-id="f0db7-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend toohave a fallback service.</span></span>

<span data-ttu-id="f0db7-202">Raadpleeg toohello API Management [back-end voor API-naslagdocumentatie](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) voor meer informatie over elk veld.</span><span class="sxs-lookup"><span data-stu-id="f0db7-202">Refer toohello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="f0db7-203">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="f0db7-203">Example</span></span>

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="f0db7-204">Een Service Fabric-back-end-service implementeren</span><span class="sxs-lookup"><span data-stu-id="f0db7-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="f0db7-205">Nu dat u Service Fabric geconfigureerd als een back-end tooAPI Management Hallo hebt, kunt u back-end-beleid schrijven voor uw API's die verkeer tooyour Service Fabric-services verzenden.</span><span class="sxs-lookup"><span data-stu-id="f0db7-205">Now that you have hello Service Fabric configured as a backend tooAPI Management, you can author backend policies for your APIs that send traffic tooyour Service Fabric services.</span></span> <span data-ttu-id="f0db7-206">Maar u moet eerst een service die wordt uitgevoerd in Service Fabric tooaccept aanvragen.</span><span class="sxs-lookup"><span data-stu-id="f0db7-206">But first you need a service running in Service Fabric tooaccept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="f0db7-207">Een Service Fabric-service met een HTTP-eindpunt maken</span><span class="sxs-lookup"><span data-stu-id="f0db7-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="f0db7-208">Voor deze zelfstudie maken we een eenvoudige staatloze ASP.NET Core betrouwbare Service met Web-API Hallo-project standaardsjabloon.</span><span class="sxs-lookup"><span data-stu-id="f0db7-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using hello default Web API project template.</span></span> <span data-ttu-id="f0db7-209">Hiermee maakt u een HTTP-eindpunt voor uw service, die u via Azure API Management gebruiken zult:</span><span class="sxs-lookup"><span data-stu-id="f0db7-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="f0db7-210">Start [instellen van uw ontwikkelomgeving voor het ontwikkelen van ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span><span class="sxs-lookup"><span data-stu-id="f0db7-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="f0db7-211">Zodra uw ontwikkelomgeving is ingesteld, start Visual Studio als beheerder en maak een ASP.NET Core-service:</span><span class="sxs-lookup"><span data-stu-id="f0db7-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="f0db7-212">In Visual Studio-Selecteer-Bestand > Nieuw Project.</span><span class="sxs-lookup"><span data-stu-id="f0db7-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="f0db7-213">Selecteer Hallo Service Fabric-toepassing sjabloon onder Cloud en geef deze de naam **'ApiApplication'**.</span><span class="sxs-lookup"><span data-stu-id="f0db7-213">Select hello Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="f0db7-214">Selecteer Hallo ASP.NET Core-servicesjabloon en naam Hallo project **'WebApiService'**.</span><span class="sxs-lookup"><span data-stu-id="f0db7-214">Select hello ASP.NET Core service template and name hello project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="f0db7-215">Hallo Web API ASP.NET Core 1.1-projectsjabloon selecteren.</span><span class="sxs-lookup"><span data-stu-id="f0db7-215">Select hello Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="f0db7-216">Zodra het Hallo-project is gemaakt, opent u `PackageRoot\ServiceManifest.xml` en verwijder Hallo `Port` kenmerk van de eindpuntconfiguratie resource Hallo:</span><span class="sxs-lookup"><span data-stu-id="f0db7-216">Once hello project is created, open `PackageRoot\ServiceManifest.xml` and remove hello `Port` attribute from hello endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="f0db7-217">Hierdoor kunnen Service Fabric toospecify een poort dynamisch van Hallo toepassingspoortbereik, dat wordt geopend via Hallo Netwerkbeveiligingsgroep in Hallo cluster Resource Manager-sjabloon, zodat u verkeer tooflow tooit van API Management.</span><span class="sxs-lookup"><span data-stu-id="f0db7-217">This allows Service Fabric toospecify a port dynamically from hello application port range, which we opened through hello Network Security Group in hello cluster Resource Manager template, allowing traffic tooflow tooit from API Management.</span></span>
 
 6. <span data-ttu-id="f0db7-218">Druk op F5 in Visual Studio tooverify Hallo web-API is lokaal beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f0db7-218">Press F5 in Visual Studio tooverify hello web API is available locally.</span></span> 

    <span data-ttu-id="f0db7-219">Service Fabric Explorer te openen en inzoomen tooa specifieke instantie van Hallo ASP.NET Core service toosee Hallo basisadres Hallo service luistert op.</span><span class="sxs-lookup"><span data-stu-id="f0db7-219">Open Service Fabric Explorer and drill down tooa specific instance of hello ASP.NET Core service toosee hello base address hello service is listening on.</span></span> <span data-ttu-id="f0db7-220">Voeg `/api/values` toohello basisadres en geopend in een browser.</span><span class="sxs-lookup"><span data-stu-id="f0db7-220">Add `/api/values` toohello base address and open it in a browser.</span></span> <span data-ttu-id="f0db7-221">Hiermee wordt de Hallo Get-methode op Hallo ValuesController in Hallo Web API-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f0db7-221">This invokes hello Get method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="f0db7-222">Deze retourneert Hallo standaardreactie die wordt geleverd door het Hallo-sjabloon, een JSON-matrix die twee tekenreeksen bevat:</span><span class="sxs-lookup"><span data-stu-id="f0db7-222">It returns hello default response that is provided by hello template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="f0db7-223">Dit is Hallo-eindpunt dat u via API Management in Azure gebruiken zult.</span><span class="sxs-lookup"><span data-stu-id="f0db7-223">This is hello endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="f0db7-224">Ten slotte Hallo toepassing tooyour cluster in Azure implementeren.</span><span class="sxs-lookup"><span data-stu-id="f0db7-224">Finally, deploy hello application tooyour cluster in Azure.</span></span> <span data-ttu-id="f0db7-225">[Met Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), met de rechtermuisknop op Hallo Application-project en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="f0db7-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click hello Application project and select **Publish**.</span></span> <span data-ttu-id="f0db7-226">Geef uw clustereindpunt (bijvoorbeeld `mycluster.westus.cloudapp.azure.com:19000`) toodeploy Hallo toepassing tooyour Service Fabric-cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="f0db7-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello application tooyour Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="f0db7-227">Een stateless service met de naam van ASP.NET Core `fabric:/ApiApplication/WebApiService` moet nu worden uitgevoerd in het Service Fabric-cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="f0db7-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="f0db7-228">Een API-bewerking maken</span><span class="sxs-lookup"><span data-stu-id="f0db7-228">Create an API operation</span></span>

<span data-ttu-id="f0db7-229">Nu we klaar toocreate een bewerking in API Management Hallo die toocommunicate voor het gebruik van externe clients met ASP.NET Core staatloze service wordt uitgevoerd op Hallo Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="f0db7-229">Now we're ready toocreate an operation in API Management that external clients use toocommunicate with hello ASP.NET Core stateless service running in hello Service Fabric cluster.</span></span>

 1. <span data-ttu-id="f0db7-230">Meld u bij toohello Azure-portal en navigeer tooyour API Management service-implementatie.</span><span class="sxs-lookup"><span data-stu-id="f0db7-230">Log in toohello Azure portal and navigate tooyour API Management service deployment.</span></span>
 2. <span data-ttu-id="f0db7-231">Selecteer in de blade voor Hallo API Management-service, **-API's - Preview**</span><span class="sxs-lookup"><span data-stu-id="f0db7-231">In hello API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="f0db7-232">Een nieuwe API toevoegen door te klikken op Hallo **leeg API** vak en invullen van het dialoogvenster Hallo:</span><span class="sxs-lookup"><span data-stu-id="f0db7-232">Add a new API by clicking hello **Blank API** box and filling out hello dialog box:</span></span>

     - <span data-ttu-id="f0db7-233">**Webservice-URL**: voor Service Fabric-back-ends, deze URL-waarde niet wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f0db7-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="f0db7-234">Hier kunt u een willekeurige waarde plaatsen.</span><span class="sxs-lookup"><span data-stu-id="f0db7-234">You can put any value here.</span></span> <span data-ttu-id="f0db7-235">Gebruik voor deze zelfstudie: `http://servicefabric`.</span><span class="sxs-lookup"><span data-stu-id="f0db7-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="f0db7-236">**Naam**: Geef een naam op voor uw API.</span><span class="sxs-lookup"><span data-stu-id="f0db7-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="f0db7-237">Gebruik voor deze zelfstudie `Service Fabric App`.</span><span class="sxs-lookup"><span data-stu-id="f0db7-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="f0db7-238">**URL-schema**: Selecteer HTTP, HTTPS of beide.</span><span class="sxs-lookup"><span data-stu-id="f0db7-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="f0db7-239">Gebruik voor deze zelfstudie `both`.</span><span class="sxs-lookup"><span data-stu-id="f0db7-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="f0db7-240">**Achtervoegsel voor API-URL**: Geef een achtervoegsel voor de API.</span><span class="sxs-lookup"><span data-stu-id="f0db7-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="f0db7-241">Gebruik voor deze zelfstudie `myapp`.</span><span class="sxs-lookup"><span data-stu-id="f0db7-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="f0db7-242">Zodra het Hallo-API is gemaakt, klikt u op **+ toevoegbewerking** tooadd een front-API-bewerking.</span><span class="sxs-lookup"><span data-stu-id="f0db7-242">Once hello API is created, click **+ Add operation** tooadd a front-end API operation.</span></span> <span data-ttu-id="f0db7-243">Vul Hallo waarden:</span><span class="sxs-lookup"><span data-stu-id="f0db7-243">Fill out hello values:</span></span>
    
     - <span data-ttu-id="f0db7-244">**URL**: Selecteer `GET` en een URL-pad opgeven voor Hallo API.</span><span class="sxs-lookup"><span data-stu-id="f0db7-244">**URL**: Select `GET` and provide a URL path for hello API.</span></span> <span data-ttu-id="f0db7-245">Gebruik voor deze zelfstudie `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="f0db7-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="f0db7-246">Standaard worden Hallo URL-pad hier opgegeven URL-pad Hallo toohello backend Service Fabric-service verzonden.</span><span class="sxs-lookup"><span data-stu-id="f0db7-246">By default, hello URL path specified here is hello URL path sent toohello backend Service Fabric service.</span></span> <span data-ttu-id="f0db7-247">Als u Hallo dezelfde URL-pad hier uw service in dit geval gebruikt `/api/values`, vervolgens Hallo-bewerking werkt zonder verdere aanpassing.</span><span class="sxs-lookup"><span data-stu-id="f0db7-247">If you use hello same URL path here that your service uses, in this case `/api/values`, then hello operation works without further modification.</span></span> <span data-ttu-id="f0db7-248">U kunt ook een URL-pad hier die verschilt van Hallo URL-pad gebruikt door uw back-end Service Fabric-service opgeven in dat geval u ziet ook nodig toospecify herschrijven van een pad in uw beleid voor de bewerking later.</span><span class="sxs-lookup"><span data-stu-id="f0db7-248">You may also specify a URL path here that is different from hello URL path used by your backend Service Fabric service, in which case you will also need toospecify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="f0db7-249">**Weergavenaam**: Geef een naam op voor Hallo API.</span><span class="sxs-lookup"><span data-stu-id="f0db7-249">**Display name**: Provide any name for hello API.</span></span> <span data-ttu-id="f0db7-250">Gebruik voor deze zelfstudie `Values`.</span><span class="sxs-lookup"><span data-stu-id="f0db7-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="f0db7-251">Een back-end-beleid configureren</span><span class="sxs-lookup"><span data-stu-id="f0db7-251">Configure a backend policy</span></span>

<span data-ttu-id="f0db7-252">Hallo back-end van beleid koppelt alles bij elkaar.</span><span class="sxs-lookup"><span data-stu-id="f0db7-252">hello backend policy ties everything together.</span></span> <span data-ttu-id="f0db7-253">Dit is waar het configureren van Hallo back-end Service Fabric toowhich serviceaanvragen worden gerouteerd.</span><span class="sxs-lookup"><span data-stu-id="f0db7-253">This is where you configure hello backend Service Fabric service toowhich requests are routed.</span></span> <span data-ttu-id="f0db7-254">U kunt deze bewerking beleid tooany API toepassen.</span><span class="sxs-lookup"><span data-stu-id="f0db7-254">You can apply this policy tooany API operation.</span></span> <span data-ttu-id="f0db7-255">Hallo [back-endconfiguratie voor Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) Hallo volgende aanvragen routering besturingselementen bevat:</span><span class="sxs-lookup"><span data-stu-id="f0db7-255">hello [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides hello following request routing controls:</span></span> 
 - <span data-ttu-id="f0db7-256">Service-exemplaar selecteren door op te geven van een naam in Service Fabric-service-exemplaar, ofwel hardcoded (bijvoorbeeld `"fabric:/myapp/myservice"`) of gegenereerd op basis van Hallo HTTP-aanvraag (bijvoorbeeld `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span><span class="sxs-lookup"><span data-stu-id="f0db7-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from hello HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="f0db7-257">Omzetting van de partitie een partitiesleutel met behulp van een Service Fabric-partitieschema te genereren.</span><span class="sxs-lookup"><span data-stu-id="f0db7-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="f0db7-258">De selectie van de replica voor stateful services.</span><span class="sxs-lookup"><span data-stu-id="f0db7-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="f0db7-259">Resolutie voorwaarden waarmee u toospecify Hallo voorwaarden voor een servicelocatie opnieuw op te lossen en het opnieuw verzenden van een aanvraag opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f0db7-259">Resolution retry conditions that allow you toospecify hello conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="f0db7-260">Voor deze zelfstudie maakt u een back-end-beleid routes aanvragen rechtstreeks toohello ASP.NET Core staatloze service eerder hebt geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="f0db7-260">For this tutorial, create a backend policy that routes requests directly toohello ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="f0db7-261">Selecteren en bewerken van Hallo **inkomende beleidsregels** voor Hallo `Values` bewerking door te klikken op het bewerkingspictogram Hallo en vervolgens te klikken op **codeweergave**.</span><span class="sxs-lookup"><span data-stu-id="f0db7-261">Select and edit hello **inbound policies** for hello `Values` operation by clicking hello edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="f0db7-262">Hallo beleid code-editor, Voeg een `set-backend-service` beleid onder inkomende beleidsregels, zoals hier wordt weergegeven en klik op Hallo **opslaan** knop:</span><span class="sxs-lookup"><span data-stu-id="f0db7-262">In hello policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click hello **Save** button:</span></span>
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

<span data-ttu-id="f0db7-263">Raadpleeg voor een volledige set van kenmerken voor Service Fabric-back-end beleid toohello [back-end-documentatie voor API Management](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span><span class="sxs-lookup"><span data-stu-id="f0db7-263">For a full set of Service Fabric back-end policy attributes, refer toohello [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-hello-api-tooa-product"></a><span data-ttu-id="f0db7-264">Hallo API tooa product toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f0db7-264">Add hello API tooa product.</span></span> 

<span data-ttu-id="f0db7-265">Voordat u Hallo API aanroepen kunt, moet worden deze tooa product waar u toousers toegang kunt geven toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f0db7-265">Before you can call hello API, it must be added tooa product where you can grant access toousers.</span></span> 

 1. <span data-ttu-id="f0db7-266">Selecteer in de Hallo API Management-service, **producten - PREVIEW**.</span><span class="sxs-lookup"><span data-stu-id="f0db7-266">In hello API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="f0db7-267">Standaard API Management providers twee producten: Starter en onbeperkt.</span><span class="sxs-lookup"><span data-stu-id="f0db7-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="f0db7-268">Selecteer Hallo onbeperkte product.</span><span class="sxs-lookup"><span data-stu-id="f0db7-268">Select hello Unlimited product.</span></span>
 3. <span data-ttu-id="f0db7-269">Selecteer de API's.</span><span class="sxs-lookup"><span data-stu-id="f0db7-269">Select APIs.</span></span>
 4. <span data-ttu-id="f0db7-270">Klik op Hallo **+ toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f0db7-270">Click hello **+ Add** button.</span></span>
 5. <span data-ttu-id="f0db7-271">Selecteer Hallo `Service Fabric App` API die u hebt gemaakt in de vorige stappen Hallo en klikt u op Hallo **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="f0db7-271">Select hello `Service Fabric App` API you created in hello previous steps and click hello **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="f0db7-272">Testen</span><span class="sxs-lookup"><span data-stu-id="f0db7-272">Test it</span></span>

<span data-ttu-id="f0db7-273">U kunt nu verzenden van een aanvraag tooyour back-endservice in Service Fabric via API Management rechtstreeks vanuit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f0db7-273">You can now try sending a request tooyour back-end service in Service Fabric through API Management directly from hello Azure portal.</span></span>

 1. <span data-ttu-id="f0db7-274">Selecteer in de Hallo API Management-service, **API - voorbeeld**.</span><span class="sxs-lookup"><span data-stu-id="f0db7-274">In hello API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="f0db7-275">In Hallo `Service Fabric App` API die u hebt gemaakt in de vorige stappen hello, selecteer Hallo **Test** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f0db7-275">In hello `Service Fabric App` API you created in hello previous steps, select hello **Test** tab.</span></span>
 3. <span data-ttu-id="f0db7-276">Klik op Hallo **verzenden** knop toosend een test aanvraag toohello back-endservice.</span><span class="sxs-lookup"><span data-stu-id="f0db7-276">Click hello **Send** button toosend a test request toohello backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0db7-277">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f0db7-277">Next steps</span></span>

<span data-ttu-id="f0db7-278">U hebt op dit moment een basisinstellingen met Service Fabric en API Management.</span><span class="sxs-lookup"><span data-stu-id="f0db7-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="f0db7-279">Deze zelfstudie wordt verificatie op basis van certificaten basisgebruiker voor uw Service Fabric-cluster tooget die u snel instellen.</span><span class="sxs-lookup"><span data-stu-id="f0db7-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster tooget you set up quickly.</span></span> <span data-ttu-id="f0db7-280">Meer geavanceerde gebruikersverificatie voor uw Service Fabric-cluster heeft de voorkeur boven met [Azure Active Directory-verificatie](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span><span class="sxs-lookup"><span data-stu-id="f0db7-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="f0db7-281">Vervolgens [maken en configureren van geavanceerde productinstellingen in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare uw toepassing op concrete verkeer.</span><span class="sxs-lookup"><span data-stu-id="f0db7-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare your application for real world traffic.</span></span>

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
