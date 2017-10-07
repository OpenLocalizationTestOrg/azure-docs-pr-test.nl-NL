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
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a><span data-ttu-id="0fd1f-103">TooAzure App Service met de invoegtoepassing Jenkins implementeren</span><span class="sxs-lookup"><span data-stu-id="0fd1f-103">Deploy tooAzure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="0fd1f-104">een Java web-app tooAzure toodeploy, kunt u Azure CLI in [Jenkins pijplijn](/azure/jenkins/execute-cli-jenkins-pipeline) of kunt u het gebruik van Hallo [Jenkins van Azure App Service-invoegtoepassing](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="0fd1f-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of hello [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="0fd1f-105">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="0fd1f-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0fd1f-106">Jenkins toodeploy tooAzure App Service via FTP configureren</span><span class="sxs-lookup"><span data-stu-id="0fd1f-106">Configure Jenkins toodeploy tooAzure App Service through FTP</span></span> 
> * <span data-ttu-id="0fd1f-107">Jenkins toodeploy tooAzure App Service configureren op Linux via Docker</span><span class="sxs-lookup"><span data-stu-id="0fd1f-107">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="0fd1f-108">Maak en configureer Jenkins exemplaar</span><span class="sxs-lookup"><span data-stu-id="0fd1f-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="0fd1f-109">Als u nog geen een model Jenkins, begint u met de Hallo [oplossingssjabloon](install-jenkins-solution-template.md), waaronder JDK8 en Hallo vereist plugins te volgen:</span><span class="sxs-lookup"><span data-stu-id="0fd1f-109">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and hello following required plugins:</span></span>

* <span data-ttu-id="0fd1f-110">[De invoegtoepassing client Jenkins Git](https://plugins.jenkins.io/git-client) v.2.4.6</span><span class="sxs-lookup"><span data-stu-id="0fd1f-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="0fd1f-111">[Docker Commons invoegtoepassing](https://plugins.jenkins.io/docker-commons) v.1.4.0</span><span class="sxs-lookup"><span data-stu-id="0fd1f-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="0fd1f-112">[Azure-referenties](https://plugins.jenkins.io/azure-credentials) v.1.2</span><span class="sxs-lookup"><span data-stu-id="0fd1f-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="0fd1f-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span><span class="sxs-lookup"><span data-stu-id="0fd1f-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="0fd1f-114">U kunt Hallo App Service-invoegtoepassing toodeploy Web-App in alle talen (bijvoorbeeld C#, PHP, Java en node.js enz.) wordt ondersteund door Azure App Service kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-114">You can use hello App Service plugin toodeploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="0fd1f-115">In deze zelfstudie gebruiken we Hallo voorbeeld Java-app [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="0fd1f-115">In this tutorial, we are using hello sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="0fd1f-116">toofork hello opslagplaats tooyour eigenaar GitHub-account, klikt u op Hallo **Fork** knop in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-116">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>  

<span data-ttu-id="0fd1f-117">Java-JDK en Maven zijn vereist voor het bouwen van Hallo Java-project.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-117">Java JDK and Maven are required for building hello Java project.</span></span> <span data-ttu-id="0fd1f-118">Zorg ervoor dat u in Hallo Jenkins model of de VM-agent Hallo Hallo-onderdelen installeren als u een continue integratie.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-118">Make sure you install hello components in hello Jenkins master or hello VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="0fd1f-119">tooinstall, meld u bij toohello Jenkins exemplaar met gebruikmaking van SSH en Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="0fd1f-119">tooinstall, log in toohello Jenkins instance using SSH and run hello following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="0fd1f-120">Voor het implementeren van tooApp-Service op Linux, moet u ook tooinstall Docker op Hallo Jenkins master of Hallo VM-agent gebruikt om te worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-120">For deploying tooApp Service on Linux, you also need tooinstall Docker on hello Jenkins master or hello VM agent used for build.</span></span> <span data-ttu-id="0fd1f-121">Raadpleeg toothis artikel tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-121">Refer toothis article tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="0fd1f-122">Azure-service principal tooJenkins gebruikersreferentie toevoegen</span><span class="sxs-lookup"><span data-stu-id="0fd1f-122">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="0fd1f-123">Een Azure-service-principal is benodigde toodeploy tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-123">An Azure service principal is needed toodeploy tooAzure.</span></span> 

<ol>
<li><span data-ttu-id="0fd1f-124">Gebruik [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) of [Azure-portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate een Azure-service-principal</span><span class="sxs-lookup"><span data-stu-id="0fd1f-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate an Azure service principal</span></span></li>
<li><span data-ttu-id="0fd1f-125">Klik in het Hallo Jenkins dashboard op **referenties -> systeem ->**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-125">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="0fd1f-126">Klik op **globale credentials(unrestricted)**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="0fd1f-127">Klik op **toevoegen referenties** tooadd een Microsoft Azure-service-principal door in te vullen Hallo abonnements-ID, Client-ID, Client Secret en OAuth 2.0-Tokeneindpunt.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-127">Click **Add Credentials** tooadd a Microsoft Azure service principal by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="0fd1f-128">Geef een ID **mySp**, voor gebruik in de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="0fd1f-129">Azure App Service-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="0fd1f-129">Azure App Service plugin</span></span>

<span data-ttu-id="0fd1f-130">Azure App Service-invoegtoepassing v1.0 biedt ondersteuning voor doorlopende implementatie tooAzure Web-App via:</span><span class="sxs-lookup"><span data-stu-id="0fd1f-130">Azure App Service plugin v1.0 supports continuous deployment tooAzure Web App through:</span></span>

* <span data-ttu-id="0fd1f-131">GIT en FTP</span><span class="sxs-lookup"><span data-stu-id="0fd1f-131">Git and FTP</span></span>
* <span data-ttu-id="0fd1f-132">Docker voor Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="0fd1f-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a><span data-ttu-id="0fd1f-133">Jenkins toodeploy via FTP met Hallo Jenkins dashboard-Web-App configureren</span><span class="sxs-lookup"><span data-stu-id="0fd1f-133">Configure Jenkins toodeploy Web App through FTP using hello Jenkins dashboard</span></span>

<span data-ttu-id="0fd1f-134">toodeploy uw project tooAzure Web-App kunt u uw build-artefacten (bijvoorbeeld .war bestanden in Java) uploaden met Git- of FTP.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-134">toodeploy your project tooAzure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="0fd1f-135">Voordat u de taak Hallo in Jenkins instelt, moet u een Azure App Service-abonnement en een Web-App voor actieve Hallo Java-app.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-135">Before setting up hello job in Jenkins, you need an Azure App Service plan and a Web App for running hello Java app.</span></span>


1. <span data-ttu-id="0fd1f-136">Maken van een Azure App Service-abonnement met Hallo **vrije** prijscategorie Hallo met [az appservice-abonnement maken](/cli/azure/appservice/plan#create) CLI-opdracht.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-136">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="0fd1f-137">Hallo appservice-abonnement definieert Hallo fysieke resources gebruikt toohost uw apps.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-137">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="0fd1f-138">Alle toepassingen die toegewezen tooan appservice-abonnement kunt u deze resources, zodat u toosave kosten bij het hosten van meerdere apps delen.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-138">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="0fd1f-139">Maak een web-app.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-139">Create a Web App.</span></span> <span data-ttu-id="0fd1f-140">U kunt beide Hallo gebruik [Azure-portal](/azure/app-service-web/web-sites-configure) of gebruik Hallo na Az CLI-opdracht:</span><span class="sxs-lookup"><span data-stu-id="0fd1f-140">You can either use hello [Azure portal](/azure/app-service-web/web-sites-configure) or use hello following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="0fd1f-141">Zorg ervoor dat u Hallo Java runtime-configuratie die uw app moet instellen.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-141">Make sure you set up hello Java runtime configuration that your app needs.</span></span> <span data-ttu-id="0fd1f-142">Hello Azure CLI-opdracht te volgen Hallo web app toorun configureert op een recente Java 8 JDK en [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-142">hello following Azure CLI command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a><span data-ttu-id="0fd1f-143">Hallo Jenkins taak instellen</span><span class="sxs-lookup"><span data-stu-id="0fd1f-143">Set up hello Jenkins job</span></span>


1. <span data-ttu-id="0fd1f-144">Maak een nieuwe **freestyle** project in Jenkins-Dashboard</span><span class="sxs-lookup"><span data-stu-id="0fd1f-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="0fd1f-145">Configureren **Source Code Management** toouse uw lokale fork van [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample) doordat Hallo **opslagplaats URL**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-145">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="0fd1f-146">Bijvoorbeeld: http://github.com/&lt;yourID > / javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="0fd1f-147">Een Build stap toobuild Hallo project met behulp van Maven toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-147">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="0fd1f-148">Dit doen door het toevoegen van een **shell uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="0fd1f-149">Bijvoorbeeld moeten we een extra stap toorename hello *.war-bestand in map tooROOT.war van doel.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-149">For this example, we need an additional step toorename hello *.war file in target folder tooROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="0fd1f-150">Een actie na build toevoegen door te selecteren **een Azure-Web-App publiceren**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="0fd1f-151">Geef, 'mySp', hello Azure service-principal is opgeslagen in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-151">Supply, "mySp", hello Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="0fd1f-152">In **App-configuratie** sectie, kiest u Hallo resource groep en web-app in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-152">In **App Configuration** section, choose hello resource group and web app in your subscription.</span></span> <span data-ttu-id="0fd1f-153">Hallo-invoegtoepassing detecteert automatisch of Hallo Web-App Windows is of Linux-.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-153">hello plugin automatically detects whether hello Web App is Windows or Linux-based.</span></span> <span data-ttu-id="0fd1f-154">Voor een webtoepassing op basis van Windows hello optie 'Bestanden publiceren' wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-154">For a Windows-based Web App, hello option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="0fd1f-155">Vul in Hallo-bestanden die u wilt toodeploy (bijvoorbeeld een war pakket als u Java gebruikt.) Bron- en doelmap zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-155">Fill in hello files you want toodeploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="0fd1f-156">Hallo parameters kunt u de bron en doel mappen toospecify, tijdens het uploaden van bestanden.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-156">hello parameters allow you toospecify source and target folders when uploading files.</span></span> <span data-ttu-id="0fd1f-157">Java-web-app in Azure wordt uitgevoerd in een Tomcat-server.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="0fd1f-158">Zodat u uploaden war-pakket naar de map webapps.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="0fd1f-159">In dit voorbeeld ingesteld **bronmap** te 'als doel' en 'webapps' opgeven voor **doelmap**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-159">For this example, set **Source Directory** too"target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="0fd1f-160">Als u wilt dat toodeploy tooa sleuf dan productie, kunt u ook instellen **sleuf** naam.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-160">If you want toodeploy tooa slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="0fd1f-161">Sla Hallo-project en bouw het.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-161">Save hello project and build it.</span></span> <span data-ttu-id="0fd1f-162">Uw web-app is geïmplementeerd tooAzure wanneer build voltooid is.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-162">Your web app is deployed tooAzure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="0fd1f-163">Web-App via FTP Jenkins pijplijn met implementeren</span><span class="sxs-lookup"><span data-stu-id="0fd1f-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="0fd1f-164">Hallo-invoegtoepassing is-pipeline-klaar.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-164">hello plugin is pipeline-ready.</span></span> <span data-ttu-id="0fd1f-165">U kunt tooa voorbeeld in GitHub-repo-Hallo verwijzen.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-165">You can refer tooa sample in hello GitHub repo.</span></span>

1. <span data-ttu-id="0fd1f-166">Open in de GitHub-webgebruikersinterface, **Jenkinsfile_ftp_plugin** bestand.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="0fd1f-167">Klik op Hallo pen pictogram tooedit dit bestand tooupdate Hallo resourcegroep en de naam van uw web-app op regel 11 en 12 respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-167">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="0fd1f-168">Regel 14 tooupdate referentie-ID in uw exemplaar Jenkins wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-168">Change line 14 tooupdate credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="0fd1f-169">Een pijplijn Jenkins maken</span><span class="sxs-lookup"><span data-stu-id="0fd1f-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="0fd1f-170">Jenkins in een webbrowser openen, klikt u op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="0fd1f-171">Geef een naam voor de taak Hallo en selecteer **pijplijn**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-171">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="0fd1f-172">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-172">Click **OK**.</span></span>
3. <span data-ttu-id="0fd1f-173">Klik op Hallo **pijplijn** volgende tabblad.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-173">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="0fd1f-174">Voor **definitie**, selecteer **Pipeline-script uit SCM**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="0fd1f-175">Voor **SCM**, selecteer **Git**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="0fd1f-176">Voer Hallo GitHub-URL voor uw opslagplaats Gevorkte: https:&lt;uw Gevorkte opslagplaats > .git</span><span class="sxs-lookup"><span data-stu-id="0fd1f-176">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="0fd1f-177">Update **scriptpad** te 'Jenkinsfile_ftp_plugin'</span><span class="sxs-lookup"><span data-stu-id="0fd1f-177">Update **Script Path** too"Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="0fd1f-178">Klik op **opslaan** en Voer Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-178">Click **Save** and run hello job.</span></span>

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a><span data-ttu-id="0fd1f-179">Jenkins toodeploy Web-App op Linux via Docker configureren</span><span class="sxs-lookup"><span data-stu-id="0fd1f-179">Configure Jenkins toodeploy Web App on Linux through Docker</span></span>

<span data-ttu-id="0fd1f-180">Naast Git-/ FTP-, biedt ondersteuning voor Web-App op Linux implementatie met behulp van Docker.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="0fd1f-181">toodeploy met behulp van Docker, moet u tooprovide een Dockerfile die uw web-app met service runtime worden verpakt in een docker-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-181">toodeploy using Docker, you need tooprovide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="0fd1f-182">Vervolgens Hallo invoegtoepassing Hallo image wordt gemaakt, duwt deze tooa docker-register en Hallo installatiekopie tooyour web-app wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-182">Then hello plugin builds hello image, pushes it tooa docker registry and deploys hello image tooyour web app.</span></span>

<span data-ttu-id="0fd1f-183">Web-App op Linux ondersteunt ook traditionele manieren zoals Git en FTP-, maar alleen voor ingebouwde talen (.NET Core, Node.js, PHP en Ruby).</span><span class="sxs-lookup"><span data-stu-id="0fd1f-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="0fd1f-184">Voor andere talen toopackage uw code en service runtime voor de toepassing samen in een docker-installatiekopie en deze kunt docker toodeploy.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-184">For other languages, you need toopackage your application code and service runtime together into a docker image and use docker toodeploy.</span></span>

<span data-ttu-id="0fd1f-185">Voordat u de taak Hallo in Jenkins instelt, moet u een Azure app service op Linux.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-185">Before setting up hello job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="0fd1f-186">Een container-register is ook nodig toostore en beheren van uw persoonlijke installatiekopieën van de Docker-container.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-186">A container registry is also needed toostore and manage your private Docker container images.</span></span> <span data-ttu-id="0fd1f-187">U kunt DockerHub; We gebruiken Azure Container register voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="0fd1f-188">U kunt Hallo stappen [hier](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate een Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="0fd1f-188">You can follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate a Web App on Linux</span></span> 
* <span data-ttu-id="0fd1f-189">Azure Container register is een beheerde [Docker-register] (https://docs.docker.com/registry/) service op basis van Hallo open source Docker register 2.0.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on hello open-source Docker Registry 2.0.</span></span> <span data-ttu-id="0fd1f-190">Stappen Hallo [hier] (/ azure/container-registry/container-registry-get-started-azure-cli) voor meer instructies voor het toodo zodat.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-190">Follow hello steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how toodo so.</span></span> <span data-ttu-id="0fd1f-191">U kunt ook DockerHub gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-191">You can also use DockerHub.</span></span>

### <a name="toodeploy-using-docker"></a><span data-ttu-id="0fd1f-192">toodeploy met behulp van docker:</span><span class="sxs-lookup"><span data-stu-id="0fd1f-192">toodeploy using docker:</span></span>

1. <span data-ttu-id="0fd1f-193">Maak een nieuwe freestyle project in Jenkins-Dashboard.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="0fd1f-194">Configureren **Source Code Management** toouse uw lokale fork van [eenvoudige Java-Web-App voor Azure](https://github.com/azure-devops/javawebappsample) doordat Hallo **opslagplaats URL**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-194">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="0fd1f-195">Bijvoorbeeld: http://github.com/&lt;yourid > / javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="0fd1f-196">Een Build stap toobuild Hallo project met behulp van Maven toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-196">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="0fd1f-197">Dit doen door het toevoegen van een **shell uitvoeren** en voeg Hallo volgende regel in **opdracht**:</span><span class="sxs-lookup"><span data-stu-id="0fd1f-197">Do so by adding an **Execute shell** and add hello following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="0fd1f-198">Een actie na build toevoegen door te selecteren **een Azure-Web-App publiceren**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="0fd1f-199">Geef, **mySp**, hello Azure service-principal is opgeslagen in de vorige stap als Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-199">Supply, **mySp**, hello Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="0fd1f-200">In **App-configuratie** sectie, kiest u Hallo-resourcegroep en een Linux-web-app in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-200">In **App Configuration** section, choose hello resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="0fd1f-201">Kies publiceren via de Docker.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="0fd1f-202">Vul **Dockerfile** pad.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="0fd1f-203">Kunt u de standaard Hallo ' / Dockerfile ' voor **Docker register URL**, supply Hallo indeling https://&lt;myRegistry >. azurecr.io als u gebruikmaakt van Azure Container register.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-203">You can keep hello default "/Dockerfile" For **Docker registry URL**, supply in hello format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="0fd1f-204">Laat dit veld leeg als u DockerHub gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="0fd1f-205">Voor **register referenties**, Hallo-referentie voor hello Azure Container register toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-205">For **Registry credentials**, add hello credential for hello Azure Container Registry.</span></span> <span data-ttu-id="0fd1f-206">U kunt Hallo gebruikersnaam en wachtwoord door het uitvoeren van de volgende opdrachten in de Azure CLI Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-206">You can get hello userid and password by running hello following commands in Azure CLI.</span></span> <span data-ttu-id="0fd1f-207">de eerste opdracht Hallo kunt Hallo administrator-account.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-207">hello first command enables hello administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="0fd1f-208">Hallo docker installatiekopie met de naam en code in **Geavanceerd** tabblad zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-208">hello docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="0fd1f-209">Standaard installatiekopie met de naam is verkregen van de installatiekopie van het Hallo naam die u hebt geconfigureerd in Azure portal (in Docker-Container. de instelling) Hallo-code is gegenereerd op basis van $BUILD_NUMBER.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-209">By default, image name is obtained from hello image name you configured in Azure portal (in Docker Container setting.) hello tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="0fd1f-210">Zorg ervoor dat u de naam van de installatiekopie Hallo opgeven in de Azure-portal of een waarde opgeven voor **Docker-afbeelding** in **Geavanceerd** tabblad. Geef voor dit voorbeeld '&lt;yourRegistry >.azurecr.io/calculator ' voor **Docker-afbeelding** en laat **Docker afbeeldingscode** leeg.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-210">Make sure you specify hello image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="0fd1f-211">Opmerking implementatie mislukt als u ingebouwde Docker installatiekopie instelling gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="0fd1f-212">Zorg ervoor dat u docker config toouse aangepaste installatiekopie in de instelling Docker-Container in Azure-portal wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-212">Make sure you change docker config toouse custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="0fd1f-213">Gebruik bestand uploaden benadering toodeploy voor ingebouwde installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-213">For built-in image, use file upload approach toodeploy.</span></span>
11. <span data-ttu-id="0fd1f-214">Soortgelijke benadering van toofile uploaden, kunt u een andere site dan de productie.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-214">Similar toofile upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="0fd1f-215">Opslaat en bouwt Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-215">Save and build hello project.</span></span> <span data-ttu-id="0fd1f-216">U ziet uw installatiekopie container wordt doorgeschoven, tooyour register en web-app wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-216">You see your container image is pushed tooyour registry and web app is deployed.</span></span>

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="0fd1f-217">TooWeb App op Linux via Jenkins pijplijn met Docker implementeren</span><span class="sxs-lookup"><span data-stu-id="0fd1f-217">Deploy tooWeb App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="0fd1f-218">Open in de GitHub-webgebruikersinterface, **Jenkinsfile_container_plugin** bestand.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="0fd1f-219">Klik op Hallo pen pictogram tooedit dit bestand tooupdate Hallo resourcegroep en de naam van uw web-app op regel 11 en 12 respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-219">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="0fd1f-220">Regel 13 tooyour container Registerserver wijzigen</span><span class="sxs-lookup"><span data-stu-id="0fd1f-220">Change line 13 tooyour container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="0fd1f-221">Regel 16 tooupdate referentie-ID in uw exemplaar Jenkins wijzigen</span><span class="sxs-lookup"><span data-stu-id="0fd1f-221">Change line 16 tooupdate credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="0fd1f-222">Jenkins pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="0fd1f-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="0fd1f-223">Jenkins in een webbrowser openen, klikt u op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="0fd1f-224">Geef een naam voor de taak Hallo en selecteer **pijplijn**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-224">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="0fd1f-225">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-225">Click **OK**.</span></span>
3. <span data-ttu-id="0fd1f-226">Klik op Hallo **pijplijn** volgende tabblad.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-226">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="0fd1f-227">Voor **definitie**, selecteer **Pipeline-script uit SCM**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="0fd1f-228">Voor **SCM**, selecteer **Git**.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="0fd1f-229">Voer Hallo GitHub-URL voor uw opslagplaats Gevorkte: https:&lt;uw Gevorkte opslagplaats > .git</span><span class="sxs-lookup"><span data-stu-id="0fd1f-229">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="0fd1f-230">Update 7, **scriptpad** te 'Jenkinsfile_container_plugin'</span><span class="sxs-lookup"><span data-stu-id="0fd1f-230">7, Update **Script Path** too"Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="0fd1f-231">Klik op **opslaan** en Voer Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-231">Click **Save** and run hello job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="0fd1f-232">Controleer of uw web-app</span><span class="sxs-lookup"><span data-stu-id="0fd1f-232">Verify your web app</span></span>

1. <span data-ttu-id="0fd1f-233">tooverify hello WAR-bestand wordt geïmplementeerd tooyour web-app.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-233">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="0fd1f-234">Open een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-234">Open a web browser.</span></span>
2. <span data-ttu-id="0fd1f-235">Ga toohttp: / /&lt;app_naam >.azurewebsites.net/api/calculator/ping u zien:</span><span class="sxs-lookup"><span data-stu-id="0fd1f-235">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="0fd1f-236">Welkom tooJava Web-App.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-236">Welcome tooJava Web App!!!</span></span> <span data-ttu-id="0fd1f-237">Dit is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-237">This is updated!</span></span>
   <span data-ttu-id="0fd1f-238">Sun Jun 17 16:39:10 UTC 2017</span><span class="sxs-lookup"><span data-stu-id="0fd1f-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="0fd1f-239">Ga toohttp: / /&lt;app_naam >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (vervangen door &lt;x > en &lt;y > met willekeurige getallen) tooget Hallo som van de x en y</span><span class="sxs-lookup"><span data-stu-id="0fd1f-239">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>        
    ![Rekenmachine: toevoegen](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="0fd1f-241">Voor App-service op Linux</span><span class="sxs-lookup"><span data-stu-id="0fd1f-241">For App service on Linux</span></span>

* <span data-ttu-id="0fd1f-242">tooverify, in de Azure CLI uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="0fd1f-242">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="0fd1f-243">U krijgt Hallo resultaat te volgen:</span><span class="sxs-lookup"><span data-stu-id="0fd1f-243">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="0fd1f-244">Ga toohttp: / /&lt;app_naam >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-244">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="0fd1f-245">U ziet het Hallo-bericht:</span><span class="sxs-lookup"><span data-stu-id="0fd1f-245">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="0fd1f-246">Ga toohttp: / /&lt;app_naam >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (vervangen door &lt;x > en &lt;y > met willekeurige getallen) tooget Hallo som van de x en y</span><span class="sxs-lookup"><span data-stu-id="0fd1f-246">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="0fd1f-247">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0fd1f-247">Next steps</span></span>

<span data-ttu-id="0fd1f-248">In deze zelfstudie gebruikt u hello Azure App Service-invoegtoepassing toodeploy tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0fd1f-248">In this tutorial, you use hello Azure App Service plugin toodeploy tooAzure.</span></span>

<span data-ttu-id="0fd1f-249">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="0fd1f-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0fd1f-250">Jenkins toodeploy Azure App Service via FTP configureren</span><span class="sxs-lookup"><span data-stu-id="0fd1f-250">Configure Jenkins toodeploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="0fd1f-251">Jenkins toodeploy tooAzure App Service configureren op Linux via Docker</span><span class="sxs-lookup"><span data-stu-id="0fd1f-251">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 
