---
title: Service-principal voor Azure Kubernetes-cluster | Microsoft-documenten
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
ms.openlocfilehash: 37171b4e69ad7d8c41ca8e7475c33ce70379f484
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="bb437-103">Een service-principal voor Azure AD voor een Kubernetes-cluster in Container Service instellen</span><span class="sxs-lookup"><span data-stu-id="bb437-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="bb437-104">In Azure Container Service is voor een Kubernetes-cluster een [service-principal voor Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) vereist voor gebruik met Azure-API's.</span><span class="sxs-lookup"><span data-stu-id="bb437-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) to interact with Azure APIs.</span></span> <span data-ttu-id="bb437-105">De service-principal is nodig om resources zoals door [gebruikers gedefinieerde routes](../../virtual-network/virtual-networks-udr-overview.md) en de [Azure Load Balancer uit laag vier](../../load-balancer/load-balancer-overview.md) dynamisch te beheren.</span><span class="sxs-lookup"><span data-stu-id="bb437-105">The service principal is needed to dynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and the [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="bb437-106">In dit artikel worden verschillende opties getoond om een service-principal in te stellen voor uw Kubernetes-cluster.</span><span class="sxs-lookup"><span data-stu-id="bb437-106">This article shows different options to set up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="bb437-107">Bijvoorbeeld: als u de [Azure CLI 2.0](/cli/azure/install-az-cli2) hebt geïnstalleerd en ingesteld, kunt u de opdracht [`az acs create`](/cli/azure/acs#create) uitvoeren om tegelijkertijd het Kubernetes-cluster en de service-principal te maken.</span><span class="sxs-lookup"><span data-stu-id="bb437-107">For example, if you installed and set up the [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run the [`az acs create`](/cli/azure/acs#create) command to create the Kubernetes cluster and the service principal at the same time.</span></span>


## <a name="requirements-for-the-service-principal"></a><span data-ttu-id="bb437-108">Vereisten voor de service-principal</span><span class="sxs-lookup"><span data-stu-id="bb437-108">Requirements for the service principal</span></span>

<span data-ttu-id="bb437-109">U kunt een bestaande Azure AD-service-principal gebruiken die voldoet aan de volgende vereisten, maar u kunt ook een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="bb437-109">You can use an existing Azure AD service principal that meets the following requirements, or create a new one.</span></span>

* <span data-ttu-id="bb437-110">**Bereik**: de resourcegroep in het abonnement dat is gebruikt voor het implementeren van het Kubernetes-cluster of (minder beperkend) het abonnement dat is gebruikt om het cluster te implementeren.</span><span class="sxs-lookup"><span data-stu-id="bb437-110">**Scope**: the resource group in the subscription used to deploy the Kubernetes cluster, or (less restrictively) the subscription used to deploy the cluster.</span></span>

* <span data-ttu-id="bb437-111">**Rol**: **inzender**</span><span class="sxs-lookup"><span data-stu-id="bb437-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="bb437-112">**Clientgeheim**: moet een wachtwoord zijn.</span><span class="sxs-lookup"><span data-stu-id="bb437-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="bb437-113">U kunt momenteel geen service-principal gebruiken om verificatie via een certificaat in te stellen.</span><span class="sxs-lookup"><span data-stu-id="bb437-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="bb437-114">Als u een service-principal wilt maken, moet u beschikken over machtigingen voor het registreren van een toepassing bij uw Azure AD-tenant. U moet ook machtigingen hebben om de toepassing aan een rol toe te wijzen in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="bb437-114">To create a service principal, you must have permissions to register an application with your Azure AD tenant, and to assign the application to a role in your subscription.</span></span> <span data-ttu-id="bb437-115">[Open de portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) om te controleren of u over de vereiste machtigingen beschikt.</span><span class="sxs-lookup"><span data-stu-id="bb437-115">To see if you have the required permissions, [check in the Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="bb437-116">Optie 1: een service-principal maken in Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb437-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="bb437-117">Azure biedt verschillende methoden om een Azure AD-service-principal te maken voordat u het Kubernetes-cluster implementeert.</span><span class="sxs-lookup"><span data-stu-id="bb437-117">If you want to create an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="bb437-118">In de volgende voorbeeldopdrachten ziet u hoe u dit kunt doen met de [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bb437-118">The following example commands show you how to do this with the [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="bb437-119">U kunt ook een service-principal maken met behulp van [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), de [klassieke portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md) of een ander hulpmiddel.</span><span class="sxs-lookup"><span data-stu-id="bb437-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), the [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="bb437-120">De uitvoer ziet er ongeveer zo uit (dit voorbeeld is geredigeerd):</span><span class="sxs-lookup"><span data-stu-id="bb437-120">Output is similar to the following (shown here redacted):</span></span>

![Een service-principal maken](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="bb437-122">Gemarkeerd zijn de **client-id** (`appId`) en het **clientgeheim** (`password`) die u gebruikt als parameters voor de service-principal voor de implementatie van de cluster.</span><span class="sxs-lookup"><span data-stu-id="bb437-122">Highlighted are the **client ID** (`appId`) and the **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-the-kubernetes-cluster"></a><span data-ttu-id="bb437-123">Service-principal opgeven bij het maken van het Kubernetes-cluster</span><span class="sxs-lookup"><span data-stu-id="bb437-123">Specify service principal when creating the Kubernetes cluster</span></span>

<span data-ttu-id="bb437-124">Geef bij het maken van het Kubernetes-cluster de **client-id** (ook wel de `appId` genoemd, voor toepassings-id) en het **clientgeheim** (`password`) als parameters op voor een bestaande service-principal.</span><span class="sxs-lookup"><span data-stu-id="bb437-124">Provide the **client ID** (also called the `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create the Kubernetes cluster.</span></span> <span data-ttu-id="bb437-125">Zorg ervoor dat de service-principal voldoet aan de vereisten die aan het begin van dit artikel zijn vermeld.</span><span class="sxs-lookup"><span data-stu-id="bb437-125">Make sure the service principal meets the requirements at the beginning this article.</span></span>

<span data-ttu-id="bb437-126">U kunt deze parameters opgeven tijdens het implementeren van het Kubernetes-cluster via de [Azure CLI (Command-Line Interface) 2.0](container-service-kubernetes-walkthrough.md), via [Azure Portal](../dcos-swarm/container-service-deployment.md) of via een andere methode.</span><span class="sxs-lookup"><span data-stu-id="bb437-126">You can specify these parameters when deploying the Kubernetes cluster using the [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="bb437-127">Zorg ervoor dat u bij het opgeven van de **client-id** gebruikmaakt van de `appId` en niet de `ObjectId` van de service-principal.</span><span class="sxs-lookup"><span data-stu-id="bb437-127">When specifying the **client ID**, be sure to use the `appId`, not the `ObjectId`, of the service principal.</span></span>
>

<span data-ttu-id="bb437-128">In het volgende voorbeeld wordt één manier getoond om de parameters door te geven met behulp van de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="bb437-128">The following example shows one way to pass the parameters with the Azure CLI 2.0.</span></span> <span data-ttu-id="bb437-129">In dit voorbeeld wordt gebruikgemaakt van de [Kubernetes-snelstartsjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="bb437-129">This example uses the [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="bb437-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) het bestand met sjabloonparameters `azuredeploy.parameters.json` van GitHub.</span><span class="sxs-lookup"><span data-stu-id="bb437-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) the template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="bb437-131">Voer de waarden voor `servicePrincipalClientId` en `servicePrincipalClientSecret` in het bestand in om de service-principal op te geven.</span><span class="sxs-lookup"><span data-stu-id="bb437-131">To specify the service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in the file.</span></span> <span data-ttu-id="bb437-132">(U moet ook uw eigen waarden voor `dnsNamePrefix` en `sshRSAPublicKey` opgeven.</span><span class="sxs-lookup"><span data-stu-id="bb437-132">(You also need to provide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="bb437-133">De laatste waarde is de openbare SSH-sleutel voor toegang tot de cluster.) Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="bb437-133">The latter is the SSH public key to access the cluster.) Save the file.</span></span>

    ![Parameters voor de service-principal doorgeven](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="bb437-135">Voer de volgende opdracht uit met behulp van `--parameters` om het pad naar het bestand azuredeploy.parameters.json in te stellen.</span><span class="sxs-lookup"><span data-stu-id="bb437-135">Run the following command, using `--parameters` to set the path to the azuredeploy.parameters.json file.</span></span> <span data-ttu-id="bb437-136">Met deze opdracht wordt het cluster geïmplementeerd in een resourcegroep die u `myResourceGroup` hebt genoemd, in de regio VS - west.</span><span class="sxs-lookup"><span data-stu-id="bb437-136">This command deploys the cluster in a resource group you create called `myResourceGroup` in the West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-the-cluster-with-az-acs-create"></a><span data-ttu-id="bb437-137">Optie 2: een service-principal genereren tijdens het maken van het cluster met `az acs create`</span><span class="sxs-lookup"><span data-stu-id="bb437-137">Option 2: Generate a service principal when creating the cluster with `az acs create`</span></span>

<span data-ttu-id="bb437-138">Als u de opdracht [`az acs create`](/cli/azure/acs#create) hebt uitgevoerd om het Kubernetes-cluster te maken, hebt u de optie om automatisch een service-principal te laten maken.</span><span class="sxs-lookup"><span data-stu-id="bb437-138">If you run the [`az acs create`](/cli/azure/acs#create) command to create the Kubernetes cluster, you have the option to generate a service principal automatically.</span></span>

<span data-ttu-id="bb437-139">Net zoals bij andere opties voor het maken van Kubernetes-clusters kunt u parameters voor een bestaande service-principal opgeven tijdens het uitvoeren van `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="bb437-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="bb437-140">Als u deze parameters echter weglaat, maakt de Azure CLI er automatisch een voor gebruik met Container Service.</span><span class="sxs-lookup"><span data-stu-id="bb437-140">However, when you omit these parameters, the Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="bb437-141">Dit vindt transparant plaats tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="bb437-141">This takes place transparently during the deployment.</span></span> 

<span data-ttu-id="bb437-142">Met de volgende opdracht wordt een Kubernetes-cluster gemaakt en worden beide SSH-sleutels en de referenties voor de service-principal gegenereerd:</span><span class="sxs-lookup"><span data-stu-id="bb437-142">The following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="bb437-143">Als uw account niet beschikt over de Azure AD- en abonnementsmachtigingen voor het maken van een service-principal, wordt er bij de opdracht een fout gegenereerd die vergelijkbaar is met `Insufficient privileges to complete the operation.`</span><span class="sxs-lookup"><span data-stu-id="bb437-143">If your account doesn't have the Azure AD and subscription permissions to create a service principal, the command generates an error similar to `Insufficient privileges to complete the operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="bb437-144">Aanvullende overwegingen</span><span class="sxs-lookup"><span data-stu-id="bb437-144">Additional considerations</span></span>

* <span data-ttu-id="bb437-145">Als u geen machtigingen hebt om een service-principal te maken in uw abonnement, moet u mogelijk uw Azure AD- of abonnementsbeheerder vragen om de benodigde machtigingen toe te wijzen. U kunt ook de beheerder vragen om een service-principal voor gebruik met Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="bb437-145">If you don't have permissions to create a service principal in your subscription, you might need to ask your Azure AD or subscription administrator to assign the necessary permissions, or ask them for a service principal to use with Azure Container Service.</span></span> 

* <span data-ttu-id="bb437-146">De service-principal voor Kubernetes is een onderdeel van de configuratie van het cluster.</span><span class="sxs-lookup"><span data-stu-id="bb437-146">The service principal for Kubernetes is a part of the cluster configuration.</span></span> <span data-ttu-id="bb437-147">Gebruik echter niet de id voor het implementeren van het cluster.</span><span class="sxs-lookup"><span data-stu-id="bb437-147">However, don't use the identity to deploy the cluster.</span></span>

* <span data-ttu-id="bb437-148">Elke service-principal is gekoppeld aan een Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="bb437-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="bb437-149">De service-principal voor een Kubernetes-cluster kan zijn gekoppeld aan elke geldige Azure AD-toepassingsnaam (bijvoorbeeld `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="bb437-149">The service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="bb437-150">De URL van de toepassing hoeft geen echt eindpunt te zijn.</span><span class="sxs-lookup"><span data-stu-id="bb437-150">The URL for the application doesn't have to be a real endpoint.</span></span>

* <span data-ttu-id="bb437-151">Als u de **client-id** voor de service-principal opgeeft, kunt u de waarde van de `appId` gebruiken (zoals beschreven in dit artikel) of de bijbehorende service-principal `name` (bijvoorbeeld `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="bb437-151">When specifying the service principal **Client ID**, you can use the value of the `appId` (as shown in this article) or the corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="bb437-152">Op de hoofd- en agent-VM's in het Kubernetes-cluster worden de referenties voor de service-principal opgeslagen in het bestand /etc/kubernetes/azure.json.</span><span class="sxs-lookup"><span data-stu-id="bb437-152">On the master and agent VMs in the Kubernetes cluster, the service principal credentials are stored in the file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="bb437-153">Als u de opdracht `az acs create` gebruikt om de service-principal automatisch te genereren, worden de referenties voor de service-principal naar het bestand ~/.azure/acsServicePrincipal.json geschreven op de computer die wordt gebruikt om de opdracht uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="bb437-153">When you use the `az acs create` command to generate the service principal automatically, the service principal credentials are written to the file ~/.azure/acsServicePrincipal.json on the machine used to run the command.</span></span> 

* <span data-ttu-id="bb437-154">Als u de opdracht `az acs create` gebruikt om de service-principal automatisch te genereren, kan de service-principal ook worden geverifieerd bij een [Azure Container Registry](../../container-registry/container-registry-intro.md) dat in hetzelfde abonnement wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bb437-154">When you use the `az acs create` command to generate the service principal automatically, the service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in the same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="bb437-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bb437-155">Next steps</span></span>

* <span data-ttu-id="bb437-156">[Aan de slag met Kubernetes](container-service-kubernetes-walkthrough.md) in de Cluster Container Service-cluster.</span><span class="sxs-lookup"><span data-stu-id="bb437-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="bb437-157">Zie de [ACS-enginedocumentatie](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting) voor informatie over het oplossen van problemen met de service-principal voor Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bb437-157">To troubleshoot the service principal for Kubernetes, see the [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


