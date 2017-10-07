---
title: aaaJenkins CI/CD met Kubernetes in Azure Container Service | Microsoft Docs
description: Het tooautomate een CI/CD-proces met Jenkins toodeploy en een beperkte app op Kubernetes in Azure Container Service-upgrade
services: container-service
documentationcenter: 
author: chzbrgr71
manager: johny
editor: 
tags: acs, azure-container-service, jenkins
keywords: Docker, Containers, Kubernetes, Azure, Jenkins
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: briar
ms.custom: mvc
ms.openlocfilehash: e00e13bf06619bed73e82878777e55458ea3dd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="740cf-104">Jenkins integratie met Azure Container Service en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="740cf-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="740cf-105">In deze zelfstudie doorlopen we Hallo proces tooset van continue integratie van een toepassing met meerdere container in Azure Container Service Kubernetes met Hallo Jenkins-platform.</span><span class="sxs-lookup"><span data-stu-id="740cf-105">In this tutorial, we walk through hello process tooset up continuous integration of a multi-container application into Azure Container Service Kubernetes using hello Jenkins platform.</span></span> <span data-ttu-id="740cf-106">Hallo werkstroom Hallo de installatiekopie van de container in Docker-Hub updates en upgrades van Hallo Kubernetes gehele product met behulp van de implementatie van een implementatie.</span><span class="sxs-lookup"><span data-stu-id="740cf-106">hello workflow updates hello container image in Docker Hub and upgrades hello Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="740cf-107">Proces van hoog niveau</span><span class="sxs-lookup"><span data-stu-id="740cf-107">High level process</span></span>
<span data-ttu-id="740cf-108">Hallo eenvoudige stappen in dit artikel wordt beschreven, zijn:</span><span class="sxs-lookup"><span data-stu-id="740cf-108">hello basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="740cf-109">Een cluster Kubernetes in Container Service installeren</span><span class="sxs-lookup"><span data-stu-id="740cf-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="740cf-110">Jenkins instellen en configureren van access tooContainer Service</span><span class="sxs-lookup"><span data-stu-id="740cf-110">Set up Jenkins and configure access tooContainer Service</span></span>
- <span data-ttu-id="740cf-111">Een werkstroom Jenkins maken</span><span class="sxs-lookup"><span data-stu-id="740cf-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="740cf-112">Hallo CI/CD proces end tooend testen</span><span class="sxs-lookup"><span data-stu-id="740cf-112">Test hello CI/CD process end tooend</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="740cf-113">Een cluster Kubernetes installeren</span><span class="sxs-lookup"><span data-stu-id="740cf-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="740cf-114">Hallo Kubernetes cluster in Azure Container Service met behulp van de volgende stappen uit Hallo implementeren.</span><span class="sxs-lookup"><span data-stu-id="740cf-114">Deploy hello Kubernetes cluster in Azure Container Service using hello following steps.</span></span> <span data-ttu-id="740cf-115">Volledige documentatie bevindt [hier](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="740cf-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="740cf-116">Stap 1: Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="740cf-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a><span data-ttu-id="740cf-117">Stap 2: Hallo-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="740cf-117">Step 2: Deploy hello cluster</span></span>
> [!NOTE]
> <span data-ttu-id="740cf-118">Hallo moet volgende stappen een lokale openbare SSH-sleutel met de opgeslagen in Hallo ~/.ssh map.</span><span class="sxs-lookup"><span data-stu-id="740cf-118">hello following steps require a local SSH public key stored in hello ~/.ssh folder.</span></span>
>

```azurecli
RESOURCE_GROUP=my-resource-group
DNS_PREFIX=some-unique-value
CLUSTER_NAME=any-acs-cluster-name

az acs create \
--orchestrator-type=kubernetes \
--resource-group $RESOURCE_GROUP \
--name=$CLUSTER_NAME \
--dns-prefix=$DNS_PREFIX \
--ssh-key-value ~/.ssh/id_rsa.pub \
--admin-username=azureuser \
--master-count=1 \
--agent-count=5 \
--agent-vm-size=Standard_D1_v2
```

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a><span data-ttu-id="740cf-119">Jenkins instellen en configureren van access tooContainer Service</span><span class="sxs-lookup"><span data-stu-id="740cf-119">Set up Jenkins and configure access tooContainer Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="740cf-120">Stap 1: Jenkins installeren</span><span class="sxs-lookup"><span data-stu-id="740cf-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="740cf-121">Een virtuele machine in Azure maken met Ubuntu 16.04 TNS.</span><span class="sxs-lookup"><span data-stu-id="740cf-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="740cf-122">Aangezien verderop in Hallo stappen wordt moet tooconnect toothis VM gebruik bash op uw lokale computer, set Hallo 'Verificatietype' too'SSH openbare sleutel ' en plakken Hallo openbare SSH-sleutel die lokaal wordt opgeslagen in de map ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="740cf-122">Since later in hello steps you will need tooconnect toothis VM using bash on your local machine, set hello 'Authentication type' too'SSH public key' and paste hello SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="740cf-123">Bovendien Noteer van Hallo 'Gebruikersnaam', dat u opgeeft omdat deze gebruikersnaam benodigde tooview hello Jenkins dashboard en voor het verbinden van toohello Jenkins VM in latere stappen.</span><span class="sxs-lookup"><span data-stu-id="740cf-123">Also, take note of hello 'User name' that you specify since this user name will be needed tooview hello Jenkins dashboard and for connecting toohello Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="740cf-124">Jenkins installeren via deze [instructies](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="740cf-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="740cf-125">Een zelfstudie voor meer gedetailleerde loopt [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span><span class="sxs-lookup"><span data-stu-id="740cf-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="740cf-126">tooview Hallo Jenkins dashboard op uw lokale computer, hello Azure network security groep tooallow poort 8080 bijwerken door een inkomende regel waarmee toegang tooport 8080 toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="740cf-126">tooview hello Jenkins dashboard on your local machine, update hello Azure network security group tooallow port 8080 by adding an inbound rule that allows access tooport 8080.</span></span>  <span data-ttu-id="740cf-127">U mogelijk ook poort doorsturen instellen door deze opdracht uit te voeren:`ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span><span class="sxs-lookup"><span data-stu-id="740cf-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="740cf-128">Verbind tooyour Jenkins server met behulp van de browser Hallo door te navigeren toohello openbare IP-adres (http:// < your_jenkins_public_ip >: 8080) en het ontgrendelen van Hallo Jenkins dashboard voor Hallo eerst met de initiële beheerderswachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="740cf-128">Connect tooyour Jenkins server using hello browser by navigating toohello public IP (http://<your_jenkins_public_ip>:8080) and unlock hello Jenkins dashboard for hello first time with hello initial admin password.</span></span>  <span data-ttu-id="740cf-129">Hallo beheerderswachtwoord wordt opgeslagen op /var/lib/jenkins/secrets/initialAdminPassword op Hallo Jenkins VM.</span><span class="sxs-lookup"><span data-stu-id="740cf-129">hello admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on hello Jenkins VM.</span></span>  <span data-ttu-id="740cf-130">Een eenvoudige manier tooget dit wachtwoord wordt tooSSH in Hallo Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="740cf-130">An easy way tooget this password is tooSSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="740cf-131">Voer vervolgens: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span><span class="sxs-lookup"><span data-stu-id="740cf-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="740cf-132">Installeer de Docker op Hallo Jenkins machine via deze [instructies](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span><span class="sxs-lookup"><span data-stu-id="740cf-132">Install Docker on hello Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="740cf-133">Hierdoor Docker opdrachten toobe in Jenkins taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="740cf-133">This allows for Docker commands toobe run in Jenkins jobs.</span></span>
6. <span data-ttu-id="740cf-134">Docker machtigingen tooallow Jenkins tooaccess hello Docker-eindpunt configureren.</span><span class="sxs-lookup"><span data-stu-id="740cf-134">Configure Docker permissions tooallow Jenkins tooaccess hello Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="740cf-135">Installeer `kubectl` CLI op Jenkins.</span><span class="sxs-lookup"><span data-stu-id="740cf-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="740cf-136">Meer informatie vindt u op [installeren en instellen van kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="740cf-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="740cf-137">Jenkins taken 'kubectl' toomanage gebruikt en toohello Kubernetes-cluster implementeren.</span><span class="sxs-lookup"><span data-stu-id="740cf-137">Jenkins jobs will use 'kubectl' toomanage and deploy toohello Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a><span data-ttu-id="740cf-138">Stap 2: Toegang toohello Kubernetes cluster instellen</span><span class="sxs-lookup"><span data-stu-id="740cf-138">Step 2: Set up access toohello Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="740cf-139">Er zijn meerdere manieren tooaccomplishing Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="740cf-139">There are multiple approaches tooaccomplishing hello following steps.</span></span> <span data-ttu-id="740cf-140">Hallo-benadering die voor u het gemakkelijkst gebruiken.</span><span class="sxs-lookup"><span data-stu-id="740cf-140">Use hello approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="740cf-141">Kopiëren Hallo `kubectl` config bestand toohello Jenkins machine zodat Jenkins taken toegang tot toohello Kubernetes cluster hebben.</span><span class="sxs-lookup"><span data-stu-id="740cf-141">Copy hello `kubectl` config file toohello Jenkins machine so that Jenkins jobs have access toohello Kubernetes cluster.</span></span> <span data-ttu-id="740cf-142">Deze instructies wordt ervan uitgegaan dat u van bash van een andere computer gebruikmaakt dan Jenkins VM Hallo en dat een lokale openbare SSH-sleutel in van de machine Hallo ~/.ssh map is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="740cf-142">These instructions assume that you are using bash from a different machine than hello Jenkins VM and that a local SSH public key is stored in hello machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="740cf-143">Valideren van Jenkins die Hallo Kubernetes cluster toegankelijk is.</span><span class="sxs-lookup"><span data-stu-id="740cf-143">Validate from Jenkins that hello Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="740cf-144">toodo deze, SSH in Hallo Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="740cf-144">toodo this, SSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="740cf-145">Controleer vervolgens of Jenkins verbinding kan maken tooyour cluster: `kubectl cluster-info`.</span><span class="sxs-lookup"><span data-stu-id="740cf-145">Next, verify Jenkins can successfully connect tooyour cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="740cf-146">Een werkstroom Jenkins maken</span><span class="sxs-lookup"><span data-stu-id="740cf-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="740cf-147">Vereisten</span><span class="sxs-lookup"><span data-stu-id="740cf-147">Prerequisites</span></span>

- <span data-ttu-id="740cf-148">GitHub-account voor code-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="740cf-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="740cf-149">Docker Hub account toostore en update-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="740cf-149">Docker Hub account toostore and update images.</span></span>
- <span data-ttu-id="740cf-150">Beperkte toepassing die kan worden opnieuw opgebouwd en bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="740cf-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="740cf-151">U kunt deze container voorbeeldapp geschreven in Golang: https://github.com/chzbrgr71/go-web</span><span class="sxs-lookup"><span data-stu-id="740cf-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="740cf-152">Hallo volgende stappen moeten worden uitgevoerd in uw eigen GitHub-account.</span><span class="sxs-lookup"><span data-stu-id="740cf-152">hello following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="740cf-153">Kunt u gratis tooclone Hallo hierboven opslagplaats, maar moet u uw eigen account tooconfigure hello webhooks en Jenkins toegang.</span><span class="sxs-lookup"><span data-stu-id="740cf-153">Feel free tooclone hello above repo, but you must use your own account tooconfigure hello webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="740cf-154">Stap 1: Initiële v1 van toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="740cf-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="740cf-155">Hallo app van Hallo developer-machine maken met de volgende opdrachten Hallo.</span><span class="sxs-lookup"><span data-stu-id="740cf-155">Build hello app from hello developer machine with hello following commands.</span></span> <span data-ttu-id="740cf-156">Vervang `myrepo` door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="740cf-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="740cf-157">TooDocker push Hub.</span><span class="sxs-lookup"><span data-stu-id="740cf-157">Push image tooDocker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="740cf-158">Toohello Kubernetes cluster implementeren.</span><span class="sxs-lookup"><span data-stu-id="740cf-158">Deploy toohello Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="740cf-159">Hallo bewerken `go-web.yaml` tooupdate bestand uw installatiekopie van de container en de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="740cf-159">Edit hello `go-web.yaml` file tooupdate your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="740cf-160">Stap 2: Jenkins systeem configureren</span><span class="sxs-lookup"><span data-stu-id="740cf-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="740cf-161">Klik op **beheren Jenkins** > **systeem configureren**.</span><span class="sxs-lookup"><span data-stu-id="740cf-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="740cf-162">Onder **GitHub**, selecteer **GitHub-Server toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="740cf-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="740cf-163">Laat **URL van de API** als standaard.</span><span class="sxs-lookup"><span data-stu-id="740cf-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="740cf-164">Onder **referenties**, Voeg een Jenkins referentie met **geheime tekst**.</span><span class="sxs-lookup"><span data-stu-id="740cf-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="740cf-165">U wordt aangeraden met GitHub persoonlijke toegangstokens, die zijn geconfigureerd in de instellingen van uw GitHub-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="740cf-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="740cf-166">Meer informatie over dit [hier.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span><span class="sxs-lookup"><span data-stu-id="740cf-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="740cf-167">Klik op **verbinding testen** tooensure dit correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="740cf-167">Click **Test connection** tooensure this is configured correctly.</span></span>
6. <span data-ttu-id="740cf-168">Onder **algemene eigenschappen**, voegt u een omgevingsvariabele `DOCKER_HUB` en geef uw wachtwoord Docker-Hub.</span><span class="sxs-lookup"><span data-stu-id="740cf-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="740cf-169">(Dit is handig in deze demonstratie, maar een productiescenario vereist een veiliger benadering.)</span><span class="sxs-lookup"><span data-stu-id="740cf-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="740cf-170">Opslaan.</span><span class="sxs-lookup"><span data-stu-id="740cf-170">Save.</span></span>

![Jenkins GitHub-toegang](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a><span data-ttu-id="740cf-172">Stap 3: Hallo Jenkins werkstroom maken</span><span class="sxs-lookup"><span data-stu-id="740cf-172">Step 3: Create hello Jenkins workflow</span></span>
1. <span data-ttu-id="740cf-173">Een item Jenkins maken.</span><span class="sxs-lookup"><span data-stu-id="740cf-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="740cf-174">Geef een naam (bijvoorbeeld 'Ga web') en selecteer **Freestyle Project**.</span><span class="sxs-lookup"><span data-stu-id="740cf-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="740cf-175">Controleer **GitHub project** en geef de GitHub-repo-Hallo URL tooyour.</span><span class="sxs-lookup"><span data-stu-id="740cf-175">Check **GitHub project** and provide hello URL tooyour GitHub repo.</span></span>
4. <span data-ttu-id="740cf-176">In **beheer van gegevensbronnen Code**, Hallo GitHub-repo-URL en referenties opgeven.</span><span class="sxs-lookup"><span data-stu-id="740cf-176">In **Source Code Management**, provide hello GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="740cf-177">Voeg een **bouwen stap** van het type **shell uitvoeren** en Hallo gebruik de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="740cf-177">Add a **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="740cf-178">Toevoegen van een andere **bouwen stap** van het type **shell uitvoeren** en Hallo gebruik de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="740cf-178">Add another **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Jenkins bouwen stappen](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="740cf-180">Hallo Jenkins item opslaan en testen met **nu bouwen**.</span><span class="sxs-lookup"><span data-stu-id="740cf-180">Save hello Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="740cf-181">Stap 4: Verbinding maken met GitHub webhook</span><span class="sxs-lookup"><span data-stu-id="740cf-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="740cf-182">In Hallo Jenkins item dat u hebt gemaakt, klikt u op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="740cf-182">In hello Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="740cf-183">Onder **bouwen Triggers**, selecteer **GitHub haakje trigger voor polling GITScm** en **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="740cf-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="740cf-184">Hiermee Hallo GitHub webhook automatisch geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="740cf-184">This automatically configures hello GitHub webhook.</span></span>
3. <span data-ttu-id="740cf-185">Klik in uw GitHub-repo voor Ga-webtoepassingen op **instellingen > Webhooks**.</span><span class="sxs-lookup"><span data-stu-id="740cf-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="740cf-186">Controleer of deze Hallo Jenkins webhook-URL met succes is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="740cf-186">Verify that hello Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="740cf-187">Hallo-URL moet eindigen op 'github webhook'.</span><span class="sxs-lookup"><span data-stu-id="740cf-187">hello URL should end in "github-webhook".</span></span>

![Configuratie van de webhook Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a><span data-ttu-id="740cf-189">Hallo CI/CD proces end tooend testen</span><span class="sxs-lookup"><span data-stu-id="740cf-189">Test hello CI/CD process end tooend</span></span>

1. <span data-ttu-id="740cf-190">Code voor het Hallo-opslagplaats en push/synch bijwerken met Hallo GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="740cf-190">Update code for hello repo and push/synch with hello GitHub repository.</span></span>
2. <span data-ttu-id="740cf-191">Hallo Jenkins-console controleren Hallo **bouwen geschiedenis** en valideren die Hallo taak heeft uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="740cf-191">From hello Jenkins console, check hello **Build History** and validate that hello job has run.</span></span> <span data-ttu-id="740cf-192">Details voor toosee weergeven console-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="740cf-192">View console output toosee details.</span></span>
3. <span data-ttu-id="740cf-193">Details weergeven van Hallo bijgewerkt van Kubernetes, implementatie:</span><span class="sxs-lookup"><span data-stu-id="740cf-193">From Kubernetes, view details of hello upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="740cf-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="740cf-194">Next steps</span></span>

- <span data-ttu-id="740cf-195">Azure Container register implementeren en afbeeldingen in een veilige locatie opslaan.</span><span class="sxs-lookup"><span data-stu-id="740cf-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="740cf-196">Zie [Azure Container register docs](https://docs.microsoft.com/azure/container-registry).</span><span class="sxs-lookup"><span data-stu-id="740cf-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="740cf-197">Bouw een complexe workflow met side-by-side-implementatie en automatische tests in Jenkins.</span><span class="sxs-lookup"><span data-stu-id="740cf-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="740cf-198">Zie voor meer informatie over CI/CD met Jenkins en Kubernetes hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span><span class="sxs-lookup"><span data-stu-id="740cf-198">For more information about CI/CD with Jenkins and Kubernetes, see hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>
