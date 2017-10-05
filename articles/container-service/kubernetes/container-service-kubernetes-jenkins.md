---
title: Jenkins CI/CD met Kubernetes in Azure Containerservice | Microsoft Docs
description: Hoe u een CI/CD automatiseren met Jenkins te implementeren en een beperkte app op Kubernetes in Azure Container Service bijwerken
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
ms.openlocfilehash: 2078d0694fc4dd6e83ecd2792588b4254980cd78
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="d4645-104">Jenkins integratie met Azure Container Service en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d4645-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="d4645-105">In deze zelfstudie wordt het proces voor het instellen van continue integratie van een toepassing met meerdere container in Azure Container Service Kubernetes met behulp van het platform Jenkins doorlopen.</span><span class="sxs-lookup"><span data-stu-id="d4645-105">In this tutorial, we walk through the process to set up continuous integration of a multi-container application into Azure Container Service Kubernetes using the Jenkins platform.</span></span> <span data-ttu-id="d4645-106">De werkstroom de installatiekopie van de container in Docker-Hub updates en upgrades van het gehele Kubernetes product met behulp van de implementatie van een implementatie.</span><span class="sxs-lookup"><span data-stu-id="d4645-106">The workflow updates the container image in Docker Hub and upgrades the Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="d4645-107">Proces van hoog niveau</span><span class="sxs-lookup"><span data-stu-id="d4645-107">High level process</span></span>
<span data-ttu-id="d4645-108">De eenvoudige stappen in dit artikel wordt beschreven, zijn:</span><span class="sxs-lookup"><span data-stu-id="d4645-108">The basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="d4645-109">Een cluster Kubernetes in Container Service installeren</span><span class="sxs-lookup"><span data-stu-id="d4645-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="d4645-110">Jenkins instellen en configureren van toegang tot de Container Service</span><span class="sxs-lookup"><span data-stu-id="d4645-110">Set up Jenkins and configure access to Container Service</span></span>
- <span data-ttu-id="d4645-111">Een werkstroom Jenkins maken</span><span class="sxs-lookup"><span data-stu-id="d4645-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="d4645-112">Het proces CI/CD complete testen</span><span class="sxs-lookup"><span data-stu-id="d4645-112">Test the CI/CD process end to end</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="d4645-113">Een cluster Kubernetes installeren</span><span class="sxs-lookup"><span data-stu-id="d4645-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="d4645-114">Implementeer het Kubernetes-cluster in Azure Container Service met de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="d4645-114">Deploy the Kubernetes cluster in Azure Container Service using the following steps.</span></span> <span data-ttu-id="d4645-115">Volledige documentatie bevindt [hier](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="d4645-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="d4645-116">Stap 1: Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="d4645-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-the-cluster"></a><span data-ttu-id="d4645-117">Stap 2: Implementeer het cluster</span><span class="sxs-lookup"><span data-stu-id="d4645-117">Step 2: Deploy the cluster</span></span>
> [!NOTE]
> <span data-ttu-id="d4645-118">De volgende stappen moet een lokale openbare SSH-sleutel met de opgeslagen in de map ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="d4645-118">The following steps require a local SSH public key stored in the ~/.ssh folder.</span></span>
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

## <a name="set-up-jenkins-and-configure-access-to-container-service"></a><span data-ttu-id="d4645-119">Jenkins instellen en configureren van toegang tot de Container Service</span><span class="sxs-lookup"><span data-stu-id="d4645-119">Set up Jenkins and configure access to Container Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="d4645-120">Stap 1: Jenkins installeren</span><span class="sxs-lookup"><span data-stu-id="d4645-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="d4645-121">Een virtuele machine in Azure maken met Ubuntu 16.04 TNS.</span><span class="sxs-lookup"><span data-stu-id="d4645-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="d4645-122">Aangezien u verbinding maken met deze virtuele machine met behulp van bash op uw lokale machine later in de stappen wilt, het 'verificatietype' naar 'Openbare SSH-sleutel' ingesteld en de openbare SSH-sleutel die lokaal wordt opgeslagen in de map ~/.ssh plakken.</span><span class="sxs-lookup"><span data-stu-id="d4645-122">Since later in the steps you will need to connect to this VM using bash on your local machine, set the 'Authentication type' to 'SSH public key' and paste the SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="d4645-123">Ook rekening met de gebruikersnaam die u opgeeft, aangezien deze gebruikersnaam nodig om het dashboard Jenkins weer te geven en voor het verbinden met de Jenkins VM in latere stappen.</span><span class="sxs-lookup"><span data-stu-id="d4645-123">Also, take note of the 'User name' that you specify since this user name will be needed to view the Jenkins dashboard and for connecting to the Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="d4645-124">Jenkins installeren via deze [instructies](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="d4645-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="d4645-125">Een zelfstudie voor meer gedetailleerde loopt [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span><span class="sxs-lookup"><span data-stu-id="d4645-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="d4645-126">Bijwerken om weer te geven het dashboard Jenkins op uw lokale computer, de beveiligingsgroep voor de Azure-netwerk dat poort 8080 door een inkomende regel waarmee toegang tot poort 8080 toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="d4645-126">To view the Jenkins dashboard on your local machine, update the Azure network security group to allow port 8080 by adding an inbound rule that allows access to port 8080.</span></span>  <span data-ttu-id="d4645-127">U mogelijk ook poort doorsturen instellen door deze opdracht uit te voeren:`ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span><span class="sxs-lookup"><span data-stu-id="d4645-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="d4645-128">Verbinding maken met uw Jenkins-server met behulp van de browser door te navigeren naar het openbare IP-adres (http:// < your_jenkins_public_ip >: 8080) en het ontgrendelen van het dashboard Jenkins voor de eerste keer met de initiële beheerderswachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d4645-128">Connect to your Jenkins server using the browser by navigating to the public IP (http://<your_jenkins_public_ip>:8080) and unlock the Jenkins dashboard for the first time with the initial admin password.</span></span>  <span data-ttu-id="d4645-129">De Administrator-wachtwoord wordt opgeslagen op /var/lib/jenkins/secrets/initialAdminPassword op de Jenkins VM.</span><span class="sxs-lookup"><span data-stu-id="d4645-129">The admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on the Jenkins VM.</span></span>  <span data-ttu-id="d4645-130">Voeg SSH toe aan de Jenkins VM is een eenvoudige manier om dit wachtwoord te achterhalen: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="d4645-130">An easy way to get this password is to SSH into the Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="d4645-131">Voer vervolgens: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span><span class="sxs-lookup"><span data-stu-id="d4645-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="d4645-132">Docker installeren op de machine Jenkins via deze [instructies](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span><span class="sxs-lookup"><span data-stu-id="d4645-132">Install Docker on the Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="d4645-133">Hierdoor Docker-opdrachten in Jenkins taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d4645-133">This allows for Docker commands to be run in Jenkins jobs.</span></span>
6. <span data-ttu-id="d4645-134">Docker-machtigingen om toe te staan Jenkins voor toegang tot het Docker-eindpunt configureren.</span><span class="sxs-lookup"><span data-stu-id="d4645-134">Configure Docker permissions to allow Jenkins to access the Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="d4645-135">Installeer `kubectl` CLI op Jenkins.</span><span class="sxs-lookup"><span data-stu-id="d4645-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="d4645-136">Meer informatie vindt u op [installeren en instellen van kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="d4645-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="d4645-137">Jenkins taken te beheren en implementeren met het cluster Kubernetes 'kubectl' gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d4645-137">Jenkins jobs will use 'kubectl' to manage and deploy to the Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-to-the-kubernetes-cluster"></a><span data-ttu-id="d4645-138">Stap 2: Toegang tot het cluster Kubernetes instellen</span><span class="sxs-lookup"><span data-stu-id="d4645-138">Step 2: Set up access to the Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="d4645-139">Er zijn meerdere methoden voor het uitvoeren van de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="d4645-139">There are multiple approaches to accomplishing the following steps.</span></span> <span data-ttu-id="d4645-140">Gebruik de methode die voor u.</span><span class="sxs-lookup"><span data-stu-id="d4645-140">Use the approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="d4645-141">Kopieer de `kubectl` config van het bestand in de machine Jenkins zodat Jenkins taken hebben toegang tot het cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="d4645-141">Copy the `kubectl` config file to the Jenkins machine so that Jenkins jobs have access to the Kubernetes cluster.</span></span> <span data-ttu-id="d4645-142">Deze instructies wordt ervan uitgegaan dat u gebruikmaakt van een andere computer dan de Jenkins VM bash en een lokale openbare SSH-sleutel in de machine ~/.ssh map is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d4645-142">These instructions assume that you are using bash from a different machine than the Jenkins VM and that a local SSH public key is stored in the machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="d4645-143">Valideren van Jenkins dat het cluster Kubernetes toegankelijk is.</span><span class="sxs-lookup"><span data-stu-id="d4645-143">Validate from Jenkins that the Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="d4645-144">Om dit te doen, SSH in de VM Jenkins: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="d4645-144">To do this, SSH into the Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="d4645-145">Controleer vervolgens of Jenkins verbinding kan maken met uw cluster: `kubectl cluster-info`.</span><span class="sxs-lookup"><span data-stu-id="d4645-145">Next, verify Jenkins can successfully connect to your cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="d4645-146">Een werkstroom Jenkins maken</span><span class="sxs-lookup"><span data-stu-id="d4645-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d4645-147">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d4645-147">Prerequisites</span></span>

- <span data-ttu-id="d4645-148">GitHub-account voor code-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="d4645-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="d4645-149">Docker Hub account op te slaan en afbeeldingen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d4645-149">Docker Hub account to store and update images.</span></span>
- <span data-ttu-id="d4645-150">Beperkte toepassing die kan worden opnieuw opgebouwd en bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="d4645-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="d4645-151">U kunt deze container voorbeeldapp geschreven in Golang: https://github.com/chzbrgr71/go-web</span><span class="sxs-lookup"><span data-stu-id="d4645-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="d4645-152">De volgende stappen moeten worden uitgevoerd in uw eigen GitHub-account.</span><span class="sxs-lookup"><span data-stu-id="d4645-152">The following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="d4645-153">Kloon de bovenstaande opslagplaats gerust maar moet u uw eigen account gebruiken voor het configureren van de webhooks en Jenkins toegang.</span><span class="sxs-lookup"><span data-stu-id="d4645-153">Feel free to clone the above repo, but you must use your own account to configure the webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="d4645-154">Stap 1: Initiële v1 van toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="d4645-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="d4645-155">Het bouwen van de app uit de developer-machine met de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="d4645-155">Build the app from the developer machine with the following commands.</span></span> <span data-ttu-id="d4645-156">Vervang `myrepo` door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="d4645-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="d4645-157">Push-afbeelding met Docker-Hub.</span><span class="sxs-lookup"><span data-stu-id="d4645-157">Push image to Docker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="d4645-158">Op het cluster Kubernetes implementeren.</span><span class="sxs-lookup"><span data-stu-id="d4645-158">Deploy to the Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="d4645-159">Bewerk de `go-web.yaml` bestand bijwerken van uw installatiekopie van de container en de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="d4645-159">Edit the `go-web.yaml` file to update your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="d4645-160">Stap 2: Jenkins systeem configureren</span><span class="sxs-lookup"><span data-stu-id="d4645-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="d4645-161">Klik op **beheren Jenkins** > **systeem configureren**.</span><span class="sxs-lookup"><span data-stu-id="d4645-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="d4645-162">Onder **GitHub**, selecteer **GitHub-Server toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d4645-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="d4645-163">Laat **URL van de API** als standaard.</span><span class="sxs-lookup"><span data-stu-id="d4645-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="d4645-164">Onder **referenties**, Voeg een Jenkins referentie met **geheime tekst**.</span><span class="sxs-lookup"><span data-stu-id="d4645-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="d4645-165">U wordt aangeraden met GitHub persoonlijke toegangstokens, die zijn geconfigureerd in de instellingen van uw GitHub-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="d4645-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="d4645-166">Meer informatie over dit [hier.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span><span class="sxs-lookup"><span data-stu-id="d4645-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="d4645-167">Klik op **verbinding testen** om te controleren of dit juist is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d4645-167">Click **Test connection** to ensure this is configured correctly.</span></span>
6. <span data-ttu-id="d4645-168">Onder **algemene eigenschappen**, voegt u een omgevingsvariabele `DOCKER_HUB` en geef uw wachtwoord Docker-Hub.</span><span class="sxs-lookup"><span data-stu-id="d4645-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="d4645-169">(Dit is handig in deze demonstratie, maar een productiescenario vereist een veiliger benadering.)</span><span class="sxs-lookup"><span data-stu-id="d4645-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="d4645-170">Opslaan.</span><span class="sxs-lookup"><span data-stu-id="d4645-170">Save.</span></span>

![Jenkins GitHub-toegang](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-the-jenkins-workflow"></a><span data-ttu-id="d4645-172">Stap 3: De werkstroom Jenkins maken</span><span class="sxs-lookup"><span data-stu-id="d4645-172">Step 3: Create the Jenkins workflow</span></span>
1. <span data-ttu-id="d4645-173">Een item Jenkins maken.</span><span class="sxs-lookup"><span data-stu-id="d4645-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="d4645-174">Geef een naam (bijvoorbeeld 'Ga web') en selecteer **Freestyle Project**.</span><span class="sxs-lookup"><span data-stu-id="d4645-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="d4645-175">Controleer **GitHub project** en geef de URL naar uw GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="d4645-175">Check **GitHub project** and provide the URL to your GitHub repo.</span></span>
4. <span data-ttu-id="d4645-176">In **beheer van gegevensbronnen Code**, de GitHub-repo-URL en referenties opgeven.</span><span class="sxs-lookup"><span data-stu-id="d4645-176">In **Source Code Management**, provide the GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="d4645-177">Voeg een **bouwen stap** van het type **shell uitvoeren** en gebruik de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="d4645-177">Add a **Build Step** of type **Execute shell** and use the following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="d4645-178">Toevoegen van een andere **bouwen stap** van het type **shell uitvoeren** en gebruik de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="d4645-178">Add another **Build Step** of type **Execute shell** and use the following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Jenkins bouwen stappen](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="d4645-180">Het item Jenkins opslaan en testen met **nu bouwen**.</span><span class="sxs-lookup"><span data-stu-id="d4645-180">Save the Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="d4645-181">Stap 4: Verbinding maken met GitHub webhook</span><span class="sxs-lookup"><span data-stu-id="d4645-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="d4645-182">Klik in het Jenkins item dat u hebt gemaakt, op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="d4645-182">In the Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="d4645-183">Onder **bouwen Triggers**, selecteer **GitHub haakje trigger voor polling GITScm** en **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d4645-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="d4645-184">Hiermee worden de GitHub webhook automatisch geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d4645-184">This automatically configures the GitHub webhook.</span></span>
3. <span data-ttu-id="d4645-185">Klik in uw GitHub-repo voor Ga-webtoepassingen op **instellingen > Webhooks**.</span><span class="sxs-lookup"><span data-stu-id="d4645-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="d4645-186">Controleer of de Jenkins webhook-URL is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d4645-186">Verify that the Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="d4645-187">De URL moet eindigen op 'github webhook'.</span><span class="sxs-lookup"><span data-stu-id="d4645-187">The URL should end in "github-webhook".</span></span>

![Configuratie van de webhook Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-the-cicd-process-end-to-end"></a><span data-ttu-id="d4645-189">Het proces CI/CD complete testen</span><span class="sxs-lookup"><span data-stu-id="d4645-189">Test the CI/CD process end to end</span></span>

1. <span data-ttu-id="d4645-190">Code voor de opslagplaats en push/synch bijwerken met de GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="d4645-190">Update code for the repo and push/synch with the GitHub repository.</span></span>
2. <span data-ttu-id="d4645-191">Controleer op de console Jenkins de **bouwen geschiedenis** en controleert u of de taak is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d4645-191">From the Jenkins console, check the **Build History** and validate that the job has run.</span></span> <span data-ttu-id="d4645-192">Console-uitvoer weergeven om details te bekijken.</span><span class="sxs-lookup"><span data-stu-id="d4645-192">View console output to see details.</span></span>
3. <span data-ttu-id="d4645-193">Details van de bijgewerkte implementatie Kubernetes, bekijken:</span><span class="sxs-lookup"><span data-stu-id="d4645-193">From Kubernetes, view details of the upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="d4645-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d4645-194">Next steps</span></span>

- <span data-ttu-id="d4645-195">Azure Container register implementeren en afbeeldingen in een veilige locatie opslaan.</span><span class="sxs-lookup"><span data-stu-id="d4645-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="d4645-196">Zie [Azure Container register docs](https://docs.microsoft.com/azure/container-registry).</span><span class="sxs-lookup"><span data-stu-id="d4645-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="d4645-197">Bouw een complexe workflow met side-by-side-implementatie en automatische tests in Jenkins.</span><span class="sxs-lookup"><span data-stu-id="d4645-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="d4645-198">Zie voor meer informatie over CI/CD met Jenkins en Kubernetes de [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span><span class="sxs-lookup"><span data-stu-id="d4645-198">For more information about CI/CD with Jenkins and Kubernetes, see the [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>
