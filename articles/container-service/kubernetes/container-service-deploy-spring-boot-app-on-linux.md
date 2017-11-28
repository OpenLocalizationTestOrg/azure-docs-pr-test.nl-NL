---
title: een versie die voorjaar opstarten Web-App op Linux in Azure Container Service aaaDeploy | Microsoft Docs
description: Deze zelfstudie wordt u echter Hallo stappen toodeploy een toepassing Spring opstarten als een Linux-web-app in Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2c44be1c7f66a38f48239001f0be9e90c7e6edef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a><span data-ttu-id="6b55f-103">Een toepassing Spring opstarten op Linux in hello Azure Container Service implementeren</span><span class="sxs-lookup"><span data-stu-id="6b55f-103">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>

<span data-ttu-id="6b55f-104">Hallo  **[Spring Framework]**  is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken.</span><span class="sxs-lookup"><span data-stu-id="6b55f-104">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="6b55f-105">Een meer populaire Hallo-projecten die is gebaseerd op deze platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6b55f-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="6b55f-106">**[Docker]**  is open source-oplossingen waarmee ontwikkelaars automatiseren Hallo-implementatie, schaalbaarheid en beheer van hun toepassingen die worden uitgevoerd in containers.</span><span class="sxs-lookup"><span data-stu-id="6b55f-106">**[Docker]** is open-source solutions that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="6b55f-107">In deze zelfstudie leert u met behulp van Docker toodevelop en implementeren van een versie die voorjaar opstarten toepassing tooa Linux-host in Hallo [Azure Container Service (ACS)].</span><span class="sxs-lookup"><span data-stu-id="6b55f-107">This tutorial walks you through using Docker toodevelop and deploy a Spring Boot application tooa Linux host in hello [Azure Container Service (ACS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b55f-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6b55f-108">Prerequisites</span></span>

<span data-ttu-id="6b55f-109">In de volgorde toocomplete Hallo stappen in deze zelfstudie moet u toohave Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="6b55f-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="6b55f-110">Een Azure-abonnement; Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee] of zich aanmelden voor een [gratis Azure-account].</span><span class="sxs-lookup"><span data-stu-id="6b55f-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="6b55f-111">Hallo [Azure-opdrachtregelinterface (CLI)].</span><span class="sxs-lookup"><span data-stu-id="6b55f-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="6b55f-112">Een up-to-date [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="6b55f-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="6b55f-113">Apache van [Maven] bouwen tool (versie 3).</span><span class="sxs-lookup"><span data-stu-id="6b55f-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="6b55f-114">Een [Git] client.</span><span class="sxs-lookup"><span data-stu-id="6b55f-114">A [Git] client.</span></span>
* <span data-ttu-id="6b55f-115">Een [Docker] client.</span><span class="sxs-lookup"><span data-stu-id="6b55f-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="6b55f-116">Vanwege toohello virtualisatie vereisten van deze zelfstudie, kan niet u Hallo stappen in dit artikel volgen op een virtuele machine; u moet een fysieke computer gebruiken met virtualisatiefuncties ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6b55f-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="6b55f-117">Hallo Spring opstarten op Docker aan de slag web-app maken</span><span class="sxs-lookup"><span data-stu-id="6b55f-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="6b55f-118">Hallo doorlopen volgt u Hallo stappen die vereist toocreate een eenvoudige webtoepassing voor Spring opstarten en lokaal testen.</span><span class="sxs-lookup"><span data-stu-id="6b55f-118">hello following steps walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="6b55f-119">Open een opdrachtprompt en maken van een lokale map toohold uw toepassing en de wijziging toothat directory; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6b55f-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="6b55f-120">-- of--</span><span class="sxs-lookup"><span data-stu-id="6b55f-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="6b55f-121">Kloon Hallo [Spring opstarten op het Docker aan de slag] voorbeeldproject in Hallo directory die u hebt gemaakt; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6b55f-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="6b55f-122">Wijzigen van de directory toohello voltooid project. bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6b55f-122">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="6b55f-123">Hallo JAR-bestand met behulp van Maven; bouwen bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6b55f-123">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="6b55f-124">Zodra het Hallo-web-app is gemaakt, verandert directory toohello `target` directory waar Hallo JAR-bestand zich bevindt en Hallo web-app starten bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6b55f-124">Once hello web app has been created, change directory toohello `target` directory where hello JAR file is located and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="6b55f-125">Hallo-web-app testen door te bladeren tooit lokaal via een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="6b55f-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="6b55f-126">Bijvoorbeeld, als u curl beschikbaar en u geconfigureerd Hallo Tomcat-server toorun op poort 80:</span><span class="sxs-lookup"><span data-stu-id="6b55f-126">For example, if you have curl available and you configured hello Tomcat server toorun on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="6b55f-127">U ziet Hallo volgende bericht wordt weergegeven: **Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="6b55f-127">You should see hello following message displayed: **Hello Docker World!**</span></span>

   ![Lokaal voorbeeld-App bladeren][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a><span data-ttu-id="6b55f-129">Maak een Azure Container register toouse als een persoonlijke Docker-register</span><span class="sxs-lookup"><span data-stu-id="6b55f-129">Create an Azure Container Registry toouse as a Private Docker Registry</span></span>

<span data-ttu-id="6b55f-130">Hallo doorlopen volgende stappen Hallo toocreate met Azure portal een Azure Container Registry gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6b55f-130">hello following steps walk you through using hello Azure portal toocreate an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="6b55f-131">Als u wilt dat toouse hello Azure CLI in plaats van hello Azure-portal, stappen Hallo in [maken van een persoonlijke Docker-container register met behulp van Azure CLI 2.0 Hallo](../../container-registry/container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6b55f-131">If you want toouse hello Azure CLI instead of hello Azure portal, follow hello steps in [Create a private Docker container registry using hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span></span>
>

1. <span data-ttu-id="6b55f-132">Blader toohello [Azure-portal] en meld u aan.</span><span class="sxs-lookup"><span data-stu-id="6b55f-132">Browse toohello [Azure portal] and sign in.</span></span>

   <span data-ttu-id="6b55f-133">Wanneer u bent aangemeld in tooyour-account op Hallo Azure-portal, u kunt stappen Hallo in Hallo [maken van een persoonlijke Docker-container register hello Azure-portal met] artikel, dat in de volgende stappen uit voor Hallo Hallo zijn paraphrased verjaardagen praktische.</span><span class="sxs-lookup"><span data-stu-id="6b55f-133">Once you have signed in tooyour account on hello Azure portal, you can follow hello steps in hello [Create a private Docker container registry using hello Azure portal] article, which are paraphrased in hello following steps for hello sake of expediency.</span></span>

1. <span data-ttu-id="6b55f-134">Klik op Hallo menupictogram voor **+ nieuw**, klikt u vervolgens op **Containers**, en klik vervolgens op **Azure Container register**.</span><span class="sxs-lookup"><span data-stu-id="6b55f-134">Click hello menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Maak een nieuwe Azure-Container register][AR01]

1. <span data-ttu-id="6b55f-136">Wanneer de informatiepagina Hallo voor hello Azure Container register sjabloon wordt weergegeven, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="6b55f-136">When hello information page for hello Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Maak een nieuwe Azure-Container register][AR02]

1. <span data-ttu-id="6b55f-138">Wanneer Hallo **maken container register** pagina wordt weergegeven, voert u uw **naam van Routeringsregister** en **resourcegroep**, kies **inschakelen** voor Hallo **gebruiker met beheerdersrechten**, en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="6b55f-138">When hello **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for hello **Admin user**, and then click **Create**.</span></span>

   ![Azure-Container registerinstellingen configureren][AR03]

1. <span data-ttu-id="6b55f-140">Zodra het register van de container is gemaakt, gaat u tooyour container register in hello Azure-portal en klik vervolgens op **toegangstoetsen**.</span><span class="sxs-lookup"><span data-stu-id="6b55f-140">Once your container registry has been created, navigate tooyour container registry in hello Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="6b55f-141">Let op het Hallo-gebruikersnaam en wachtwoord voor de volgende stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="6b55f-141">Take note of hello username and password for hello next steps.</span></span>

   ![Azure Container toegang registersleutels][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a><span data-ttu-id="6b55f-143">Uw toegang tot Azure Container registersleutels Maven toouse configureren</span><span class="sxs-lookup"><span data-stu-id="6b55f-143">Configure Maven toouse your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="6b55f-144">Navigeer toohello configuratiemap voor uw installatie Maven en open Hallo *settings.xml* bestand met een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="6b55f-144">Navigate toohello configuration directory for your Maven installation and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="6b55f-145">Uw toegang tot Azure Container registerinstellingen toevoegen uit de vorige sectie Hallo van deze zelfstudie toohello `<servers>` verzameling in hello *settings.xml* bestand; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6b55f-145">Add your Azure Container Registry access settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="6b55f-146">Navigeer projectmap toohello voltooid voor uw toepassing Spring opstarten (bijvoorbeeld: '*C:\SpringBoot\gs-spring-boot-docker\complete*"of"*/users/robert/SpringBoot/gs-spring-boot-docker / volledige*'), en open Hallo *pom.xml* bestand met een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="6b55f-146">Navigate toohello completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="6b55f-147">Update Hallo `<properties>` verzameling in hello *pom.xml* -bestand met Hallo aanmelding serverwaarde voor uw Azure-Container register uit de vorige sectie Hallo van deze zelfstudie; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6b55f-147">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="6b55f-148">Update Hallo `<plugins>` verzameling in hello *pom.xml* bestand die Hallo `<plugin>` Hallo aanmelding adres en het register servernaam voor uw Azure-Container register uit de vorige sectie Hallo van deze zelfstudie bevat.</span><span class="sxs-lookup"><span data-stu-id="6b55f-148">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry from hello previous section of this tutorial.</span></span> <span data-ttu-id="6b55f-149">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6b55f-149">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. <span data-ttu-id="6b55f-150">Navigeer projectmap toohello voltooid voor uw toepassing Spring opstarten en uitgevoerd na opdracht toorebuild Hallo toepassing hello en push Hallo container tooyour Azure Container register:</span><span class="sxs-lookup"><span data-stu-id="6b55f-150">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="6b55f-151">Wanneer u uw tooAzure Docker-container worden gepusht, verschijnt er een foutbericht weergegeven dat vergelijkbaar tooone van Hallo volgen, ondanks dat de Docker-container is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="6b55f-151">When you are pushing your Docker container tooAzure, you may receive an error message that is similar tooone of hello following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="6b55f-152">Als dit gebeurt, moet u mogelijk toosign in tooyour Azure-account van Hallo Docker-opdrachtregel; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6b55f-152">If this happens, you may need toosign in tooyour Azure account from hello Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="6b55f-153">U kunt vervolgens de container push vanaf de opdrachtregel Hallo; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6b55f-153">You can then push your container from hello command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="6b55f-154">Een web-app maken in Linux op Azure App Service met behulp van de installatiekopie van de container</span><span class="sxs-lookup"><span data-stu-id="6b55f-154">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="6b55f-155">Blader toohello [Azure-portal] en meld u aan.</span><span class="sxs-lookup"><span data-stu-id="6b55f-155">Browse toohello [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="6b55f-156">Klik op Hallo menupictogram voor **+ nieuw**, klikt u vervolgens op **Web en mobiel**, en klik vervolgens op **Web-App op Linux**.</span><span class="sxs-lookup"><span data-stu-id="6b55f-156">Click hello menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Een nieuwe WebApp maken in hello Azure-portal][LX01]

1. <span data-ttu-id="6b55f-158">Wanneer Hallo **Web-App op Linux** pagina wordt weergegeven, voert u Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="6b55f-158">When hello **Web App on Linux** page is displayed, enter hello following information:</span></span>

   <span data-ttu-id="6b55f-159">a.</span><span class="sxs-lookup"><span data-stu-id="6b55f-159">a.</span></span> <span data-ttu-id="6b55f-160">Geef een unieke naam voor Hallo **appnaam**; bijvoorbeeld: '*wingtiptoyslinux*. "</span><span class="sxs-lookup"><span data-stu-id="6b55f-160">Enter a unique name for hello **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="6b55f-161">b.</span><span class="sxs-lookup"><span data-stu-id="6b55f-161">b.</span></span> <span data-ttu-id="6b55f-162">Kies uw **abonnement** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="6b55f-162">Choose your **Subscription** from hello drop-down list.</span></span>

   <span data-ttu-id="6b55f-163">c.</span><span class="sxs-lookup"><span data-stu-id="6b55f-163">c.</span></span> <span data-ttu-id="6b55f-164">Kies een bestaande **resourcegroep**, of geef een naam toocreate een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="6b55f-164">Choose an existing **Resource Group**, or specify a name toocreate a new resource group.</span></span>

   <span data-ttu-id="6b55f-165">d.</span><span class="sxs-lookup"><span data-stu-id="6b55f-165">d.</span></span> <span data-ttu-id="6b55f-166">Klik op **configureren container** en voer de volgende informatie Hallo:</span><span class="sxs-lookup"><span data-stu-id="6b55f-166">Click **Configure container** and enter hello following information:</span></span>

      * <span data-ttu-id="6b55f-167">Kies **persoonlijke register**.</span><span class="sxs-lookup"><span data-stu-id="6b55f-167">Choose **Private registry**.</span></span>

      * <span data-ttu-id="6b55f-168">**Installatiekopie en optionele tag**: Geef de containernaam van uw van eerder; bijvoorbeeld: '*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*'</span><span class="sxs-lookup"><span data-stu-id="6b55f-168">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="6b55f-169">**Server-URL**: Geef de URL van het register van eerder; bijvoorbeeld: '*https://wingtiptoysregistry.azurecr.io*'</span><span class="sxs-lookup"><span data-stu-id="6b55f-169">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="6b55f-170">**Gebruikersnaam voor aanmelding** en **wachtwoord**: Geef de referenties van uw **toegangstoetsen** die u gebruikt in de vorige stappen.</span><span class="sxs-lookup"><span data-stu-id="6b55f-170">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="6b55f-171">e.</span><span class="sxs-lookup"><span data-stu-id="6b55f-171">e.</span></span> <span data-ttu-id="6b55f-172">Nadat u alle Hallo boven de gegevens hebt ingevoerd, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6b55f-172">Once you have entered all of hello above information, click **OK**.</span></span>

   ![Instellingen voor web-app configureren][LX02]

1. <span data-ttu-id="6b55f-174">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6b55f-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="6b55f-175">Azure Internet aanvragen tooembedded Tomcat-server die wordt uitgevoerd op de standaardpoorten Hallo van 80 of 8080 automatisch toegewezen.</span><span class="sxs-lookup"><span data-stu-id="6b55f-175">Azure will automatically map Internet requests tooembedded Tomcat server that is running on hello standard ports of 80 or 8080.</span></span> <span data-ttu-id="6b55f-176">Als u uw ingesloten toorun van de Tomcat-server op een aangepaste poort geconfigureerd, moet u tooadd een omgeving variabele tooyour web-app die Hallo-poort voor de ingesloten Tomcat-server definieert.</span><span class="sxs-lookup"><span data-stu-id="6b55f-176">However, if you configured your embedded Tomcat server toorun on a custom port, you need tooadd an environment variable tooyour web app that defines hello port for your embedded Tomcat server.</span></span> <span data-ttu-id="6b55f-177">toodo gebruik dus Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6b55f-177">toodo so, use hello following steps:</span></span>
>
> 1. <span data-ttu-id="6b55f-178">Blader toohello [Azure-portal] en meld u aan.</span><span class="sxs-lookup"><span data-stu-id="6b55f-178">Browse toohello [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="6b55f-179">Klik op het pictogram voor Hallo **App Services**.</span><span class="sxs-lookup"><span data-stu-id="6b55f-179">Click hello icon for **App Services**.</span></span> <span data-ttu-id="6b55f-180">(Zie artikel #1 in onderstaande afbeelding voor Hallo.)</span><span class="sxs-lookup"><span data-stu-id="6b55f-180">(See item #1 in hello image below.)</span></span>
>
> 3. <span data-ttu-id="6b55f-181">Selecteer uw web-app in Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="6b55f-181">Select your web app from hello list.</span></span> <span data-ttu-id="6b55f-182">(Item #2 in onderstaande afbeelding voor Hallo.)</span><span class="sxs-lookup"><span data-stu-id="6b55f-182">(Item #2 in hello image below.)</span></span>
>
> 4. <span data-ttu-id="6b55f-183">Klik op **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="6b55f-183">Click **Application Settings**.</span></span> <span data-ttu-id="6b55f-184">(Item #3 in onderstaande afbeelding voor Hallo.)</span><span class="sxs-lookup"><span data-stu-id="6b55f-184">(Item #3 in hello image below.)</span></span>
>
> 5. <span data-ttu-id="6b55f-185">In Hallo **appinstellingen** sectie, het toevoegen van een nieuwe omgevingsvariabele met de naam **poort** en voer het nummer van uw aangepaste poort voor Hallo-waarde.</span><span class="sxs-lookup"><span data-stu-id="6b55f-185">In hello **App settings** section, add a new environment variable named **PORT** and enter your custom port number for hello value.</span></span> <span data-ttu-id="6b55f-186">(Item #4 in onderstaande afbeelding voor Hallo.)</span><span class="sxs-lookup"><span data-stu-id="6b55f-186">(Item #4 in hello image below.)</span></span>
>
> 6. <span data-ttu-id="6b55f-187">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6b55f-187">Click **Save**.</span></span> <span data-ttu-id="6b55f-188">(Item #5 in onderstaande afbeelding voor Hallo.)</span><span class="sxs-lookup"><span data-stu-id="6b55f-188">(Item #5 in hello image below.)</span></span>
>
> ![Opslaan van een aangepast poortnummer in hello Azure-portal][LX03]
>

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="6b55f-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6b55f-190">Next steps</span></span>

<span data-ttu-id="6b55f-191">Zie voor meer informatie over het gebruik van opstarten Spring toepassingen in Azure Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6b55f-191">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="6b55f-192">Een versie die voorjaar opstarten toepassing toohello Azure App Service implementeren</span><span class="sxs-lookup"><span data-stu-id="6b55f-192">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="6b55f-193">Een toepassing Spring opstarten op een Kubernetes Cluster in hello Azure Container Service implementeren</span><span class="sxs-lookup"><span data-stu-id="6b55f-193">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="6b55f-194">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="6b55f-194">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="6b55f-195">Zie voor meer informatie over Hallo Spring opstarten op Docker-voorbeeldproject [Spring opstarten op het Docker aan de slag].</span><span class="sxs-lookup"><span data-stu-id="6b55f-195">For further details about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="6b55f-196">Zie voor meer informatie over aan de slag met uw eigen toepassingen Spring opstarten, Hallo **Spring Initializr** op https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="6b55f-196">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="6b55f-197">Zie voor meer informatie over het aan de slag met het maken van een eenvoudige Spring Boot-toepassing hello Spring Initializr op https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="6b55f-197">For more information about getting started with creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="6b55f-198">Zie voor meer voorbeelden van hoe toouse aangepaste Docker met Azure afbeeldingen [met een aangepaste Docker-installatiekopie voor Azure-Web-App op Linux].</span><span class="sxs-lookup"><span data-stu-id="6b55f-198">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure-opdrachtregelinterface (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure-portal]: https://portal.azure.com/
[maken van een persoonlijke Docker-container register hello Azure-portal met]: /azure/container-registry/container-registry-get-started-portal
[met een aangepaste Docker-installatiekopie voor Azure-Web-App op Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[gratis Azure-account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[voordelen als MSDN-abonnee]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring opstarten op het Docker aan de slag]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-linux/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-linux/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-linux/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-linux/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-linux/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-linux/AR04.png

[LX01]: ./media/container-service-deploy-spring-boot-app-on-linux/LX01.png
[LX02]: ./media/container-service-deploy-spring-boot-app-on-linux/LX02.png
[LX03]: ./media/container-service-deploy-spring-boot-app-on-linux/LX03.png
