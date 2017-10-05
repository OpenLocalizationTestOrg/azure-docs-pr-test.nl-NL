---
title: Een pijplijn ontwikkeling maken in Azure met Jenkins | Microsoft Docs
description: Meer informatie over het maken van een Jenkins virtuele machine in Azure die ophaalt vanuit GitHub op elke doorvoer code en maakt een nieuwe Docker-container voor het uitvoeren van uw app
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
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d9849b5e061dd7f2ae0744a3522dc2eb1fb37035
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="94ce1-103">Het maken van een infrastructuur voor ontwikkeling op een Linux VM in Azure met Jenkins, GitHub en Docker</span><span class="sxs-lookup"><span data-stu-id="94ce1-103">How to create a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="94ce1-104">U kunt een continue integratie en implementatie (CI/CD) pijplijn gebruiken voor het automatiseren van de fase bouwen en testen van de ontwikkeling van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="94ce1-104">To automate the build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="94ce1-105">In deze zelfstudie maakt u een pijplijn CI/CD maken op een virtuele machine in Azure met inbegrip van hoe:</span><span class="sxs-lookup"><span data-stu-id="94ce1-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="94ce1-106">Maak een VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="94ce1-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="94ce1-107">Installeren en configureren van Jenkins</span><span class="sxs-lookup"><span data-stu-id="94ce1-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="94ce1-108">Webhook-integratie tussen GitHub en Jenkins maken</span><span class="sxs-lookup"><span data-stu-id="94ce1-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="94ce1-109">Maken en activeren Jenkins build taken van GitHub doorvoeringen</span><span class="sxs-lookup"><span data-stu-id="94ce1-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="94ce1-110">Een Docker-installatiekopie voor uw app maken</span><span class="sxs-lookup"><span data-stu-id="94ce1-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="94ce1-111">Controleer of de GitHub-doorvoeracties bouwen nieuwe Docker-installatiekopie en app-updates</span><span class="sxs-lookup"><span data-stu-id="94ce1-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="94ce1-112">Als u wilt installeren en gebruiken van de CLI lokaal, in deze zelfstudie vereist dat u de Azure CLI versie 2.0.4 zijn uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="94ce1-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="94ce1-113">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="94ce1-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="94ce1-114">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="94ce1-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="94ce1-115">Jenkins exemplaar maken</span><span class="sxs-lookup"><span data-stu-id="94ce1-115">Create Jenkins instance</span></span>
<span data-ttu-id="94ce1-116">In een vorige zelfstudie over [het aanpassen van een virtuele Linux-machine op de eerste keer opstarten](tutorial-automate-vm-deployment.md), hebt u geleerd hoe u de aanpassing van de virtuele machine met cloud-init automatiseren.</span><span class="sxs-lookup"><span data-stu-id="94ce1-116">In a previous tutorial on [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with cloud-init.</span></span> <span data-ttu-id="94ce1-117">Deze zelfstudie wordt een bestand cloud init Jenkins en Docker wilt installeren op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="94ce1-117">This tutorial uses a cloud-init file to install Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="94ce1-118">Maak een bestand met de naam in uw huidige shell *cloud init.txt* en plak de volgende configuratie.</span><span class="sxs-lookup"><span data-stu-id="94ce1-118">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="94ce1-119">Maak bijvoorbeeld het bestand in de Cloud-Shell niet op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="94ce1-119">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="94ce1-120">Voer `sensible-editor cloud-init-jenkins.txt` voor het maken van het bestand en een overzicht van beschikbare editors.</span><span class="sxs-lookup"><span data-stu-id="94ce1-120">Enter `sensible-editor cloud-init-jenkins.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="94ce1-121">Controleer of het hele cloud-init-bestand correct is gekopieerd met name de eerste regel:</span><span class="sxs-lookup"><span data-stu-id="94ce1-121">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

<span data-ttu-id="94ce1-122">Voordat u een virtuele machine maken kunt, maakt u een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="94ce1-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="94ce1-123">Het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroupJenkins* in de *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="94ce1-123">The following example creates a resource group named *myResourceGroupJenkins* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="94ce1-124">Maak nu een virtuele machine met [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="94ce1-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="94ce1-125">Gebruik de `--custom-data` parameter om door te geven in uw cloud-init-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="94ce1-125">Use the `--custom-data` parameter to pass in your cloud-init config file.</span></span> <span data-ttu-id="94ce1-126">Geef het volledige pad naar *cloud-init-jenkins.txt* als u het bestand buiten uw werkmap aanwezig opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="94ce1-126">Provide the full path to *cloud-init-jenkins.txt* if you saved the file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="94ce1-127">Het duurt enkele minuten duren voordat de virtuele machine worden gemaakt en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="94ce1-127">It takes a few minutes for the VM to be created and configured.</span></span>

<span data-ttu-id="94ce1-128">Gebruik zodat webverkeer bereiken van uw virtuele machine [az vm open poort](/cli/azure/vm#open-port) poort openen *8080* voor Jenkins verkeer en poort *1337* voor de Node.js-app die wordt gebruikt voor het uitvoeren van een voorbeeld-app:</span><span class="sxs-lookup"><span data-stu-id="94ce1-128">To allow web traffic to reach your VM, use [az vm open-port](/cli/azure/vm#open-port) to open port *8080* for Jenkins traffic and port *1337* for the Node.js app that is used to run a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="94ce1-129">Jenkins configureren</span><span class="sxs-lookup"><span data-stu-id="94ce1-129">Configure Jenkins</span></span>
<span data-ttu-id="94ce1-130">Voor toegang tot uw Jenkins-exemplaar moet u het openbare IP-adres van uw virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="94ce1-130">To access your Jenkins instance, obtain the public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="94ce1-131">Uit veiligheidsoverwegingen moet u Geef de eerste Administrator-wachtwoord die zijn opgeslagen in een tekstbestand op de virtuele machine om de Jenkins-installatie te beginnen.</span><span class="sxs-lookup"><span data-stu-id="94ce1-131">For security purposes, you need to enter the initial admin password that is stored in a text file on your VM to start the Jenkins install.</span></span> <span data-ttu-id="94ce1-132">Gebruik het openbare IP-adres dat is verkregen in de vorige stap voor SSH met uw virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="94ce1-132">Use the public IP address obtained in the previous step to SSH to your VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="94ce1-133">Weergave de `initialAdminPassword` voor uw Jenkins installeren en dit te kopiëren:</span><span class="sxs-lookup"><span data-stu-id="94ce1-133">View the `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="94ce1-134">Als het bestand is nog niet beschikbaar, wacht u een paar minuten totdat de cloud-init om de Jenkins en Docker-installatie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="94ce1-134">If the file isn't available yet, wait a couple more minutes for cloud-init to complete the Jenkins and Docker install.</span></span>

<span data-ttu-id="94ce1-135">Nu open een webbrowser en Ga naar `http://<publicIps>:8080`.</span><span class="sxs-lookup"><span data-stu-id="94ce1-135">Now open a web browser and go to `http://<publicIps>:8080`.</span></span> <span data-ttu-id="94ce1-136">Voer de eerste Jenkins installatie als volgt:</span><span class="sxs-lookup"><span data-stu-id="94ce1-136">Complete the initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="94ce1-137">Voer de *initialAdminPassword* verkregen van de virtuele machine in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="94ce1-137">Enter the *initialAdminPassword* obtained from the VM in the previous step.</span></span>
- <span data-ttu-id="94ce1-138">Klik op **selecteren van invoegtoepassingen installeren**</span><span class="sxs-lookup"><span data-stu-id="94ce1-138">Click **Select plugins to install**</span></span>
- <span data-ttu-id="94ce1-139">Zoeken naar *GitHub* selecteren in het tekstvak bovenaan de *GitHub-invoegtoepassing*, klikt u vervolgens op **installeren**</span><span class="sxs-lookup"><span data-stu-id="94ce1-139">Search for *GitHub* in the text box across the top, select the *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="94ce1-140">Vul het formulier voor het maken van een gebruikersaccount Jenkins.</span><span class="sxs-lookup"><span data-stu-id="94ce1-140">To create a Jenkins user account, fill out the form as desired.</span></span> <span data-ttu-id="94ce1-141">Vanuit beveiligingsoogpunt, moet u deze eerste Jenkins-gebruiker in plaats van voortgezet als de standaard admin-account maken.</span><span class="sxs-lookup"><span data-stu-id="94ce1-141">From a security perspective, you should create this first Jenkins user rather than continuing as the default admin account.</span></span>
- <span data-ttu-id="94ce1-142">Wanneer u klaar bent, klikt u op **Jenkins gebruiken**</span><span class="sxs-lookup"><span data-stu-id="94ce1-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="94ce1-143">GitHub webhook maken</span><span class="sxs-lookup"><span data-stu-id="94ce1-143">Create GitHub webhook</span></span>
<span data-ttu-id="94ce1-144">Voor het configureren van de integratie met GitHub, opent u de [Node.js Hallo wereld-voorbeeld-app](https://github.com/Azure-Samples/nodejs-docs-hello-world) uit de opslagplaats Azure-voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="94ce1-144">To configure the integration with GitHub, open the [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from the Azure samples repo.</span></span> <span data-ttu-id="94ce1-145">Om te vertakken de opslagplaats op uw eigen GitHub-account, klikt u op de **Fork** knop in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="94ce1-145">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>

<span data-ttu-id="94ce1-146">Maak een webhook binnen de fork die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="94ce1-146">Create a webhook inside the fork you created:</span></span>

- <span data-ttu-id="94ce1-147">Klik op **instellingen**, selecteer daarna **integraties & services** aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="94ce1-147">Click **Settings**, then select **Integrations & services** on the left-hand side.</span></span>
- <span data-ttu-id="94ce1-148">Klik op **service toevoegen**, voer dan *Jenkins* in het filtervak.</span><span class="sxs-lookup"><span data-stu-id="94ce1-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="94ce1-149">Selecteer *Jenkins (GitHub-invoegtoepassing)*</span><span class="sxs-lookup"><span data-stu-id="94ce1-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="94ce1-150">Voor de **Jenkins hook URL**, voer `http://<publicIps>:8080/github-webhook/`.</span><span class="sxs-lookup"><span data-stu-id="94ce1-150">For the **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="94ce1-151">Zorg ervoor dat u de afsluitende /</span><span class="sxs-lookup"><span data-stu-id="94ce1-151">Make sure you include the trailing /</span></span>
- <span data-ttu-id="94ce1-152">Klik op **service toevoegen**</span><span class="sxs-lookup"><span data-stu-id="94ce1-152">Click **Add service**</span></span>

![GitHub webhook toevoegen aan uw Gevorkte opslagplaats](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="94ce1-154">Jenkins taak maken</span><span class="sxs-lookup"><span data-stu-id="94ce1-154">Create Jenkins job</span></span>
<span data-ttu-id="94ce1-155">Om te reageren op een gebeurtenis Jenkins in GitHub zoals het vastleggen van de code hebt, kunt u een Jenkins-taak maken.</span><span class="sxs-lookup"><span data-stu-id="94ce1-155">To have Jenkins respond to an event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="94ce1-156">Klik op in uw website Jenkins **nieuwe taken maken** vanaf de startpagina:</span><span class="sxs-lookup"><span data-stu-id="94ce1-156">In your Jenkins website, click **Create new jobs** from the home page:</span></span>

- <span data-ttu-id="94ce1-157">Voer *HelloWorld* als de taaknaam van de.</span><span class="sxs-lookup"><span data-stu-id="94ce1-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="94ce1-158">Kies **Freestyle project**, selecteer daarna **OK**.</span><span class="sxs-lookup"><span data-stu-id="94ce1-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="94ce1-159">Onder de **algemene** sectie **GitHub** project en voer uw Gevorkte repo-URL, zoals *https://github.com/iainfoulds/nodejs-docs-hello-world*</span><span class="sxs-lookup"><span data-stu-id="94ce1-159">Under the **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="94ce1-160">Onder de **Source code management** sectie **Git**, Voer uw Gevorkte opslagplaats *.git* -URL, zoals *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span><span class="sxs-lookup"><span data-stu-id="94ce1-160">Under the **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="94ce1-161">Onder de **bouwen Triggers** sectie **GitHub haakje trigger voor GITscm polling**.</span><span class="sxs-lookup"><span data-stu-id="94ce1-161">Under the **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="94ce1-162">Onder de **bouwen** sectie **toevoegen build stap**.</span><span class="sxs-lookup"><span data-stu-id="94ce1-162">Under the **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="94ce1-163">Selecteer **shell uitvoeren**, voer dan `echo "Testing"` in naar opdrachtvenster.</span><span class="sxs-lookup"><span data-stu-id="94ce1-163">Select **Execute shell**, then enter `echo "Testing"` in to command window.</span></span>
- <span data-ttu-id="94ce1-164">Klik op **opslaan** aan de onderkant van het venster met taken.</span><span class="sxs-lookup"><span data-stu-id="94ce1-164">Click **Save** at the bottom of the jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="94ce1-165">Integratie van GitHub testen</span><span class="sxs-lookup"><span data-stu-id="94ce1-165">Test GitHub integration</span></span>
<span data-ttu-id="94ce1-166">Als u wilt testen op de GitHub-integratie met Jenkins, een wijziging in uw fork worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="94ce1-166">To test the GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="94ce1-167">Terug in de GitHub-webgebruikersinterface, selecteer uw Gevorkte opslagplaats en klik op de **index.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="94ce1-167">Back in GitHub web UI, select your forked repo, and then click the **index.js** file.</span></span> <span data-ttu-id="94ce1-168">Klik op het potloodpictogram om dit bestand bewerken, zodat de regel 6 leest:</span><span class="sxs-lookup"><span data-stu-id="94ce1-168">Click the pencil icon to edit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="94ce1-169">Klik om uw wijzigingen op de **wijzigingen doorvoeren** knop onderaan.</span><span class="sxs-lookup"><span data-stu-id="94ce1-169">To commit your changes, click the **Commit changes** button at the bottom.</span></span>

<span data-ttu-id="94ce1-170">Een nieuwe build begint in Jenkins, onder de **bouwen geschiedenis** sectie van de linkerbenedenhoek van de pagina van de taak.</span><span class="sxs-lookup"><span data-stu-id="94ce1-170">In Jenkins, a new build starts under the **Build history** section of the bottom left-hand corner of your job page.</span></span> <span data-ttu-id="94ce1-171">Klik op de koppeling van build-nummer en selecteer **Console uitvoer** op de links grootte.</span><span class="sxs-lookup"><span data-stu-id="94ce1-171">Click the build number link and select **Console output** on the left-hand size.</span></span> <span data-ttu-id="94ce1-172">U kunt de stappen Jenkins wordt als uw code wordt opgehaald uit GitHub bekijken en de build-actie levert het bericht `Testing` naar de console.</span><span class="sxs-lookup"><span data-stu-id="94ce1-172">You can view the steps Jenkins takes as your code is pulled from GitHub and the build action outputs the message `Testing` to the console.</span></span> <span data-ttu-id="94ce1-173">Telkens wanneer een doorvoer wordt gemaakt in GitHub, de webhook gezocht naar Jenkins en activeren van een nieuwe build op deze manier.</span><span class="sxs-lookup"><span data-stu-id="94ce1-173">Each time a commit is made in GitHub, the webhook reaches out to Jenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="94ce1-174">Afbeelding van Docker-build definiëren</span><span class="sxs-lookup"><span data-stu-id="94ce1-174">Define Docker build image</span></span>
<span data-ttu-id="94ce1-175">Om te zien van de Node.js-app uitgevoerd op basis van uw GitHub-doorvoeracties kunnen maken van een installatiekopie Docker uitvoeren van de app.</span><span class="sxs-lookup"><span data-stu-id="94ce1-175">To see the Node.js app running based on your GitHub commits, lets build a Docker image to run the app.</span></span> <span data-ttu-id="94ce1-176">De afbeelding wordt samengesteld uit een Dockerfile die definieert het configureren van de container waarin de app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="94ce1-176">The image is built from a Dockerfile that defines how to configure the container that runs the app.</span></span> 

<span data-ttu-id="94ce1-177">Wijzig de Jenkins werkruimte map met de naam van de taak die u in de vorige stap hebt gemaakt van de SSH-verbinding met uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="94ce1-177">From the SSH connection to your VM, change to the Jenkins workspace directory named after the job you created in a previous step.</span></span> <span data-ttu-id="94ce1-178">In ons voorbeeld die heette *HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="94ce1-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="94ce1-179">Maken van een bestand met de in deze map werkruimte met `sudo sensible-editor Dockerfile` en plak de volgende inhoud.</span><span class="sxs-lookup"><span data-stu-id="94ce1-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste the following contents.</span></span> <span data-ttu-id="94ce1-180">Controleer of de hele Dockerfile correct is gekopieerd met name de eerste regel:</span><span class="sxs-lookup"><span data-stu-id="94ce1-180">Make sure that the whole Dockerfile is copied correctly, especially the first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="94ce1-181">Deze Dockerfile maakt gebruik van de Node.js basisinstallatiekopie gebruik Alpine Linux, zichtbaar gemaakt poort 1337 die de Hallo wereld-app wordt uitgevoerd, klikt u vervolgens kopieert de app-bestanden en geïnitialiseerd met behulp van.</span><span class="sxs-lookup"><span data-stu-id="94ce1-181">This Dockerfile uses the base Node.js image using Alpine Linux, exposes port 1337 that the Hello World app runs on, then copies the app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="94ce1-182">Jenkins build regels maken</span><span class="sxs-lookup"><span data-stu-id="94ce1-182">Create Jenkins build rules</span></span>
<span data-ttu-id="94ce1-183">In de vorige stap, moet u een eenvoudige Jenkins build regel die een bericht naar de console uitvoeren gemaakt.</span><span class="sxs-lookup"><span data-stu-id="94ce1-183">In a previous step, you created a basic Jenkins build rule that output a message to the console.</span></span> <span data-ttu-id="94ce1-184">U kunt de build-stap voor het gebruik van onze Dockerfile en voer de app te maken.</span><span class="sxs-lookup"><span data-stu-id="94ce1-184">Lets create the build step to use our Dockerfile and run the app.</span></span>

<span data-ttu-id="94ce1-185">Terug in uw exemplaar Jenkins selecteert u de taak die u in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="94ce1-185">Back in your Jenkins instance, select the job you created in a previous step.</span></span> <span data-ttu-id="94ce1-186">Klik op **configureren** op de linkerkant en blader omlaag naar de **bouwen** sectie:</span><span class="sxs-lookup"><span data-stu-id="94ce1-186">Click **Configure** on the left-hand side and scroll down to the **Build** section:</span></span>

- <span data-ttu-id="94ce1-187">Verwijder de bestaande `echo "Test"` stap bouwen.</span><span class="sxs-lookup"><span data-stu-id="94ce1-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="94ce1-188">Klik op de rode x in de rechterbovenhoek van het bestaande build stap vak.</span><span class="sxs-lookup"><span data-stu-id="94ce1-188">Click the red cross on the top right-hand corner of the existing build step box.</span></span>
- <span data-ttu-id="94ce1-189">Klik op **toevoegen build stap**, selecteer daarna **shell uitvoeren**</span><span class="sxs-lookup"><span data-stu-id="94ce1-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="94ce1-190">In de **opdracht** vak, voert de volgende Docker-opdrachten en selecteer **opslaan**:</span><span class="sxs-lookup"><span data-stu-id="94ce1-190">In the **Command** box, enter the following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="94ce1-191">De stappen van de build Docker maken een installatiekopie en de tag met de Jenkins build-nummer zodat u kunt een geschiedenis van installatiekopieën onderhouden.</span><span class="sxs-lookup"><span data-stu-id="94ce1-191">The Docker build steps create an image and tag it with the Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="94ce1-192">Eventuele bestaande containers uitvoeren van de app worden gestopt en verwijderd.</span><span class="sxs-lookup"><span data-stu-id="94ce1-192">Any existing containers running the app are stopped and then removed.</span></span> <span data-ttu-id="94ce1-193">Een nieuwe container vervolgens met behulp van de installatiekopie is gestart en voert u uw Node.js-app op basis van de meest recente doorvoeringen in GitHub.</span><span class="sxs-lookup"><span data-stu-id="94ce1-193">A new container is then started using the image and runs your Node.js app based on the latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="94ce1-194">Test uw pijplijn</span><span class="sxs-lookup"><span data-stu-id="94ce1-194">Test your pipeline</span></span>
<span data-ttu-id="94ce1-195">Overzicht van de hele pijplijn in actie bewerken de *index.js* bestand in uw GitHub-repo-Gevorkte opnieuw en klik op **wijziging doorvoeren**.</span><span class="sxs-lookup"><span data-stu-id="94ce1-195">To see the whole pipeline in action, edit the *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="94ce1-196">Een nieuwe taak wordt gestart met Jenkins op basis van de webhook voor GitHub.</span><span class="sxs-lookup"><span data-stu-id="94ce1-196">A new job starts in Jenkins based on the webhook for GitHub.</span></span> <span data-ttu-id="94ce1-197">Het duurt een paar seconden de Docker-installatiekopie maken en uw app te starten in een nieuwe container.</span><span class="sxs-lookup"><span data-stu-id="94ce1-197">It takes a few seconds to create the Docker image and start your app in a new container.</span></span>

<span data-ttu-id="94ce1-198">Indien nodig, moet u het openbare IP-adres van uw virtuele machine opnieuw:</span><span class="sxs-lookup"><span data-stu-id="94ce1-198">If needed, obtain the public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="94ce1-199">Open een webbrowser en voer `http://<publicIps>:1337`.</span><span class="sxs-lookup"><span data-stu-id="94ce1-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="94ce1-200">Uw Node.js-app wordt weergegeven en reflecteert de meest recente doorvoeringen in uw GitHub-fork als volgt:</span><span class="sxs-lookup"><span data-stu-id="94ce1-200">Your Node.js app is displayed and reflects the latest commits in your GitHub fork as follows:</span></span>

![Actieve Node.js-app](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="94ce1-202">Maak nu een andere bewerken naar de *index.js* bestand in GitHub en de wijziging doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="94ce1-202">Now make another edit to the *index.js* file in GitHub and commit the change.</span></span> <span data-ttu-id="94ce1-203">Wacht een paar seconden voor de taak te voltooien in Jenkins en vernieuw vervolgens uw webbrowser als u wilt zien van de bijgewerkte versie van uw app uitgevoerd in een nieuwe container als volgt:</span><span class="sxs-lookup"><span data-stu-id="94ce1-203">Wait a few seconds for the job to complete in Jenkins, then refresh your web browser to see the updated version of your app running in a new container as follows:</span></span>

![Node.js-app uitgevoerd na een ander GitHub doorvoeren](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="94ce1-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="94ce1-205">Next steps</span></span>
<span data-ttu-id="94ce1-206">In deze zelfstudie maakt u geconfigureerd GitHub als u wilt een Jenkins build-taak uitvoeren op elke doorvoer code en vervolgens implementeert een Docker-container als uw app wilt testen.</span><span class="sxs-lookup"><span data-stu-id="94ce1-206">In this tutorial, you configured GitHub to run a Jenkins build job on each code commit and then deploy a Docker container to test your app.</span></span> <span data-ttu-id="94ce1-207">U leert hoe naar:</span><span class="sxs-lookup"><span data-stu-id="94ce1-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="94ce1-208">Maak een VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="94ce1-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="94ce1-209">Installeren en configureren van Jenkins</span><span class="sxs-lookup"><span data-stu-id="94ce1-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="94ce1-210">Webhook-integratie tussen GitHub en Jenkins maken</span><span class="sxs-lookup"><span data-stu-id="94ce1-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="94ce1-211">Maken en activeren Jenkins build taken van GitHub doorvoeringen</span><span class="sxs-lookup"><span data-stu-id="94ce1-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="94ce1-212">Een Docker-installatiekopie voor uw app maken</span><span class="sxs-lookup"><span data-stu-id="94ce1-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="94ce1-213">Controleer of de GitHub-doorvoeracties bouwen nieuwe Docker-installatiekopie en app-updates</span><span class="sxs-lookup"><span data-stu-id="94ce1-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="94ce1-214">Ga naar de volgende zelfstudie voor meer informatie over het integreren van Jenkins met Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="94ce1-214">Advance to the next tutorial to learn more about how to integrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94ce1-215">Apps implementeren met Jenkins en teamservices</span><span class="sxs-lookup"><span data-stu-id="94ce1-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)