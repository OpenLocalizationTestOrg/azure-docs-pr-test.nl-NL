---
title: aaaExecute hello Azure CLI met Jenkins | Microsoft Docs
description: Meer informatie over hoe toouse Azure CLI toodeploy een Java web-app tooAzure in Jenkins pijplijn
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a>App Service met Jenkins tooAzure implementeren en hello Azure CLI
een Java web-app tooAzure toodeploy, kunt u Azure CLI in [Jenkins pijplijn](https://jenkins.io/doc/book/pipeline/). In deze zelfstudie maakt u een pijplijn CI/CD maken op een virtuele machine in Azure met inbegrip van hoe:

> [!div class="checklist"]
> * Maak een VM Jenkins
> * Jenkins configureren
> * Een web-app maken in Azure
> * Voorbereiden van een GitHub-opslagplaats
> * Jenkins pijplijn maken
> * Hallo pijplijn uitvoeren en controleer of Hallo web-app

Deze zelfstudie vereist hello Azure CLI versie 2.0.4 of hoger. toofind hello versie, voer `az --version`. Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a>Maak en configureer Jenkins exemplaar
Als u nog geen een model Jenkins, begint u met de Hallo [oplossingssjabloon](install-jenkins-solution-template.md), waaronder Hallo vereist [Azure-referenties](https://plugins.jenkins.io/azure-credentials) invoegtoepassing standaard. 

Hello Azure referentie-invoegtoepassing kunt u toostore Microsoft Azure-service-principal referenties in Jenkins. In versie 1.2, we Hallo is ondersteuning toegevoegd zodat deze Jenkins Pipeline hello Azure-referenties. 

Controleer of dat u versie 1.2 of hoger hebt:
* Binnen Hallo Jenkins dashboard, klikt u op **Jenkins beheren -> Manager van de invoegtoepassing ->** en zoek naar **Azure referentie**. 
* Hallo-invoegtoepassing worden bijgewerkt als het Hallo-versie ouder is dan 1.2.

Java-JDK en Maven zijn ook vereist in Hallo Jenkins master. tooinstall, tooJenkins master via SSH aanmelden en Voer Hallo volgende opdrachten uit:
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a>Azure-service principal tooJenkins gebruikersreferentie toevoegen

Een Azure-referentie is benodigde tooexecute Azure CLI.

* Klik in het Hallo Jenkins dashboard op **referenties -> systeem ->**. Klik op **globale credentials(unrestricted)**.
* Klik op **toevoegen referenties** tooadd een [Microsoft Azure service-principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) door in te vullen Hallo abonnements-ID, Client-ID, Client Secret en OAuth 2.0-Tokeneindpunt. Geef een ID voor gebruik in de volgende stap.

![Referenties toevoegen](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a>Een Azure App Service voor het implementeren van Hallo Java-web-app maken

Maken van een Azure App Service-abonnement met Hallo **vrije** prijscategorie Hallo met [az appservice-abonnement maken](/cli/azure/appservice/plan#create) CLI-opdracht. Hallo appservice-abonnement definieert Hallo fysieke resources gebruikt toohost uw apps. Alle toepassingen die toegewezen tooan appservice-abonnement kunt u deze resources, zodat u toosave kosten bij het hosten van meerdere apps delen. 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

Wanneer Hallo plan klaar is, uitvoer hello die Azure CLI ongeveer dezelfde wordt toohello voorbeeld te volgen:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a>Een Azure-Web-app maken

 Gebruik Hallo [az webapp maken](/cli/azure/appservice/web#create) CLI opdracht toocreate de definitie van een web-app in Hallo `myAppServicePlan` App Service-abonnement. Hallo web app definitie voorziet in uw toepassing met een URL-tooaccess en verschillende opties toodeploy uw code tooAzure configureert. 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

Vervang Hallo `<app_name>` aanduiding voor items met uw eigen unieke app-naam. Deze unieke naam is onderdeel van de standaarddomeinnaam Hallo voor Hallo-web-app Hallo naam moet toobe uniek zijn in alle apps in Azure. U kunt een aangepast domein de naam van vermelding toohello web-app kunt toewijzen, voordat u deze tooyour gebruikers weergeven.

Wanneer de definitie van Hallo web apps klaar is, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen: 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a>Java configureren 

Hallo Java runtime-configuratie die uw app Hello moet instellen [az appservice web config update](/cli/azure/appservice/web/config#update) opdracht.

Hallo volgende opdracht configureert u Hallo web app toorun op een recente Java 8 JDK en [Apache Tomcat](http://tomcat.apache.org/) 8.0.

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a>Voorbereiden van een GitHub-opslagplaats
Open Hallo [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample) opslagplaats. toofork hello opslagplaats tooyour eigenaar GitHub-account, klikt u op Hallo **Fork** knop in de rechterbovenhoek Hallo.

* Open in de GitHub-webgebruikersinterface, **Jenkinsfile** bestand. Klik op Hallo pen pictogram tooedit dit bestand tooupdate Hallo resourcegroep en de naam van uw web-app op regel 20 en 21 respectievelijk.

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* Regel 23 tooupdate referentie-ID in uw exemplaar Jenkins wijzigen

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a>Jenkins pijplijn maken
Jenkins in een webbrowser openen, klikt u op **Nieuw Item**. 

* Geef een naam voor de taak Hallo en selecteer **pijplijn**. Klik op **OK**.
* Klik op Hallo **pijplijn** volgende tabblad. 
* Voor **definitie**, selecteer **Pipeline-script uit SCM**.
* Voor **SCM**, selecteer **Git**.
* Voer Hallo GitHub-URL voor uw opslagplaats Gevorkte: https:\<uw Gevorkte opslagplaats\>.git
* Klik op **opslaan**

## <a name="test-your-pipeline"></a>Test uw pijplijn
* Ga toohello pijplijn die u hebt gemaakt, klikt u op **nu bouwen**
* Een build moet slagen binnen een paar seconden en kunt u toohello build gaan en op **Console-uitvoer** toosee Hallo details

## <a name="verify-your-web-app"></a>Controleer of uw web-app
tooverify hello WAR-bestand wordt geïmplementeerd tooyour web-app. Open een webbrowser:

* Ga toohttp: / /&lt;app_naam >.azurewebsites.net/api/calculator/ping  
U ziet:

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* Ga toohttp: / /&lt;app_naam >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (vervangen door &lt;x > en &lt;y > met willekeurige getallen) tooget Hallo som van de x en y

![Rekenmachine: toevoegen](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a>TooAzure op Linux-Web-App implementeren
Nu dat u hoe toouse Azure CLI in uw Jenkins pijplijn weet, kunt u Hallo script toodeploy tooan Azure-Web-App op Linux kunt wijzigen.

Een andere manier toodo Hallo implementatie, die toouse Docker biedt ondersteuning voor Web-App op Linux. toodeploy, moet u tooprovide een Dockerfile die uw web-app met service runtime worden verpakt in een Docker-installatiekopie. Hallo-invoegtoepassing wordt vervolgens Hallo-installatiekopie bouwen, dit tooa Docker register doorgeven en Hallo installatiekopie tooyour web-app implementeren.

* Volg de stappen Hallo [hier](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate een Azure-Web-App uitgevoerd op Linux.
* Docker installeren op uw exemplaar Jenkins door Hallo-instructies in dit [artikel](https://docs.docker.com/engine/installation/linux/ubuntu/).
* Maken van een register-Container in hello Azure-portal met behulp van Hallo stappen [hier](/azure/container-registry/container-registry-get-started-azure-cli).
* Hallo in dezelfde [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample) opslagplaats u forked bewerken Hallo **Jenkinsfile2** bestand:
    * Regel 18-21, respectievelijk toohello namen van de resourcegroep, web-app en ACR bijwerken. 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * Regel 24-, update \<azsrvprincipal\> tooyour verwijzings-ID
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* Een nieuwe Jenkins pijplijn maken net als bij het implementeren van tooAzure web-app in Windows, alleen deze keer gebruik **Jenkinsfile2** in plaats daarvan.
* Uw nieuwe taak uitvoeren.
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
In deze zelfstudie maakt u een Jenkins pijplijn die de broncode Hallo in GitHub-repo-uitgecheckt geconfigureerd. Maven toobuild voert een war-bestand en gebruikt vervolgens Azure CLI toodeploy tooAzure App Service. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Maak een VM Jenkins
> * Jenkins configureren
> * Een web-app maken in Azure
> * Voorbereiden van een GitHub-opslagplaats
> * Jenkins pijplijn maken
> * Hallo pijplijn uitvoeren en controleer of Hallo web-app
