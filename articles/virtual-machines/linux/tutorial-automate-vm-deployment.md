---
title: Aanpassen van een Linux-VM voor eerst wordt opgestart in Azure | Microsoft Docs
description: Meer informatie over het cloud-init en Sleutelkluis te gebruiken customze Linux VM's de eerste keer dat ze worden opgestart in Azure
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
ms.openlocfilehash: 6adf4e43aa80c28c6f5f8d8a071966323ba85723
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-customize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="b08d0-103">Het aanpassen van een virtuele Linux-machine op de eerste keer opstarten</span><span class="sxs-lookup"><span data-stu-id="b08d0-103">How to customize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="b08d0-104">In een vorige zelfstudie hebt u geleerd hoe u voor SSH aan een virtuele machine (VM) en handmatig installeren NGINX.</span><span class="sxs-lookup"><span data-stu-id="b08d0-104">In a previous tutorial, you learned how to SSH to a virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="b08d0-105">Voor het maken van virtuele machines op een snelle en consistente manier, is een vorm van automatisering doorgaans gewenst.</span><span class="sxs-lookup"><span data-stu-id="b08d0-105">To create VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="b08d0-106">Een gemeenschappelijke aanpak voor het aanpassen van een virtuele machine op de eerste keer opstarten is het gebruik [cloud init](https://cloudinit.readthedocs.io).</span><span class="sxs-lookup"><span data-stu-id="b08d0-106">A common approach to customize a VM on first boot is to use [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="b08d0-107">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="b08d0-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b08d0-108">Maken van een cloud-init-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="b08d0-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="b08d0-109">Een virtuele machine die gebruikmaakt van een cloud-init-bestand maken</span><span class="sxs-lookup"><span data-stu-id="b08d0-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="b08d0-110">Een actieve Node.js-app weergeven nadat de virtuele machine is gemaakt</span><span class="sxs-lookup"><span data-stu-id="b08d0-110">View a running Node.js app after the VM is created</span></span>
> * <span data-ttu-id="b08d0-111">Sleutelkluis gebruiken voor het veilig opslaan van certificaten</span><span class="sxs-lookup"><span data-stu-id="b08d0-111">Use Key Vault to securely store certificates</span></span>
> * <span data-ttu-id="b08d0-112">Beveiligde implementaties van NGINX met cloud-init automatiseren</span><span class="sxs-lookup"><span data-stu-id="b08d0-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b08d0-113">Als u wilt installeren en gebruiken van de CLI lokaal, in deze zelfstudie vereist dat u de Azure CLI versie 2.0.4 zijn uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="b08d0-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="b08d0-114">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="b08d0-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="b08d0-115">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b08d0-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="b08d0-116">Cloud-init-overzicht</span><span class="sxs-lookup"><span data-stu-id="b08d0-116">Cloud-init overview</span></span>
<span data-ttu-id="b08d0-117">[Cloud-init](https://cloudinit.readthedocs.io) is een veelgebruikte benadering voor het aanpassen van een Linux-VM als deze voor de eerste keer wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="b08d0-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach to customize a Linux VM as it boots for the first time.</span></span> <span data-ttu-id="b08d0-118">U kunt cloud init gebruiken voor het installeren van pakketten en bestanden schrijven of om gebruikers en beveiliging te configureren.</span><span class="sxs-lookup"><span data-stu-id="b08d0-118">You can use cloud-init to install packages and write files, or to configure users and security.</span></span> <span data-ttu-id="b08d0-119">Als de initialisatie van de cloud wordt uitgevoerd tijdens het opstartproces, zijn er geen extra stappen of vereist agents naar uw configuratie toe te passen.</span><span class="sxs-lookup"><span data-stu-id="b08d0-119">As cloud-init runs during the initial boot process, there are no additional steps or required agents to apply your configuration.</span></span>

<span data-ttu-id="b08d0-120">Cloud-init werkt ook via distributies.</span><span class="sxs-lookup"><span data-stu-id="b08d0-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="b08d0-121">Bijvoorbeeld, u niet gebruikt **apt get-installatie** of **yum installeren** om een pakket te installeren.</span><span class="sxs-lookup"><span data-stu-id="b08d0-121">For example, you don't use **apt-get install** or **yum install** to install a package.</span></span> <span data-ttu-id="b08d0-122">In plaats daarvan kunt u een lijst met pakketten te installeren.</span><span class="sxs-lookup"><span data-stu-id="b08d0-122">Instead you can define a list of packages to install.</span></span> <span data-ttu-id="b08d0-123">Het hulpprogramma voor systeemeigen pakket cloud init automatisch gebruikt voor de distro die u selecteert.</span><span class="sxs-lookup"><span data-stu-id="b08d0-123">Cloud-init automatically uses the native package management tool for the distro you select.</span></span>

<span data-ttu-id="b08d0-124">We werken met onze partners ophalen van cloud-init opgenomen en in de afbeeldingen die ze naar Azure bieden werkt.</span><span class="sxs-lookup"><span data-stu-id="b08d0-124">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span> <span data-ttu-id="b08d0-125">De volgende tabel geeft een overzicht van de huidige beschikbaarheid van de cloud init op Azure-platform installatiekopieën:</span><span class="sxs-lookup"><span data-stu-id="b08d0-125">The following table outlines the current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="b08d0-126">Alias</span><span class="sxs-lookup"><span data-stu-id="b08d0-126">Alias</span></span> | <span data-ttu-id="b08d0-127">Uitgever</span><span class="sxs-lookup"><span data-stu-id="b08d0-127">Publisher</span></span> | <span data-ttu-id="b08d0-128">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="b08d0-128">Offer</span></span> | <span data-ttu-id="b08d0-129">SKU</span><span class="sxs-lookup"><span data-stu-id="b08d0-129">SKU</span></span> | <span data-ttu-id="b08d0-130">Versie</span><span class="sxs-lookup"><span data-stu-id="b08d0-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="b08d0-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="b08d0-131">UbuntuLTS</span></span> |<span data-ttu-id="b08d0-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="b08d0-132">Canonical</span></span> |<span data-ttu-id="b08d0-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="b08d0-133">UbuntuServer</span></span> |<span data-ttu-id="b08d0-134">16.04 TNS</span><span class="sxs-lookup"><span data-stu-id="b08d0-134">16.04-LTS</span></span> |<span data-ttu-id="b08d0-135">meest recente</span><span class="sxs-lookup"><span data-stu-id="b08d0-135">latest</span></span> |
| <span data-ttu-id="b08d0-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="b08d0-136">UbuntuLTS</span></span> |<span data-ttu-id="b08d0-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="b08d0-137">Canonical</span></span> |<span data-ttu-id="b08d0-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="b08d0-138">UbuntuServer</span></span> |<span data-ttu-id="b08d0-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="b08d0-139">14.04.5-LTS</span></span> |<span data-ttu-id="b08d0-140">meest recente</span><span class="sxs-lookup"><span data-stu-id="b08d0-140">latest</span></span> |
| <span data-ttu-id="b08d0-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b08d0-141">CoreOS</span></span> |<span data-ttu-id="b08d0-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b08d0-142">CoreOS</span></span> |<span data-ttu-id="b08d0-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b08d0-143">CoreOS</span></span> |<span data-ttu-id="b08d0-144">Stabiel</span><span class="sxs-lookup"><span data-stu-id="b08d0-144">Stable</span></span> |<span data-ttu-id="b08d0-145">meest recente</span><span class="sxs-lookup"><span data-stu-id="b08d0-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="b08d0-146">Cloud-init-configuratiebestand maken</span><span class="sxs-lookup"><span data-stu-id="b08d0-146">Create cloud-init config file</span></span>
<span data-ttu-id="b08d0-147">Overzicht van cloud-init in actie, maak een VM die NGINX installeert en een eenvoudige 'Hallo wereld' Node.js-app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b08d0-147">To see cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="b08d0-148">De volgende cloud init-configuratie installeert de vereiste pakketten, maakt u een Node.js-app en vervolgens initialiseren en start u de app.</span><span class="sxs-lookup"><span data-stu-id="b08d0-148">The following cloud-init configuration installs the required packages, creates a Node.js app, then initialize and starts the app.</span></span>

<span data-ttu-id="b08d0-149">Maak een bestand met de naam in uw huidige shell *cloud init.txt* en plak de volgende configuratie.</span><span class="sxs-lookup"><span data-stu-id="b08d0-149">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="b08d0-150">Maak bijvoorbeeld het bestand in de Cloud-Shell niet op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="b08d0-150">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="b08d0-151">U kunt een editor die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b08d0-151">You can use any editor you wish.</span></span> <span data-ttu-id="b08d0-152">Voer `sensible-editor cloud-init.txt` voor het maken van het bestand en een overzicht van beschikbare editors.</span><span class="sxs-lookup"><span data-stu-id="b08d0-152">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="b08d0-153">Controleer of het hele cloud-init-bestand correct is gekopieerd met name de eerste regel:</span><span class="sxs-lookup"><span data-stu-id="b08d0-153">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

<span data-ttu-id="b08d0-154">Zie voor meer informatie over configuratieopties voor cloud-init [cloud init config voorbeelden](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span><span class="sxs-lookup"><span data-stu-id="b08d0-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="b08d0-155">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="b08d0-155">Create virtual machine</span></span>
<span data-ttu-id="b08d0-156">Voordat u een virtuele machine maken kunt, maakt u een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b08d0-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b08d0-157">Het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroupAutomate* in de *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="b08d0-157">The following example creates a resource group named *myResourceGroupAutomate* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="b08d0-158">Maak nu een virtuele machine met [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b08d0-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="b08d0-159">Gebruik de `--custom-data` parameter om door te geven in uw cloud-init-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="b08d0-159">Use the `--custom-data` parameter to pass in your cloud-init config file.</span></span> <span data-ttu-id="b08d0-160">Geef het volledige pad naar de *cloud init.txt* config als u het bestand buiten uw werkmap aanwezig opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b08d0-160">Provide the full path to the *cloud-init.txt* config if you saved the file outside of your present working directory.</span></span> <span data-ttu-id="b08d0-161">Het volgende voorbeeld wordt een virtuele machine met de naam *myAutomatedVM*:</span><span class="sxs-lookup"><span data-stu-id="b08d0-161">The following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="b08d0-162">Het duurt enkele minuten duren voordat de virtuele machine moet worden gemaakt, de pakketten te installeren en de app te starten.</span><span class="sxs-lookup"><span data-stu-id="b08d0-162">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="b08d0-163">Er zijn achtergrondtaken die uitvoeren blijven nadat de Azure CLI keert u terug naar de prompt.</span><span class="sxs-lookup"><span data-stu-id="b08d0-163">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="b08d0-164">Het is mogelijk een andere paar minuten voordat u toegang hebt tot de app.</span><span class="sxs-lookup"><span data-stu-id="b08d0-164">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="b08d0-165">Wanneer de virtuele machine is gemaakt, dient u de `publicIpAddress` weergegeven door de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b08d0-165">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="b08d0-166">Dit adres wordt gebruikt voor toegang tot de Node.js-app via een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="b08d0-166">This address is used to access the Node.js app via a web browser.</span></span>

<span data-ttu-id="b08d0-167">Open poort 80 via Internet met zodat webverkeer bereiken van uw virtuele machine [az vm open poort](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="b08d0-167">To allow web traffic to reach your VM, open port 80 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="b08d0-168">Test-web-app</span><span class="sxs-lookup"><span data-stu-id="b08d0-168">Test web app</span></span>
<span data-ttu-id="b08d0-169">Nu kunt u een webbrowser openen en voer *http://<publicIpAddress>*  in de adresbalk.</span><span class="sxs-lookup"><span data-stu-id="b08d0-169">Now you can open a web browser and enter *http://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="b08d0-170">Geef uw eigen openbare IP-adres van de virtuele machine proces maken.</span><span class="sxs-lookup"><span data-stu-id="b08d0-170">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="b08d0-171">Uw Node.js-app wordt weergegeven zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b08d0-171">Your Node.js app is displayed as in the following example:</span></span>

![Bekijk actieve NGINX-website](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="b08d0-173">Certificaten van de Sleutelkluis invoeren</span><span class="sxs-lookup"><span data-stu-id="b08d0-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="b08d0-174">Deze optionele sectie wordt beschreven hoe u veilig opslaan van certificaten in Azure Sleutelkluis en ze tijdens de implementatie van de virtuele machine te injecteren.</span><span class="sxs-lookup"><span data-stu-id="b08d0-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during the VM deployment.</span></span> <span data-ttu-id="b08d0-175">In plaats van met een aangepaste installatiekopie met de certificaten standaard uitbreidbaar, in dit proces zorgt ervoor dat de meest recente certificaten zijn ingevoegd op een virtuele machine op de eerste keer wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="b08d0-175">Rather than using a custom image that includes the certificates baked-in, this process ensures that the most up-to-date certificates are injected to a VM on first boot.</span></span> <span data-ttu-id="b08d0-176">Tijdens het proces is het certificaat nooit verlaat de Azure-platform, of wordt weergegeven in een script, opdrachtregel geschiedenis of sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b08d0-176">During the process, the certificate never leaves the Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="b08d0-177">Azure Sleutelkluis beschermt cryptografische sleutels en geheimen, zoals certificaten of wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="b08d0-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="b08d0-178">Sleutelkluis helpt te stroomlijnen van het sleutelbeheerproces en kunt u controle houdt over sleutels die toegang tot en uw gegevens te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="b08d0-178">Key Vault helps streamline the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="b08d0-179">Dit scenario bevat enkele concepten die Sleutelkluis voor het maken en een certificaat te gebruiken, maar is niet een volledig overzicht over het gebruik van de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="b08d0-179">This scenario introduces some Key Vault concepts to create and use a certificate, though is not an exhaustive overview on how to use Key Vault.</span></span>

<span data-ttu-id="b08d0-180">De volgende stappen laten zien hoe u kunt:</span><span class="sxs-lookup"><span data-stu-id="b08d0-180">The following steps show how you can:</span></span>

- <span data-ttu-id="b08d0-181">Maken van een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="b08d0-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="b08d0-182">Genereren of een certificaat uploaden naar de Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="b08d0-182">Generate or upload a certificate to the Key Vault</span></span>
- <span data-ttu-id="b08d0-183">Een geheim van het certificaat invoeren voor een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="b08d0-183">Create a secret from the certificate to inject in to a VM</span></span>
- <span data-ttu-id="b08d0-184">Een virtuele machine maken en het certificaat invoeren</span><span class="sxs-lookup"><span data-stu-id="b08d0-184">Create a VM and inject the certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="b08d0-185">Maken van een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="b08d0-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="b08d0-186">Maak eerst een Sleutelkluis met [az keyvault maken](/cli/azure/keyvault#create) en inschakelen voor gebruik wanneer u een virtuele machine implementeert.</span><span class="sxs-lookup"><span data-stu-id="b08d0-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="b08d0-187">Elke Sleutelkluis moet een unieke naam hebben en moet alle kleine letters.</span><span class="sxs-lookup"><span data-stu-id="b08d0-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="b08d0-188">Vervang *mykeyvault* in het volgende voorbeeld met de naam van uw eigen unieke Sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="b08d0-188">Replace *mykeyvault* in the following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="b08d0-189">Certificaat genereren en opslaan in de Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="b08d0-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="b08d0-190">Voor gebruik in productieomgevingen, moet u een geldig certificaat dat is ondertekend door een vertrouwde provider met importeren [az keyvault certificaat importeren](/cli/azure/keyvault/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="b08d0-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="b08d0-191">Voor deze zelfstudie, het volgende voorbeeld toont hoe kunt u een zelfondertekend certificaat met genereren [az keyvault-certificaat maken](/cli/azure/keyvault/certificate#create) die gebruikmaakt van het standaardbeleid voor certificaat:</span><span class="sxs-lookup"><span data-stu-id="b08d0-191">For this tutorial, the following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses the default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="b08d0-192">Certificaat voor gebruik met de virtuele machine voorbereiden</span><span class="sxs-lookup"><span data-stu-id="b08d0-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="b08d0-193">Het certificaat te gebruiken tijdens de virtuele machine proces voor het maken, verkrijgen van de ID van het certificaat met [az keyvault lijst-versies van het clientgeheim](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="b08d0-193">To use the certificate during the VM create process, obtain the ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="b08d0-194">De virtuele machine moet het certificaat in een bepaalde indeling invoeren deze bij het opstarten, converteert u dus het certificaat met [az vm indeling-geheim](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="b08d0-194">The VM needs the certificate in a certain format to inject it on boot, so convert the certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="b08d0-195">Het volgende voorbeeld wordt de uitvoer van deze opdrachten naar variabelen voor eenvoudig te gebruiken in de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="b08d0-195">The following example assigns the output of these commands to variables for ease of use in the next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-to-secure-nginx"></a><span data-ttu-id="b08d0-196">Maken van cloud-init-config NGINX beveiligen</span><span class="sxs-lookup"><span data-stu-id="b08d0-196">Create cloud-init config to secure NGINX</span></span>
<span data-ttu-id="b08d0-197">Wanneer u maakt een virtuele machine, certificaten en sleutels worden opgeslagen in de beveiligde */var/lib/waagent/* directory.</span><span class="sxs-lookup"><span data-stu-id="b08d0-197">When you create a VM, certificates and keys are stored in the protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="b08d0-198">U kunt een bijgewerkte cloud-init-configuratie van het vorige voorbeeld gebruiken voor het automatiseren van het certificaat toevoegen aan de virtuele machine en NGINX configureren.</span><span class="sxs-lookup"><span data-stu-id="b08d0-198">To automate adding the certificate to the VM and configuring NGINX, you can use an updated cloud-init config from the previous example.</span></span>

<span data-ttu-id="b08d0-199">Maak een bestand met de naam *cloud-init-secured.txt* en plak de volgende configuratie.</span><span class="sxs-lookup"><span data-stu-id="b08d0-199">Create a file named *cloud-init-secured.txt* and paste the following configuration.</span></span> <span data-ttu-id="b08d0-200">Opnieuw als u de Shell Cloud gebruikt, maken het configuratiebestand van de cloud init er en niet op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="b08d0-200">Again, if you use the Cloud Shell, create the cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="b08d0-201">Gebruik `sensible-editor cloud-init-secured.txt` voor het maken van het bestand en een overzicht van beschikbare editors.</span><span class="sxs-lookup"><span data-stu-id="b08d0-201">Use `sensible-editor cloud-init-secured.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="b08d0-202">Controleer of het hele cloud-init-bestand correct is gekopieerd met name de eerste regel:</span><span class="sxs-lookup"><span data-stu-id="b08d0-202">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

### <a name="create-secure-vm"></a><span data-ttu-id="b08d0-203">Beveiligde virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="b08d0-203">Create secure VM</span></span>
<span data-ttu-id="b08d0-204">Maak nu een virtuele machine met [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b08d0-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="b08d0-205">De gegevens van het certificaat wordt geïnjecteerd uit de Sleutelkluis met de `--secrets` parameter.</span><span class="sxs-lookup"><span data-stu-id="b08d0-205">The certificate data is injected from Key Vault with the `--secrets` parameter.</span></span> <span data-ttu-id="b08d0-206">Zoals in het vorige voorbeeld, geeft u ook in de cloud init-configuratie met de `--custom-data` parameter:</span><span class="sxs-lookup"><span data-stu-id="b08d0-206">As in the previous example, you also pass in the cloud-init config with the `--custom-data` parameter:</span></span>

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

<span data-ttu-id="b08d0-207">Het duurt enkele minuten duren voordat de virtuele machine moet worden gemaakt, de pakketten te installeren en de app te starten.</span><span class="sxs-lookup"><span data-stu-id="b08d0-207">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="b08d0-208">Er zijn achtergrondtaken die uitvoeren blijven nadat de Azure CLI keert u terug naar de prompt.</span><span class="sxs-lookup"><span data-stu-id="b08d0-208">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="b08d0-209">Het is mogelijk een andere paar minuten voordat u toegang hebt tot de app.</span><span class="sxs-lookup"><span data-stu-id="b08d0-209">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="b08d0-210">Wanneer de virtuele machine is gemaakt, dient u de `publicIpAddress` weergegeven door de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b08d0-210">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="b08d0-211">Dit adres wordt gebruikt voor toegang tot de Node.js-app via een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="b08d0-211">This address is used to access the Node.js app via a web browser.</span></span>

<span data-ttu-id="b08d0-212">Zodat beveiligde webverkeer bereiken van uw virtuele machine poort 443 openen vanaf het Internet met [az vm open poort](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="b08d0-212">To allow secure web traffic to reach your VM, open port 443 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="b08d0-213">Test beveiligde web-app</span><span class="sxs-lookup"><span data-stu-id="b08d0-213">Test secure web app</span></span>
<span data-ttu-id="b08d0-214">Nu kunt u een webbrowser openen en voer *https://<publicIpAddress>*  in de adresbalk.</span><span class="sxs-lookup"><span data-stu-id="b08d0-214">Now you can open a web browser and enter *https://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="b08d0-215">Geef uw eigen openbare IP-adres van de virtuele machine proces maken.</span><span class="sxs-lookup"><span data-stu-id="b08d0-215">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="b08d0-216">De beveiligingswaarschuwing accepteren als u een zelfondertekend certificaat gebruikt:</span><span class="sxs-lookup"><span data-stu-id="b08d0-216">Accept the security warning if you used a self-signed certificate:</span></span>

![Beveiligingswaarschuwing voor web browser accepteren](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="b08d0-218">Uw beveiligde NGINX-site en Node.js app wordt vervolgens weergegeven zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b08d0-218">Your secured NGINX site and Node.js app is then displayed as in the following example:</span></span>

![Actief beveiligde NGINX-site weergeven](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="b08d0-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b08d0-220">Next steps</span></span>
<span data-ttu-id="b08d0-221">In deze zelfstudie kunt u virtuele machines op de eerste keer opstarten met cloud-init geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b08d0-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="b08d0-222">U leert hoe naar:</span><span class="sxs-lookup"><span data-stu-id="b08d0-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b08d0-223">Maken van een cloud-init-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="b08d0-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="b08d0-224">Een virtuele machine die gebruikmaakt van een cloud-init-bestand maken</span><span class="sxs-lookup"><span data-stu-id="b08d0-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="b08d0-225">Een actieve Node.js-app weergeven nadat de virtuele machine is gemaakt</span><span class="sxs-lookup"><span data-stu-id="b08d0-225">View a running Node.js app after the VM is created</span></span>
> * <span data-ttu-id="b08d0-226">Sleutelkluis gebruiken voor het veilig opslaan van certificaten</span><span class="sxs-lookup"><span data-stu-id="b08d0-226">Use Key Vault to securely store certificates</span></span>
> * <span data-ttu-id="b08d0-227">Beveiligde implementaties van NGINX met cloud-init automatiseren</span><span class="sxs-lookup"><span data-stu-id="b08d0-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="b08d0-228">Ga naar de volgende zelfstudie voor informatie over het maken van aangepaste installatiekopieën van virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b08d0-228">Advance to the next tutorial to learn how to create custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b08d0-229">Aangepaste VM-installatiekopieën maken</span><span class="sxs-lookup"><span data-stu-id="b08d0-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
