---
title: Implementeren in Azure App Service met de invoegtoepassing Jenkins | Microsoft Docs
description: Informatie over het gebruik van Azure App Service Jenkins-invoegtoepassing voor het implementeren van een Java-web-app in Azure in Jenkins
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 646daad1785f3de067544b6dd38abfcb6bc67d4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-plugin"></a>Implementeren in Azure App Service met Jenkins-invoegtoepassing 
Als u wilt een Java-web-app implementeren in Azure, kunt u Azure CLI in [Jenkins pijplijn](/azure/jenkins/execute-cli-jenkins-pipeline) of kunt u het gebruik van de [invoegtoepassing van Azure App Service Jenkins](https://plugins.jenkins.io/azure-app-service). In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Jenkins implementeren in Azure App Service via FTP configureren 
> * Jenkins implementeren in Azure App Service op Linux via Docker configureren 

## <a name="create-and-configure-jenkins-instance"></a>Maak en configureer Jenkins exemplaar
Als u nog geen een model Jenkins, begint u met de [oplossingssjabloon](install-jenkins-solution-template.md), waaronder JDK8 en de volgende vereiste invoegtoepassingen:

* [De invoegtoepassing client Jenkins Git](https://plugins.jenkins.io/git-client) v.2.4.6 
* [Docker Commons invoegtoepassing](https://plugins.jenkins.io/docker-commons) v.1.4.0
* [Azure-referenties](https://plugins.jenkins.io/azure-credentials) v.1.2
* [Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1

De App Service-invoegtoepassing kunt u Web-App implementeren in alle talen (bijvoorbeeld C#, PHP, Java en node.js enz.) wordt ondersteund door Azure App Service. In deze zelfstudie gebruiken we de Java voorbeeldapp [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample). Om te vertakken de opslagplaats op uw eigen GitHub-account, klikt u op de **Fork** knop in de rechterbovenhoek.  

Java-JDK en Maven zijn vereist voor het bouwen van de Java-project. Zorg ervoor dat u de onderdelen in het model Jenkins of de VM-agent installeren als u een continue integratie. 

Als u wilt installeren, aanmelden bij het gebruik van SSH Jenkins-exemplaar en voer de volgende opdrachten:

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

Voor op Linux-App Service-implementatie, moet u ook Docker installeren op de master Jenkins of de VM-agent gebruikt om te worden gemaakt. Raadpleeg dit artikel voor het installeren van Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.

## <a name="add-azure-service-principal-to-jenkins-credential"></a>Azure-service-principal tot Jenkins referentie toevoegen

Een Azure-service-principal is nodig om te implementeren in Azure. 

<ol>
<li>Gebruik [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) of [Azure-portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) een Azure-service-principal maken</li>
<li>Klik in het dashboard Jenkins op **referenties -> systeem ->**. Klik op **globale credentials(unrestricted)**.</li>
<li>Klik op **referenties toevoegen** toevoegen van een Microsoft Azure service-principal met de abonnements-ID, de Client-ID, het Clientgeheim en de OAuth 2.0-Tokeneindpunt invullen. Geef een ID **mySp**, voor gebruik in de volgende stappen.</li>
</ol>

## <a name="azure-app-service-plugin"></a>Azure App Service-invoegtoepassing

Azure App Service-invoegtoepassing v1.0 biedt ondersteuning voor continue implementatie naar Azure-Web-App via:

* GIT en FTP
* Docker voor Web-App op Linux

## <a name="configure-jenkins-to-deploy-web-app-through-ftp-using-the-jenkins-dashboard"></a>Jenkins voor het implementeren van Web-App via met het dashboard Jenkins FTP configureren

Als u wilt uw project op Azure-Web-App implementeert, kunt u uw build-artefacten (bijvoorbeeld .war bestanden in Java) uploaden met Git- of FTP.

Voordat u de taak in Jenkins instelt, moet u een Azure App Service-abonnement en een Web-App voor het uitvoeren van de Java-app.


1. Maken van een Azure App Service-abonnement met de **vrije** prijzen met behulp van laag de [az appservice-abonnement maken](/cli/azure/appservice/plan#create) CLI-opdracht. Het plan appservice definieert de fysieke resources gebruikt voor het hosten van uw apps. Alle toepassingen die zijn toegewezen aan een appservice-abonnement kunt u deze resources, zodat u kosten opslaan bij het hosten van meerdere apps delen.
2. Maak een web-app. Kunt u ofwel de [Azure-portal](/azure/app-service-web/web-sites-configure) of gebruik de volgende Az CLI-opdracht:
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. Zorg ervoor dat u de Java runtime-configuratie die uw app moet instellen. De volgende opdracht in de Azure CLI configureert u de web-app uit te voeren op een recente Java 8 JDK en [Apache Tomcat](http://tomcat.apache.org/) 8.0.
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-the-jenkins-job"></a>De taak Jenkins instellen


1. Maak een nieuwe **freestyle** project in Jenkins-Dashboard
2. Configureren **Source Code Management** gebruik van uw lokale fork van [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample) doordat de **opslagplaats URL**. Bijvoorbeeld: http://github.com/&lt;yourID > / javawebappsample.
3. Een stap Build bouw het project met behulp van Maven toevoegen. Dit doen door het toevoegen van een **shell uitvoeren**. In dit voorbeeld moet een aanvullende stap in de naam van het bestand *.war in doelmap ROOT.war.   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. Een actie na build toevoegen door te selecteren **een Azure-Web-App publiceren**.
5. Geef, 'mySp', de Azure service-principal die is opgeslagen in de vorige stap.
6. In **App-configuratie** sectie, kiest u de resource-groep en web-app in uw abonnement. De invoegtoepassing detecteert automatisch of de Web-App van Windows is of Linux-. Voor een Windows gebaseerde Web-App de optie "bestanden publiceren' weergegeven.
7. Vul in de bestanden die u wilt implementeren (bijvoorbeeld, een pakket war als u Java gebruikt.) Bron- en doelmap zijn optioneel. De parameters kunnen u mappen bron en doel opgeven tijdens het uploaden van bestanden. Java-web-app in Azure wordt uitgevoerd in een Tomcat-server. Zodat u uploaden war-pakket naar de map webapps. In dit voorbeeld ingesteld **bronmap** 'doelgroep' en 'webapps' opgeven voor **doelmap**.
8. Als u implementeren in een sleuf dan productie wilt, kunt u ook instellen **sleuf** naam.
9. Sla het project en bouw het. Uw web-app wordt geïmplementeerd op Azure als build voltooid is.

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a>Web-App via FTP Jenkins pijplijn met implementeren

De invoegtoepassing is-pipeline-klaar. U kunt verwijzen naar een voorbeeld van een in de GitHub-opslagplaats.

1. Open in de GitHub-webgebruikersinterface, **Jenkinsfile_ftp_plugin** bestand. Klik op het potloodpictogram om dit bestand voor het bijwerken van de resourcegroep en de naam van uw web-app op regel 11 en 12 respectievelijk te bewerken.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Wijzig de regel 14 verwijzings-ID in uw exemplaar Jenkins bijwerken.    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a>Een pijplijn Jenkins maken

1. Jenkins in een webbrowser openen, klikt u op **Nieuw Item**.
2. Geef een naam op voor de taak en selecteer **pijplijn**. Klik op **OK**.
3. Klik op de **pijplijn** volgende tabblad.
4. Voor **definitie**, selecteer **Pipeline-script uit SCM**.
5. Voor **SCM**, selecteer **Git**. Geef de GitHub-URL voor uw opslagplaats Gevorkte: https:&lt;uw Gevorkte opslagplaats > .git
6. Update **pad Script** naar 'Jenkinsfile_ftp_plugin'
7. Klik op **opslaan** en voer de taak.

## <a name="configure-jenkins-to-deploy-web-app-on-linux-through-docker"></a>Jenkins als u wilt implementeren op Linux via de Docker-Web-App configureren

Naast Git-/ FTP-, biedt ondersteuning voor Web-App op Linux implementatie met behulp van Docker. Als u wilt implementeren met behulp van Docker, moet u een Dockerfile die uw web-app met service runtime worden verpakt in een docker-installatiekopie opgeven. Vervolgens de invoegtoepassing voor de installatiekopie is gebaseerd, duwt deze met een docker-register en implementeert de installatiekopie naar uw web-app.

Web-App op Linux ondersteunt ook traditionele manieren zoals Git en FTP-, maar alleen voor ingebouwde talen (.NET Core, Node.js, PHP en Ruby). Voor andere talen moet u uw toepassing en de service een runtime-pakket samen in een docker-installatiekopie en docker gebruiken om te implementeren.

Voordat u de taak in Jenkins instelt, moet u een Azure app service op Linux. Een container-register is ook nodig opslaan en beheren van uw persoonlijke installatiekopieën van de Docker-container. U kunt DockerHub; We gebruiken Azure Container register voor dit voorbeeld.

* U kunt de stappen [hier](/azure/app-service-web/app-service-linux-how-to-create-web-app) voor het maken van een Web-App op Linux 
* Azure Container register is een beheerde [Docker-register] (https://docs.docker.com/registry/) service op basis van de open source Docker register 2.0. Volg de stappen [hier] (/ azure/container-registry/container-registry-get-started-azure-cli) voor meer instructies voor het om dit te doen. U kunt ook DockerHub gebruiken.

### <a name="to-deploy-using-docker"></a>Implementeren met behulp van docker:

1. Maak een nieuwe freestyle project in Jenkins-Dashboard.
2. Configureren **Source Code Management** gebruik van uw lokale fork van [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample) doordat de **opslagplaats URL**. Bijvoorbeeld: http://github.com/&lt;yourid > / javawebappsample.
Een stap Build bouw het project met behulp van Maven toevoegen. Dit doen door het toevoegen van een **shell uitvoeren** en voeg de volgende regel in **opdracht**:    
```bash
mvn clean package
```

3. Een actie na build toevoegen door te selecteren **een Azure-Web-App publiceren**.
4. Geef, **mySp**, de Azure service-principal die is opgeslagen in de vorige stap als Azure-referenties.
5. In **App-configuratie** sectie, kiest u de resourcegroep en een Linux-web-app in uw abonnement.
6. Kies publiceren via de Docker.
7. Vul **Dockerfile** pad. U kunt de standaardinstelling behouden ' / Dockerfile ' voor **Docker register URL**, in de indeling van https:// supply&lt;myRegistry >. azurecr.io als u gebruikmaakt van Azure Container register. Laat dit veld leeg als u DockerHub gebruikt.
8. Voor **register referenties**, de referentie voor het register Azure-Container toevoegen. U kunt de gebruikersnaam en wachtwoord ophalen met de volgende opdrachten in de Azure CLI. De eerste opdracht kunt het administrator-account.    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. De docker installatiekopie met de naam en code in **Geavanceerd** tabblad zijn optioneel. Standaard wordt installatiekopie met de naam opgehaald uit de naam van de installatiekopie die u hebt geconfigureerd in Azure-portal (in Docker-Container-instelling.) De code is gegenereerd op basis van $BUILD_NUMBER. Zorg ervoor dat u de naam van de installatiekopie opgeven in de Azure-portal of een waarde opgeven voor **Docker-afbeelding** in **Geavanceerd** tabblad. Geef voor dit voorbeeld '&lt;yourRegistry >.azurecr.io/calculator ' voor **Docker-afbeelding** en laat **Docker afbeeldingscode** leeg.
10. Opmerking implementatie mislukt als u ingebouwde Docker installatiekopie instelling gebruiken. Zorg ervoor dat u docker-configuratie voor het gebruik van aangepaste installatiekopie in de instelling Docker-Container in Azure-portal wijzigen. Gebruik voor ingebouwde installatiekopie bestand uploaden aanpak om te implementeren.
11. Net als bij benadering van bestand uploaden, kunt u een andere site dan de productie.
12. Sla en bouw het project. U ziet uw installatiekopie container wordt doorgeschoven, toe aan het register en web-app wordt geïmplementeerd.

### <a name="deploy-to-web-app-on-linux-through-docker-using-jenkins-pipeline"></a>Implementeren naar Web-App op Linux via Jenkins pijplijn met Docker

1. Open in de GitHub-webgebruikersinterface, **Jenkinsfile_container_plugin** bestand. Klik op het potloodpictogram om dit bestand voor het bijwerken van de resourcegroep en de naam van uw web-app op regel 11 en 12 respectievelijk te bewerken.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Regel 13 wijzigen in de container register-server    
```java
def registryServer = '<registryURL>'
```    

3. Wijzig regel 16 verwijzings-ID in uw exemplaar Jenkins bijwerken    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a>Jenkins pijplijn maken    

1. Jenkins in een webbrowser openen, klikt u op **Nieuw Item**.
2. Geef een naam op voor de taak en selecteer **pijplijn**. Klik op **OK**.
3. Klik op de **pijplijn** volgende tabblad.
4. Voor **definitie**, selecteer **Pipeline-script uit SCM**.
5. Voor **SCM**, selecteer **Git**.
6. Geef de GitHub-URL voor uw opslagplaats Gevorkte: https:&lt;uw Gevorkte opslagplaats > .git</li>
Update 7, **pad Script** naar 'Jenkinsfile_container_plugin'
8. Klik op **opslaan** en voer de taak.

## <a name="verify-your-web-app"></a>Controleer of uw web-app

1. Om te controleren of het WAR-bestand is geïmplementeerd in uw web-app. Open een webbrowser.
2. Ga naar http://&lt;app_naam >.azurewebsites.net/api/calculator/ping u zien:    
     Welkom bij de Java-Web-App. Dit is bijgewerkt.
   Sun Jun 17 16:39:10 UTC 2017
3. Ga naar http://&lt;app_naam >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (vervangen door &lt;x > en &lt;y > met willekeurige getallen) om op te halen van de som van de x en y        
    ![Rekenmachine: toevoegen](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a>Voor App-service op Linux

* Om te controleren, in de Azure CLI uitvoeren:

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    U krijgen het volgende resultaat:
    
    ```
    [
    "calculator"
    ]
    ```
    
    Ga naar http://&lt;app_naam >.azurewebsites.net/api/calculator/ping. U ziet het bericht: 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    Ga naar http://&lt;app_naam >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (vervangen door &lt;x > en &lt;y > met willekeurige getallen) om op te halen van de som van de x en y
    
## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie kunt u de invoegtoepassing van Azure App Service implementeren in Azure.

U leert hoe naar:

> [!div class="checklist"]
> * Jenkins voor het implementeren van Azure App Service via FTP configureren 
> * Jenkins implementeren in Azure App Service op Linux via Docker configureren 