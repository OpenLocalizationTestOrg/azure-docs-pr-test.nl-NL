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
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a><span data-ttu-id="cf67d-103">App Service met Jenkins tooAzure implementeren en hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cf67d-103">Deploy tooAzure App Service with Jenkins and hello Azure CLI</span></span>
<span data-ttu-id="cf67d-104">een Java web-app tooAzure toodeploy, kunt u Azure CLI in [Jenkins pijplijn](https://jenkins.io/doc/book/pipeline/).</span><span class="sxs-lookup"><span data-stu-id="cf67d-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="cf67d-105">In deze zelfstudie maakt u een pijplijn CI/CD maken op een virtuele machine in Azure met inbegrip van hoe:</span><span class="sxs-lookup"><span data-stu-id="cf67d-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cf67d-106">Maak een VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="cf67d-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="cf67d-107">Jenkins configureren</span><span class="sxs-lookup"><span data-stu-id="cf67d-107">Configure Jenkins</span></span>
> * <span data-ttu-id="cf67d-108">Een web-app maken in Azure</span><span class="sxs-lookup"><span data-stu-id="cf67d-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="cf67d-109">Voorbereiden van een GitHub-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="cf67d-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="cf67d-110">Jenkins pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="cf67d-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="cf67d-111">Hallo pijplijn uitvoeren en controleer of Hallo web-app</span><span class="sxs-lookup"><span data-stu-id="cf67d-111">Run hello pipeline and verify hello web app</span></span>

<span data-ttu-id="cf67d-112">Deze zelfstudie vereist hello Azure CLI versie 2.0.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="cf67d-112">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cf67d-113">toofind hello versie, voer `az --version`.</span><span class="sxs-lookup"><span data-stu-id="cf67d-113">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="cf67d-114">Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cf67d-114">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="cf67d-115">Maak en configureer Jenkins exemplaar</span><span class="sxs-lookup"><span data-stu-id="cf67d-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="cf67d-116">Als u nog geen een model Jenkins, begint u met de Hallo [oplossingssjabloon](install-jenkins-solution-template.md), waaronder Hallo vereist [Azure-referenties](https://plugins.jenkins.io/azure-credentials) invoegtoepassing standaard.</span><span class="sxs-lookup"><span data-stu-id="cf67d-116">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes hello required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="cf67d-117">Hello Azure referentie-invoegtoepassing kunt u toostore Microsoft Azure-service-principal referenties in Jenkins.</span><span class="sxs-lookup"><span data-stu-id="cf67d-117">hello Azure Credential plugin allows you toostore Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="cf67d-118">In versie 1.2, we Hallo is ondersteuning toegevoegd zodat deze Jenkins Pipeline hello Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="cf67d-118">In version 1.2, we added hello support so that Jenkins Pipeline can get hello Azure credentials.</span></span> 

<span data-ttu-id="cf67d-119">Controleer of dat u versie 1.2 of hoger hebt:</span><span class="sxs-lookup"><span data-stu-id="cf67d-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="cf67d-120">Binnen Hallo Jenkins dashboard, klikt u op **Jenkins beheren -> Manager van de invoegtoepassing ->** en zoek naar **Azure referentie**.</span><span class="sxs-lookup"><span data-stu-id="cf67d-120">Within hello Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="cf67d-121">Hallo-invoegtoepassing worden bijgewerkt als het Hallo-versie ouder is dan 1.2.</span><span class="sxs-lookup"><span data-stu-id="cf67d-121">Update hello plugin if hello version is earlier than 1.2.</span></span>

<span data-ttu-id="cf67d-122">Java-JDK en Maven zijn ook vereist in Hallo Jenkins master.</span><span class="sxs-lookup"><span data-stu-id="cf67d-122">Java JDK and Maven are also required in hello Jenkins master.</span></span> <span data-ttu-id="cf67d-123">tooinstall, tooJenkins master via SSH aanmelden en Voer Hallo volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="cf67d-123">tooinstall, log in tooJenkins master using SSH and run hello following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="cf67d-124">Azure-service principal tooJenkins gebruikersreferentie toevoegen</span><span class="sxs-lookup"><span data-stu-id="cf67d-124">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="cf67d-125">Een Azure-referentie is benodigde tooexecute Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="cf67d-125">An Azure credential is needed tooexecute Azure CLI.</span></span>

* <span data-ttu-id="cf67d-126">Klik in het Hallo Jenkins dashboard op **referenties -> systeem ->**.</span><span class="sxs-lookup"><span data-stu-id="cf67d-126">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="cf67d-127">Klik op **globale credentials(unrestricted)**.</span><span class="sxs-lookup"><span data-stu-id="cf67d-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="cf67d-128">Klik op **toevoegen referenties** tooadd een [Microsoft Azure service-principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) door in te vullen Hallo abonnements-ID, Client-ID, Client Secret en OAuth 2.0-Tokeneindpunt.</span><span class="sxs-lookup"><span data-stu-id="cf67d-128">Click **Add Credentials** tooadd a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="cf67d-129">Geef een ID voor gebruik in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="cf67d-129">Provide an ID for use in subsequent step.</span></span>

![Referenties toevoegen](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a><span data-ttu-id="cf67d-131">Een Azure App Service voor het implementeren van Hallo Java-web-app maken</span><span class="sxs-lookup"><span data-stu-id="cf67d-131">Create an Azure App Service for deploying hello Java web app</span></span>

<span data-ttu-id="cf67d-132">Maken van een Azure App Service-abonnement met Hallo **vrije** prijscategorie Hallo met [az appservice-abonnement maken](/cli/azure/appservice/plan#create) CLI-opdracht.</span><span class="sxs-lookup"><span data-stu-id="cf67d-132">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="cf67d-133">Hallo appservice-abonnement definieert Hallo fysieke resources gebruikt toohost uw apps.</span><span class="sxs-lookup"><span data-stu-id="cf67d-133">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="cf67d-134">Alle toepassingen die toegewezen tooan appservice-abonnement kunt u deze resources, zodat u toosave kosten bij het hosten van meerdere apps delen.</span><span class="sxs-lookup"><span data-stu-id="cf67d-134">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="cf67d-135">Wanneer Hallo plan klaar is, uitvoer hello die Azure CLI ongeveer dezelfde wordt toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="cf67d-135">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="cf67d-136">Een Azure-Web-app maken</span><span class="sxs-lookup"><span data-stu-id="cf67d-136">Create an Azure Web app</span></span>

 <span data-ttu-id="cf67d-137">Gebruik Hallo [az webapp maken](/cli/azure/appservice/web#create) CLI opdracht toocreate de definitie van een web-app in Hallo `myAppServicePlan` App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="cf67d-137">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="cf67d-138">Hallo web app definitie voorziet in uw toepassing met een URL-tooaccess en verschillende opties toodeploy uw code tooAzure configureert.</span><span class="sxs-lookup"><span data-stu-id="cf67d-138">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="cf67d-139">Vervang Hallo `<app_name>` aanduiding voor items met uw eigen unieke app-naam.</span><span class="sxs-lookup"><span data-stu-id="cf67d-139">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="cf67d-140">Deze unieke naam is onderdeel van de standaarddomeinnaam Hallo voor Hallo-web-app Hallo naam moet toobe uniek zijn in alle apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="cf67d-140">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="cf67d-141">U kunt een aangepast domein de naam van vermelding toohello web-app kunt toewijzen, voordat u deze tooyour gebruikers weergeven.</span><span class="sxs-lookup"><span data-stu-id="cf67d-141">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="cf67d-142">Wanneer de definitie van Hallo web apps klaar is, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="cf67d-142">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="cf67d-143">Java configureren</span><span class="sxs-lookup"><span data-stu-id="cf67d-143">Configure Java</span></span> 

<span data-ttu-id="cf67d-144">Hallo Java runtime-configuratie die uw app Hello moet instellen [az appservice web config update](/cli/azure/appservice/web/config#update) opdracht.</span><span class="sxs-lookup"><span data-stu-id="cf67d-144">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="cf67d-145">Hallo volgende opdracht configureert u Hallo web app toorun op een recente Java 8 JDK en [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="cf67d-145">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="cf67d-146">Voorbereiden van een GitHub-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="cf67d-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="cf67d-147">Open Hallo [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample) opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="cf67d-147">Open hello [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="cf67d-148">toofork hello opslagplaats tooyour eigenaar GitHub-account, klikt u op Hallo **Fork** knop in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="cf67d-148">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

* <span data-ttu-id="cf67d-149">Open in de GitHub-webgebruikersinterface, **Jenkinsfile** bestand.</span><span class="sxs-lookup"><span data-stu-id="cf67d-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="cf67d-150">Klik op Hallo pen pictogram tooedit dit bestand tooupdate Hallo resourcegroep en de naam van uw web-app op regel 20 en 21 respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="cf67d-150">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="cf67d-151">Regel 23 tooupdate referentie-ID in uw exemplaar Jenkins wijzigen</span><span class="sxs-lookup"><span data-stu-id="cf67d-151">Change line 23 tooupdate credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="cf67d-152">Jenkins pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="cf67d-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="cf67d-153">Jenkins in een webbrowser openen, klikt u op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="cf67d-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="cf67d-154">Geef een naam voor de taak Hallo en selecteer **pijplijn**.</span><span class="sxs-lookup"><span data-stu-id="cf67d-154">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="cf67d-155">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf67d-155">Click **OK**.</span></span>
* <span data-ttu-id="cf67d-156">Klik op Hallo **pijplijn** volgende tabblad.</span><span class="sxs-lookup"><span data-stu-id="cf67d-156">Click hello **Pipeline** tab next.</span></span> 
* <span data-ttu-id="cf67d-157">Voor **definitie**, selecteer **Pipeline-script uit SCM**.</span><span class="sxs-lookup"><span data-stu-id="cf67d-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="cf67d-158">Voor **SCM**, selecteer **Git**.</span><span class="sxs-lookup"><span data-stu-id="cf67d-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="cf67d-159">Voer Hallo GitHub-URL voor uw opslagplaats Gevorkte: https:\<uw Gevorkte opslagplaats\>.git</span><span class="sxs-lookup"><span data-stu-id="cf67d-159">Enter hello GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="cf67d-160">Klik op **opslaan**</span><span class="sxs-lookup"><span data-stu-id="cf67d-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="cf67d-161">Test uw pijplijn</span><span class="sxs-lookup"><span data-stu-id="cf67d-161">Test your pipeline</span></span>
* <span data-ttu-id="cf67d-162">Ga toohello pijplijn die u hebt gemaakt, klikt u op **nu bouwen**</span><span class="sxs-lookup"><span data-stu-id="cf67d-162">Go toohello pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="cf67d-163">Een build moet slagen binnen een paar seconden en kunt u toohello build gaan en op **Console-uitvoer** toosee Hallo details</span><span class="sxs-lookup"><span data-stu-id="cf67d-163">A build should succeed in a few seconds, and you can go toohello build and click **Console Output** toosee hello details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="cf67d-164">Controleer of uw web-app</span><span class="sxs-lookup"><span data-stu-id="cf67d-164">Verify your web app</span></span>
<span data-ttu-id="cf67d-165">tooverify hello WAR-bestand wordt geïmplementeerd tooyour web-app.</span><span class="sxs-lookup"><span data-stu-id="cf67d-165">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="cf67d-166">Open een webbrowser:</span><span class="sxs-lookup"><span data-stu-id="cf67d-166">Open a web browser:</span></span>

* <span data-ttu-id="cf67d-167">Ga toohttp: / /&lt;app_naam >.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="cf67d-167">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="cf67d-168">U ziet:</span><span class="sxs-lookup"><span data-stu-id="cf67d-168">You see:</span></span>

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="cf67d-169">Ga toohttp: / /&lt;app_naam >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (vervangen door &lt;x > en &lt;y > met willekeurige getallen) tooget Hallo som van de x en y</span><span class="sxs-lookup"><span data-stu-id="cf67d-169">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>

![Rekenmachine: toevoegen](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a><span data-ttu-id="cf67d-171">TooAzure op Linux-Web-App implementeren</span><span class="sxs-lookup"><span data-stu-id="cf67d-171">Deploy tooAzure Web App on Linux</span></span>
<span data-ttu-id="cf67d-172">Nu dat u hoe toouse Azure CLI in uw Jenkins pijplijn weet, kunt u Hallo script toodeploy tooan Azure-Web-App op Linux kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cf67d-172">Now that you know how toouse Azure CLI in your Jenkins pipeline, you can modify hello script toodeploy tooan Azure Web App on Linux.</span></span>

<span data-ttu-id="cf67d-173">Een andere manier toodo Hallo implementatie, die toouse Docker biedt ondersteuning voor Web-App op Linux.</span><span class="sxs-lookup"><span data-stu-id="cf67d-173">Web App on Linux supports a different way toodo hello deployment, which is toouse Docker.</span></span> <span data-ttu-id="cf67d-174">toodeploy, moet u tooprovide een Dockerfile die uw web-app met service runtime worden verpakt in een Docker-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="cf67d-174">toodeploy, you need tooprovide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="cf67d-175">Hallo-invoegtoepassing wordt vervolgens Hallo-installatiekopie bouwen, dit tooa Docker register doorgeven en Hallo installatiekopie tooyour web-app implementeren.</span><span class="sxs-lookup"><span data-stu-id="cf67d-175">hello plugin will then build hello image, push it tooa Docker registry and deploy hello image tooyour web app.</span></span>

* <span data-ttu-id="cf67d-176">Volg de stappen Hallo [hier](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate een Azure-Web-App uitgevoerd op Linux.</span><span class="sxs-lookup"><span data-stu-id="cf67d-176">Follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="cf67d-177">Docker installeren op uw exemplaar Jenkins door Hallo-instructies in dit [artikel](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="cf67d-177">Install Docker on your Jenkins instance by following hello instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="cf67d-178">Maken van een register-Container in hello Azure-portal met behulp van Hallo stappen [hier](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cf67d-178">Create a Container Registry in hello Azure portal by using hello steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="cf67d-179">Hallo in dezelfde [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample) opslagplaats u forked bewerken Hallo **Jenkinsfile2** bestand:</span><span class="sxs-lookup"><span data-stu-id="cf67d-179">In hello same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit hello **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="cf67d-180">Regel 18-21, respectievelijk toohello namen van de resourcegroep, web-app en ACR bijwerken.</span><span class="sxs-lookup"><span data-stu-id="cf67d-180">Line 18-21, update toohello names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="cf67d-181">Regel 24-, update \<azsrvprincipal\> tooyour verwijzings-ID</span><span class="sxs-lookup"><span data-stu-id="cf67d-181">Line 24, update \<azsrvprincipal\> tooyour credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="cf67d-182">Een nieuwe Jenkins pijplijn maken net als bij het implementeren van tooAzure web-app in Windows, alleen deze keer gebruik **Jenkinsfile2** in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="cf67d-182">Create a new Jenkins pipeline as you did when deploying tooAzure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="cf67d-183">Uw nieuwe taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cf67d-183">Run your new job.</span></span>
* <span data-ttu-id="cf67d-184">tooverify, in de Azure CLI uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="cf67d-184">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="cf67d-185">U krijgt Hallo resultaat te volgen:</span><span class="sxs-lookup"><span data-stu-id="cf67d-185">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="cf67d-186">Ga toohttp: / /&lt;app_naam >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="cf67d-186">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="cf67d-187">U ziet het Hallo-bericht:</span><span class="sxs-lookup"><span data-stu-id="cf67d-187">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="cf67d-188">Ga toohttp: / /&lt;app_naam >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (vervangen door &lt;x > en &lt;y > met willekeurige getallen) tooget Hallo som van de x en y</span><span class="sxs-lookup"><span data-stu-id="cf67d-188">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="cf67d-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cf67d-189">Next steps</span></span>
<span data-ttu-id="cf67d-190">In deze zelfstudie maakt u een Jenkins pijplijn die de broncode Hallo in GitHub-repo-uitgecheckt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="cf67d-190">In this tutorial, you configured a Jenkins pipeline that checks out hello source code in GitHub repo.</span></span> <span data-ttu-id="cf67d-191">Maven toobuild voert een war-bestand en gebruikt vervolgens Azure CLI toodeploy tooAzure App Service.</span><span class="sxs-lookup"><span data-stu-id="cf67d-191">Runs Maven toobuild a war file and then uses Azure CLI toodeploy tooAzure App Service.</span></span> <span data-ttu-id="cf67d-192">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="cf67d-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cf67d-193">Maak een VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="cf67d-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="cf67d-194">Jenkins configureren</span><span class="sxs-lookup"><span data-stu-id="cf67d-194">Configure Jenkins</span></span>
> * <span data-ttu-id="cf67d-195">Een web-app maken in Azure</span><span class="sxs-lookup"><span data-stu-id="cf67d-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="cf67d-196">Voorbereiden van een GitHub-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="cf67d-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="cf67d-197">Jenkins pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="cf67d-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="cf67d-198">Hallo pijplijn uitvoeren en controleer of Hallo web-app</span><span class="sxs-lookup"><span data-stu-id="cf67d-198">Run hello pipeline and verify hello web app</span></span>
