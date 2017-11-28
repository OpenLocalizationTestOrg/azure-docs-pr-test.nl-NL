---
title: een webserver met SSL-in Azure certificaten aaaSecure | Microsoft Docs
description: Meer informatie over hoe toosecure hello NGINX-webserver met SSL-certificaten op een Linux VM in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="8a0e2-103">Een webserver met SSL-certificaten op een virtuele Linux-machine in Azure beveiligen</span><span class="sxs-lookup"><span data-stu-id="8a0e2-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="8a0e2-104">toosecure webservers, een certificaat Later SSL (Secure Sockets) kan worden gebruikt tooencrypt internetverkeer.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="8a0e2-105">Deze SSL-certificaten kunnen worden opgeslagen in Azure Sleutelkluis en beveiligde implementaties van certificaten tooLinux virtuele machines (VM's) in Azure toestaan.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooLinux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="8a0e2-106">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="8a0e2-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a0e2-107">Maken van een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="8a0e2-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="8a0e2-108">Upload een certificaat toohello Sleutelkluis of genereren</span><span class="sxs-lookup"><span data-stu-id="8a0e2-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="8a0e2-109">Een virtuele machine maken en Hallo NGINX-webserver installeren</span><span class="sxs-lookup"><span data-stu-id="8a0e2-109">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="8a0e2-110">Hallo certificaat invoeren in Hallo VM en NGINX configureren met een SSL-binding</span><span class="sxs-lookup"><span data-stu-id="8a0e2-110">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8a0e2-111">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8a0e2-112">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8a0e2-113">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8a0e2-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="8a0e2-114">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8a0e2-114">Overview</span></span>
<span data-ttu-id="8a0e2-115">Azure Sleutelkluis beschermt cryptografische sleutels en geheimen, zoals certificaten of wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="8a0e2-116">Sleutelkluis helpt Hallo certificate management stroomlijnen en kunt u toomaintain beheer van sleutels die toegang hebben tot deze certificaten.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="8a0e2-117">U kunt een zelfondertekend certificaat in de Sleutelkluis maken of een bestaande, vertrouwd certificaat dat u al bezit uploaden.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="8a0e2-118">In plaats van met een aangepaste VM-installatiekopie die certificaten bevat standaard uitbreidbaar module u certificaten kunt invoeren in een actieve virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="8a0e2-119">Dit proces zorgt ervoor dat de meest recente certificaten Hallo tijdens de implementatie op een webserver zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="8a0e2-120">Als u vernieuwen of vervangen van een certificaat, hebt u niet ook toocreate een nieuwe aangepaste VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="8a0e2-121">Hallo nieuwste certificaten worden automatisch ingevoegd als u extra virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="8a0e2-122">Tijdens het hele proces hello, Hallo certificaten nooit laat hello Azure-platform of beschikbaar worden gesteld in een script, opdrachtregel geschiedenis of sjabloon.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="8a0e2-123">Maken van een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="8a0e2-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="8a0e2-124">Voordat u certificaten en een Sleutelkluis maken kunt, maakt u een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8a0e2-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8a0e2-125">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupSecureWeb* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="8a0e2-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="8a0e2-126">Maak vervolgens een Sleutelkluis met [az keyvault maken](/cli/azure/keyvault#create) en inschakelen voor gebruik wanneer u een virtuele machine implementeert.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="8a0e2-127">Elke Sleutelkluis moet een unieke naam hebben en moet alle kleine letters.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="8a0e2-128">Vervang  *<mykeyvault>*  in het volgende voorbeeld met de naam van uw eigen unieke Sleutelkluis Hallo:</span><span class="sxs-lookup"><span data-stu-id="8a0e2-128">Replace *<mykeyvault>* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="8a0e2-129">Een certificaat genereren en opslaan in de Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="8a0e2-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="8a0e2-130">Voor gebruik in productieomgevingen, moet u een geldig certificaat dat is ondertekend door een vertrouwde provider met importeren [az keyvault certificaat importeren](/cli/azure/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="8a0e2-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="8a0e2-131">Voor deze zelfstudie hello volgende voorbeeld ziet u hoe u een zelfondertekend certificaat met genereren [az keyvault-certificaat maken](/cli/azure/certificate#create) die gebruikmaakt van Hallo-standaardbeleid certificaat:</span><span class="sxs-lookup"><span data-stu-id="8a0e2-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="8a0e2-132">Een certificaat voor gebruik met een virtuele machine voorbereiden</span><span class="sxs-lookup"><span data-stu-id="8a0e2-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="8a0e2-133">toouse hello certificaat tijdens Hallo VM proces voor het maken, verkrijgen Hallo-ID van uw certificaat met [az keyvault lijst-versies van het clientgeheim](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="8a0e2-133">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="8a0e2-134">Hallo-certificaat met converteren [az vm indeling-geheim](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="8a0e2-134">Convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="8a0e2-135">Hallo volgt toegewezen Hallo-uitvoer van deze opdrachten toovariables voor eenvoudig te gebruiken in Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="8a0e2-135">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="8a0e2-136">Maken van een cloud-init config toosecure NGINX</span><span class="sxs-lookup"><span data-stu-id="8a0e2-136">Create a cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="8a0e2-137">[Cloud-init](https://cloudinit.readthedocs.io) is een veelgebruikte methode toocustomize zoals deze wordt opgestart voor Hallo eerst een Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="8a0e2-138">U kunt de cloud init tooinstall pakketten gebruiken en schrijven van bestanden, of tooconfigure gebruikers en beveiliging.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-138">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="8a0e2-139">Cloud-init wordt uitgevoerd tijdens het opstartproces hello, er zijn geen extra stappen of agents tooapply uw configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-139">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="8a0e2-140">Wanneer u maakt een virtuele machine, certificaten en sleutels worden opgeslagen in Hallo beveiligd */var/lib/waagent/* directory.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-140">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="8a0e2-141">tooautomate toe te voegen Hallo certificaat toohello VM en cloud-init Hallo webserver configureren gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-141">tooautomate adding hello certificate toohello VM and configuring hello web server, use cloud-init.</span></span> <span data-ttu-id="8a0e2-142">In dit voorbeeld we installeren en configureren van Hallo NGINX-webserver.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-142">In this example, we install and configure hello NGINX web server.</span></span> <span data-ttu-id="8a0e2-143">U kunt Hallo dezelfde tooinstall verwerken en Apache configureren.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-143">You can use hello same process tooinstall and configure Apache.</span></span> 

<span data-ttu-id="8a0e2-144">Maak een bestand met de naam *cloud-init-web-server.txt* en plakken Hallo volgende configuratie:</span><span class="sxs-lookup"><span data-stu-id="8a0e2-144">Create a file named *cloud-init-web-server.txt* and paste hello following configuration:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a><span data-ttu-id="8a0e2-145">Een beveiligde virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="8a0e2-145">Create a secure VM</span></span>
<span data-ttu-id="8a0e2-146">Maak nu een virtuele machine met [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="8a0e2-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="8a0e2-147">Hallo certificaatgegevens wordt geïnjecteerd uit Sleutelkluis Hello `--secrets` parameter.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-147">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="8a0e2-148">U doorgeeft in Hallo cloud init-config Hallo `--custom-data` parameter:</span><span class="sxs-lookup"><span data-stu-id="8a0e2-148">You pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="8a0e2-149">Het duurt enkele minuten voordat Hallo VM toobe gemaakt, hello-pakketten tooinstall en Hallo app toostart.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-149">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="8a0e2-150">Wanneer Hallo VM is gemaakt, noteer Hallo `publicIpAddress` weergegeven door hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-150">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="8a0e2-151">Dit adres wordt gebruikt tooaccess uw site in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-151">This address is used tooaccess your site in a web browser.</span></span>

<span data-ttu-id="8a0e2-152">virtuele machine, open poort 443 van Hallo Internet met voor secure web verkeer tooreach tooallow [az vm open poort](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="8a0e2-152">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="8a0e2-153">Test Hallo beveiligde web-app</span><span class="sxs-lookup"><span data-stu-id="8a0e2-153">Test hello secure web app</span></span>
<span data-ttu-id="8a0e2-154">Nu kunt u een webbrowser openen en voer *https://<publicIpAddress>*  in de adresbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-154">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="8a0e2-155">Geef uw eigen openbare IP-adres uit Hallo VM proces maken.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-155">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="8a0e2-156">Beveiligingswaarschuwing Hallo accepteren als u een zelfondertekend certificaat gebruikt:</span><span class="sxs-lookup"><span data-stu-id="8a0e2-156">Accept hello security warning if you used a self-signed certificate:</span></span>

![Beveiligingswaarschuwing voor web browser accepteren](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="8a0e2-158">Uw beveiligde NGINX-site wordt vervolgens weergegeven zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="8a0e2-158">Your secured NGINX site is then displayed as in hello following example:</span></span>

![Actief beveiligde NGINX-site weergeven](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="8a0e2-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a0e2-160">Next steps</span></span>

<span data-ttu-id="8a0e2-161">In deze zelfstudie maakt beveiligd u een NGINX-webserver met een SSL-certificaat dat is opgeslagen in Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="8a0e2-162">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="8a0e2-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a0e2-163">Maken van een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="8a0e2-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="8a0e2-164">Upload een certificaat toohello Sleutelkluis of genereren</span><span class="sxs-lookup"><span data-stu-id="8a0e2-164">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="8a0e2-165">Een virtuele machine maken en Hallo NGINX-webserver installeren</span><span class="sxs-lookup"><span data-stu-id="8a0e2-165">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="8a0e2-166">Hallo certificaat invoeren in Hallo VM en NGINX configureren met een SSL-binding</span><span class="sxs-lookup"><span data-stu-id="8a0e2-166">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="8a0e2-167">Volg deze link toosee vooraf gemaakte virtuele machine scriptvoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="8a0e2-167">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8a0e2-168">Windows virtuele machine scriptvoorbeelden</span><span class="sxs-lookup"><span data-stu-id="8a0e2-168">Windows virtual machine script samples</span></span>](./cli-samples.md)