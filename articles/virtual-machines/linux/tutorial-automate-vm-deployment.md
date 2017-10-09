---
title: aaaCustomize een Linux-VM voor eerst wordt opgestart in Azure | Microsoft Docs
description: Meer informatie over hoe toouse cloud-init en Sleutelkluis toocustomze virtuele Linux-machines Hallo eerste keer dat ze worden opgestart in Azure
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
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="47745-103">Hoe toocustomize virtuele Linux-machine op de eerste keer opstarten</span><span class="sxs-lookup"><span data-stu-id="47745-103">How toocustomize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="47745-104">In een vorige zelfstudie hebt u geleerd hoe tooSSH tooa virtuele machine (VM) en NGINX handmatig installeren.</span><span class="sxs-lookup"><span data-stu-id="47745-104">In a previous tutorial, you learned how tooSSH tooa virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="47745-105">toocreate virtuele machines op een snelle en consistente manier, een vorm van automatisering is doorgaans gewenste.</span><span class="sxs-lookup"><span data-stu-id="47745-105">toocreate VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="47745-106">Een algemene methode toocustomize een VM op de eerste keer opstarten is toouse [cloud init](https://cloudinit.readthedocs.io).</span><span class="sxs-lookup"><span data-stu-id="47745-106">A common approach toocustomize a VM on first boot is toouse [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="47745-107">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="47745-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="47745-108">Maken van een cloud-init-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="47745-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="47745-109">Een virtuele machine die gebruikmaakt van een cloud-init-bestand maken</span><span class="sxs-lookup"><span data-stu-id="47745-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="47745-110">Een actieve Node.js-app weergeven na Hallo die virtuele machine wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="47745-110">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="47745-111">Sleutelkluis toosecurely store certificaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="47745-111">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="47745-112">Beveiligde implementaties van NGINX met cloud-init automatiseren</span><span class="sxs-lookup"><span data-stu-id="47745-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="47745-113">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="47745-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="47745-114">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="47745-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="47745-115">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="47745-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="47745-116">Cloud-init-overzicht</span><span class="sxs-lookup"><span data-stu-id="47745-116">Cloud-init overview</span></span>
<span data-ttu-id="47745-117">[Cloud-init](https://cloudinit.readthedocs.io) is een veelgebruikte methode toocustomize zoals deze wordt opgestart voor Hallo eerst een Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="47745-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="47745-118">U kunt de cloud init tooinstall pakketten gebruiken en schrijven van bestanden, of tooconfigure gebruikers en beveiliging.</span><span class="sxs-lookup"><span data-stu-id="47745-118">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="47745-119">Cloud-init wordt uitgevoerd tijdens het opstartproces hello, er zijn geen extra stappen of agents tooapply uw configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="47745-119">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="47745-120">Cloud-init werkt ook via distributies.</span><span class="sxs-lookup"><span data-stu-id="47745-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="47745-121">Bijvoorbeeld, u niet gebruikt **apt get-installatie** of **yum installeren** tooinstall een pakket.</span><span class="sxs-lookup"><span data-stu-id="47745-121">For example, you don't use **apt-get install** or **yum install** tooinstall a package.</span></span> <span data-ttu-id="47745-122">In plaats daarvan kunt u een lijst met pakketten tooinstall definiëren.</span><span class="sxs-lookup"><span data-stu-id="47745-122">Instead you can define a list of packages tooinstall.</span></span> <span data-ttu-id="47745-123">Hallo systeemeigen pakket beheerprogramma cloud init automatisch gebruikt voor Hallo distro die u selecteert.</span><span class="sxs-lookup"><span data-stu-id="47745-123">Cloud-init automatically uses hello native package management tool for hello distro you select.</span></span>

<span data-ttu-id="47745-124">We kunnen werken met onze partners tooget cloud-init opgenomen en werken in dat ze tooAzure bieden Hallo-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="47745-124">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span> <span data-ttu-id="47745-125">Hallo volgende tabel geeft een overzicht van de huidige cloud init-beschikbaarheid Hallo op Azure-platform installatiekopieën:</span><span class="sxs-lookup"><span data-stu-id="47745-125">hello following table outlines hello current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="47745-126">Alias</span><span class="sxs-lookup"><span data-stu-id="47745-126">Alias</span></span> | <span data-ttu-id="47745-127">Uitgever</span><span class="sxs-lookup"><span data-stu-id="47745-127">Publisher</span></span> | <span data-ttu-id="47745-128">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="47745-128">Offer</span></span> | <span data-ttu-id="47745-129">SKU</span><span class="sxs-lookup"><span data-stu-id="47745-129">SKU</span></span> | <span data-ttu-id="47745-130">Versie</span><span class="sxs-lookup"><span data-stu-id="47745-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="47745-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="47745-131">UbuntuLTS</span></span> |<span data-ttu-id="47745-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="47745-132">Canonical</span></span> |<span data-ttu-id="47745-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="47745-133">UbuntuServer</span></span> |<span data-ttu-id="47745-134">16.04 TNS</span><span class="sxs-lookup"><span data-stu-id="47745-134">16.04-LTS</span></span> |<span data-ttu-id="47745-135">meest recente</span><span class="sxs-lookup"><span data-stu-id="47745-135">latest</span></span> |
| <span data-ttu-id="47745-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="47745-136">UbuntuLTS</span></span> |<span data-ttu-id="47745-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="47745-137">Canonical</span></span> |<span data-ttu-id="47745-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="47745-138">UbuntuServer</span></span> |<span data-ttu-id="47745-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="47745-139">14.04.5-LTS</span></span> |<span data-ttu-id="47745-140">meest recente</span><span class="sxs-lookup"><span data-stu-id="47745-140">latest</span></span> |
| <span data-ttu-id="47745-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="47745-141">CoreOS</span></span> |<span data-ttu-id="47745-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="47745-142">CoreOS</span></span> |<span data-ttu-id="47745-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="47745-143">CoreOS</span></span> |<span data-ttu-id="47745-144">Stabiel</span><span class="sxs-lookup"><span data-stu-id="47745-144">Stable</span></span> |<span data-ttu-id="47745-145">meest recente</span><span class="sxs-lookup"><span data-stu-id="47745-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="47745-146">Cloud-init-configuratiebestand maken</span><span class="sxs-lookup"><span data-stu-id="47745-146">Create cloud-init config file</span></span>
<span data-ttu-id="47745-147">toosee cloud-init in actie, maak een VM die NGINX installeert en een eenvoudige 'Hallo wereld' Node.js-app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="47745-147">toosee cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="47745-148">Hallo na configuratie voor cloud-init vereist hello-pakketten worden geïnstalleerd, maakt u een Node.js-app en vervolgens initialiseren en Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="47745-148">hello following cloud-init configuration installs hello required packages, creates a Node.js app, then initialize and starts hello app.</span></span>

<span data-ttu-id="47745-149">Maak een bestand met de naam in uw huidige shell *cloud init.txt* en plakken Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="47745-149">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="47745-150">Bijvoorbeeld, Hallo-bestand in Hallo Cloud-Shell op uw lokale machine niet maken.</span><span class="sxs-lookup"><span data-stu-id="47745-150">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="47745-151">U kunt een editor die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="47745-151">You can use any editor you wish.</span></span> <span data-ttu-id="47745-152">Voer `sensible-editor cloud-init.txt` toocreate Hallo bestand en een overzicht van beschikbare editors.</span><span class="sxs-lookup"><span data-stu-id="47745-152">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="47745-153">Zorg ervoor dat Hallo hele cloud-init-bestand correct is gekopieerd, met name Hallo eerste regel:</span><span class="sxs-lookup"><span data-stu-id="47745-153">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

<span data-ttu-id="47745-154">Zie voor meer informatie over configuratieopties voor cloud-init [cloud init config voorbeelden](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span><span class="sxs-lookup"><span data-stu-id="47745-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="47745-155">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="47745-155">Create virtual machine</span></span>
<span data-ttu-id="47745-156">Voordat u een virtuele machine maken kunt, maakt u een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="47745-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="47745-157">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupAutomate* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="47745-157">hello following example creates a resource group named *myResourceGroupAutomate* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="47745-158">Maak nu een virtuele machine met [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="47745-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="47745-159">Gebruik Hallo `--custom-data` parameter toopass in uw cloud-init-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="47745-159">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="47745-160">Hallo volledig pad toohello bieden *cloud init.txt* config als Hallo bestand buiten de huidige werkmap is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="47745-160">Provide hello full path toohello *cloud-init.txt* config if you saved hello file outside of your present working directory.</span></span> <span data-ttu-id="47745-161">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myAutomatedVM*:</span><span class="sxs-lookup"><span data-stu-id="47745-161">hello following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="47745-162">Het duurt enkele minuten voordat Hallo VM toobe gemaakt, hello-pakketten tooinstall en Hallo app toostart.</span><span class="sxs-lookup"><span data-stu-id="47745-162">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="47745-163">Er zijn achtergrondtaken die toorun verder gaat nadat hello Azure CLI keert u terug toohello prompt.</span><span class="sxs-lookup"><span data-stu-id="47745-163">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="47745-164">Het is mogelijk een andere paar minuten voordat u toegang hebt tot Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="47745-164">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="47745-165">Wanneer Hallo VM is gemaakt, noteer Hallo `publicIpAddress` weergegeven door hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="47745-165">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="47745-166">Dit adres is gebruikte tooaccess hello Node.js-app via een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="47745-166">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="47745-167">virtuele machine, open poort 80 van Hallo Internet met het web verkeer tooreach tooallow [az vm open poort](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="47745-167">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="47745-168">Test-web-app</span><span class="sxs-lookup"><span data-stu-id="47745-168">Test web app</span></span>
<span data-ttu-id="47745-169">Nu kunt u een webbrowser openen en voer *http://<publicIpAddress>*  in de adresbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="47745-169">Now you can open a web browser and enter *http://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="47745-170">Geef uw eigen openbare IP-adres uit Hallo VM proces maken.</span><span class="sxs-lookup"><span data-stu-id="47745-170">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="47745-171">Uw Node.js-app wordt weergegeven zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="47745-171">Your Node.js app is displayed as in hello following example:</span></span>

![Bekijk actieve NGINX-website](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="47745-173">Certificaten van de Sleutelkluis invoeren</span><span class="sxs-lookup"><span data-stu-id="47745-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="47745-174">Deze optionele sectie wordt beschreven hoe u veilig opslaan van certificaten in Azure Sleutelkluis en ze tijdens het Hallo-VM-implementatie te injecteren.</span><span class="sxs-lookup"><span data-stu-id="47745-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during hello VM deployment.</span></span> <span data-ttu-id="47745-175">In plaats van met een aangepaste installatiekopie met de Hallo certificaten standaard uitbreidbaar, in dit proces zorgt ervoor dat de meest recente certificaten Hallo tooa VM op de eerste keer opstarten zijn ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="47745-175">Rather than using a custom image that includes hello certificates baked-in, this process ensures that hello most up-to-date certificates are injected tooa VM on first boot.</span></span> <span data-ttu-id="47745-176">Tijdens Hallo Hallo certificaat nooit verlaat hello Azure-platform of in een script, opdrachtregel geschiedenis of sjabloon wordt blootgesteld.</span><span class="sxs-lookup"><span data-stu-id="47745-176">During hello process, hello certificate never leaves hello Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="47745-177">Azure Sleutelkluis beschermt cryptografische sleutels en geheimen, zoals certificaten of wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="47745-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="47745-178">Sleutelkluis helpt Hallo Sleutelbeheer stroomlijnen en kunt u toomaintain beheer van sleutels die toegang tot en uw gegevens te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="47745-178">Key Vault helps streamline hello key management process and enables you toomaintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="47745-179">Dit scenario maakt u kennis met enkele Sleutelkluis concepten toocreate en een certificaat gebruiken, maar is niet een volledig overzicht over het toouse Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="47745-179">This scenario introduces some Key Vault concepts toocreate and use a certificate, though is not an exhaustive overview on how toouse Key Vault.</span></span>

<span data-ttu-id="47745-180">Hallo stappen te volgen laten zien hoe u kunt:</span><span class="sxs-lookup"><span data-stu-id="47745-180">hello following steps show how you can:</span></span>

- <span data-ttu-id="47745-181">Maken van een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="47745-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="47745-182">Upload een certificaat toohello Sleutelkluis of genereren</span><span class="sxs-lookup"><span data-stu-id="47745-182">Generate or upload a certificate toohello Key Vault</span></span>
- <span data-ttu-id="47745-183">Een geheim van Hallo certificaat tooinject in tooa VM maken</span><span class="sxs-lookup"><span data-stu-id="47745-183">Create a secret from hello certificate tooinject in tooa VM</span></span>
- <span data-ttu-id="47745-184">Een virtuele machine maken en te ' injecteren ' hello certificaat</span><span class="sxs-lookup"><span data-stu-id="47745-184">Create a VM and inject hello certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="47745-185">Maken van een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="47745-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="47745-186">Maak eerst een Sleutelkluis met [az keyvault maken](/cli/azure/keyvault#create) en inschakelen voor gebruik wanneer u een virtuele machine implementeert.</span><span class="sxs-lookup"><span data-stu-id="47745-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="47745-187">Elke Sleutelkluis moet een unieke naam hebben en moet alle kleine letters.</span><span class="sxs-lookup"><span data-stu-id="47745-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="47745-188">Vervang *mykeyvault* in het volgende voorbeeld met de naam van uw eigen unieke Sleutelkluis Hallo:</span><span class="sxs-lookup"><span data-stu-id="47745-188">Replace *mykeyvault* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="47745-189">Certificaat genereren en opslaan in de Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="47745-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="47745-190">Voor gebruik in productieomgevingen, moet u een geldig certificaat dat is ondertekend door een vertrouwde provider met importeren [az keyvault certificaat importeren](/cli/azure/keyvault/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="47745-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="47745-191">Voor deze zelfstudie hello volgende voorbeeld ziet u hoe u een zelfondertekend certificaat met genereren [az keyvault-certificaat maken](/cli/azure/keyvault/certificate#create) die gebruikmaakt van Hallo-standaardbeleid certificaat:</span><span class="sxs-lookup"><span data-stu-id="47745-191">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="47745-192">Certificaat voor gebruik met de virtuele machine voorbereiden</span><span class="sxs-lookup"><span data-stu-id="47745-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="47745-193">toouse hello certificaat tijdens Hallo VM proces voor het maken, verkrijgen Hallo-ID van uw certificaat met [az keyvault lijst-versies van het clientgeheim](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="47745-193">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="47745-194">Hallo VM Hallo certificaat moet in een bepaalde opmaak tooinject converteren deze opstart, dus Hallo-certificaat met [az vm indeling-geheim](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="47745-194">hello VM needs hello certificate in a certain format tooinject it on boot, so convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="47745-195">Hallo volgt toegewezen Hallo-uitvoer van deze opdrachten toovariables voor eenvoudig te gebruiken in Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="47745-195">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="47745-196">Cloud-init config toosecure NGINX maken</span><span class="sxs-lookup"><span data-stu-id="47745-196">Create cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="47745-197">Wanneer u maakt een virtuele machine, certificaten en sleutels worden opgeslagen in Hallo beveiligd */var/lib/waagent/* directory.</span><span class="sxs-lookup"><span data-stu-id="47745-197">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="47745-198">tooautomate toe te voegen Hallo certificaat toohello VM en NGINX te configureren, kunt u een bijgewerkte cloud-init-configuratie van het vorige voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="47745-198">tooautomate adding hello certificate toohello VM and configuring NGINX, you can use an updated cloud-init config from hello previous example.</span></span>

<span data-ttu-id="47745-199">Maak een bestand met de naam *cloud-init-secured.txt* en plakken Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="47745-199">Create a file named *cloud-init-secured.txt* and paste hello following configuration.</span></span> <span data-ttu-id="47745-200">Opnieuw als u Hallo Cloud-Shell, maakt Hallo cloud init-configuratiebestand er en niet op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="47745-200">Again, if you use hello Cloud Shell, create hello cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="47745-201">Gebruik `sensible-editor cloud-init-secured.txt` toocreate Hallo bestand en een overzicht van beschikbare editors.</span><span class="sxs-lookup"><span data-stu-id="47745-201">Use `sensible-editor cloud-init-secured.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="47745-202">Zorg ervoor dat Hallo hele cloud-init-bestand correct is gekopieerd, met name Hallo eerste regel:</span><span class="sxs-lookup"><span data-stu-id="47745-202">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a><span data-ttu-id="47745-203">Beveiligde virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="47745-203">Create secure VM</span></span>
<span data-ttu-id="47745-204">Maak nu een virtuele machine met [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="47745-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="47745-205">Hallo certificaatgegevens wordt geïnjecteerd uit Sleutelkluis Hello `--secrets` parameter.</span><span class="sxs-lookup"><span data-stu-id="47745-205">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="47745-206">Zoals in het vorige voorbeeld hello, u ook doorgeven in de configuratie van cloud-init Hallo Hello `--custom-data` parameter:</span><span class="sxs-lookup"><span data-stu-id="47745-206">As in hello previous example, you also pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="47745-207">Het duurt enkele minuten voordat Hallo VM toobe gemaakt, hello-pakketten tooinstall en Hallo app toostart.</span><span class="sxs-lookup"><span data-stu-id="47745-207">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="47745-208">Er zijn achtergrondtaken die toorun verder gaat nadat hello Azure CLI keert u terug toohello prompt.</span><span class="sxs-lookup"><span data-stu-id="47745-208">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="47745-209">Het is mogelijk een andere paar minuten voordat u toegang hebt tot Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="47745-209">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="47745-210">Wanneer Hallo VM is gemaakt, noteer Hallo `publicIpAddress` weergegeven door hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="47745-210">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="47745-211">Dit adres is gebruikte tooaccess hello Node.js-app via een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="47745-211">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="47745-212">virtuele machine, open poort 443 van Hallo Internet met voor secure web verkeer tooreach tooallow [az vm open poort](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="47745-212">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="47745-213">Test beveiligde web-app</span><span class="sxs-lookup"><span data-stu-id="47745-213">Test secure web app</span></span>
<span data-ttu-id="47745-214">Nu kunt u een webbrowser openen en voer *https://<publicIpAddress>*  in de adresbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="47745-214">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="47745-215">Geef uw eigen openbare IP-adres uit Hallo VM proces maken.</span><span class="sxs-lookup"><span data-stu-id="47745-215">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="47745-216">Beveiligingswaarschuwing Hallo accepteren als u een zelfondertekend certificaat gebruikt:</span><span class="sxs-lookup"><span data-stu-id="47745-216">Accept hello security warning if you used a self-signed certificate:</span></span>

![Beveiligingswaarschuwing voor web browser accepteren](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="47745-218">Uw beveiligde NGINX-site en Node.js app wordt vervolgens weergegeven zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="47745-218">Your secured NGINX site and Node.js app is then displayed as in hello following example:</span></span>

![Actief beveiligde NGINX-site weergeven](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="47745-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="47745-220">Next steps</span></span>
<span data-ttu-id="47745-221">In deze zelfstudie kunt u virtuele machines op de eerste keer opstarten met cloud-init geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="47745-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="47745-222">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="47745-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="47745-223">Maken van een cloud-init-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="47745-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="47745-224">Een virtuele machine die gebruikmaakt van een cloud-init-bestand maken</span><span class="sxs-lookup"><span data-stu-id="47745-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="47745-225">Een actieve Node.js-app weergeven na Hallo die virtuele machine wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="47745-225">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="47745-226">Sleutelkluis toosecurely store certificaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="47745-226">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="47745-227">Beveiligde implementaties van NGINX met cloud-init automatiseren</span><span class="sxs-lookup"><span data-stu-id="47745-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="47745-228">Hoe gaan van de volgende zelfstudie toolearn toohello toocreate aangepaste VM-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="47745-228">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="47745-229">Aangepaste VM-installatiekopieën maken</span><span class="sxs-lookup"><span data-stu-id="47745-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
