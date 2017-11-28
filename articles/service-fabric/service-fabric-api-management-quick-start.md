---
title: Azure Service Fabric met API Management snel aan de slag | Microsoft Docs
description: Deze handleiding wordt beschreven hoe u snel aan de slag met Azure API Management en Service Fabric.
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
ms.openlocfilehash: e9f44d8a43d274768f43261fea68f0da9c681ae1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="c47b6-103">Service Fabric met Azure API Management snel starten</span><span class="sxs-lookup"><span data-stu-id="c47b6-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="c47b6-104">Deze handleiding wordt beschreven hoe u Azure API Management met Service Fabric instellen en configureren van uw eerste API-bewerking voor het verzenden van verkeer naar de back-endservices in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c47b6-104">This guide shows you how to set up Azure API Management with Service Fabric and configure your first API operation to send traffic to back-end services in Service Fabric.</span></span> <span data-ttu-id="c47b6-105">Zie voor meer informatie over Azure API Management-scenario's met Service Fabric, de [overzicht](service-fabric-api-management-overview.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c47b6-105">To learn more about Azure API Management scenarios with Service Fabric, see the [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-to-azure"></a><span data-ttu-id="c47b6-106">API Management en Service Fabric implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="c47b6-106">Deploy API Management and Service Fabric to Azure</span></span>

<span data-ttu-id="c47b6-107">De eerste stap is het implementeren van API Management en een Service Fabric-cluster in Azure in een gedeelde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="c47b6-107">The first step is to deploy API Management and a Service Fabric cluster to Azure in a shared Virtual Network.</span></span> <span data-ttu-id="c47b6-108">Hiermee kunt API Management voor directe communicatie met Service Fabric zodat het detectie-service, service partitie resolutie en voorwaarts-verkeer rechtstreeks naar een back-endservice in Service Fabric kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c47b6-108">This allows API Management to communicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly to any backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="c47b6-109">Topologie</span><span class="sxs-lookup"><span data-stu-id="c47b6-109">Topology</span></span>

<span data-ttu-id="c47b6-110">Deze handleiding implementeert u de volgende topologie naar Azure waarin API Management en Service Fabric in de subnetten van hetzelfde virtuele netwerk zijn:</span><span class="sxs-lookup"><span data-stu-id="c47b6-110">This guide deploys the following topology to Azure in which API Management and Service Fabric are in subnets of the same Virtual Network:</span></span>

 ![Een bijschrift][sf-apim-topology-overview]

<span data-ttu-id="c47b6-112">Om snel aan de slag, zijn voor elke stap van de implementatie van Resource Manager-sjablonen beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="c47b6-112">To get started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="c47b6-113">Netwerktopologie:</span><span class="sxs-lookup"><span data-stu-id="c47b6-113">Network topology:</span></span>
    - <span data-ttu-id="c47b6-114">[Network.JSON][network-arm]</span><span class="sxs-lookup"><span data-stu-id="c47b6-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="c47b6-115">[Network.parameters.JSON][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="c47b6-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="c47b6-116">Service Fabric-cluster:</span><span class="sxs-lookup"><span data-stu-id="c47b6-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="c47b6-117">[cluster.JSON][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="c47b6-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="c47b6-118">[cluster.parameters.JSON][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="c47b6-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="c47b6-119">API Management:</span><span class="sxs-lookup"><span data-stu-id="c47b6-119">API Management:</span></span>
    - <span data-ttu-id="c47b6-120">[APIM.JSON][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="c47b6-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="c47b6-121">[APIM.parameters.JSON][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="c47b6-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-to-azure-and-select-your-subscription"></a><span data-ttu-id="c47b6-122">Aanmelden bij Azure en uw abonnement te selecteren</span><span class="sxs-lookup"><span data-stu-id="c47b6-122">Sign in to Azure and select your subscription</span></span>

<span data-ttu-id="c47b6-123">Maakt gebruik van deze handleiding [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="c47b6-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="c47b6-124">Wanneer u een nieuwe PowerShell-sessie start, zich aanmelden bij uw Azure-account en uw abonnement te selecteren voordat u Azure-opdrachten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c47b6-124">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="c47b6-125">Meld u bij uw Azure-account:</span><span class="sxs-lookup"><span data-stu-id="c47b6-125">Sign in to your Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="c47b6-126">Selecteer uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="c47b6-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="c47b6-127">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="c47b6-127">Create a resource group</span></span>

<span data-ttu-id="c47b6-128">Maak een nieuwe resourcegroep voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="c47b6-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="c47b6-129">Geef deze een naam en een locatie.</span><span class="sxs-lookup"><span data-stu-id="c47b6-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-the-network-topology"></a><span data-ttu-id="c47b6-130">De netwerktopologie implementeren</span><span class="sxs-lookup"><span data-stu-id="c47b6-130">Deploy the network topology</span></span>

<span data-ttu-id="c47b6-131">De eerste stap is het instellen van de netwerktopologie die API Management en de Service Fabric-cluster wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c47b6-131">The first step is to set up the network topology to which API Management and the Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="c47b6-132">De [network.json] [ network-arm] Resource Manager-sjabloon is geconfigureerd voor het maken van een virtueel netwerk (VNET) met twee subnetten en twee Netwerkbeveiligingsgroep groepen (NSG).</span><span class="sxs-lookup"><span data-stu-id="c47b6-132">The [network.json][network-arm] Resource Manager template is configured to create a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="c47b6-133">De [network.parameters.json] [ network-parameters-arm] parameterbestand bevat de namen van de subnetten en nsg's die API Management en Service Fabric om te worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c47b6-133">The [network.parameters.json][network-parameters-arm] parameters file contains the names of the subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="c47b6-134">Voor deze handleiding hoeft de parameterwaarden die niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c47b6-134">For this guide, the parameter values do not need to be changed.</span></span> <span data-ttu-id="c47b6-135">De sjablonen API Management en Service Fabric-Resource Manager gebruikt deze waarden, zodat ze hier zijn gewijzigd, moeten ze worden gewijzigd in de Resource Manager-sjablonen dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="c47b6-135">The API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in the other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="c47b6-136">De volgende Resource Manager-sjabloon en parameters bestand te downloaden:</span><span class="sxs-lookup"><span data-stu-id="c47b6-136">Download the following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="c47b6-137">[Network.JSON][network-arm]</span><span class="sxs-lookup"><span data-stu-id="c47b6-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="c47b6-138">[Network.parameters.JSON][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="c47b6-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="c47b6-139">Gebruik de volgende PowerShell-opdracht de Resource Manager-sjabloon en de parameterbestanden bestanden voor de netwerkinstallatie van de te implementeren:</span><span class="sxs-lookup"><span data-stu-id="c47b6-139">Use the following PowerShell command to deploy the Resource Manager template and parameter files for the network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-the-service-fabric-cluster"></a><span data-ttu-id="c47b6-140">De Service Fabric-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="c47b6-140">Deploy the Service Fabric cluster</span></span>

<span data-ttu-id="c47b6-141">Zodra de netwerkbronnen hebt implementeren, wordt de volgende stap is een Service Fabric-cluster implementeren voor het VNET in het subnet en NSG aangewezen voor de Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="c47b6-141">Once the network resources have finished deploying, the next step is to deploy a Service Fabric cluster to the VNET in the subnet and NSG designated for the Service Fabric cluster.</span></span> <span data-ttu-id="c47b6-142">Voor deze zelfstudie zijn de Service Fabric-Resource Manager-sjabloon is vooraf geconfigureerd voor het gebruik van de namen van de VNET, subnet en NSG die u in de vorige stap hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c47b6-142">For this tutorial, the Service Fabric Resource Manager template is pre-configured to use the names of the VNET, subnet, and NSG that you set up in the previous step.</span></span> 

<span data-ttu-id="c47b6-143">De Service Fabric-cluster Resource Manager-sjabloon is geconfigureerd voor het maken van een beveiligde cluster met Certificaatbeveiliging.</span><span class="sxs-lookup"><span data-stu-id="c47b6-143">The Service Fabric cluster Resource Manager template is configured to create a secure cluster with certificate security.</span></span> <span data-ttu-id="c47b6-144">Het certificaat wordt gebruikt voor het beveiligen van communicatie van knooppunt naar voor uw cluster en voor het beheren van de gebruikerstoegang tot uw Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="c47b6-144">The certificate is used to secure node-to-node communication for your cluster and to manage user access to your Service Fabric cluster.</span></span> <span data-ttu-id="c47b6-145">API Management gebruikt dit certificaat voor toegang tot de Service Fabric Naming Service voor de servicedetectie van de.</span><span class="sxs-lookup"><span data-stu-id="c47b6-145">API Management uses this certificate to access  the Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="c47b6-146">Deze stap is vereist dat u een certificaat in de Sleutelkluis voor clusterbeveiliging.</span><span class="sxs-lookup"><span data-stu-id="c47b6-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="c47b6-147">Zie voor meer informatie over het instellen van een beveiligde cluster met Sleutelkluis [in deze handleiding over het maken van een cluster in Azure Resource Manager gebruiken](service-fabric-cluster-creation-via-arm.md)</span><span class="sxs-lookup"><span data-stu-id="c47b6-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="c47b6-148">U kunt Azure Active Directory-verificatie naast het certificaat dat wordt gebruikt voor toegang tot cluster toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c47b6-148">You may add Azure Active Directory authentication in addition to the certificate used for cluster access.</span></span> <span data-ttu-id="c47b6-149">Azure Active Directory is de aanbevolen manier om de gebruikerstoegang beheren voor uw Service Fabric-cluster, maar is niet nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="c47b6-149">Azure Active Directory is the recommended way to manage user access to your Service Fabric cluster, but is not necessary to complete this tutorial.</span></span> <span data-ttu-id="c47b6-150">Een certificaat is vereist in beide gevallen voor cluster knooppunt naar beveiliging en Azure API Management-verificatie op dit moment biedt geen ondersteuning voor verificatie met Azure Active Directory voor een Service Fabric-back-end.</span><span class="sxs-lookup"><span data-stu-id="c47b6-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="c47b6-151">De volgende Resource Manager-sjabloon en parameters bestand te downloaden:</span><span class="sxs-lookup"><span data-stu-id="c47b6-151">Download the following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="c47b6-152">[cluster.JSON][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="c47b6-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="c47b6-153">[cluster.parameters.JSON][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="c47b6-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="c47b6-154">Vul de lege parameters in de `cluster.parameters.json` bestand voor uw implementatie, inclusief de [Sleutelkluis informatie](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) voor uw cluster-certificaat.</span><span class="sxs-lookup"><span data-stu-id="c47b6-154">Fill in the empty parameters in the `cluster.parameters.json` file for your deployment, including the [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="c47b6-155">Gebruik de volgende PowerShell-opdracht voor het implementeren van de Resource Manager-sjabloon en de parameterbestanden bestanden om de Service Fabric-cluster te maken:</span><span class="sxs-lookup"><span data-stu-id="c47b6-155">Use the following PowerShell command to deploy the Resource Manager template and parameter files to create the Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="c47b6-156">Implementeren van API Management</span><span class="sxs-lookup"><span data-stu-id="c47b6-156">Deploy API Management</span></span>

<span data-ttu-id="c47b6-157">Ten slotte API Management te implementeren naar het VNET in het subnet en NSG die is aangewezen voor API Management.</span><span class="sxs-lookup"><span data-stu-id="c47b6-157">Finally, deploy API Management to the VNET in the subnet and NSG designated for API Management.</span></span> <span data-ttu-id="c47b6-158">U hoeft niet te wachten op de implementatie van de Service Fabric-cluster te voltooien voordat u implementeert API Management.</span><span class="sxs-lookup"><span data-stu-id="c47b6-158">You do not need to wait for the Service Fabric cluster deployment to finish before deploying API Management.</span></span> 

<span data-ttu-id="c47b6-159">Voor deze zelfstudie zijn de API Management-Resource Manager-sjabloon is vooraf geconfigureerd voor het gebruik van de namen van de VNET, subnet en NSG die u in de vorige stap hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c47b6-159">For this tutorial, the API Management Resource Manager template is pre-configured to use the names of the VNET, subnet, and NSG that you set up in the previous step.</span></span> 

 1. <span data-ttu-id="c47b6-160">De volgende Resource Manager-sjabloon en parameters bestand te downloaden:</span><span class="sxs-lookup"><span data-stu-id="c47b6-160">Download the following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="c47b6-161">[APIM.JSON][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="c47b6-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="c47b6-162">[APIM.parameters.JSON][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="c47b6-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="c47b6-163">Vul de lege parameters in de `apim.parameters.json` voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="c47b6-163">Fill in the empty parameters in the `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="c47b6-164">Gebruik de volgende PowerShell-opdracht voor het implementeren van de Resource Manager-sjabloon en de parameter-bestanden voor API Management:</span><span class="sxs-lookup"><span data-stu-id="c47b6-164">Use the following PowerShell command to deploy the Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="c47b6-165">API Management configureren</span><span class="sxs-lookup"><span data-stu-id="c47b6-165">Configure API Management</span></span>

<span data-ttu-id="c47b6-166">Zodra uw API Management en Service Fabric-cluster worden geïmplementeerd, kunt u een Service Fabric-back-end kunt configureren in API Management.</span><span class="sxs-lookup"><span data-stu-id="c47b6-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="c47b6-167">Hiermee kunt u het beleid van een back-end die verkeer naar uw Service Fabric-cluster verzendt maken.</span><span class="sxs-lookup"><span data-stu-id="c47b6-167">This allows you to create a backend service policy that sends traffic to your Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="c47b6-168">Beveiliging van API Management</span><span class="sxs-lookup"><span data-stu-id="c47b6-168">API Management Security</span></span>

<span data-ttu-id="c47b6-169">Voor het configureren van de Service Fabric-back-end, moet u eerst API Management-beveiligingsinstellingen te configureren.</span><span class="sxs-lookup"><span data-stu-id="c47b6-169">To configure the Service Fabric backend, you first need to configure API Management security settings.</span></span> <span data-ttu-id="c47b6-170">Ga naar uw API Management-service in de Azure portal beveiligingsinstellingen voor configureren.</span><span class="sxs-lookup"><span data-stu-id="c47b6-170">To configure security settings, go to your API Management service in the Azure portal.</span></span>

#### <a name="enable-the-api-management-rest-api"></a><span data-ttu-id="c47b6-171">De REST-API van de API-beheer inschakelen</span><span class="sxs-lookup"><span data-stu-id="c47b6-171">Enable the API Management REST API</span></span>

<span data-ttu-id="c47b6-172">De API Management REST API is momenteel de enige manier om een back-endservice configureren.</span><span class="sxs-lookup"><span data-stu-id="c47b6-172">The API Management REST API is currently the only way to configure a backend service.</span></span> <span data-ttu-id="c47b6-173">De eerste stap is het inschakelen van de REST-API van API Management en beveilig deze.</span><span class="sxs-lookup"><span data-stu-id="c47b6-173">The first step is to enable the API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="c47b6-174">Selecteer in de API Management-service **Management-API - voorbeeld** onder **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="c47b6-174">In the API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="c47b6-175">Controleer de **API Management REST API inschakelen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="c47b6-175">Check the **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="c47b6-176">De URL van de API Management Opmerking: dit is de URL die we later gebruiken voor het instellen van de Service Fabric-back-end</span><span class="sxs-lookup"><span data-stu-id="c47b6-176">Note the Management API URL - this is the URL we'll use later to set up the Service Fabric backend</span></span>
 4. <span data-ttu-id="c47b6-177">Genereren een **toegangstoken** als u een vervaldatum en een sleutel selecteert, klikt u vervolgens op de **genereren** knop naar de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="c47b6-177">Generate an **access Token** by selecting an expiry date and a key, then click the **Generate** button toward the bottom of the page.</span></span>
 5. <span data-ttu-id="c47b6-178">Kopieer de **toegangstoken** en sla deze - kun je in de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="c47b6-178">Copy the **access token** and save it - we'll use this in the following steps.</span></span> <span data-ttu-id="c47b6-179">Houd er rekening mee dat deze verschilt van de primaire en secundaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="c47b6-179">Note this is different from the primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="c47b6-180">Een Service Fabric-client-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="c47b6-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="c47b6-181">API Management moet verifiëren met uw Service Fabric-cluster voor detectie van de service met behulp van een clientcertificaat dat toegang tot het cluster heeft.</span><span class="sxs-lookup"><span data-stu-id="c47b6-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access to your cluster.</span></span> <span data-ttu-id="c47b6-182">In deze zelfstudie gebruikt voor het gemak, hetzelfde certificaat opgegeven bij het maken van de Service Fabric-cluster, die standaard kan worden gebruikt voor toegang tot uw cluster.</span><span class="sxs-lookup"><span data-stu-id="c47b6-182">For simplicity, this tutorial uses the same certificate specified when creating the Service Fabric cluster, which by default can be used to access your cluster.</span></span>

 1. <span data-ttu-id="c47b6-183">Selecteer in de API Management-service **clientcertificaten - PREVIEW** onder **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="c47b6-183">In the API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="c47b6-184">Klik op de **+ toevoegen** knop</span><span class="sxs-lookup"><span data-stu-id="c47b6-184">Click the **+ Add** button</span></span>
 2. <span data-ttu-id="c47b6-185">Selecteer het persoonlijke sleutelbestand (.pfx) van het cluster-certificaat dat u hebt opgegeven bij het maken van uw Service Fabric-cluster, een naam geven en het wachtwoord van de persoonlijke sleutel bevatten.</span><span class="sxs-lookup"><span data-stu-id="c47b6-185">Select the private key file (.pfx) of the cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide the private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="c47b6-186">Deze zelfstudie gebruikt hetzelfde certificaat voor clientverificatie en clusterbeveiliging knooppunt naar.</span><span class="sxs-lookup"><span data-stu-id="c47b6-186">This tutorial uses the same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="c47b6-187">U kunt een afzonderlijke clientcertificaat als u geconfigureerd hebt voor toegang tot uw Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="c47b6-187">You may use a separate client certificate if you have one configured to access your Service Fabric cluster.</span></span>

### <a name="configure-the-backend"></a><span data-ttu-id="c47b6-188">De back-end configureren</span><span class="sxs-lookup"><span data-stu-id="c47b6-188">Configure the backend</span></span>

<span data-ttu-id="c47b6-189">Nu dat API Management-beveiliging is geconfigureerd, kunt u de Service Fabric-back-end kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="c47b6-189">Now that API Management security is configured, you can configure the Service Fabric backend.</span></span> <span data-ttu-id="c47b6-190">Voor Service Fabric-back-ends is de Service Fabric-cluster de back-end, in plaats van een specifieke Service Fabric-service.</span><span class="sxs-lookup"><span data-stu-id="c47b6-190">For Service Fabric backends, the Service Fabric cluster is the backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="c47b6-191">Hierdoor kan een enkele beleidsregel voor het routeren naar meer dan één service in het cluster.</span><span class="sxs-lookup"><span data-stu-id="c47b6-191">This allows a single policy to route to more than one service in the cluster.</span></span>

<span data-ttu-id="c47b6-192">Deze stap is vereist van het toegangstoken dat u eerder hebt gegenereerd en de vingerafdruk voor uw cluster-certificaat dat u hebt geüpload naar de API Management in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="c47b6-192">This step requires the access token you generated earlier and the thumbprint for your cluster certificate you uploaded to API Management in the previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="c47b6-193">Als u een afzonderlijke clientcertificaat in de vorige stap voor API Management gebruikt, moet u de vingerafdruk voor het clientcertificaat naast de certificaatvingerafdruk cluster in deze stap.</span><span class="sxs-lookup"><span data-stu-id="c47b6-193">If you used a separate client certificate in the previous step for API Management, you need the thumbprint for the client certificate in addition to the cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="c47b6-194">Verzenden van de volgende HTTP PUT-aanvraag naar de URL van API Management API u eerder hebt genoteerd bij het inschakelen van de API Management REST API voor het configureren van de Service Fabric-back-endservice.</span><span class="sxs-lookup"><span data-stu-id="c47b6-194">Send the following HTTP PUT request to the API Management API URL you noted earlier when enabling the API Management REST API to configure the Service Fabric backend service.</span></span> <span data-ttu-id="c47b6-195">U ziet een `HTTP 201 Created` antwoord als de opdracht is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="c47b6-195">You should see an `HTTP 201 Created` response when the command succeeds.</span></span> <span data-ttu-id="c47b6-196">Zie voor meer informatie over elk veld de API Management [back-end voor API-naslagdocumentatie](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span><span class="sxs-lookup"><span data-stu-id="c47b6-196">For more information on each field, see the API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="c47b6-197">HTTP-opdracht en URL:</span><span class="sxs-lookup"><span data-stu-id="c47b6-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="c47b6-198">Headers voor aanvraag:</span><span class="sxs-lookup"><span data-stu-id="c47b6-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="c47b6-199">Hoofdtekst van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="c47b6-199">Request body:</span></span>
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

<span data-ttu-id="c47b6-200">De **url** parameter hier is een volledig gekwalificeerde servicenaam van een service in het cluster dat alle aanvragen worden doorgestuurd naar standaard als er geen servicenaam is opgegeven in een back-end-beleid.</span><span class="sxs-lookup"><span data-stu-id="c47b6-200">The **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed to by default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="c47b6-201">U kunt de naam van een valse service, zoals "fabric: / valse/service ' als u niet van plan bent om een fallback-service.</span><span class="sxs-lookup"><span data-stu-id="c47b6-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend to have a fallback service.</span></span>

<span data-ttu-id="c47b6-202">Verwijzen naar de API Management [back-end voor API-naslagdocumentatie](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) voor meer informatie over elk veld.</span><span class="sxs-lookup"><span data-stu-id="c47b6-202">Refer to the API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="c47b6-203">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c47b6-203">Example</span></span>

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

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="c47b6-204">Een Service Fabric-back-end-service implementeren</span><span class="sxs-lookup"><span data-stu-id="c47b6-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="c47b6-205">Nu dat u de Fabric-Service is geconfigureerd als een back-end voor API Management hebt, kunt u back-end-beleid schrijven voor uw API's die verkeer aan uw Service Fabric-services verzenden.</span><span class="sxs-lookup"><span data-stu-id="c47b6-205">Now that you have the Service Fabric configured as a backend to API Management, you can author backend policies for your APIs that send traffic to your Service Fabric services.</span></span> <span data-ttu-id="c47b6-206">Maar u moet eerst een service die wordt uitgevoerd in Service Fabric om aanvragen te accepteren.</span><span class="sxs-lookup"><span data-stu-id="c47b6-206">But first you need a service running in Service Fabric to accept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="c47b6-207">Een Service Fabric-service met een HTTP-eindpunt maken</span><span class="sxs-lookup"><span data-stu-id="c47b6-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="c47b6-208">Voor deze zelfstudie maken we een eenvoudige staatloze ASP.NET Core betrouwbare Service met de standaardsjabloon voor de Web-API-project.</span><span class="sxs-lookup"><span data-stu-id="c47b6-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using the default Web API project template.</span></span> <span data-ttu-id="c47b6-209">Hiermee maakt u een HTTP-eindpunt voor uw service, die u via Azure API Management gebruiken zult:</span><span class="sxs-lookup"><span data-stu-id="c47b6-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="c47b6-210">Start [instellen van uw ontwikkelomgeving voor het ontwikkelen van ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span><span class="sxs-lookup"><span data-stu-id="c47b6-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="c47b6-211">Zodra uw ontwikkelomgeving is ingesteld, start Visual Studio als beheerder en maak een ASP.NET Core-service:</span><span class="sxs-lookup"><span data-stu-id="c47b6-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="c47b6-212">In Visual Studio-Selecteer-Bestand > Nieuw Project.</span><span class="sxs-lookup"><span data-stu-id="c47b6-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="c47b6-213">Selecteer de sjabloon Service Fabric-toepassing in de Cloud en geef deze de naam **'ApiApplication'**.</span><span class="sxs-lookup"><span data-stu-id="c47b6-213">Select the Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="c47b6-214">Selecteer de servicesjabloon ASP.NET Core en noem het project **'WebApiService'**.</span><span class="sxs-lookup"><span data-stu-id="c47b6-214">Select the ASP.NET Core service template and name the project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="c47b6-215">Selecteer de projectsjabloon Web API ASP.NET Core 1.1.</span><span class="sxs-lookup"><span data-stu-id="c47b6-215">Select the Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="c47b6-216">Zodra het project is gemaakt, opent u `PackageRoot\ServiceManifest.xml` en verwijder de `Port` kenmerk van de eindpuntconfiguratie resource:</span><span class="sxs-lookup"><span data-stu-id="c47b6-216">Once the project is created, open `PackageRoot\ServiceManifest.xml` and remove the `Port` attribute from the endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="c47b6-217">Hierdoor kunnen Service Fabric om op te geven van een poort dynamisch van de toepassing-poortbereik wordt geopend via de Netwerkbeveiligingsgroep in het cluster Resource Manager-sjabloon die het verkeer naar deze stromen van API Management.</span><span class="sxs-lookup"><span data-stu-id="c47b6-217">This allows Service Fabric to specify a port dynamically from the application port range, which we opened through the Network Security Group in the cluster Resource Manager template, allowing traffic to flow to it from API Management.</span></span>
 
 6. <span data-ttu-id="c47b6-218">Druk op F5 in Visual Studio om te controleren of de web-API is lokaal beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="c47b6-218">Press F5 in Visual Studio to verify the web API is available locally.</span></span> 

    <span data-ttu-id="c47b6-219">Open Service Fabric Explorer en inzoomen naar beneden op een specifiek exemplaar van de service ASP.NET Core ziet u het basisadres wordt de service luistert op.</span><span class="sxs-lookup"><span data-stu-id="c47b6-219">Open Service Fabric Explorer and drill down to a specific instance of the ASP.NET Core service to see the base address the service is listening on.</span></span> <span data-ttu-id="c47b6-220">Voeg `/api/values` naar de basistabel adres en in een browser te openen.</span><span class="sxs-lookup"><span data-stu-id="c47b6-220">Add `/api/values` to the base address and open it in a browser.</span></span> <span data-ttu-id="c47b6-221">Hiermee wordt de Get-methode op de ValuesController in de Web-API-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c47b6-221">This invokes the Get method on the ValuesController in the Web API template.</span></span> <span data-ttu-id="c47b6-222">Deze retourneert de standaardreactie die wordt geleverd door de sjabloon, een JSON-matrix die twee tekenreeksen bevat:</span><span class="sxs-lookup"><span data-stu-id="c47b6-222">It returns the default response that is provided by the template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="c47b6-223">Dit is het eindpunt dat u via API Management in Azure gebruiken zult.</span><span class="sxs-lookup"><span data-stu-id="c47b6-223">This is the endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="c47b6-224">Ten slotte de toepassing aan het cluster in Azure implementeren.</span><span class="sxs-lookup"><span data-stu-id="c47b6-224">Finally, deploy the application to your cluster in Azure.</span></span> <span data-ttu-id="c47b6-225">[Met Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), met de rechtermuisknop op het toepassingsproject en selecteert u **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="c47b6-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click the Application project and select **Publish**.</span></span> <span data-ttu-id="c47b6-226">Geef uw clustereindpunt (bijvoorbeeld `mycluster.westus.cloudapp.azure.com:19000`) om de toepassing aan uw Service Fabric-cluster in Azure te implementeren.</span><span class="sxs-lookup"><span data-stu-id="c47b6-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) to deploy the application to your Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="c47b6-227">Een stateless service met de naam van ASP.NET Core `fabric:/ApiApplication/WebApiService` moet nu worden uitgevoerd in het Service Fabric-cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="c47b6-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="c47b6-228">Een API-bewerking maken</span><span class="sxs-lookup"><span data-stu-id="c47b6-228">Create an API operation</span></span>

<span data-ttu-id="c47b6-229">Nu we gaan maken van een bewerking in API Management waarmee externe clients communiceren met de ASP.NET Core staatloze service in de Service Fabric-cluster wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c47b6-229">Now we're ready to create an operation in API Management that external clients use to communicate with the ASP.NET Core stateless service running in the Service Fabric cluster.</span></span>

 1. <span data-ttu-id="c47b6-230">Aanmelden bij de Azure-portal en navigeer naar uw API Management-service-implementatie.</span><span class="sxs-lookup"><span data-stu-id="c47b6-230">Log in to the Azure portal and navigate to your API Management service deployment.</span></span>
 2. <span data-ttu-id="c47b6-231">Selecteer in de blade API Management-service **-API's - Preview**</span><span class="sxs-lookup"><span data-stu-id="c47b6-231">In the API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="c47b6-232">Een nieuwe API toevoegen door te klikken op de **leeg API** vak en invullen van het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="c47b6-232">Add a new API by clicking the **Blank API** box and filling out the dialog box:</span></span>

     - <span data-ttu-id="c47b6-233">**Webservice-URL**: voor Service Fabric-back-ends, deze URL-waarde niet wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c47b6-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="c47b6-234">Hier kunt u een willekeurige waarde plaatsen.</span><span class="sxs-lookup"><span data-stu-id="c47b6-234">You can put any value here.</span></span> <span data-ttu-id="c47b6-235">Gebruik voor deze zelfstudie: `http://servicefabric`.</span><span class="sxs-lookup"><span data-stu-id="c47b6-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="c47b6-236">**Naam**: Geef een naam op voor uw API.</span><span class="sxs-lookup"><span data-stu-id="c47b6-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="c47b6-237">Gebruik voor deze zelfstudie `Service Fabric App`.</span><span class="sxs-lookup"><span data-stu-id="c47b6-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="c47b6-238">**URL-schema**: Selecteer HTTP, HTTPS of beide.</span><span class="sxs-lookup"><span data-stu-id="c47b6-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="c47b6-239">Gebruik voor deze zelfstudie `both`.</span><span class="sxs-lookup"><span data-stu-id="c47b6-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="c47b6-240">**Achtervoegsel voor API-URL**: Geef een achtervoegsel voor de API.</span><span class="sxs-lookup"><span data-stu-id="c47b6-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="c47b6-241">Gebruik voor deze zelfstudie `myapp`.</span><span class="sxs-lookup"><span data-stu-id="c47b6-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="c47b6-242">Zodra de API is gemaakt, klikt u op **+ toevoegbewerking** toevoegen van een front-API-bewerking.</span><span class="sxs-lookup"><span data-stu-id="c47b6-242">Once the API is created, click **+ Add operation** to add a front-end API operation.</span></span> <span data-ttu-id="c47b6-243">Vul de parameterwaarden:</span><span class="sxs-lookup"><span data-stu-id="c47b6-243">Fill out the values:</span></span>
    
     - <span data-ttu-id="c47b6-244">**URL**: Selecteer `GET` en geef een URL-pad voor de API.</span><span class="sxs-lookup"><span data-stu-id="c47b6-244">**URL**: Select `GET` and provide a URL path for the API.</span></span> <span data-ttu-id="c47b6-245">Gebruik voor deze zelfstudie `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="c47b6-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="c47b6-246">Standaard worden de URL-pad hier opgegeven wordt het URL-pad naar de back-end Service Fabric-service verzonden.</span><span class="sxs-lookup"><span data-stu-id="c47b6-246">By default, the URL path specified here is the URL path sent to the backend Service Fabric service.</span></span> <span data-ttu-id="c47b6-247">Als u de dezelfde URL-pad hier uw service in dit geval gebruikt `/api/values`, klikt u vervolgens de bewerking werkt zonder verdere aanpassing.</span><span class="sxs-lookup"><span data-stu-id="c47b6-247">If you use the same URL path here that your service uses, in this case `/api/values`, then the operation works without further modification.</span></span> <span data-ttu-id="c47b6-248">U kunt ook een URL-pad hier die verschilt van het URL-pad gebruikt door uw back-end Service Fabric-service opgeven, in welk geval u moet ook later een herschrijven pad opgeven in het beleid opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c47b6-248">You may also specify a URL path here that is different from the URL path used by your backend Service Fabric service, in which case you will also need to specify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="c47b6-249">**Weergavenaam**: Geef een naam op voor de API.</span><span class="sxs-lookup"><span data-stu-id="c47b6-249">**Display name**: Provide any name for the API.</span></span> <span data-ttu-id="c47b6-250">Gebruik voor deze zelfstudie `Values`.</span><span class="sxs-lookup"><span data-stu-id="c47b6-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="c47b6-251">Een back-end-beleid configureren</span><span class="sxs-lookup"><span data-stu-id="c47b6-251">Configure a backend policy</span></span>

<span data-ttu-id="c47b6-252">Het back-end-beleid bindt alles bij elkaar.</span><span class="sxs-lookup"><span data-stu-id="c47b6-252">The backend policy ties everything together.</span></span> <span data-ttu-id="c47b6-253">Dit is waar het configureren van de Service Fabric-service van het back-end waarnaar aanvragen worden doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="c47b6-253">This is where you configure the backend Service Fabric service to which requests are routed.</span></span> <span data-ttu-id="c47b6-254">U kunt dit beleid toepassen op alle API-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="c47b6-254">You can apply this policy to any API operation.</span></span> <span data-ttu-id="c47b6-255">De [back-endconfiguratie voor Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) biedt de volgende vragen routering besturingselementen:</span><span class="sxs-lookup"><span data-stu-id="c47b6-255">The [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides the following request routing controls:</span></span> 
 - <span data-ttu-id="c47b6-256">Service-exemplaar selecteren door op te geven van een naam in Service Fabric-service-exemplaar, ofwel hardcoded (bijvoorbeeld `"fabric:/myapp/myservice"`) of gegenereerd op basis van de HTTP-aanvraag (bijvoorbeeld `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span><span class="sxs-lookup"><span data-stu-id="c47b6-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from the HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="c47b6-257">Omzetting van de partitie een partitiesleutel met behulp van een Service Fabric-partitieschema te genereren.</span><span class="sxs-lookup"><span data-stu-id="c47b6-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="c47b6-258">De selectie van de replica voor stateful services.</span><span class="sxs-lookup"><span data-stu-id="c47b6-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="c47b6-259">Oplossing opnieuw voorwaarden waarmee u kunt de voorwaarden opgeven voor een servicelocatie opnieuw op te lossen en het opnieuw verzenden van een aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c47b6-259">Resolution retry conditions that allow you to specify the conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="c47b6-260">Voor deze zelfstudie maakt u een back-end-beleid waarmee aanvragen rechtstreeks worden doorgestuurd naar de ASP.NET Core staatloze service eerder hebt geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="c47b6-260">For this tutorial, create a backend policy that routes requests directly to the ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="c47b6-261">Selecteren en te bewerken de **inkomende beleidsregels** voor de `Values` bewerking door te klikken op het bewerkingspictogram en vervolgens te klikken op **codeweergave**.</span><span class="sxs-lookup"><span data-stu-id="c47b6-261">Select and edit the **inbound policies** for the `Values` operation by clicking the edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="c47b6-262">Voeg in de beleidseditor code een `set-backend-service` beleid onder inkomende beleidsregels, zoals hier wordt weergegeven en klik op de **opslaan** knop:</span><span class="sxs-lookup"><span data-stu-id="c47b6-262">In the policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click the **Save** button:</span></span>
    
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

<span data-ttu-id="c47b6-263">Voor een volledige set kenmerken voor Service Fabric-back-end-beleid, raadpleegt u de [API Management-documentatie voor back-end](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span><span class="sxs-lookup"><span data-stu-id="c47b6-263">For a full set of Service Fabric back-end policy attributes, refer to the [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-the-api-to-a-product"></a><span data-ttu-id="c47b6-264">De API toevoegen aan een product.</span><span class="sxs-lookup"><span data-stu-id="c47b6-264">Add the API to a product.</span></span> 

<span data-ttu-id="c47b6-265">Voordat u de API aanroepen kunt, moet deze worden toegevoegd aan een product waar u toegang aan gebruikers verlenen.</span><span class="sxs-lookup"><span data-stu-id="c47b6-265">Before you can call the API, it must be added to a product where you can grant access to users.</span></span> 

 1. <span data-ttu-id="c47b6-266">Selecteer in de API Management-service **producten - PREVIEW**.</span><span class="sxs-lookup"><span data-stu-id="c47b6-266">In the API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="c47b6-267">Standaard API Management providers twee producten: Starter en onbeperkt.</span><span class="sxs-lookup"><span data-stu-id="c47b6-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="c47b6-268">Selecteer het onbeperkte product.</span><span class="sxs-lookup"><span data-stu-id="c47b6-268">Select the Unlimited product.</span></span>
 3. <span data-ttu-id="c47b6-269">Selecteer de API's.</span><span class="sxs-lookup"><span data-stu-id="c47b6-269">Select APIs.</span></span>
 4. <span data-ttu-id="c47b6-270">Klik op de **+ toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c47b6-270">Click the **+ Add** button.</span></span>
 5. <span data-ttu-id="c47b6-271">Selecteer de `Service Fabric App` API die u hebt gemaakt in de vorige stappen en klik op de **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="c47b6-271">Select the `Service Fabric App` API you created in the previous steps and click the **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="c47b6-272">Testen</span><span class="sxs-lookup"><span data-stu-id="c47b6-272">Test it</span></span>

<span data-ttu-id="c47b6-273">U kunt nu een aanvraag verzenden naar uw back-endservice in Service Fabric via API Management rechtstreeks vanuit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c47b6-273">You can now try sending a request to your back-end service in Service Fabric through API Management directly from the Azure portal.</span></span>

 1. <span data-ttu-id="c47b6-274">Selecteer in de API Management-service **API - voorbeeld**.</span><span class="sxs-lookup"><span data-stu-id="c47b6-274">In the API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="c47b6-275">In de `Service Fabric App` API die u hebt gemaakt in de vorige stappen, selecteer de **Test** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c47b6-275">In the `Service Fabric App` API you created in the previous steps, select the **Test** tab.</span></span>
 3. <span data-ttu-id="c47b6-276">Klik op de **verzenden** knop een testaanvraag verzenden naar de back-endservice.</span><span class="sxs-lookup"><span data-stu-id="c47b6-276">Click the **Send** button to send a test request to the backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c47b6-277">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c47b6-277">Next steps</span></span>

<span data-ttu-id="c47b6-278">U hebt op dit moment een basisinstellingen met Service Fabric en API Management.</span><span class="sxs-lookup"><span data-stu-id="c47b6-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="c47b6-279">Deze zelfstudie maakt gebruik van verificatie op basis van certificaten basisgebruiker voor uw Service Fabric-cluster weer om u snel instellen.</span><span class="sxs-lookup"><span data-stu-id="c47b6-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster to get you set up quickly.</span></span> <span data-ttu-id="c47b6-280">Meer geavanceerde gebruikersverificatie voor uw Service Fabric-cluster heeft de voorkeur boven met [Azure Active Directory-verificatie](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span><span class="sxs-lookup"><span data-stu-id="c47b6-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="c47b6-281">Vervolgens [maken en configureren van geavanceerde productinstellingen in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) voorbereiden van uw toepassing op concrete verkeer.</span><span class="sxs-lookup"><span data-stu-id="c47b6-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) to prepare your application for real world traffic.</span></span>

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
