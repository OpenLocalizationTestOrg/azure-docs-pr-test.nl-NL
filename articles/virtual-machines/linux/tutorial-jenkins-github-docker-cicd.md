---
title: een pijplijn ontwikkeling in Azure met Jenkins aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een Jenkins virtuele machine in Azure dat worden vanuit GitHub op elke code doorvoeren en een nieuwe Docker-container toorun builds uw app
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
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="fb492-103">Hoe een ontwikkeling infrastructuur op een Linux-VM in Azure met Jenkins, GitHub en Docker toocreate</span><span class="sxs-lookup"><span data-stu-id="fb492-103">How toocreate a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="fb492-104">tooautomate Hallo build en fase testen van de ontwikkeling van toepassingen, kunt u een continue integratie en implementatie (CI/CD) pijplijn.</span><span class="sxs-lookup"><span data-stu-id="fb492-104">tooautomate hello build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="fb492-105">In deze zelfstudie maakt u een pijplijn CI/CD maken op een virtuele machine in Azure met inbegrip van hoe:</span><span class="sxs-lookup"><span data-stu-id="fb492-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fb492-106">Maak een VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="fb492-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="fb492-107">Installeren en configureren van Jenkins</span><span class="sxs-lookup"><span data-stu-id="fb492-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="fb492-108">Webhook-integratie tussen GitHub en Jenkins maken</span><span class="sxs-lookup"><span data-stu-id="fb492-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="fb492-109">Maken en activeren Jenkins build taken van GitHub doorvoeringen</span><span class="sxs-lookup"><span data-stu-id="fb492-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="fb492-110">Een Docker-installatiekopie voor uw app maken</span><span class="sxs-lookup"><span data-stu-id="fb492-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="fb492-111">Controleer of de GitHub-doorvoeracties bouwen nieuwe Docker-installatiekopie en app-updates</span><span class="sxs-lookup"><span data-stu-id="fb492-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fb492-112">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="fb492-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="fb492-113">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="fb492-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fb492-114">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fb492-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="fb492-115">Jenkins exemplaar maken</span><span class="sxs-lookup"><span data-stu-id="fb492-115">Create Jenkins instance</span></span>
<span data-ttu-id="fb492-116">In een vorige zelfstudie over [hoe een virtuele Linux-machine op de eerste keer opstarten toocustomize](tutorial-automate-vm-deployment.md), u leert hoe tooautomate VM aanpassing met cloud-init.</span><span class="sxs-lookup"><span data-stu-id="fb492-116">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="fb492-117">Deze zelfstudie maakt gebruik van een cloud-init bestand tooinstall Jenkins en Docker op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fb492-117">This tutorial uses a cloud-init file tooinstall Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="fb492-118">Maak een bestand met de naam in uw huidige shell *cloud init.txt* en plakken Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="fb492-118">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="fb492-119">Bijvoorbeeld, Hallo-bestand in Hallo Cloud-Shell op uw lokale machine niet maken.</span><span class="sxs-lookup"><span data-stu-id="fb492-119">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="fb492-120">Voer `sensible-editor cloud-init-jenkins.txt` toocreate Hallo bestand en een overzicht van beschikbare editors.</span><span class="sxs-lookup"><span data-stu-id="fb492-120">Enter `sensible-editor cloud-init-jenkins.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="fb492-121">Zorg ervoor dat Hallo hele cloud-init-bestand correct is gekopieerd, met name Hallo eerste regel:</span><span class="sxs-lookup"><span data-stu-id="fb492-121">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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

<span data-ttu-id="fb492-122">Voordat u een virtuele machine maken kunt, maakt u een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fb492-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fb492-123">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupJenkins* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="fb492-123">hello following example creates a resource group named *myResourceGroupJenkins* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="fb492-124">Maak nu een virtuele machine met [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fb492-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="fb492-125">Gebruik Hallo `--custom-data` parameter toopass in uw cloud-init-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="fb492-125">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="fb492-126">Volledig pad hello te bieden*cloud-init-jenkins.txt* als Hallo bestand buiten de huidige werkmap is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="fb492-126">Provide hello full path too*cloud-init-jenkins.txt* if you saved hello file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="fb492-127">Het duurt enkele minuten duren voordat Hallo VM toobe gemaakt en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="fb492-127">It takes a few minutes for hello VM toobe created and configured.</span></span>

<span data-ttu-id="fb492-128">virtuele machine, gebruik van web verkeer tooreach tooallow [az vm open poort](/cli/azure/vm#open-port) tooopen poort *8080* voor Jenkins verkeer en poort *1337* voor Hallo Node.js-app die is gebruikt toorun een voorbeeld-app:</span><span class="sxs-lookup"><span data-stu-id="fb492-128">tooallow web traffic tooreach your VM, use [az vm open-port](/cli/azure/vm#open-port) tooopen port *8080* for Jenkins traffic and port *1337* for hello Node.js app that is used toorun a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="fb492-129">Jenkins configureren</span><span class="sxs-lookup"><span data-stu-id="fb492-129">Configure Jenkins</span></span>
<span data-ttu-id="fb492-130">tooaccess uw Jenkins exemplaar, Hallo openbare IP-adres van uw virtuele machine verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="fb492-130">tooaccess your Jenkins instance, obtain hello public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="fb492-131">Uit veiligheidsoverwegingen moet u tooenter Hallo initiële beheerderswachtwoord die is opgeslagen in een tekstbestand op uw VM toostart hello die jenkins installeren.</span><span class="sxs-lookup"><span data-stu-id="fb492-131">For security purposes, you need tooenter hello initial admin password that is stored in a text file on your VM toostart hello Jenkins install.</span></span> <span data-ttu-id="fb492-132">Hallo openbare IP-adres verkregen in Hallo vorige stap tooSSH tooyour VM gebruiken:</span><span class="sxs-lookup"><span data-stu-id="fb492-132">Use hello public IP address obtained in hello previous step tooSSH tooyour VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="fb492-133">Weergave Hallo `initialAdminPassword` voor uw Jenkins installeren en dit te kopiëren:</span><span class="sxs-lookup"><span data-stu-id="fb492-133">View hello `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="fb492-134">Als het Hallo-bestand is nog niet beschikbaar, wacht u enkele minuten voor cloud-init toocomplete hello Jenkins en Docker-installatie.</span><span class="sxs-lookup"><span data-stu-id="fb492-134">If hello file isn't available yet, wait a couple more minutes for cloud-init toocomplete hello Jenkins and Docker install.</span></span>

<span data-ttu-id="fb492-135">Nu open een webbrowser en ga te`http://<publicIps>:8080`.</span><span class="sxs-lookup"><span data-stu-id="fb492-135">Now open a web browser and go too`http://<publicIps>:8080`.</span></span> <span data-ttu-id="fb492-136">Voer Hallo initiële Jenkins setup als volgt:</span><span class="sxs-lookup"><span data-stu-id="fb492-136">Complete hello initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="fb492-137">Voer Hallo *initialAdminPassword* verkregen van Hallo VM in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="fb492-137">Enter hello *initialAdminPassword* obtained from hello VM in hello previous step.</span></span>
- <span data-ttu-id="fb492-138">Klik op **plugins tooinstall selecteren**</span><span class="sxs-lookup"><span data-stu-id="fb492-138">Click **Select plugins tooinstall**</span></span>
- <span data-ttu-id="fb492-139">Zoeken naar *GitHub* selecteren in het tekstvak Hallo Hallo bovenaan, Hallo *GitHub-invoegtoepassing*, klikt u vervolgens op **installeren**</span><span class="sxs-lookup"><span data-stu-id="fb492-139">Search for *GitHub* in hello text box across hello top, select hello *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="fb492-140">een gebruikersaccount Jenkins toocreate Hallo-formulier naar wens invullen.</span><span class="sxs-lookup"><span data-stu-id="fb492-140">toocreate a Jenkins user account, fill out hello form as desired.</span></span> <span data-ttu-id="fb492-141">Vanuit beveiligingsoogpunt, moet u deze eerste Jenkins-gebruiker in plaats van u doorgaat als Hallo standaard admin-account maken.</span><span class="sxs-lookup"><span data-stu-id="fb492-141">From a security perspective, you should create this first Jenkins user rather than continuing as hello default admin account.</span></span>
- <span data-ttu-id="fb492-142">Wanneer u klaar bent, klikt u op **Jenkins gebruiken**</span><span class="sxs-lookup"><span data-stu-id="fb492-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="fb492-143">GitHub webhook maken</span><span class="sxs-lookup"><span data-stu-id="fb492-143">Create GitHub webhook</span></span>
<span data-ttu-id="fb492-144">tooconfigure hello integratie met GitHub, open Hallo [Node.js Hallo wereld-voorbeeld-app](https://github.com/Azure-Samples/nodejs-docs-hello-world) uit hello Azure-voorbeelden opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="fb492-144">tooconfigure hello integration with GitHub, open hello [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from hello Azure samples repo.</span></span> <span data-ttu-id="fb492-145">toofork hello opslagplaats tooyour eigenaar GitHub-account, klikt u op Hallo **Fork** knop in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="fb492-145">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

<span data-ttu-id="fb492-146">Maak een webhook binnen Hallo fork die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="fb492-146">Create a webhook inside hello fork you created:</span></span>

- <span data-ttu-id="fb492-147">Klik op **instellingen**, selecteer daarna **integraties & services** aan de linkerkant Hallo.</span><span class="sxs-lookup"><span data-stu-id="fb492-147">Click **Settings**, then select **Integrations & services** on hello left-hand side.</span></span>
- <span data-ttu-id="fb492-148">Klik op **service toevoegen**, voer dan *Jenkins* in het filtervak.</span><span class="sxs-lookup"><span data-stu-id="fb492-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="fb492-149">Selecteer *Jenkins (GitHub-invoegtoepassing)*</span><span class="sxs-lookup"><span data-stu-id="fb492-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="fb492-150">Voor Hallo **Jenkins hook URL**, voer `http://<publicIps>:8080/github-webhook/`.</span><span class="sxs-lookup"><span data-stu-id="fb492-150">For hello **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="fb492-151">Zorg ervoor dat u hallo afsluitende /</span><span class="sxs-lookup"><span data-stu-id="fb492-151">Make sure you include hello trailing /</span></span>
- <span data-ttu-id="fb492-152">Klik op **service toevoegen**</span><span class="sxs-lookup"><span data-stu-id="fb492-152">Click **Add service**</span></span>

![GitHub-repo-webhook tooyour forked toevoegen](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="fb492-154">Jenkins taak maken</span><span class="sxs-lookup"><span data-stu-id="fb492-154">Create Jenkins job</span></span>
<span data-ttu-id="fb492-155">toohave Jenkins reageren tooan gebeurtenis in GitHub zoals het vastleggen van de code wordt een taak Jenkins maken.</span><span class="sxs-lookup"><span data-stu-id="fb492-155">toohave Jenkins respond tooan event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="fb492-156">Klik op in uw website Jenkins **nieuwe taken maken** vanaf de startpagina Hallo:</span><span class="sxs-lookup"><span data-stu-id="fb492-156">In your Jenkins website, click **Create new jobs** from hello home page:</span></span>

- <span data-ttu-id="fb492-157">Voer *HelloWorld* als de taaknaam van de.</span><span class="sxs-lookup"><span data-stu-id="fb492-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="fb492-158">Kies **Freestyle project**, selecteer daarna **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb492-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="fb492-159">Onder Hallo **algemene** sectie **GitHub** project en voer uw Gevorkte repo-URL, zoals *https://github.com/iainfoulds/nodejs-docs-hello-world*</span><span class="sxs-lookup"><span data-stu-id="fb492-159">Under hello **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="fb492-160">Onder Hallo **Source code management** sectie **Git**, Voer uw Gevorkte opslagplaats *.git* -URL, zoals *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span><span class="sxs-lookup"><span data-stu-id="fb492-160">Under hello **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="fb492-161">Onder Hallo **bouwen Triggers** sectie **GitHub haakje trigger voor GITscm polling**.</span><span class="sxs-lookup"><span data-stu-id="fb492-161">Under hello **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="fb492-162">Onder Hallo **bouwen** sectie **toevoegen build stap**.</span><span class="sxs-lookup"><span data-stu-id="fb492-162">Under hello **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="fb492-163">Selecteer **shell uitvoeren**, voer dan `echo "Testing"` toocommand-venster.</span><span class="sxs-lookup"><span data-stu-id="fb492-163">Select **Execute shell**, then enter `echo "Testing"` in toocommand window.</span></span>
- <span data-ttu-id="fb492-164">Klik op **opslaan** aan Hallo onderkant van het venster taken Hallo.</span><span class="sxs-lookup"><span data-stu-id="fb492-164">Click **Save** at hello bottom of hello jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="fb492-165">Integratie van GitHub testen</span><span class="sxs-lookup"><span data-stu-id="fb492-165">Test GitHub integration</span></span>
<span data-ttu-id="fb492-166">tootest hello GitHub-integratie met Jenkins, een wijziging in uw fork doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="fb492-166">tootest hello GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="fb492-167">Terug in de GitHub-webgebruikersinterface, selecteer uw Gevorkte opslagplaats en klik vervolgens op Hallo **index.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="fb492-167">Back in GitHub web UI, select your forked repo, and then click hello **index.js** file.</span></span> <span data-ttu-id="fb492-168">Klik op Hallo pen pictogram tooedit dit bestand zodat de regel 6 leest:</span><span class="sxs-lookup"><span data-stu-id="fb492-168">Click hello pencil icon tooedit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="fb492-169">toocommit uw wijzigingen, klikt u op Hallo **wijzigingen doorvoeren** knop Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="fb492-169">toocommit your changes, click hello **Commit changes** button at hello bottom.</span></span>

<span data-ttu-id="fb492-170">Een nieuwe build begint in Jenkins, onder Hallo **bouwen geschiedenis** sectie van de linkerbenedenhoek van de pagina van de taak Hallo.</span><span class="sxs-lookup"><span data-stu-id="fb492-170">In Jenkins, a new build starts under hello **Build history** section of hello bottom left-hand corner of your job page.</span></span> <span data-ttu-id="fb492-171">Klik op de koppeling van Hallo build en selecteer **Console uitvoer** op Hallo links grootte.</span><span class="sxs-lookup"><span data-stu-id="fb492-171">Click hello build number link and select **Console output** on hello left-hand size.</span></span> <span data-ttu-id="fb492-172">U kunt bekijken Hallo stappen Jenkins wordt als uw code wordt opgehaald uit GitHub en Hallo build actie uitvoer Hallo-bericht `Testing` toohello-console.</span><span class="sxs-lookup"><span data-stu-id="fb492-172">You can view hello steps Jenkins takes as your code is pulled from GitHub and hello build action outputs hello message `Testing` toohello console.</span></span> <span data-ttu-id="fb492-173">Telkens wanneer een doorvoer wordt gedaan in GitHub webhook hello tooJenkins gezocht en activeren van een nieuwe build op deze manier.</span><span class="sxs-lookup"><span data-stu-id="fb492-173">Each time a commit is made in GitHub, hello webhook reaches out tooJenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="fb492-174">Afbeelding van Docker-build definiëren</span><span class="sxs-lookup"><span data-stu-id="fb492-174">Define Docker build image</span></span>
<span data-ttu-id="fb492-175">toosee hello Node.js-app uitgevoerd op basis van uw GitHub-doorvoeracties kunt bouwen van een Docker-afbeelding toorun Hallo app.</span><span class="sxs-lookup"><span data-stu-id="fb492-175">toosee hello Node.js app running based on your GitHub commits, lets build a Docker image toorun hello app.</span></span> <span data-ttu-id="fb492-176">Hallo-installatiekopie wordt gemaakt van een Dockerfile die definieert hoe tooconfigure Hallo-container die Hallo app uitvoert.</span><span class="sxs-lookup"><span data-stu-id="fb492-176">hello image is built from a Dockerfile that defines how tooconfigure hello container that runs hello app.</span></span> 

<span data-ttu-id="fb492-177">Wijzigen van Hallo SSH-verbinding tooyour VM toohello Jenkins werkruimte map na Hallo-taak die u in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fb492-177">From hello SSH connection tooyour VM, change toohello Jenkins workspace directory named after hello job you created in a previous step.</span></span> <span data-ttu-id="fb492-178">In ons voorbeeld die heette *HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="fb492-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="fb492-179">Maken van een bestand met de in deze map werkruimte met `sudo sensible-editor Dockerfile` en inhoud te plakken Hallo volgen.</span><span class="sxs-lookup"><span data-stu-id="fb492-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste hello following contents.</span></span> <span data-ttu-id="fb492-180">Zorg ervoor dat Hallo die hele Dockerfile is correct, met name Hallo eerste regel gekopieerd:</span><span class="sxs-lookup"><span data-stu-id="fb492-180">Make sure that hello whole Dockerfile is copied correctly, especially hello first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="fb492-181">Deze Dockerfile gebruikt Hallo Node.js basisinstallatiekopie gebruik Alpine Linux, zichtbaar gemaakt poort 1337 die app Hallo wereld Hallo wordt uitgevoerd op, en vervolgens kopieert Hallo app-bestanden en geïnitialiseerd met behulp van.</span><span class="sxs-lookup"><span data-stu-id="fb492-181">This Dockerfile uses hello base Node.js image using Alpine Linux, exposes port 1337 that hello Hello World app runs on, then copies hello app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="fb492-182">Jenkins build regels maken</span><span class="sxs-lookup"><span data-stu-id="fb492-182">Create Jenkins build rules</span></span>
<span data-ttu-id="fb492-183">In de vorige stap, moet u een basic Jenkins build regel die een bericht toohello console uitvoeren gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fb492-183">In a previous step, you created a basic Jenkins build rule that output a message toohello console.</span></span> <span data-ttu-id="fb492-184">Hiermee kunt Hallo build stap toouse onze Dockerfile maken en uitvoeren van Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="fb492-184">Lets create hello build step toouse our Dockerfile and run hello app.</span></span>

<span data-ttu-id="fb492-185">Selecteer terug in uw exemplaar Jenkins Hallo-taak die u in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fb492-185">Back in your Jenkins instance, select hello job you created in a previous step.</span></span> <span data-ttu-id="fb492-186">Klik op **configureren** op Hallo linkerkant en schuif omlaag toohello **bouwen** sectie:</span><span class="sxs-lookup"><span data-stu-id="fb492-186">Click **Configure** on hello left-hand side and scroll down toohello **Build** section:</span></span>

- <span data-ttu-id="fb492-187">Verwijder de bestaande `echo "Test"` stap bouwen.</span><span class="sxs-lookup"><span data-stu-id="fb492-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="fb492-188">Klik op Hallo rode kruislings op Hallo rechterbovenhoek van Hallo bestaande build stap box.</span><span class="sxs-lookup"><span data-stu-id="fb492-188">Click hello red cross on hello top right-hand corner of hello existing build step box.</span></span>
- <span data-ttu-id="fb492-189">Klik op **toevoegen build stap**, selecteer daarna **shell uitvoeren**</span><span class="sxs-lookup"><span data-stu-id="fb492-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="fb492-190">In Hallo **opdracht** vak, Voer Hallo Docker-opdrachten te volgen en selecteer **opslaan**:</span><span class="sxs-lookup"><span data-stu-id="fb492-190">In hello **Command** box, enter hello following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="fb492-191">Hallo Docker build stappen maakt een installatiekopie en de tag met Hallo Jenkins build-nummer zodat u kunt een geschiedenis van installatiekopieën onderhouden.</span><span class="sxs-lookup"><span data-stu-id="fb492-191">hello Docker build steps create an image and tag it with hello Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="fb492-192">Eventuele bestaande containers Hallo app uitgevoerd worden gestopt en verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fb492-192">Any existing containers running hello app are stopped and then removed.</span></span> <span data-ttu-id="fb492-193">Een nieuwe container wordt gestart met behulp van de installatiekopie Hallo en voert u uw Node.js-app op basis van de meest recente doorvoeracties Hallo in GitHub.</span><span class="sxs-lookup"><span data-stu-id="fb492-193">A new container is then started using hello image and runs your Node.js app based on hello latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="fb492-194">Test uw pijplijn</span><span class="sxs-lookup"><span data-stu-id="fb492-194">Test your pipeline</span></span>
<span data-ttu-id="fb492-195">toosee hello hele pijplijn in actie bewerken Hallo *index.js* bestand in uw GitHub-repo-Gevorkte opnieuw en klik op **wijziging doorvoeren**.</span><span class="sxs-lookup"><span data-stu-id="fb492-195">toosee hello whole pipeline in action, edit hello *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="fb492-196">Een nieuwe taak wordt gestart met Jenkins op basis van de webhook Hallo voor GitHub.</span><span class="sxs-lookup"><span data-stu-id="fb492-196">A new job starts in Jenkins based on hello webhook for GitHub.</span></span> <span data-ttu-id="fb492-197">Het duurt enkele seconden toocreate hello Docker installatiekopie en uw app te starten in een nieuwe container.</span><span class="sxs-lookup"><span data-stu-id="fb492-197">It takes a few seconds toocreate hello Docker image and start your app in a new container.</span></span>

<span data-ttu-id="fb492-198">Indien nodig, opnieuw Hallo openbare IP-adres van uw virtuele machine verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="fb492-198">If needed, obtain hello public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="fb492-199">Open een webbrowser en voer `http://<publicIps>:1337`.</span><span class="sxs-lookup"><span data-stu-id="fb492-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="fb492-200">Uw Node.js-app wordt weergegeven en reflecteert de meest recente doorvoeracties Hallo in uw GitHub-fork als volgt:</span><span class="sxs-lookup"><span data-stu-id="fb492-200">Your Node.js app is displayed and reflects hello latest commits in your GitHub fork as follows:</span></span>

![Actieve Node.js-app](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="fb492-202">Maak nu een andere bewerken toohello *index.js* bestand in GitHub en doorvoeren Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fb492-202">Now make another edit toohello *index.js* file in GitHub and commit hello change.</span></span> <span data-ttu-id="fb492-203">Wacht een paar seconden voor Hallo taak toocomplete in Jenkins en vernieuw vervolgens uw web browser toosee Hallo bijgewerkt versie van uw app uitgevoerd in een nieuwe container als volgt:</span><span class="sxs-lookup"><span data-stu-id="fb492-203">Wait a few seconds for hello job toocomplete in Jenkins, then refresh your web browser toosee hello updated version of your app running in a new container as follows:</span></span>

![Node.js-app uitgevoerd na een ander GitHub doorvoeren](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="fb492-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fb492-205">Next steps</span></span>
<span data-ttu-id="fb492-206">In deze zelfstudie GitHub toorun een taak van de build Jenkins geconfigureerd op elke doorvoer code en vervolgens uw app implementeert een Docker-container tootest.</span><span class="sxs-lookup"><span data-stu-id="fb492-206">In this tutorial, you configured GitHub toorun a Jenkins build job on each code commit and then deploy a Docker container tootest your app.</span></span> <span data-ttu-id="fb492-207">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="fb492-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fb492-208">Maak een VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="fb492-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="fb492-209">Installeren en configureren van Jenkins</span><span class="sxs-lookup"><span data-stu-id="fb492-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="fb492-210">Webhook-integratie tussen GitHub en Jenkins maken</span><span class="sxs-lookup"><span data-stu-id="fb492-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="fb492-211">Maken en activeren Jenkins build taken van GitHub doorvoeringen</span><span class="sxs-lookup"><span data-stu-id="fb492-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="fb492-212">Een Docker-installatiekopie voor uw app maken</span><span class="sxs-lookup"><span data-stu-id="fb492-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="fb492-213">Controleer of de GitHub-doorvoeracties bouwen nieuwe Docker-installatiekopie en app-updates</span><span class="sxs-lookup"><span data-stu-id="fb492-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="fb492-214">Gaan de volgende zelfstudie toolearn toohello meer informatie over hoe toointegrate Jenkins met Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="fb492-214">Advance toohello next tutorial toolearn more about how toointegrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fb492-215">Apps implementeren met Jenkins en teamservices</span><span class="sxs-lookup"><span data-stu-id="fb492-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)