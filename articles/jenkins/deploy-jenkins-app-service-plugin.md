---
title: aaaDeploy tooAzure App Service met Jenkins Plugin | Microsoft Docs
description: Meer informatie over hoe toouse Azure App Service Jenkins invoegtoepassing toodeploy een Java web-app tooAzure in Jenkins
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
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a>TooAzure App Service met de invoegtoepassing Jenkins implementeren 
een Java web-app tooAzure toodeploy, kunt u Azure CLI in [Jenkins pijplijn](/azure/jenkins/execute-cli-jenkins-pipeline) of kunt u het gebruik van Hallo [Jenkins van Azure App Service-invoegtoepassing](https://plugins.jenkins.io/azure-app-service). In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Jenkins toodeploy tooAzure App Service via FTP configureren 
> * Jenkins toodeploy tooAzure App Service configureren op Linux via Docker 

## <a name="create-and-configure-jenkins-instance"></a>Maak en configureer Jenkins exemplaar
Als u nog geen een model Jenkins, begint u met de Hallo [oplossingssjabloon](install-jenkins-solution-template.md), waaronder JDK8 en Hallo vereist plugins te volgen:

* [De invoegtoepassing client Jenkins Git](https://plugins.jenkins.io/git-client) v.2.4.6 
* [Docker Commons invoegtoepassing](https://plugins.jenkins.io/docker-commons) v.1.4.0
* [Azure-referenties](https://plugins.jenkins.io/azure-credentials) v.1.2
* [Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1

U kunt Hallo App Service-invoegtoepassing toodeploy Web-App in alle talen (bijvoorbeeld C#, PHP, Java en node.js enz.) wordt ondersteund door Azure App Service kunt gebruiken. In deze zelfstudie gebruiken we Hallo voorbeeld Java-app [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample). toofork hello opslagplaats tooyour eigenaar GitHub-account, klikt u op Hallo **Fork** knop in de rechterbovenhoek Hallo.  

Java-JDK en Maven zijn vereist voor het bouwen van Hallo Java-project. Zorg ervoor dat u in Hallo Jenkins model of de VM-agent Hallo Hallo-onderdelen installeren als u een continue integratie. 

tooinstall, meld u bij toohello Jenkins exemplaar met gebruikmaking van SSH en Voer Hallo volgende opdrachten:

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

Voor het implementeren van tooApp-Service op Linux, moet u ook tooinstall Docker op Hallo Jenkins master of Hallo VM-agent gebruikt om te worden gemaakt. Raadpleeg toothis artikel tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.

## <a name="add-azure-service-principal-toojenkins-credential"></a>Azure-service principal tooJenkins gebruikersreferentie toevoegen

Een Azure-service-principal is benodigde toodeploy tooAzure. 

<ol>
<li>Gebruik [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) of [Azure-portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate een Azure-service-principal</li>
<li>Klik in het Hallo Jenkins dashboard op **referenties -> systeem ->**. Klik op **globale credentials(unrestricted)**.</li>
<li>Klik op **toevoegen referenties** tooadd een Microsoft Azure-service-principal door in te vullen Hallo abonnements-ID, Client-ID, Client Secret en OAuth 2.0-Tokeneindpunt. Geef een ID **mySp**, voor gebruik in de volgende stappen.</li>
</ol>

## <a name="azure-app-service-plugin"></a>Azure App Service-invoegtoepassing

Azure App Service-invoegtoepassing v1.0 biedt ondersteuning voor doorlopende implementatie tooAzure Web-App via:

* GIT en FTP
* Docker voor Web-App op Linux

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a>Jenkins toodeploy via FTP met Hallo Jenkins dashboard-Web-App configureren

toodeploy uw project tooAzure Web-App kunt u uw build-artefacten (bijvoorbeeld .war bestanden in Java) uploaden met Git- of FTP.

Voordat u de taak Hallo in Jenkins instelt, moet u een Azure App Service-abonnement en een Web-App voor actieve Hallo Java-app.


1. Maken van een Azure App Service-abonnement met Hallo **vrije** prijscategorie Hallo met [az appservice-abonnement maken](/cli/azure/appservice/plan#create) CLI-opdracht. Hallo appservice-abonnement definieert Hallo fysieke resources gebruikt toohost uw apps. Alle toepassingen die toegewezen tooan appservice-abonnement kunt u deze resources, zodat u toosave kosten bij het hosten van meerdere apps delen.
2. Maak een web-app. U kunt beide Hallo gebruik [Azure-portal](/azure/app-service-web/web-sites-configure) of gebruik Hallo na Az CLI-opdracht:
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. Zorg ervoor dat u Hallo Java runtime-configuratie die uw app moet instellen. Hello Azure CLI-opdracht te volgen Hallo web app toorun configureert op een recente Java 8 JDK en [Apache Tomcat](http://tomcat.apache.org/) 8.0.
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a>Hallo Jenkins taak instellen


1. Maak een nieuwe **freestyle** project in Jenkins-Dashboard
2. Configureren **Source Code Management** toouse uw lokale fork van [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample) doordat Hallo **opslagplaats URL**. Bijvoorbeeld: http://github.com/&lt;yourID > / javawebappsample.
3. Een Build stap toobuild Hallo project met behulp van Maven toevoegen. Dit doen door het toevoegen van een **shell uitvoeren**. Bijvoorbeeld moeten we een extra stap toorename hello *.war-bestand in map tooROOT.war van doel.   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. Een actie na build toevoegen door te selecteren **een Azure-Web-App publiceren**.
5. Geef, 'mySp', hello Azure service-principal is opgeslagen in de vorige stap.
6. In **App-configuratie** sectie, kiest u Hallo resource groep en web-app in uw abonnement. Hallo-invoegtoepassing detecteert automatisch of Hallo Web-App Windows is of Linux-. Voor een webtoepassing op basis van Windows hello optie 'Bestanden publiceren' wordt weergegeven.
7. Vul in Hallo-bestanden die u wilt toodeploy (bijvoorbeeld een war pakket als u Java gebruikt.) Bron- en doelmap zijn optioneel. Hallo parameters kunt u de bron en doel mappen toospecify, tijdens het uploaden van bestanden. Java-web-app in Azure wordt uitgevoerd in een Tomcat-server. Zodat u uploaden war-pakket naar de map webapps. In dit voorbeeld ingesteld **bronmap** te 'als doel' en 'webapps' opgeven voor **doelmap**.
8. Als u wilt dat toodeploy tooa sleuf dan productie, kunt u ook instellen **sleuf** naam.
9. Sla Hallo-project en bouw het. Uw web-app is geïmplementeerd tooAzure wanneer build voltooid is.

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a>Web-App via FTP Jenkins pijplijn met implementeren

Hallo-invoegtoepassing is-pipeline-klaar. U kunt tooa voorbeeld in GitHub-repo-Hallo verwijzen.

1. Open in de GitHub-webgebruikersinterface, **Jenkinsfile_ftp_plugin** bestand. Klik op Hallo pen pictogram tooedit dit bestand tooupdate Hallo resourcegroep en de naam van uw web-app op regel 11 en 12 respectievelijk.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Regel 14 tooupdate referentie-ID in uw exemplaar Jenkins wijzigen.    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a>Een pijplijn Jenkins maken

1. Jenkins in een webbrowser openen, klikt u op **Nieuw Item**.
2. Geef een naam voor de taak Hallo en selecteer **pijplijn**. Klik op **OK**.
3. Klik op Hallo **pijplijn** volgende tabblad.
4. Voor **definitie**, selecteer **Pipeline-script uit SCM**.
5. Voor **SCM**, selecteer **Git**. Voer Hallo GitHub-URL voor uw opslagplaats Gevorkte: https:&lt;uw Gevorkte opslagplaats > .git
6. Update **scriptpad** te 'Jenkinsfile_ftp_plugin'
7. Klik op **opslaan** en Voer Hallo-taak.

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a>Jenkins toodeploy Web-App op Linux via Docker configureren

Naast Git-/ FTP-, biedt ondersteuning voor Web-App op Linux implementatie met behulp van Docker. toodeploy met behulp van Docker, moet u tooprovide een Dockerfile die uw web-app met service runtime worden verpakt in een docker-installatiekopie. Vervolgens Hallo invoegtoepassing Hallo image wordt gemaakt, duwt deze tooa docker-register en Hallo installatiekopie tooyour web-app wordt geïmplementeerd.

Web-App op Linux ondersteunt ook traditionele manieren zoals Git en FTP-, maar alleen voor ingebouwde talen (.NET Core, Node.js, PHP en Ruby). Voor andere talen toopackage uw code en service runtime voor de toepassing samen in een docker-installatiekopie en deze kunt docker toodeploy.

Voordat u de taak Hallo in Jenkins instelt, moet u een Azure app service op Linux. Een container-register is ook nodig toostore en beheren van uw persoonlijke installatiekopieën van de Docker-container. U kunt DockerHub; We gebruiken Azure Container register voor dit voorbeeld.

* U kunt Hallo stappen [hier](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate een Web-App op Linux 
* Azure Container register is een beheerde [Docker-register] (https://docs.docker.com/registry/) service op basis van Hallo open source Docker register 2.0. Stappen Hallo [hier] (/ azure/container-registry/container-registry-get-started-azure-cli) voor meer instructies voor het toodo zodat. U kunt ook DockerHub gebruiken.

### <a name="toodeploy-using-docker"></a>toodeploy met behulp van docker:

1. Maak een nieuwe freestyle project in Jenkins-Dashboard.
2. Configureren **Source Code Management** toouse uw lokale fork van [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample) doordat Hallo **opslagplaats URL**. Bijvoorbeeld: http://github.com/&lt;yourid > / javawebappsample.
Een Build stap toobuild Hallo project met behulp van Maven toevoegen. Dit doen door het toevoegen van een **shell uitvoeren** en voeg Hallo volgende regel in **opdracht**:    
```bash
mvn clean package
```

3. Een actie na build toevoegen door te selecteren **een Azure-Web-App publiceren**.
4. Geef, **mySp**, hello Azure service-principal is opgeslagen in de vorige stap als Azure-referenties.
5. In **App-configuratie** sectie, kiest u Hallo-resourcegroep en een Linux-web-app in uw abonnement.
6. Kies publiceren via de Docker.
7. Vul **Dockerfile** pad. Kunt u de standaard Hallo ' / Dockerfile ' voor **Docker register URL**, supply Hallo indeling https://&lt;myRegistry >. azurecr.io als u gebruikmaakt van Azure Container register. Laat dit veld leeg als u DockerHub gebruikt.
8. Voor **register referenties**, Hallo-referentie voor hello Azure Container register toevoegen. U kunt Hallo gebruikersnaam en wachtwoord door het uitvoeren van de volgende opdrachten in de Azure CLI Hallo ophalen. de eerste opdracht Hallo kunt Hallo administrator-account.    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. Hallo docker installatiekopie met de naam en code in **Geavanceerd** tabblad zijn optioneel. Standaard installatiekopie met de naam is verkregen van de installatiekopie van het Hallo naam die u hebt geconfigureerd in Azure portal (in Docker-Container. de instelling) Hallo-code is gegenereerd op basis van $BUILD_NUMBER. Zorg ervoor dat u de naam van de installatiekopie Hallo opgeven in de Azure-portal of een waarde opgeven voor **Docker-afbeelding** in **Geavanceerd** tabblad. Geef voor dit voorbeeld '&lt;yourRegistry >.azurecr.io/calculator ' voor **Docker-afbeelding** en laat **Docker afbeeldingscode** leeg.
10. Opmerking implementatie mislukt als u ingebouwde Docker installatiekopie instelling gebruiken. Zorg ervoor dat u docker config toouse aangepaste installatiekopie in de instelling Docker-Container in Azure-portal wijzigen. Gebruik bestand uploaden benadering toodeploy voor ingebouwde installatiekopie.
11. Soortgelijke benadering van toofile uploaden, kunt u een andere site dan de productie.
12. Opslaat en bouwt Hallo-project. U ziet uw installatiekopie container wordt doorgeschoven, tooyour register en web-app wordt geïmplementeerd.

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a>TooWeb App op Linux via Jenkins pijplijn met Docker implementeren

1. Open in de GitHub-webgebruikersinterface, **Jenkinsfile_container_plugin** bestand. Klik op Hallo pen pictogram tooedit dit bestand tooupdate Hallo resourcegroep en de naam van uw web-app op regel 11 en 12 respectievelijk.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Regel 13 tooyour container Registerserver wijzigen    
```java
def registryServer = '<registryURL>'
```    

3. Regel 16 tooupdate referentie-ID in uw exemplaar Jenkins wijzigen    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a>Jenkins pijplijn maken    

1. Jenkins in een webbrowser openen, klikt u op **Nieuw Item**.
2. Geef een naam voor de taak Hallo en selecteer **pijplijn**. Klik op **OK**.
3. Klik op Hallo **pijplijn** volgende tabblad.
4. Voor **definitie**, selecteer **Pipeline-script uit SCM**.
5. Voor **SCM**, selecteer **Git**.
6. Voer Hallo GitHub-URL voor uw opslagplaats Gevorkte: https:&lt;uw Gevorkte opslagplaats > .git</li>
Update 7, **scriptpad** te 'Jenkinsfile_container_plugin'
8. Klik op **opslaan** en Voer Hallo-taak.

## <a name="verify-your-web-app"></a>Controleer of uw web-app

1. tooverify hello WAR-bestand wordt geïmplementeerd tooyour web-app. Open een webbrowser.
2. Ga toohttp: / /&lt;app_naam >.azurewebsites.net/api/calculator/ping u zien:    
     Welkom tooJava Web-App. Dit is bijgewerkt.
   Sun Jun 17 16:39:10 UTC 2017
3. Ga toohttp: / /&lt;app_naam >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (vervangen door &lt;x > en &lt;y > met willekeurige getallen) tooget Hallo som van de x en y        
    ![Rekenmachine: toevoegen](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a>Voor App-service op Linux

* tooverify, in de Azure CLI uitvoeren:

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    U krijgt Hallo resultaat te volgen:
    
    ```
    [
    "calculator"
    ]
    ```
    
    Ga toohttp: / /&lt;app_naam >.azurewebsites.net/api/calculator/ping. U ziet het Hallo-bericht: 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    Ga toohttp: / /&lt;app_naam >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (vervangen door &lt;x > en &lt;y > met willekeurige getallen) tooget Hallo som van de x en y
    
## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie gebruikt u hello Azure App Service-invoegtoepassing toodeploy tooAzure.

U hebt geleerd hoe u:

> [!div class="checklist"]
> * Jenkins toodeploy Azure App Service via FTP configureren 
> * Jenkins toodeploy tooAzure App Service configureren op Linux via Docker 
