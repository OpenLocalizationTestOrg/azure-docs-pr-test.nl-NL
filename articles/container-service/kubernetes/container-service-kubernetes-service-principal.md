---
title: aaaService principal voor Azure Kubernetes cluster | Microsoft Docs
description: Een service-principal voor Azure Active Directory voor een Kubernetes-cluster in Azure Container Service maken en beheren
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="64e1c-103">Een service-principal voor Azure AD voor een Kubernetes-cluster in Container Service instellen</span><span class="sxs-lookup"><span data-stu-id="64e1c-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="64e1c-104">In Azure Container Service een cluster Kubernetes vereist een [Azure Active Directory-service-principal](../../active-directory/develop/active-directory-application-objects.md) toointeract met Azure-API's.</span><span class="sxs-lookup"><span data-stu-id="64e1c-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) toointeract with Azure APIs.</span></span> <span data-ttu-id="64e1c-105">Hallo service-principal is nodig toodynamically beheren van resources, zoals [gebruiker gedefinieerde routes](../../virtual-network/virtual-networks-udr-overview.md) en Hallo [laag 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64e1c-105">hello service principal is needed toodynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and hello [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="64e1c-106">In dit artikel bevat verschillende opties tooset van een service principal voor uw cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="64e1c-106">This article shows different options tooset up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="64e1c-107">Bijvoorbeeld, als u geïnstalleerd en geconfigureerd Hallo [Azure CLI 2.0](/cli/azure/install-az-cli2), kunt u Hallo uitvoeren [ `az acs create` ](/cli/azure/acs#create) opdracht toocreate hello Kubernetes cluster en Hallo service-principal op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="64e1c-107">For example, if you installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster and hello service principal at hello same time.</span></span>


## <a name="requirements-for-hello-service-principal"></a><span data-ttu-id="64e1c-108">Vereisten voor service-principal Hallo</span><span class="sxs-lookup"><span data-stu-id="64e1c-108">Requirements for hello service principal</span></span>

<span data-ttu-id="64e1c-109">U kunt een bestaande Azure AD-service-principal Hallo volgens de vereisten voldoet aan of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="64e1c-109">You can use an existing Azure AD service principal that meets hello following requirements, or create a new one.</span></span>

* <span data-ttu-id="64e1c-110">**Bereik**: Hallo resourcegroep in Hallo abonnement toodeploy hello Kubernetes cluster gebruikt of (minder restrictief) Hallo abonnement toodeploy Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="64e1c-110">**Scope**: hello resource group in hello subscription used toodeploy hello Kubernetes cluster, or (less restrictively) hello subscription used toodeploy hello cluster.</span></span>

* <span data-ttu-id="64e1c-111">**Rol**: **inzender**</span><span class="sxs-lookup"><span data-stu-id="64e1c-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="64e1c-112">**Clientgeheim**: moet een wachtwoord zijn.</span><span class="sxs-lookup"><span data-stu-id="64e1c-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="64e1c-113">U kunt momenteel geen service-principal gebruiken om verificatie via een certificaat in te stellen.</span><span class="sxs-lookup"><span data-stu-id="64e1c-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="64e1c-114">een service-principal toocreate, u moet machtigingen tooregister een toepassing hebt met uw Azure AD-tenant en tooassign Hallo toepassingsrol tooa in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="64e1c-114">toocreate a service principal, you must have permissions tooregister an application with your Azure AD tenant, and tooassign hello application tooa role in your subscription.</span></span> <span data-ttu-id="64e1c-115">toosee als u Hallo vereist machtigingen hebt, [inchecken Hallo Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="64e1c-115">toosee if you have hello required permissions, [check in hello Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="64e1c-116">Optie 1: een service-principal maken in Azure AD</span><span class="sxs-lookup"><span data-stu-id="64e1c-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="64e1c-117">Als u een Azure AD-service-principal toocreate wilt voordat u uw cluster Kubernetes implementeert, biedt Azure verschillende methoden.</span><span class="sxs-lookup"><span data-stu-id="64e1c-117">If you want toocreate an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="64e1c-118">Hallo volgende voorbeeldopdrachten laten zien hoe u toodo dit Hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="64e1c-118">hello following example commands show you how toodo this with hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="64e1c-119">U kunt ook een maken service principal met [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), Hallo [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), of andere methoden.</span><span class="sxs-lookup"><span data-stu-id="64e1c-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="64e1c-120">Uitvoer is vergelijkbaar toohello volgende (hier weergegeven geredigeerde):</span><span class="sxs-lookup"><span data-stu-id="64e1c-120">Output is similar toohello following (shown here redacted):</span></span>

![Een service-principal maken](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="64e1c-122">Hallo gemarkeerd zijn **client-ID** (`appId`) en Hallo **clientgeheim** (`password`) die u gebruikt als parameters van de service-principal voor implementatie van het cluster.</span><span class="sxs-lookup"><span data-stu-id="64e1c-122">Highlighted are hello **client ID** (`appId`) and hello **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a><span data-ttu-id="64e1c-123">Service-principal bij het maken van Hallo Kubernetes cluster opgeven</span><span class="sxs-lookup"><span data-stu-id="64e1c-123">Specify service principal when creating hello Kubernetes cluster</span></span>

<span data-ttu-id="64e1c-124">Hallo bieden **client-ID** (ook wel Hallo `appId`, voor toepassings-ID) en **clientgeheim** (`password`) van een bestaande service-principal als parameters bij het maken van Hallo Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="64e1c-124">Provide hello **client ID** (also called hello `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create hello Kubernetes cluster.</span></span> <span data-ttu-id="64e1c-125">Zorg ervoor dat service-principal Hallo Hallo voldoet op Hallo vanaf dit artikel.</span><span class="sxs-lookup"><span data-stu-id="64e1c-125">Make sure hello service principal meets hello requirements at hello beginning this article.</span></span>

<span data-ttu-id="64e1c-126">U kunt deze parameters opgeven bij het implementeren van Hallo Kubernetes cluster met behulp van Hallo [Azure opdrachtregelinterface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure-portal](../dcos-swarm/container-service-deployment.md), of andere methoden.</span><span class="sxs-lookup"><span data-stu-id="64e1c-126">You can specify these parameters when deploying hello Kubernetes cluster using hello [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="64e1c-127">Bij het opgeven van Hallo **client-ID**, worden ervoor toouse hello `appId`, niet Hallo `ObjectId`, van de service-principal Hallo.</span><span class="sxs-lookup"><span data-stu-id="64e1c-127">When specifying hello **client ID**, be sure toouse hello `appId`, not hello `ObjectId`, of hello service principal.</span></span>
>

<span data-ttu-id="64e1c-128">Hallo volgende voorbeeld ziet eenrichtingssessie toopass Hallo parameters Hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="64e1c-128">hello following example shows one way toopass hello parameters with hello Azure CLI 2.0.</span></span> <span data-ttu-id="64e1c-129">In dit voorbeeld wordt Hallo [Kubernetes snelstartsjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="64e1c-129">This example uses hello [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="64e1c-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) Hallo parameters sjabloonbestand `azuredeploy.parameters.json` vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="64e1c-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) hello template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="64e1c-131">toospecify hello service-principal, voer waarden in voor `servicePrincipalClientId` en `servicePrincipalClientSecret` in Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="64e1c-131">toospecify hello service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in hello file.</span></span> <span data-ttu-id="64e1c-132">(U moet ook tooprovide uw eigen waarden voor `dnsNamePrefix` en `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="64e1c-132">(You also need tooprovide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="64e1c-133">Hallo laatstgenoemde is Hallo SSH openbare sleutel tooaccess Hallo cluster.) Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="64e1c-133">hello latter is hello SSH public key tooaccess hello cluster.) Save hello file.</span></span>

    ![Parameters voor de service-principal doorgeven](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="64e1c-135">Voer Hallo de volgende opdracht, met behulp van `--parameters` tooset Hallo pad toohello azuredeploy.parameters.json bestand.</span><span class="sxs-lookup"><span data-stu-id="64e1c-135">Run hello following command, using `--parameters` tooset hello path toohello azuredeploy.parameters.json file.</span></span> <span data-ttu-id="64e1c-136">Met deze opdracht implementeert Hallo-cluster in een resourcegroep die u aangeroepen maakt `myResourceGroup` in de regio VS-West Hallo.</span><span class="sxs-lookup"><span data-stu-id="64e1c-136">This command deploys hello cluster in a resource group you create called `myResourceGroup` in hello West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a><span data-ttu-id="64e1c-137">Optie 2: Een service-principal genereren bij het maken van Hallo-cluster met`az acs create`</span><span class="sxs-lookup"><span data-stu-id="64e1c-137">Option 2: Generate a service principal when creating hello cluster with `az acs create`</span></span>

<span data-ttu-id="64e1c-138">Als u Hallo uitvoert [ `az acs create` ](/cli/azure/acs#create) opdracht toocreate Hallo Kubernetes cluster, hebt u Hallo optie toogenerate een service-principal automatisch.</span><span class="sxs-lookup"><span data-stu-id="64e1c-138">If you run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster, you have hello option toogenerate a service principal automatically.</span></span>

<span data-ttu-id="64e1c-139">Net zoals bij andere opties voor het maken van Kubernetes-clusters kunt u parameters voor een bestaande service-principal opgeven tijdens het uitvoeren van `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="64e1c-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="64e1c-140">Echter, wanneer u deze parameters weglaat, hello Azure CLI maakt een automatisch voor gebruik met Container Service.</span><span class="sxs-lookup"><span data-stu-id="64e1c-140">However, when you omit these parameters, hello Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="64e1c-141">Dit vindt plaats transparant tijdens het Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="64e1c-141">This takes place transparently during hello deployment.</span></span> 

<span data-ttu-id="64e1c-142">Hallo volgende opdracht maakt u een cluster Kubernetes en genereert zowel SSH-sleutels en service-principal referenties:</span><span class="sxs-lookup"><span data-stu-id="64e1c-142">hello following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="64e1c-143">Als uw account geen hello Azure AD- en abonnement machtigingen toocreate een service-principal, Hallo-opdracht wordt een fout gegenereerd vergelijkbaar te`Insufficient privileges toocomplete hello operation.`</span><span class="sxs-lookup"><span data-stu-id="64e1c-143">If your account doesn't have hello Azure AD and subscription permissions toocreate a service principal, hello command generates an error similar too`Insufficient privileges toocomplete hello operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="64e1c-144">Aanvullende overwegingen</span><span class="sxs-lookup"><span data-stu-id="64e1c-144">Additional considerations</span></span>

* <span data-ttu-id="64e1c-145">Als u geen machtigingen toocreate een service-principal in uw abonnement, moet u mogelijk tooask uw Azure AD of abonnement beheerder tooassign Hallo vereiste machtigingen of vraag om een service-principal toouse met Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="64e1c-145">If you don't have permissions toocreate a service principal in your subscription, you might need tooask your Azure AD or subscription administrator tooassign hello necessary permissions, or ask them for a service principal toouse with Azure Container Service.</span></span> 

* <span data-ttu-id="64e1c-146">Hallo service-principal voor Kubernetes is een onderdeel van de clusterconfiguratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="64e1c-146">hello service principal for Kubernetes is a part of hello cluster configuration.</span></span> <span data-ttu-id="64e1c-147">Echter niet gebruiken Hallo identiteit toodeploy Hallo cluster.</span><span class="sxs-lookup"><span data-stu-id="64e1c-147">However, don't use hello identity toodeploy hello cluster.</span></span>

* <span data-ttu-id="64e1c-148">Elke service-principal is gekoppeld aan een Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="64e1c-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="64e1c-149">Hallo service-principal voor een cluster Kubernetes kan worden gekoppeld aan een geldig Azure AD-toepassingsnaam (bijvoorbeeld: `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="64e1c-149">hello service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="64e1c-150">Hallo-URL voor de toepassing hello beschikt niet over toobe een echte-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="64e1c-150">hello URL for hello application doesn't have toobe a real endpoint.</span></span>

* <span data-ttu-id="64e1c-151">Opgeven wanneer Hallo service-principal **Client-ID**, kunt u Hallo-waarde van Hallo `appId` (zoals weergegeven in dit artikel) of de bijbehorende service-principal Hallo `name` (bijvoorbeeld`https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="64e1c-151">When specifying hello service principal **Client ID**, you can use hello value of hello `appId` (as shown in this article) or hello corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="64e1c-152">Hallo-service-principal referenties worden op Hallo hoofd- en agent Hallo Kubernetes cluster virtuele machines opgeslagen in Hallo bestand /etc/kubernetes/azure.json.</span><span class="sxs-lookup"><span data-stu-id="64e1c-152">On hello master and agent VMs in hello Kubernetes cluster, hello service principal credentials are stored in hello file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="64e1c-153">Wanneer u Hallo gebruikt `az acs create` toogenerate Hallo service-principal met de opdracht automatisch, principal Servicereferenties Hallo toohello bestand ~/.azure/acsServicePrincipal.json op Hallo machine toorun Hallo opdracht gebruikt worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="64e1c-153">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal credentials are written toohello file ~/.azure/acsServicePrincipal.json on hello machine used toorun hello command.</span></span> 

* <span data-ttu-id="64e1c-154">Bij het gebruik van Hallo `az acs create` toogenerate Hallo service-principal met de opdracht automatisch, service-principal Hallo kan ook worden geverifieerd met een [Azure container register](../../container-registry/container-registry-intro.md) gemaakt in Hallo hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="64e1c-154">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in hello same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="64e1c-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="64e1c-155">Next steps</span></span>

* <span data-ttu-id="64e1c-156">[Aan de slag met Kubernetes](container-service-kubernetes-walkthrough.md) in de Cluster Container Service-cluster.</span><span class="sxs-lookup"><span data-stu-id="64e1c-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="64e1c-157">tootroubleshoot hello service-principal voor Kubernetes, Zie Hallo [ACS-Engine documentatie](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="64e1c-157">tootroubleshoot hello service principal for Kubernetes, see hello [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


