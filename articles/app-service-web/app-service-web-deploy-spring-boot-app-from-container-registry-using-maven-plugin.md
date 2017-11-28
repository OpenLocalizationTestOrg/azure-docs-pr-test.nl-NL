---
title: aaaHow toouse hello Maven-invoegtoepassing voor Azure Web Apps toodeploy een versie die voorjaar Boot-app in Azure Container register tooAzure App Service
description: Deze zelfstudie leert u echter Hallo stappen toodeploy een versie die voorjaar Boot-toepassing in Azure Container register tooAzure tooAzure App Service met behulp van een Maven-invoegtoepassing.
services: 
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a><span data-ttu-id="7281c-103">Hoe toouse hello Maven-invoegtoepassing voor Azure Web Apps toodeploy een versie die voorjaar Boot-app in Azure Container register tooAzure App Service</span><span class="sxs-lookup"><span data-stu-id="7281c-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app in Azure Container Registry tooAzure App Service</span></span>

<span data-ttu-id="7281c-104">Hallo  **[Spring Framework]**  is een populaire open-source framework waarmee ontwikkelaars van Java web, mobiel en API-toepassingen maken.</span><span class="sxs-lookup"><span data-stu-id="7281c-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="7281c-105">In deze zelfstudie wordt een voorbeeld-app gemaakt met behulp van [Spring Boot], een conventie voor gestuurde benadering voor het gebruik van Spring tooget snel aan de slag.</span><span class="sxs-lookup"><span data-stu-id="7281c-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="7281c-106">In dit artikel laat zien hoe een voorbeeld Spring opstarten toepassing tooAzure Container register toodeploy, en gebruik hello Maven-invoegtoepassing voor Azure Web Apps toodeploy uw toepassing tooAzure App Service.</span><span class="sxs-lookup"><span data-stu-id="7281c-106">This article demonstrates how toodeploy a sample Spring Boot application tooAzure Container Registry, and then use hello Maven Plugin for Azure Web Apps toodeploy your application tooAzure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="7281c-107">Hallo Maven-invoegtoepassing voor Azure-Web-Apps is momenteel beschikbaar als een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7281c-107">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="7281c-108">Alleen FTP-publicatie wordt nu ondersteund, maar aanvullende functies zijn gepland voor toekomstige Hallo.</span><span class="sxs-lookup"><span data-stu-id="7281c-108">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="7281c-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7281c-109">Prerequisites</span></span>

<span data-ttu-id="7281c-110">In de volgorde toocomplete Hallo stappen in deze zelfstudie moet u toohave Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="7281c-110">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="7281c-111">Een Azure-abonnement; Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee] of zich aanmelden voor een [gratis Azure-account].</span><span class="sxs-lookup"><span data-stu-id="7281c-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="7281c-112">Hallo [Azure-opdrachtregelinterface (CLI)].</span><span class="sxs-lookup"><span data-stu-id="7281c-112">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="7281c-113">Een up-to-date [Java Development Kit (JDK)], versie 1.7 of hoger.</span><span class="sxs-lookup"><span data-stu-id="7281c-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="7281c-114">Apache van [Maven] bouwen tool (versie 3).</span><span class="sxs-lookup"><span data-stu-id="7281c-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="7281c-115">Een [Git] client.</span><span class="sxs-lookup"><span data-stu-id="7281c-115">A [Git] client.</span></span>
* <span data-ttu-id="7281c-116">Een [Docker] client.</span><span class="sxs-lookup"><span data-stu-id="7281c-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="7281c-117">Vanwege toohello virtualisatie vereisten van deze zelfstudie, kan niet u Hallo stappen in dit artikel volgen op een virtuele machine; u moet een fysieke computer gebruiken met virtualisatiefuncties ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="7281c-117">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="7281c-118">Kloon Hallo voorbeeld Spring opstarten op Docker-web-app</span><span class="sxs-lookup"><span data-stu-id="7281c-118">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="7281c-119">In dit gedeelte klonen van een beperkte Spring Boot-toepassing en lokaal testen.</span><span class="sxs-lookup"><span data-stu-id="7281c-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="7281c-120">Open een opdrachtprompt of een terminalvenster en maken van een lokale map toohold uw toepassing Spring opstarten en wijziging toothat directory; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7281c-120">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="7281c-121">-- of--</span><span class="sxs-lookup"><span data-stu-id="7281c-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="7281c-122">Kloon Hallo [Spring opstarten op het Docker aan de slag] voorbeeldproject in Hallo directory die u hebt gemaakt; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7281c-122">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="7281c-123">Wijzigen van de directory toohello voltooid project. bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7281c-123">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="7281c-124">Hallo JAR-bestand met behulp van Maven; bouwen bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7281c-124">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="7281c-125">Wanneer het Hallo-web-app is gemaakt, start u Hallo web-app met behulp van Maven; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7281c-125">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="7281c-126">Hallo-web-app testen door te bladeren tooit lokaal via een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="7281c-126">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="7281c-127">U kunt bijvoorbeeld Hallo volgende opdracht als u curl beschikbaar hebt:</span><span class="sxs-lookup"><span data-stu-id="7281c-127">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="7281c-128">U ziet Hallo volgende bericht wordt weergegeven: **Hallo Docker wereld**</span><span class="sxs-lookup"><span data-stu-id="7281c-128">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Lokaal voorbeeld-App bladeren][SB01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="7281c-130">Een Azure-service-principal maken</span><span class="sxs-lookup"><span data-stu-id="7281c-130">Create an Azure service principal</span></span>

<span data-ttu-id="7281c-131">In deze sectie maakt u een Azure service-principal die Hallo Maven-invoegtoepassing gebruikt bij het implementeren van uw tooAzure container.</span><span class="sxs-lookup"><span data-stu-id="7281c-131">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="7281c-132">Open een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="7281c-132">Open a command prompt.</span></span>

1. <span data-ttu-id="7281c-133">Meld u aan bij uw Azure-account met behulp van Hallo Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="7281c-133">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="7281c-134">Doe Hallo instructies toocomplete Hallo aanmelden.</span><span class="sxs-lookup"><span data-stu-id="7281c-134">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="7281c-135">Een Azure-service-principal maken:</span><span class="sxs-lookup"><span data-stu-id="7281c-135">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="7281c-136">Waar `uuuuuuuu` Hallo-gebruikersnaam en `pppppppp` Hallo wachtwoord voor de service-principal Hallo is.</span><span class="sxs-lookup"><span data-stu-id="7281c-136">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="7281c-137">Azure reageert met JSON dat lijkt op Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="7281c-137">Azure responds with JSON that resembles hello following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="7281c-138">U gebruikt Hallo waarden van deze JSON-antwoord als u uw tooAzure container Hallo Maven-invoegtoepassing toodeploy configureert.</span><span class="sxs-lookup"><span data-stu-id="7281c-138">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="7281c-139">Hallo `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, en `tttttttt` tijdelijke aanduiding voor waarden die worden gebruikt in dit voorbeeld toomake deze eenvoudiger toomap deze waarden tootheir respectieve elementen bij het configureren van uw Maven `settings.xml` bestanden per Hallo naast sectie.</span><span class="sxs-lookup"><span data-stu-id="7281c-139">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="7281c-140">Maken van een Azure Container Registry hello Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="7281c-140">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="7281c-141">Open een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="7281c-141">Open a command prompt.</span></span>

1. <span data-ttu-id="7281c-142">Meld u bij tooyour Azure-account:</span><span class="sxs-lookup"><span data-stu-id="7281c-142">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="7281c-143">Maak een resourcegroep voor hello Azure-resources die gaat u in dit artikel:</span><span class="sxs-lookup"><span data-stu-id="7281c-143">Create a resource group for hello Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="7281c-144">Vervang `wingtiptoysresources` in dit voorbeeld met een unieke naam voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="7281c-144">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="7281c-145">Maak een register persoonlijke Azure-container in Hallo resourcegroep voor uw app Spring opstarten:</span><span class="sxs-lookup"><span data-stu-id="7281c-145">Create a private Azure container registry in hello resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="7281c-146">Vervang `wingtiptoysregistry` in dit voorbeeld met een unieke naam voor de container-register.</span><span class="sxs-lookup"><span data-stu-id="7281c-146">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="7281c-147">Hallo-wachtwoord voor de container-register worden opgehaald:</span><span class="sxs-lookup"><span data-stu-id="7281c-147">Retrieve hello password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="7281c-148">Azure reageert met je wachtwoord; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7281c-148">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a><span data-ttu-id="7281c-149">Uw Azure-container register en de Azure service principal tooyour Maven-instellingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="7281c-149">Add your Azure container registry and Azure service principal tooyour Maven settings</span></span>

1. <span data-ttu-id="7281c-150">Open uw Maven `settings.xml` bestand in een teksteditor; dit bestand is mogelijk in een pad zoals Hallo volgen voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="7281c-150">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="7281c-151">Uw toegang tot Azure Container registerinstellingen toevoegen uit de vorige sectie Hallo van dit artikel toohello `<servers>` verzameling in hello *settings.xml* bestand; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7281c-151">Add your Azure Container Registry access settings from hello previous section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="7281c-152">Waar:</span><span class="sxs-lookup"><span data-stu-id="7281c-152">Where:</span></span>
   <span data-ttu-id="7281c-153">Element</span><span class="sxs-lookup"><span data-stu-id="7281c-153">Element</span></span> | <span data-ttu-id="7281c-154">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7281c-154">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="7281c-155">Hallo-naam van het register persoonlijke Azure-container bevat.</span><span class="sxs-lookup"><span data-stu-id="7281c-155">Contains hello name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="7281c-156">Hallo-naam van het register persoonlijke Azure-container bevat.</span><span class="sxs-lookup"><span data-stu-id="7281c-156">Contains hello name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="7281c-157">Hallo wachtwoord dat u hebt opgehaald in de vorige sectie Hallo van dit artikel bevat.</span><span class="sxs-lookup"><span data-stu-id="7281c-157">Contains hello password you retrieved in hello previous section of this article.</span></span>

1. <span data-ttu-id="7281c-158">Toevoegen van uw Azure-service-principal-instellingen in een eerder gedeelte van dit artikel toohello `<servers>` verzameling in hello *settings.xml* bestand; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7281c-158">Add your Azure service principal settings from an earlier section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="7281c-159">Waar:</span><span class="sxs-lookup"><span data-stu-id="7281c-159">Where:</span></span>
   <span data-ttu-id="7281c-160">Element</span><span class="sxs-lookup"><span data-stu-id="7281c-160">Element</span></span> | <span data-ttu-id="7281c-161">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7281c-161">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="7281c-162">Hiermee geeft u een unieke naam op die Maven toolook van uw beveiligingsinstellingen worden gebruikt wanneer u uw web-app tooAzure implementeert.</span><span class="sxs-lookup"><span data-stu-id="7281c-162">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="7281c-163">Hallo bevat `appId` waarde van uw service-principal.</span><span class="sxs-lookup"><span data-stu-id="7281c-163">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="7281c-164">Hallo bevat `tenant` waarde van uw service-principal.</span><span class="sxs-lookup"><span data-stu-id="7281c-164">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="7281c-165">Hallo bevat `password` waarde van uw service-principal.</span><span class="sxs-lookup"><span data-stu-id="7281c-165">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="7281c-166">Hallo doel-Azure-cloudomgeving, die definieert `AZURE` in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7281c-166">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="7281c-167">(Een volledige lijst met omgevingen is beschikbaar in Hallo [Maven-invoegtoepassing voor Azure-Web-Apps] documentatie)</span><span class="sxs-lookup"><span data-stu-id="7281c-167">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="7281c-168">Opslaan en sluiten Hallo *settings.xml* bestand.</span><span class="sxs-lookup"><span data-stu-id="7281c-168">Save and close hello *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a><span data-ttu-id="7281c-169">Uw Docker-container-installatiekopie maken en dit tooyour Azure container register doorgeven</span><span class="sxs-lookup"><span data-stu-id="7281c-169">Build your Docker container image and push it tooyour Azure container registry</span></span>

1. <span data-ttu-id="7281c-170">Navigeer projectmap toohello voltooid voor uw toepassing Spring opstarten (bijvoorbeeld) "*C:\SpringBoot\gs-spring-boot-docker\complete*"of"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*'), en open Hallo *pom.xml* het bestand met een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="7281c-170">Navigate toohello completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="7281c-171">Update Hallo `<properties>` verzameling in hello *pom.xml* -bestand met Hallo aanmelding serverwaarde voor uw Azure-Container register uit de vorige sectie Hallo van deze zelfstudie; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7281c-171">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="7281c-172">Waar:</span><span class="sxs-lookup"><span data-stu-id="7281c-172">Where:</span></span>
   <span data-ttu-id="7281c-173">Element</span><span class="sxs-lookup"><span data-stu-id="7281c-173">Element</span></span> | <span data-ttu-id="7281c-174">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7281c-174">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="7281c-175">Hiermee geeft u Hallo-naam van het register persoonlijke Azure-container.</span><span class="sxs-lookup"><span data-stu-id="7281c-175">Specifies hello name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="7281c-176">Hallo-URL van het register persoonlijke Azure-container, die is afgeleid door toe te voegen '. azurecr.io ' toohello-naam van het register privé-container.</span><span class="sxs-lookup"><span data-stu-id="7281c-176">Specifies hello URL of your private Azure container registry, which is derived by appending ".azurecr.io" toohello name of your private container registry.</span></span>

1. <span data-ttu-id="7281c-177">Controleer `<plugin>` voor Hallo Docker-invoegtoepassing in uw *pom.xml* bestand bevat de juiste eigenschappen Hallo voor Hallo-server en het register aanmeldingsnaam van de vorige stap Hallo in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7281c-177">Verify that `<plugin>` for hello Docker plugin in your *pom.xml* file contains hello correct properties for hello login server address and registry name from hello previous step in this tutorial.</span></span> <span data-ttu-id="7281c-178">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7281c-178">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   <span data-ttu-id="7281c-179">Waar:</span><span class="sxs-lookup"><span data-stu-id="7281c-179">Where:</span></span>
   <span data-ttu-id="7281c-180">Element</span><span class="sxs-lookup"><span data-stu-id="7281c-180">Element</span></span> | <span data-ttu-id="7281c-181">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7281c-181">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="7281c-182">Hiermee geeft u Hallo-eigenschap met de naam van het register persoonlijke Azure-container.</span><span class="sxs-lookup"><span data-stu-id="7281c-182">Specifies hello property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="7281c-183">Hiermee geeft u Hallo-eigenschap die Hallo-URL van het register persoonlijke Azure-container bevat.</span><span class="sxs-lookup"><span data-stu-id="7281c-183">Specifies hello property which contains hello URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="7281c-184">Navigeer projectmap toohello voltooid voor uw toepassing Spring opstarten en uitvoeren na opdracht toorebuild Hallo toepassing hello en push Hallo container tooyour Azure container register:</span><span class="sxs-lookup"><span data-stu-id="7281c-184">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="7281c-185">Optioneel: Bladeren toohello [Azure-portal] en controleer of er een installatiekopie van Docker-container met de naam **gs-spring-boot-docker** in het register van de container.</span><span class="sxs-lookup"><span data-stu-id="7281c-185">OPTIONAL: Browse toohello [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Controleer of de container in Azure-portal][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a><span data-ttu-id="7281c-187">Uw pom.xml aanpassen en vervolgens te bouwen en implementeren van uw tooAzure container</span><span class="sxs-lookup"><span data-stu-id="7281c-187">Customize your pom.xml, then build and deploy your container tooAzure</span></span>

<span data-ttu-id="7281c-188">Open Hallo `pom.xml` bestand voor uw toepassing Spring opstarten in een teksteditor en zoek vervolgens Hallo `<plugin>` element voor `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="7281c-188">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="7281c-189">Dit element moet eruitzien als Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="7281c-189">This element should resemble hello following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="7281c-190">Er zijn verschillende waarden die u voor Hallo Maven-invoegtoepassing wijzigen kunt en een gedetailleerde beschrijving in voor elk van deze elementen is beschikbaar in Hallo [Maven-invoegtoepassing voor Azure-Web-Apps] documentatie.</span><span class="sxs-lookup"><span data-stu-id="7281c-190">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="7281c-191">Die wordt aangegeven, er zijn verschillende waarden die waard markeren in dit artikel zijn:</span><span class="sxs-lookup"><span data-stu-id="7281c-191">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="7281c-192">Element</span><span class="sxs-lookup"><span data-stu-id="7281c-192">Element</span></span> | <span data-ttu-id="7281c-193">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7281c-193">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="7281c-194">Hiermee geeft u de versie Hallo Hallo [Maven-invoegtoepassing voor Azure-Web-Apps].</span><span class="sxs-lookup"><span data-stu-id="7281c-194">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="7281c-195">Controleer Hallo-versie die worden vermeld in Hallo [Maven centrale opslagplaats](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure die u gebruikt Hallo meest recente versie.</span><span class="sxs-lookup"><span data-stu-id="7281c-195">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="7281c-196">Hiermee geeft u op Hallo verificatie-informatie voor Azure, die in dit voorbeeld bevat een `<serverId>` element met `azure-auth`; Maven maakt gebruik van die waarde toolook hello Azure-service-principal waarden in uw Maven *settings.xml* bestand, dat u hebt gedefinieerd in een eerdere sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="7281c-196">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="7281c-197">Hiermee geeft u op Hallo doelresourcegroep, die `wingtiptoysresources` in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7281c-197">Specifies hello target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="7281c-198">Hallo resourcegroep wordt gemaakt tijdens de implementatie als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="7281c-198">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="7281c-199">Hiermee geeft u de doelnaam Hallo voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="7281c-199">Specifies hello target name for your web app.</span></span> <span data-ttu-id="7281c-200">In dit voorbeeld is de naam van Hallo doel `maven-linux-app-${maven.build.timestamp}`, waarbij hello `${maven.build.timestamp}` achtervoegsel wordt toegevoegd in dit voorbeeld tooavoid conflict.</span><span class="sxs-lookup"><span data-stu-id="7281c-200">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="7281c-201">(Hallo tijdstempel is optioneel, kunt u een unieke tekenreeks voor de naam van de app Hallo.)</span><span class="sxs-lookup"><span data-stu-id="7281c-201">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="7281c-202">Hiermee geeft u de doelregio hello, die in dit voorbeeld is `westus`.</span><span class="sxs-lookup"><span data-stu-id="7281c-202">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="7281c-203">(Een volledige lijst is in Hallo [Maven-invoegtoepassing voor Azure-Web-Apps] documentatie.)</span><span class="sxs-lookup"><span data-stu-id="7281c-203">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="7281c-204">Hiermee geeft u Hallo-eigenschappen die Hallo naam en de URL van de container bevatten.</span><span class="sxs-lookup"><span data-stu-id="7281c-204">Specifies hello properties which contain hello name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="7281c-205">Hiermee geeft u een unieke instellingen voor Maven toouse bij het implementeren van uw web-app tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7281c-205">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="7281c-206">In dit voorbeeld wordt een `<property>` element bevat een naam/waarde-paar van onderliggende elementen die Hallo-poort voor uw app opgeven.</span><span class="sxs-lookup"><span data-stu-id="7281c-206">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="7281c-207">Hallo instellingen toochange Hallo-poortnummer in dit voorbeeld zijn alleen nodig als u poort Hallo van Hallo standaardwaarde wijzigt.</span><span class="sxs-lookup"><span data-stu-id="7281c-207">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

1. <span data-ttu-id="7281c-208">Opnieuw samenstellen Hallo JAR-bestand met behulp van Maven, als u toohello wijzigingen aangebracht van Hallo-opdrachtprompt of terminalvenster die u eerder gebruikte *pom.xml* bestand; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7281c-208">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="7281c-209">Uw web-app tooAzure implementeren met behulp van Maven; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7281c-209">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="7281c-210">Maven implementeert uw web-app tooAzure; Als het Hallo-web-app niet al bestaat, wordt deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7281c-210">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="7281c-211">Als Hallo regio die u in Hallo opgeeft `<region>` element van uw *pom.xml* bestand beschikt niet over voldoende beschikbare servers wanneer u de implementatie start, ziet u mogelijk een foutbericht vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="7281c-211">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="7281c-212">Als dit gebeurt, kunt u dat een andere regio en Voer Hallo Maven-opdracht toodeploy uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7281c-212">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="7281c-213">Wanneer uw web-is geïmplementeerd, kunt u zich kunt toomanage deze met behulp van Hallo [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="7281c-213">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="7281c-214">Uw web-app wordt weergegeven in **App Services**:</span><span class="sxs-lookup"><span data-stu-id="7281c-214">Your web app will be listed in **App Services**:</span></span>

   ![Web-app die worden vermeld in Azure-portal App Services][AP01]

* <span data-ttu-id="7281c-216">En Hallo URL voor uw web-app wordt weergegeven in Hallo **overzicht** voor uw web-app:</span><span class="sxs-lookup"><span data-stu-id="7281c-216">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Hallo-URL voor uw web-app te bepalen][AP02]

## <a name="next-steps"></a><span data-ttu-id="7281c-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7281c-218">Next steps</span></span>

<span data-ttu-id="7281c-219">Verschillende technologieën die worden beschreven in dit artikel, Zie voor meer informatie over Hallo Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7281c-219">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="7281c-220">[Maven-invoegtoepassing voor Azure-Web-Apps]</span><span class="sxs-lookup"><span data-stu-id="7281c-220">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="7281c-221">Meld u bij tooAzure van hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7281c-221">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="7281c-222">Een Azure-service-principal maken met Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7281c-222">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="7281c-223">Naslaginformatie over maven</span><span class="sxs-lookup"><span data-stu-id="7281c-223">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="7281c-224">[Maven docker-invoegtoepassing]</span><span class="sxs-lookup"><span data-stu-id="7281c-224">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure-opdrachtregelinterface (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure-portal]: https://portal.azure.com/
[Maven-invoegtoepassing voor Azure-Web-Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Maven docker-invoegtoepassing]: https://github.com/spotify/docker-maven-plugin
[gratis Azure-account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[voordelen als MSDN-abonnee]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring opstarten op het Docker aan de slag]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
