---
title: aaaDeploy OpenShift oorsprong tooAzure | Microsoft Docs
description: Meer informatie over toodeploy OpenShift oorsprong tooAzure virtuele machines.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a><span data-ttu-id="9b11e-103">OpenShift oorsprong tooAzure virtuele Machines implementeren</span><span class="sxs-lookup"><span data-stu-id="9b11e-103">Deploy OpenShift Origin tooAzure Virtual Machines</span></span> 

<span data-ttu-id="9b11e-104">[OpenShift oorsprong](https://www.openshift.org/) is een open-source container-platform gebouwd op [Kubernetes](https://kubernetes.io/).</span><span class="sxs-lookup"><span data-stu-id="9b11e-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="9b11e-105">Het vereenvoudigt Hallo implementeren, schaal en werken met multitenant-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="9b11e-105">It simplifies hello process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="9b11e-106">Deze handleiding wordt beschreven hoe toodeploy OpenShift oorsprong over het gebruik van Azure Virtual Machines hello Azure CLI en Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="9b11e-106">This guide describes how toodeploy OpenShift Origin on Azure Virtual Machines using hello Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="9b11e-107">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="9b11e-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9b11e-108">Een toomanage KeyVault SSH-sleutels voor Hallo OpenShift cluster maken.</span><span class="sxs-lookup"><span data-stu-id="9b11e-108">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="9b11e-109">Een cluster OpenShift op Azure VM's implementeren.</span><span class="sxs-lookup"><span data-stu-id="9b11e-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="9b11e-110">Installeer en configureer Hallo [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b11e-110">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>
> * <span data-ttu-id="9b11e-111">Hallo OpenShift implementatie aanpassen.</span><span class="sxs-lookup"><span data-stu-id="9b11e-111">Customize hello OpenShift deployment.</span></span>

<span data-ttu-id="9b11e-112">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="9b11e-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="9b11e-113">Deze snel starten vereist hello Azure CLI versie 2.0.8 of hoger.</span><span class="sxs-lookup"><span data-stu-id="9b11e-113">This quick start requires hello Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="9b11e-114">toofind hello versie, voer `az --version`.</span><span class="sxs-lookup"><span data-stu-id="9b11e-114">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="9b11e-115">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9b11e-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="9b11e-116">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="9b11e-116">Log in tooAzure</span></span> 
<span data-ttu-id="9b11e-117">Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht en volg Hallo op het scherm instructies of klik op **Try it** toouse Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="9b11e-117">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions or click **Try it** toouse Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="9b11e-118">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="9b11e-118">Create a resource group</span></span>

<span data-ttu-id="9b11e-119">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="9b11e-119">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="9b11e-120">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="9b11e-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="9b11e-121">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie.</span><span class="sxs-lookup"><span data-stu-id="9b11e-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="9b11e-122">Een sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="9b11e-122">Create a Key Vault</span></span>
<span data-ttu-id="9b11e-123">Maken van een KeyVault toostore Hallo SSH-sleutels voor Hallo cluster Hello [az keyvault maken](/cli/azure/keyvault#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="9b11e-123">Create a KeyVault toostore hello SSH keys for hello cluster with hello [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="9b11e-124">Een SSH-sleutel maken</span><span class="sxs-lookup"><span data-stu-id="9b11e-124">Create an SSH key</span></span> 
<span data-ttu-id="9b11e-125">Een SSH-sleutel is vereist toosecure toegang toohello OpenShift oorsprong cluster.</span><span class="sxs-lookup"><span data-stu-id="9b11e-125">An SSH key is needed toosecure access toohello OpenShift Origin cluster.</span></span> <span data-ttu-id="9b11e-126">Maken van een SSH-sleutelpaar met Hallo `ssh-keygen` opdracht.</span><span class="sxs-lookup"><span data-stu-id="9b11e-126">Create an SSH key-pair using hello `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="9b11e-127">Hallo SSH-sleutelpaar, hebt u geen een wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="9b11e-127">hello SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="9b11e-128">Voor meer informatie over de SSH-sleutels op Windows, [hoe toocreate SSH-sleutels op Windows](/azure/virtual-machines/linux/ssh-from-windows).</span><span class="sxs-lookup"><span data-stu-id="9b11e-128">For more information on SSH keys on Windows, [How toocreate SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="9b11e-129">Opslaan van persoonlijke SSH-sleutel in de Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="9b11e-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="9b11e-130">Hallo OpenShift implementatie maakt gebruik van SSH-sleutel Hallo u toosecure toegang toohello OpenShift master gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b11e-130">hello OpenShift deployment uses hello SSH key you created toosecure access toohello OpenShift master.</span></span> <span data-ttu-id="9b11e-131">tooenable hello implementatie toosecurely Hallo SSH-sleutel ophalen, Hallo sleutel opslaan in de Sleutelkluis met behulp van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="9b11e-131">tooenable hello deployment toosecurely retrieve hello SSH key, store hello key in Key Vault using hello following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="9b11e-132">Ingeschakeld voor de sjabloonimplementatie van</span><span class="sxs-lookup"><span data-stu-id="9b11e-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="9b11e-133">Een service-principal maken</span><span class="sxs-lookup"><span data-stu-id="9b11e-133">Create a service principal</span></span> 
<span data-ttu-id="9b11e-134">OpenShift communiceert met Azure met behulp van een gebruikersnaam en wachtwoord of een service-principal.</span><span class="sxs-lookup"><span data-stu-id="9b11e-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="9b11e-135">Een Azure-service-principal is een beveiligings-id die u met apps, services en automatiseringsprogramma's zoals OpenShift gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="9b11e-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="9b11e-136">U bepaalt de en definieer Hallo machtigingen als toowhat operations Hallo service-principal in Azure uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="9b11e-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="9b11e-137">tooimprove beveiliging via gewoon een gebruikersnaam en wachtwoord voor het bieden, in dit voorbeeld wordt een basic service principal.</span><span class="sxs-lookup"><span data-stu-id="9b11e-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="9b11e-138">Maken van een service principal met [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac) en uitvoer Hallo de referenties die OpenShift moet:</span><span class="sxs-lookup"><span data-stu-id="9b11e-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="9b11e-139">Let op de eigenschap appId Hallo van Hallo-opdracht geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9b11e-139">Take note of hello appId property returned from hello command.</span></span>
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > <span data-ttu-id="9b11e-140">Maak geen onbeveiligd wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="9b11e-140">Don't create an insecure password.</span></span>  <span data-ttu-id="9b11e-141">Volg de richtlijnen in [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) (Regels en beperkingen voor wachtwoorden in Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9b11e-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="9b11e-142">Zie voor meer informatie over service-principals [een Azure-service-principal maken met Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="9b11e-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-hello-openshift-origin-template"></a><span data-ttu-id="9b11e-143">Hallo OpenShift oorsprong sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="9b11e-143">Deploy hello OpenShift Origin template</span></span>
<span data-ttu-id="9b11e-144">Naast OpenShift oorsprong met een Azure Resource Manager-sjabloon implementeren.</span><span class="sxs-lookup"><span data-stu-id="9b11e-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="9b11e-145">Hallo volgende opdracht vereist az CLI 2.0.8 of hoger.</span><span class="sxs-lookup"><span data-stu-id="9b11e-145">hello following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="9b11e-146">U kunt controleren of Hallo az CLI versie Hello `az --version` opdracht.</span><span class="sxs-lookup"><span data-stu-id="9b11e-146">You can verify hello az CLI version with hello `az --version` command.</span></span> <span data-ttu-id="9b11e-147">tooupdate hello CLI versie, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9b11e-147">tooupdate hello CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="9b11e-148">Gebruik Hallo `appId` waarde van de service-principal Hallo u eerder hebt gemaakt voor Hallo `aadClientId` parameter.</span><span class="sxs-lookup"><span data-stu-id="9b11e-148">Use hello `appId` value from hello service principal you created earlier for hello `aadClientId` parameter.</span></span>

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
<span data-ttu-id="9b11e-149">Hallo-implementatie kan toocomplete van too20 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="9b11e-149">hello deployment may take up too20 minutes toocomplete.</span></span> <span data-ttu-id="9b11e-150">Hallo Hallo OpenShift console-URL en DNS-naam van Hallo OpenShift-master is afgedrukt toohello terminal wanneer Hallo-implementatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9b11e-150">hello URL of hello OpenShift console and DNS name of hello OpenShift master is printed toohello terminal when hello deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a><span data-ttu-id="9b11e-151">Verbinding maken met toohello OpenShift cluster</span><span class="sxs-lookup"><span data-stu-id="9b11e-151">Connect toohello OpenShift cluster</span></span>
<span data-ttu-id="9b11e-152">Wanneer het Hallo-implementatie is voltooid, verbinding maken met toohello OpenShift console met behulp van Hallo browser met Hallo `OpenShift Console Uri`.</span><span class="sxs-lookup"><span data-stu-id="9b11e-152">When hello deployment completes, connect toohello OpenShift console using hello browser using hello `OpenShift Console Uri`.</span></span> <span data-ttu-id="9b11e-153">U kunt ook toohello OpenShift master met behulp van de volgende opdracht Hallo verbinden.</span><span class="sxs-lookup"><span data-stu-id="9b11e-153">Alternatively, you can connect toohello OpenShift master using hello following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="9b11e-154">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="9b11e-154">Clean up resources</span></span>
<span data-ttu-id="9b11e-155">Wanneer deze niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, OpenShift cluster en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="9b11e-155">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="9b11e-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9b11e-156">Next steps</span></span>

<span data-ttu-id="9b11e-157">In deze zelfstudie, geleerde procedure:</span><span class="sxs-lookup"><span data-stu-id="9b11e-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="9b11e-158">Een toomanage KeyVault SSH-sleutels voor Hallo OpenShift cluster maken.</span><span class="sxs-lookup"><span data-stu-id="9b11e-158">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="9b11e-159">Een cluster OpenShift op Azure VM's implementeren.</span><span class="sxs-lookup"><span data-stu-id="9b11e-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="9b11e-160">Installeer en configureer Hallo [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b11e-160">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>

<span data-ttu-id="9b11e-161">Nu wordt dat OpenShift oorsprong-cluster geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="9b11e-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="9b11e-162">U kunt OpenShift zelfstudies toolearn hoe volgen toodeploy uw eerste toepassing en gebruik Hallo OpenShift hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="9b11e-162">You can follow OpenShift tutorials toolearn how toodeploy your first application and use hello OpenShift tools.</span></span> <span data-ttu-id="9b11e-163">Zie [aan de slag met OpenShift oorsprong](https://docs.openshift.org/latest/getting_started/index.html) tooget gestart.</span><span class="sxs-lookup"><span data-stu-id="9b11e-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) tooget started.</span></span> 
