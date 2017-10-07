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
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a>Jenkins integratie met Azure Container Service en Kubernetes 
In deze zelfstudie doorlopen we Hallo proces tooset van continue integratie van een toepassing met meerdere container in Azure Container Service Kubernetes met Hallo Jenkins-platform. Hallo werkstroom Hallo de installatiekopie van de container in Docker-Hub updates en upgrades van Hallo Kubernetes gehele product met behulp van de implementatie van een implementatie. 

## <a name="high-level-process"></a>Proces van hoog niveau
Hallo eenvoudige stappen in dit artikel wordt beschreven, zijn: 
- Een cluster Kubernetes in Container Service installeren
- Jenkins instellen en configureren van access tooContainer Service
- Een werkstroom Jenkins maken
- Hallo CI/CD proces end tooend testen

## <a name="install-a-kubernetes-cluster"></a>Een cluster Kubernetes installeren
    
Hallo Kubernetes cluster in Azure Container Service met behulp van de volgende stappen uit Hallo implementeren. Volledige documentatie bevindt [hier](container-service-kubernetes-walkthrough.md).

### <a name="step-1-create-a-resource-group"></a>Stap 1: Een resourcegroep maken
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a>Stap 2: Hallo-cluster implementeren
> [!NOTE]
> Hallo moet volgende stappen een lokale openbare SSH-sleutel met de opgeslagen in Hallo ~/.ssh map.
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

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a>Jenkins instellen en configureren van access tooContainer Service

### <a name="step-1-install-jenkins"></a>Stap 1: Jenkins installeren
1. Een virtuele machine in Azure maken met Ubuntu 16.04 TNS.  Aangezien verderop in Hallo stappen wordt moet tooconnect toothis VM gebruik bash op uw lokale computer, set Hallo 'Verificatietype' too'SSH openbare sleutel ' en plakken Hallo openbare SSH-sleutel die lokaal wordt opgeslagen in de map ~/.ssh.  Bovendien Noteer van Hallo 'Gebruikersnaam', dat u opgeeft omdat deze gebruikersnaam benodigde tooview hello Jenkins dashboard en voor het verbinden van toohello Jenkins VM in latere stappen.
2. Jenkins installeren via deze [instructies](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu). Een zelfstudie voor meer gedetailleerde loopt [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).
3. tooview Hallo Jenkins dashboard op uw lokale computer, hello Azure network security groep tooallow poort 8080 bijwerken door een inkomende regel waarmee toegang tooport 8080 toe te voegen.  U mogelijk ook poort doorsturen instellen door deze opdracht uit te voeren:`ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`
4. Verbind tooyour Jenkins server met behulp van de browser Hallo door te navigeren toohello openbare IP-adres (http:// < your_jenkins_public_ip >: 8080) en het ontgrendelen van Hallo Jenkins dashboard voor Hallo eerst met de initiële beheerderswachtwoord Hallo.  Hallo beheerderswachtwoord wordt opgeslagen op /var/lib/jenkins/secrets/initialAdminPassword op Hallo Jenkins VM.  Een eenvoudige manier tooget dit wachtwoord wordt tooSSH in Hallo Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  Voer vervolgens: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
5. Installeer de Docker op Hallo Jenkins machine via deze [instructies](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts). Hierdoor Docker opdrachten toobe in Jenkins taken worden uitgevoerd.
6. Docker machtigingen tooallow Jenkins tooaccess hello Docker-eindpunt configureren.

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. Installeer `kubectl` CLI op Jenkins. Meer informatie vindt u op [installeren en instellen van kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).  Jenkins taken 'kubectl' toomanage gebruikt en toohello Kubernetes-cluster implementeren.

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a>Stap 2: Toegang toohello Kubernetes cluster instellen

> [!NOTE]
> Er zijn meerdere manieren tooaccomplishing Hallo stappen te volgen. Hallo-benadering die voor u het gemakkelijkst gebruiken.
>

1. Kopiëren Hallo `kubectl` config bestand toohello Jenkins machine zodat Jenkins taken toegang tot toohello Kubernetes cluster hebben. Deze instructies wordt ervan uitgegaan dat u van bash van een andere computer gebruikmaakt dan Jenkins VM Hallo en dat een lokale openbare SSH-sleutel in van de machine Hallo ~/.ssh map is opgeslagen.

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. Valideren van Jenkins die Hallo Kubernetes cluster toegankelijk is.  toodo deze, SSH in Hallo Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  Controleer vervolgens of Jenkins verbinding kan maken tooyour cluster: `kubectl cluster-info`.
    

## <a name="create-a-jenkins-workflow"></a>Een werkstroom Jenkins maken

### <a name="prerequisites"></a>Vereisten

- GitHub-account voor code-opslagplaats.
- Docker Hub account toostore en update-installatiekopieën.
- Beperkte toepassing die kan worden opnieuw opgebouwd en bijgewerkt. U kunt deze container voorbeeldapp geschreven in Golang: https://github.com/chzbrgr71/go-web 

> [!NOTE]
> Hallo volgende stappen moeten worden uitgevoerd in uw eigen GitHub-account. Kunt u gratis tooclone Hallo hierboven opslagplaats, maar moet u uw eigen account tooconfigure hello webhooks en Jenkins toegang.
>

### <a name="step-1-deploy-initial-v1-of-application"></a>Stap 1: Initiële v1 van toepassing implementeren
1. Hallo app van Hallo developer-machine maken met de volgende opdrachten Hallo. Vervang `myrepo` door uw eigen.
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. TooDocker push Hub.

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. Toohello Kubernetes cluster implementeren.
    
    > [!NOTE] 
    > Hallo bewerken `go-web.yaml` tooupdate bestand uw installatiekopie van de container en de opslagplaats.
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a>Stap 2: Jenkins systeem configureren
1. Klik op **beheren Jenkins** > **systeem configureren**.
2. Onder **GitHub**, selecteer **GitHub-Server toevoegen**.
3. Laat **URL van de API** als standaard.
4. Onder **referenties**, Voeg een Jenkins referentie met **geheime tekst**. U wordt aangeraden met GitHub persoonlijke toegangstokens, die zijn geconfigureerd in de instellingen van uw GitHub-gebruikersaccount. Meer informatie over dit [hier.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)
5. Klik op **verbinding testen** tooensure dit correct is geconfigureerd.
6. Onder **algemene eigenschappen**, voegt u een omgevingsvariabele `DOCKER_HUB` en geef uw wachtwoord Docker-Hub. (Dit is handig in deze demonstratie, maar een productiescenario vereist een veiliger benadering.)
7. Opslaan.

![Jenkins GitHub-toegang](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a>Stap 3: Hallo Jenkins werkstroom maken
1. Een item Jenkins maken.
2. Geef een naam (bijvoorbeeld 'Ga web') en selecteer **Freestyle Project**. 
3. Controleer **GitHub project** en geef de GitHub-repo-Hallo URL tooyour.
4. In **beheer van gegevensbronnen Code**, Hallo GitHub-repo-URL en referenties opgeven. 
5. Voeg een **bouwen stap** van het type **shell uitvoeren** en Hallo gebruik de volgende tekst:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. Toevoegen van een andere **bouwen stap** van het type **shell uitvoeren** en Hallo gebruik de volgende tekst:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Jenkins bouwen stappen](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. Hallo Jenkins item opslaan en testen met **nu bouwen**.

### <a name="step-4-connect-github-webhook"></a>Stap 4: Verbinding maken met GitHub webhook
1. In Hallo Jenkins item dat u hebt gemaakt, klikt u op **configureren**.
2. Onder **bouwen Triggers**, selecteer **GitHub haakje trigger voor polling GITScm** en **opslaan**. Hiermee Hallo GitHub webhook automatisch geconfigureerd.
3. Klik in uw GitHub-repo voor Ga-webtoepassingen op **instellingen > Webhooks**.
4. Controleer of deze Hallo Jenkins webhook-URL met succes is toegevoegd. Hallo-URL moet eindigen op 'github webhook'.

![Configuratie van de webhook Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a>Hallo CI/CD proces end tooend testen

1. Code voor het Hallo-opslagplaats en push/synch bijwerken met Hallo GitHub-opslagplaats.
2. Hallo Jenkins-console controleren Hallo **bouwen geschiedenis** en valideren die Hallo taak heeft uitgevoerd. Details voor toosee weergeven console-uitvoer.
3. Details weergeven van Hallo bijgewerkt van Kubernetes, implementatie:

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a>Volgende stappen

- Azure Container register implementeren en afbeeldingen in een veilige locatie opslaan. Zie [Azure Container register docs](https://docs.microsoft.com/azure/container-registry).
- Bouw een complexe workflow met side-by-side-implementatie en automatische tests in Jenkins.
- Zie voor meer informatie over CI/CD met Jenkins en Kubernetes hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).
