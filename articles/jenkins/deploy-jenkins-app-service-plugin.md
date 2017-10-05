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
# <a name="deploy-to-azure-app-service-with-jenkins-plugin"></a><span data-ttu-id="8b4b1-103">Implementeren in Azure App Service met Jenkins-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="8b4b1-103">Deploy to Azure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="8b4b1-104">Als u wilt een Java-web-app implementeren in Azure, kunt u Azure CLI in [Jenkins pijplijn](/azure/jenkins/execute-cli-jenkins-pipeline) of kunt u het gebruik van de [invoegtoepassing van Azure App Service Jenkins](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="8b4b1-104">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of the [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="8b4b1-105">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="8b4b1-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8b4b1-106">Jenkins implementeren in Azure App Service via FTP configureren</span><span class="sxs-lookup"><span data-stu-id="8b4b1-106">Configure Jenkins to deploy to Azure App Service through FTP</span></span> 
> * <span data-ttu-id="8b4b1-107">Jenkins implementeren in Azure App Service op Linux via Docker configureren</span><span class="sxs-lookup"><span data-stu-id="8b4b1-107">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="8b4b1-108">Maak en configureer Jenkins exemplaar</span><span class="sxs-lookup"><span data-stu-id="8b4b1-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="8b4b1-109">Als u nog geen een model Jenkins, begint u met de [oplossingssjabloon](install-jenkins-solution-template.md), waaronder JDK8 en de volgende vereiste invoegtoepassingen:</span><span class="sxs-lookup"><span data-stu-id="8b4b1-109">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and the following required plugins:</span></span>

* <span data-ttu-id="8b4b1-110">[De invoegtoepassing client Jenkins Git](https://plugins.jenkins.io/git-client) v.2.4.6</span><span class="sxs-lookup"><span data-stu-id="8b4b1-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="8b4b1-111">[Docker Commons invoegtoepassing](https://plugins.jenkins.io/docker-commons) v.1.4.0</span><span class="sxs-lookup"><span data-stu-id="8b4b1-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="8b4b1-112">[Azure-referenties](https://plugins.jenkins.io/azure-credentials) v.1.2</span><span class="sxs-lookup"><span data-stu-id="8b4b1-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="8b4b1-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span><span class="sxs-lookup"><span data-stu-id="8b4b1-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="8b4b1-114">De App Service-invoegtoepassing kunt u Web-App implementeren in alle talen (bijvoorbeeld C#, PHP, Java en node.js enz.) wordt ondersteund door Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-114">You can use the App Service plugin to deploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="8b4b1-115">In deze zelfstudie gebruiken we de Java voorbeeldapp [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="8b4b1-115">In this tutorial, we are using the sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="8b4b1-116">Om te vertakken de opslagplaats op uw eigen GitHub-account, klikt u op de **Fork** knop in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-116">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>  

<span data-ttu-id="8b4b1-117">Java-JDK en Maven zijn vereist voor het bouwen van de Java-project.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-117">Java JDK and Maven are required for building the Java project.</span></span> <span data-ttu-id="8b4b1-118">Zorg ervoor dat u de onderdelen in het model Jenkins of de VM-agent installeren als u een continue integratie.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-118">Make sure you install the components in the Jenkins master or the VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="8b4b1-119">Als u wilt installeren, aanmelden bij het gebruik van SSH Jenkins-exemplaar en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="8b4b1-119">To install, log in to the Jenkins instance using SSH and run the following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="8b4b1-120">Voor op Linux-App Service-implementatie, moet u ook Docker installeren op de master Jenkins of de VM-agent gebruikt om te worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-120">For deploying to App Service on Linux, you also need to install Docker on the Jenkins master or the VM agent used for build.</span></span> <span data-ttu-id="8b4b1-121">Raadpleeg dit artikel voor het installeren van Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-121">Refer to this article to install Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="8b4b1-122">Azure-service-principal tot Jenkins referentie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8b4b1-122">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="8b4b1-123">Een Azure-service-principal is nodig om te implementeren in Azure.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-123">An Azure service principal is needed to deploy to Azure.</span></span> 

<ol>
<li><span data-ttu-id="8b4b1-124">Gebruik [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) of [Azure-portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) een Azure-service-principal maken</span><span class="sxs-lookup"><span data-stu-id="8b4b1-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) to create an Azure service principal</span></span></li>
<li><span data-ttu-id="8b4b1-125">Klik in het dashboard Jenkins op **referenties -> systeem ->**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-125">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="8b4b1-126">Klik op **globale credentials(unrestricted)**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="8b4b1-127">Klik op **referenties toevoegen** toevoegen van een Microsoft Azure service-principal met de abonnements-ID, de Client-ID, het Clientgeheim en de OAuth 2.0-Tokeneindpunt invullen.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-127">Click **Add Credentials** to add a Microsoft Azure service principal by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="8b4b1-128">Geef een ID **mySp**, voor gebruik in de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="8b4b1-129">Azure App Service-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="8b4b1-129">Azure App Service plugin</span></span>

<span data-ttu-id="8b4b1-130">Azure App Service-invoegtoepassing v1.0 biedt ondersteuning voor continue implementatie naar Azure-Web-App via:</span><span class="sxs-lookup"><span data-stu-id="8b4b1-130">Azure App Service plugin v1.0 supports continuous deployment to Azure Web App through:</span></span>

* <span data-ttu-id="8b4b1-131">GIT en FTP</span><span class="sxs-lookup"><span data-stu-id="8b4b1-131">Git and FTP</span></span>
* <span data-ttu-id="8b4b1-132">Docker voor Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="8b4b1-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-to-deploy-web-app-through-ftp-using-the-jenkins-dashboard"></a><span data-ttu-id="8b4b1-133">Jenkins voor het implementeren van Web-App via met het dashboard Jenkins FTP configureren</span><span class="sxs-lookup"><span data-stu-id="8b4b1-133">Configure Jenkins to deploy Web App through FTP using the Jenkins dashboard</span></span>

<span data-ttu-id="8b4b1-134">Als u wilt uw project op Azure-Web-App implementeert, kunt u uw build-artefacten (bijvoorbeeld .war bestanden in Java) uploaden met Git- of FTP.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-134">To deploy your project to Azure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="8b4b1-135">Voordat u de taak in Jenkins instelt, moet u een Azure App Service-abonnement en een Web-App voor het uitvoeren van de Java-app.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-135">Before setting up the job in Jenkins, you need an Azure App Service plan and a Web App for running the Java app.</span></span>


1. <span data-ttu-id="8b4b1-136">Maken van een Azure App Service-abonnement met de **vrije** prijzen met behulp van laag de [az appservice-abonnement maken](/cli/azure/appservice/plan#create) CLI-opdracht.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-136">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="8b4b1-137">Het plan appservice definieert de fysieke resources gebruikt voor het hosten van uw apps.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-137">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="8b4b1-138">Alle toepassingen die zijn toegewezen aan een appservice-abonnement kunt u deze resources, zodat u kosten opslaan bij het hosten van meerdere apps delen.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-138">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="8b4b1-139">Maak een web-app.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-139">Create a Web App.</span></span> <span data-ttu-id="8b4b1-140">Kunt u ofwel de [Azure-portal](/azure/app-service-web/web-sites-configure) of gebruik de volgende Az CLI-opdracht:</span><span class="sxs-lookup"><span data-stu-id="8b4b1-140">You can either use the [Azure portal](/azure/app-service-web/web-sites-configure) or use the following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="8b4b1-141">Zorg ervoor dat u de Java runtime-configuratie die uw app moet instellen.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-141">Make sure you set up the Java runtime configuration that your app needs.</span></span> <span data-ttu-id="8b4b1-142">De volgende opdracht in de Azure CLI configureert u de web-app uit te voeren op een recente Java 8 JDK en [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-142">The following Azure CLI command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-the-jenkins-job"></a><span data-ttu-id="8b4b1-143">De taak Jenkins instellen</span><span class="sxs-lookup"><span data-stu-id="8b4b1-143">Set up the Jenkins job</span></span>


1. <span data-ttu-id="8b4b1-144">Maak een nieuwe **freestyle** project in Jenkins-Dashboard</span><span class="sxs-lookup"><span data-stu-id="8b4b1-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="8b4b1-145">Configureren **Source Code Management** gebruik van uw lokale fork van [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample) doordat de **opslagplaats URL**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-145">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="8b4b1-146">Bijvoorbeeld: http://github.com/&lt;yourID > / javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="8b4b1-147">Een stap Build bouw het project met behulp van Maven toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-147">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="8b4b1-148">Dit doen door het toevoegen van een **shell uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="8b4b1-149">In dit voorbeeld moet een aanvullende stap in de naam van het bestand *.war in doelmap ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-149">For this example, we need an additional step to rename the *.war file in target folder to ROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="8b4b1-150">Een actie na build toevoegen door te selecteren **een Azure-Web-App publiceren**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="8b4b1-151">Geef, 'mySp', de Azure service-principal die is opgeslagen in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-151">Supply, "mySp", the Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="8b4b1-152">In **App-configuratie** sectie, kiest u de resource-groep en web-app in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-152">In **App Configuration** section, choose the resource group and web app in your subscription.</span></span> <span data-ttu-id="8b4b1-153">De invoegtoepassing detecteert automatisch of de Web-App van Windows is of Linux-.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-153">The plugin automatically detects whether the Web App is Windows or Linux-based.</span></span> <span data-ttu-id="8b4b1-154">Voor een Windows gebaseerde Web-App de optie "bestanden publiceren' weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-154">For a Windows-based Web App, the option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="8b4b1-155">Vul in de bestanden die u wilt implementeren (bijvoorbeeld, een pakket war als u Java gebruikt.) Bron- en doelmap zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-155">Fill in the files you want to deploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="8b4b1-156">De parameters kunnen u mappen bron en doel opgeven tijdens het uploaden van bestanden.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-156">The parameters allow you to specify source and target folders when uploading files.</span></span> <span data-ttu-id="8b4b1-157">Java-web-app in Azure wordt uitgevoerd in een Tomcat-server.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="8b4b1-158">Zodat u uploaden war-pakket naar de map webapps.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="8b4b1-159">In dit voorbeeld ingesteld **bronmap** 'doelgroep' en 'webapps' opgeven voor **doelmap**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-159">For this example, set **Source Directory** to "target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="8b4b1-160">Als u implementeren in een sleuf dan productie wilt, kunt u ook instellen **sleuf** naam.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-160">If you want to deploy to a slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="8b4b1-161">Sla het project en bouw het.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-161">Save the project and build it.</span></span> <span data-ttu-id="8b4b1-162">Uw web-app wordt geïmplementeerd op Azure als build voltooid is.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-162">Your web app is deployed to Azure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="8b4b1-163">Web-App via FTP Jenkins pijplijn met implementeren</span><span class="sxs-lookup"><span data-stu-id="8b4b1-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="8b4b1-164">De invoegtoepassing is-pipeline-klaar.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-164">The plugin is pipeline-ready.</span></span> <span data-ttu-id="8b4b1-165">U kunt verwijzen naar een voorbeeld van een in de GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-165">You can refer to a sample in the GitHub repo.</span></span>

1. <span data-ttu-id="8b4b1-166">Open in de GitHub-webgebruikersinterface, **Jenkinsfile_ftp_plugin** bestand.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="8b4b1-167">Klik op het potloodpictogram om dit bestand voor het bijwerken van de resourcegroep en de naam van uw web-app op regel 11 en 12 respectievelijk te bewerken.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-167">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="8b4b1-168">Wijzig de regel 14 verwijzings-ID in uw exemplaar Jenkins bijwerken.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-168">Change line 14 to update credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="8b4b1-169">Een pijplijn Jenkins maken</span><span class="sxs-lookup"><span data-stu-id="8b4b1-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="8b4b1-170">Jenkins in een webbrowser openen, klikt u op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="8b4b1-171">Geef een naam op voor de taak en selecteer **pijplijn**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-171">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="8b4b1-172">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-172">Click **OK**.</span></span>
3. <span data-ttu-id="8b4b1-173">Klik op de **pijplijn** volgende tabblad.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-173">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="8b4b1-174">Voor **definitie**, selecteer **Pipeline-script uit SCM**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="8b4b1-175">Voor **SCM**, selecteer **Git**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="8b4b1-176">Geef de GitHub-URL voor uw opslagplaats Gevorkte: https:&lt;uw Gevorkte opslagplaats > .git</span><span class="sxs-lookup"><span data-stu-id="8b4b1-176">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="8b4b1-177">Update **pad Script** naar 'Jenkinsfile_ftp_plugin'</span><span class="sxs-lookup"><span data-stu-id="8b4b1-177">Update **Script Path** to "Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="8b4b1-178">Klik op **opslaan** en voer de taak.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-178">Click **Save** and run the job.</span></span>

## <a name="configure-jenkins-to-deploy-web-app-on-linux-through-docker"></a><span data-ttu-id="8b4b1-179">Jenkins als u wilt implementeren op Linux via de Docker-Web-App configureren</span><span class="sxs-lookup"><span data-stu-id="8b4b1-179">Configure Jenkins to deploy Web App on Linux through Docker</span></span>

<span data-ttu-id="8b4b1-180">Naast Git-/ FTP-, biedt ondersteuning voor Web-App op Linux implementatie met behulp van Docker.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="8b4b1-181">Als u wilt implementeren met behulp van Docker, moet u een Dockerfile die uw web-app met service runtime worden verpakt in een docker-installatiekopie opgeven.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-181">To deploy using Docker, you need to provide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="8b4b1-182">Vervolgens de invoegtoepassing voor de installatiekopie is gebaseerd, duwt deze met een docker-register en implementeert de installatiekopie naar uw web-app.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-182">Then the plugin builds the image, pushes it to a docker registry and deploys the image to your web app.</span></span>

<span data-ttu-id="8b4b1-183">Web-App op Linux ondersteunt ook traditionele manieren zoals Git en FTP-, maar alleen voor ingebouwde talen (.NET Core, Node.js, PHP en Ruby).</span><span class="sxs-lookup"><span data-stu-id="8b4b1-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="8b4b1-184">Voor andere talen moet u uw toepassing en de service een runtime-pakket samen in een docker-installatiekopie en docker gebruiken om te implementeren.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-184">For other languages, you need to package your application code and service runtime together into a docker image and use docker to deploy.</span></span>

<span data-ttu-id="8b4b1-185">Voordat u de taak in Jenkins instelt, moet u een Azure app service op Linux.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-185">Before setting up the job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="8b4b1-186">Een container-register is ook nodig opslaan en beheren van uw persoonlijke installatiekopieën van de Docker-container.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-186">A container registry is also needed to store and manage your private Docker container images.</span></span> <span data-ttu-id="8b4b1-187">U kunt DockerHub; We gebruiken Azure Container register voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="8b4b1-188">U kunt de stappen [hier](/azure/app-service-web/app-service-linux-how-to-create-web-app) voor het maken van een Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="8b4b1-188">You can follow the steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) to create a Web App on Linux</span></span> 
* <span data-ttu-id="8b4b1-189">Azure Container register is een beheerde [Docker-register] (https://docs.docker.com/registry/) service op basis van de open source Docker register 2.0.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on the open-source Docker Registry 2.0.</span></span> <span data-ttu-id="8b4b1-190">Volg de stappen [hier] (/ azure/container-registry/container-registry-get-started-azure-cli) voor meer instructies voor het om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-190">Follow the steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how to do so.</span></span> <span data-ttu-id="8b4b1-191">U kunt ook DockerHub gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-191">You can also use DockerHub.</span></span>

### <a name="to-deploy-using-docker"></a><span data-ttu-id="8b4b1-192">Implementeren met behulp van docker:</span><span class="sxs-lookup"><span data-stu-id="8b4b1-192">To deploy using docker:</span></span>

1. <span data-ttu-id="8b4b1-193">Maak een nieuwe freestyle project in Jenkins-Dashboard.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="8b4b1-194">Configureren **Source Code Management** gebruik van uw lokale fork van [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample) doordat de **opslagplaats URL**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-194">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="8b4b1-195">Bijvoorbeeld: http://github.com/&lt;yourid > / javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="8b4b1-196">Een stap Build bouw het project met behulp van Maven toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-196">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="8b4b1-197">Dit doen door het toevoegen van een **shell uitvoeren** en voeg de volgende regel in **opdracht**:</span><span class="sxs-lookup"><span data-stu-id="8b4b1-197">Do so by adding an **Execute shell** and add the following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="8b4b1-198">Een actie na build toevoegen door te selecteren **een Azure-Web-App publiceren**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="8b4b1-199">Geef, **mySp**, de Azure service-principal die is opgeslagen in de vorige stap als Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-199">Supply, **mySp**, the Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="8b4b1-200">In **App-configuratie** sectie, kiest u de resourcegroep en een Linux-web-app in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-200">In **App Configuration** section, choose the resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="8b4b1-201">Kies publiceren via de Docker.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="8b4b1-202">Vul **Dockerfile** pad.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="8b4b1-203">U kunt de standaardinstelling behouden ' / Dockerfile ' voor **Docker register URL**, in de indeling van https:// supply&lt;myRegistry >. azurecr.io als u gebruikmaakt van Azure Container register.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-203">You can keep the default "/Dockerfile" For **Docker registry URL**, supply in the format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="8b4b1-204">Laat dit veld leeg als u DockerHub gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="8b4b1-205">Voor **register referenties**, de referentie voor het register Azure-Container toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-205">For **Registry credentials**, add the credential for the Azure Container Registry.</span></span> <span data-ttu-id="8b4b1-206">U kunt de gebruikersnaam en wachtwoord ophalen met de volgende opdrachten in de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-206">You can get the userid and password by running the following commands in Azure CLI.</span></span> <span data-ttu-id="8b4b1-207">De eerste opdracht kunt het administrator-account.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-207">The first command enables the administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="8b4b1-208">De docker installatiekopie met de naam en code in **Geavanceerd** tabblad zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-208">The docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="8b4b1-209">Standaard wordt installatiekopie met de naam opgehaald uit de naam van de installatiekopie die u hebt geconfigureerd in Azure-portal (in Docker-Container-instelling.) De code is gegenereerd op basis van $BUILD_NUMBER.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-209">By default, image name is obtained from the image name you configured in Azure portal (in Docker Container setting.) The tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="8b4b1-210">Zorg ervoor dat u de naam van de installatiekopie opgeven in de Azure-portal of een waarde opgeven voor **Docker-afbeelding** in **Geavanceerd** tabblad. Geef voor dit voorbeeld '&lt;yourRegistry >.azurecr.io/calculator ' voor **Docker-afbeelding** en laat **Docker afbeeldingscode** leeg.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-210">Make sure you specify the image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="8b4b1-211">Opmerking implementatie mislukt als u ingebouwde Docker installatiekopie instelling gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="8b4b1-212">Zorg ervoor dat u docker-configuratie voor het gebruik van aangepaste installatiekopie in de instelling Docker-Container in Azure-portal wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-212">Make sure you change docker config to use custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="8b4b1-213">Gebruik voor ingebouwde installatiekopie bestand uploaden aanpak om te implementeren.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-213">For built-in image, use file upload approach to deploy.</span></span>
11. <span data-ttu-id="8b4b1-214">Net als bij benadering van bestand uploaden, kunt u een andere site dan de productie.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-214">Similar to file upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="8b4b1-215">Sla en bouw het project.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-215">Save and build the project.</span></span> <span data-ttu-id="8b4b1-216">U ziet uw installatiekopie container wordt doorgeschoven, toe aan het register en web-app wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-216">You see your container image is pushed to your registry and web app is deployed.</span></span>

### <a name="deploy-to-web-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="8b4b1-217">Implementeren naar Web-App op Linux via Jenkins pijplijn met Docker</span><span class="sxs-lookup"><span data-stu-id="8b4b1-217">Deploy to Web App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="8b4b1-218">Open in de GitHub-webgebruikersinterface, **Jenkinsfile_container_plugin** bestand.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="8b4b1-219">Klik op het potloodpictogram om dit bestand voor het bijwerken van de resourcegroep en de naam van uw web-app op regel 11 en 12 respectievelijk te bewerken.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-219">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="8b4b1-220">Regel 13 wijzigen in de container register-server</span><span class="sxs-lookup"><span data-stu-id="8b4b1-220">Change line 13 to your container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="8b4b1-221">Wijzig regel 16 verwijzings-ID in uw exemplaar Jenkins bijwerken</span><span class="sxs-lookup"><span data-stu-id="8b4b1-221">Change line 16 to update credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="8b4b1-222">Jenkins pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="8b4b1-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="8b4b1-223">Jenkins in een webbrowser openen, klikt u op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="8b4b1-224">Geef een naam op voor de taak en selecteer **pijplijn**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-224">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="8b4b1-225">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-225">Click **OK**.</span></span>
3. <span data-ttu-id="8b4b1-226">Klik op de **pijplijn** volgende tabblad.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-226">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="8b4b1-227">Voor **definitie**, selecteer **Pipeline-script uit SCM**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="8b4b1-228">Voor **SCM**, selecteer **Git**.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="8b4b1-229">Geef de GitHub-URL voor uw opslagplaats Gevorkte: https:&lt;uw Gevorkte opslagplaats > .git</span><span class="sxs-lookup"><span data-stu-id="8b4b1-229">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="8b4b1-230">Update 7, **pad Script** naar 'Jenkinsfile_container_plugin'</span><span class="sxs-lookup"><span data-stu-id="8b4b1-230">7, Update **Script Path** to "Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="8b4b1-231">Klik op **opslaan** en voer de taak.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-231">Click **Save** and run the job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="8b4b1-232">Controleer of uw web-app</span><span class="sxs-lookup"><span data-stu-id="8b4b1-232">Verify your web app</span></span>

1. <span data-ttu-id="8b4b1-233">Om te controleren of het WAR-bestand is geïmplementeerd in uw web-app.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-233">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="8b4b1-234">Open een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-234">Open a web browser.</span></span>
2. <span data-ttu-id="8b4b1-235">Ga naar http://&lt;app_naam >.azurewebsites.net/api/calculator/ping u zien:</span><span class="sxs-lookup"><span data-stu-id="8b4b1-235">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="8b4b1-236">Welkom bij de Java-Web-App.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-236">Welcome to Java Web App!!!</span></span> <span data-ttu-id="8b4b1-237">Dit is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-237">This is updated!</span></span>
   <span data-ttu-id="8b4b1-238">Sun Jun 17 16:39:10 UTC 2017</span><span class="sxs-lookup"><span data-stu-id="8b4b1-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="8b4b1-239">Ga naar http://&lt;app_naam >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (vervangen door &lt;x > en &lt;y > met willekeurige getallen) om op te halen van de som van de x en y</span><span class="sxs-lookup"><span data-stu-id="8b4b1-239">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>        
    ![Rekenmachine: toevoegen](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="8b4b1-241">Voor App-service op Linux</span><span class="sxs-lookup"><span data-stu-id="8b4b1-241">For App service on Linux</span></span>

* <span data-ttu-id="8b4b1-242">Om te controleren, in de Azure CLI uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8b4b1-242">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="8b4b1-243">U krijgen het volgende resultaat:</span><span class="sxs-lookup"><span data-stu-id="8b4b1-243">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="8b4b1-244">Ga naar http://&lt;app_naam >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-244">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="8b4b1-245">U ziet het bericht:</span><span class="sxs-lookup"><span data-stu-id="8b4b1-245">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="8b4b1-246">Ga naar http://&lt;app_naam >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (vervangen door &lt;x > en &lt;y > met willekeurige getallen) om op te halen van de som van de x en y</span><span class="sxs-lookup"><span data-stu-id="8b4b1-246">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="8b4b1-247">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8b4b1-247">Next steps</span></span>

<span data-ttu-id="8b4b1-248">In deze zelfstudie kunt u de invoegtoepassing van Azure App Service implementeren in Azure.</span><span class="sxs-lookup"><span data-stu-id="8b4b1-248">In this tutorial, you use the Azure App Service plugin to deploy to Azure.</span></span>

<span data-ttu-id="8b4b1-249">U leert hoe naar:</span><span class="sxs-lookup"><span data-stu-id="8b4b1-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8b4b1-250">Jenkins voor het implementeren van Azure App Service via FTP configureren</span><span class="sxs-lookup"><span data-stu-id="8b4b1-250">Configure Jenkins to deploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="8b4b1-251">Jenkins implementeren in Azure App Service op Linux via Docker configureren</span><span class="sxs-lookup"><span data-stu-id="8b4b1-251">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 