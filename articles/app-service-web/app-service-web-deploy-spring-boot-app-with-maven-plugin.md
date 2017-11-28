---
title: aaaHow toouse hello Maven-invoegtoepassing voor Azure Web Apps toodeploy een tooAzure Spring Boot-app
description: Meer informatie over hoe toouse hello Maven-invoegtoepassing voor Azure Web Apps toodeploy een tooAzure Spring Boot-app.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a><span data-ttu-id="40a76-103">Hoe toouse hello Maven-invoegtoepassing voor Azure Web Apps toodeploy een tooAzure Spring Boot-app</span><span class="sxs-lookup"><span data-stu-id="40a76-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure</span></span>

<span data-ttu-id="40a76-104">Hallo [Maven-invoegtoepassing voor Azure-Web-Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) voor [Apache Maven](http://maven.apache.org/) biedt naadloze integratie van Azure App Service met Maven-projecten en stroomlijnt het Hallo-proces voor ontwikkelaars toodeploy web-apps tooAzure App Service.</span><span class="sxs-lookup"><span data-stu-id="40a76-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service.</span></span>

<span data-ttu-id="40a76-105">Dit artikel wordt gedemonstreerd met behulp van Hallo Maven-invoegtoepassing voor Azure Web Apps toodeploy een voorbeeld Spring opstarten toepassing tooAzure App-Services.</span><span class="sxs-lookup"><span data-stu-id="40a76-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="40a76-106">Hallo Maven-invoegtoepassing voor Azure-Web-Apps is momenteel beschikbaar als een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="40a76-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="40a76-107">Alleen FTP-publicatie wordt nu ondersteund, maar aanvullende functies zijn gepland voor toekomstige Hallo.</span><span class="sxs-lookup"><span data-stu-id="40a76-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="40a76-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="40a76-108">Prerequisites</span></span>

<span data-ttu-id="40a76-109">In de volgorde toocomplete Hallo stappen in deze zelfstudie moet u toohave Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="40a76-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="40a76-110">Een Azure-abonnement; Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee] of zich aanmelden voor een [gratis Azure-account].</span><span class="sxs-lookup"><span data-stu-id="40a76-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="40a76-111">Hallo [Azure-opdrachtregelinterface (CLI)].</span><span class="sxs-lookup"><span data-stu-id="40a76-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="40a76-112">Een up-to-date [Java Development Kit (JDK)], versie 1.7 of hoger.</span><span class="sxs-lookup"><span data-stu-id="40a76-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="40a76-113">Apache van [Maven] bouwen tool (versie 3).</span><span class="sxs-lookup"><span data-stu-id="40a76-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="40a76-114">Een [Git] client.</span><span class="sxs-lookup"><span data-stu-id="40a76-114">A [Git] client.</span></span>

## <a name="clone-hello-sample-spring-boot-web-app"></a><span data-ttu-id="40a76-115">Kloon Hallo voorbeeld Spring opstarten web-app</span><span class="sxs-lookup"><span data-stu-id="40a76-115">Clone hello sample Spring Boot web app</span></span>

<span data-ttu-id="40a76-116">In dit gedeelte klonen van een voltooide Spring Boot-toepassing en lokaal testen.</span><span class="sxs-lookup"><span data-stu-id="40a76-116">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="40a76-117">Open een opdrachtprompt of een terminalvenster en maken van een lokale map toohold uw toepassing Spring opstarten en wijziging toothat directory; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="40a76-117">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="40a76-118">-- of--</span><span class="sxs-lookup"><span data-stu-id="40a76-118">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="40a76-119">Kloon Hallo [Spring opstarten aan de slag] voorbeeldproject in Hallo directory die u hebt gemaakt; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="40a76-119">Clone hello [Spring Boot Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="40a76-120">Wijzigen van de directory toohello voltooid project. bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="40a76-120">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="40a76-121">Hallo JAR-bestand met behulp van Maven; bouwen bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="40a76-121">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="40a76-122">Wanneer het Hallo-web-app is gemaakt, start u Hallo web-app met behulp van Maven; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="40a76-122">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="40a76-123">Hallo-web-app testen door te bladeren tooit lokaal via een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="40a76-123">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="40a76-124">U kunt bijvoorbeeld Hallo volgende opdracht als u curl beschikbaar hebt:</span><span class="sxs-lookup"><span data-stu-id="40a76-124">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="40a76-125">U ziet Hallo volgende bericht wordt weergegeven: **begroetingen vanaf Spring opstart!**</span><span class="sxs-lookup"><span data-stu-id="40a76-125">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="40a76-126">Een Azure-service-principal maken</span><span class="sxs-lookup"><span data-stu-id="40a76-126">Create an Azure service principal</span></span>

<span data-ttu-id="40a76-127">In deze sectie maakt u een Azure service-principal die Hallo Maven-invoegtoepassing gebruikt bij het implementeren van uw web-app tooAzure.</span><span class="sxs-lookup"><span data-stu-id="40a76-127">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="40a76-128">Open een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="40a76-128">Open a command prompt.</span></span>

1. <span data-ttu-id="40a76-129">Meld u aan bij uw Azure-account met behulp van Hallo Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="40a76-129">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="40a76-130">Doe Hallo instructies toocomplete Hallo aanmelden.</span><span class="sxs-lookup"><span data-stu-id="40a76-130">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="40a76-131">Een Azure-service-principal maken:</span><span class="sxs-lookup"><span data-stu-id="40a76-131">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="40a76-132">Waar `uuuuuuuu` Hallo-gebruikersnaam en `pppppppp` Hallo wachtwoord voor de service-principal Hallo is.</span><span class="sxs-lookup"><span data-stu-id="40a76-132">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="40a76-133">Azure reageert met JSON dat lijkt op Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="40a76-133">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="40a76-134">U gebruikt Hallo waarden van deze JSON-antwoord als u uw web-app tooAzure hello Maven-invoegtoepassing toodeploy configureert.</span><span class="sxs-lookup"><span data-stu-id="40a76-134">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your web app tooAzure.</span></span> <span data-ttu-id="40a76-135">Hallo `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, en `tttttttt` tijdelijke aanduiding voor waarden die worden gebruikt in dit voorbeeld toomake deze eenvoudiger toomap deze waarden tootheir respectieve elementen bij het configureren van uw Maven `settings.xml` bestanden per Hallo naast sectie.</span><span class="sxs-lookup"><span data-stu-id="40a76-135">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="40a76-136">Uw Azure-service-principal voor Maven toouse configureren</span><span class="sxs-lookup"><span data-stu-id="40a76-136">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="40a76-137">In deze sectie kunt u Hallo waarden van uw Azure-service principal tooconfigure Hallo authentication Maven gebruikt bij het implementeren van uw web-app tooAzure gebruiken.</span><span class="sxs-lookup"><span data-stu-id="40a76-137">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="40a76-138">Open uw Maven `settings.xml` bestand in een teksteditor; dit bestand is mogelijk in een pad zoals Hallo volgen voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="40a76-138">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="40a76-139">Toevoegen van uw Azure-service-principal-instellingen van de vorige sectie Hallo van deze zelfstudie toohello `<servers>` verzameling in hello *settings.xml* bestand; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="40a76-139">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="40a76-140">Waar:</span><span class="sxs-lookup"><span data-stu-id="40a76-140">Where:</span></span>
   <span data-ttu-id="40a76-141">Element</span><span class="sxs-lookup"><span data-stu-id="40a76-141">Element</span></span> | <span data-ttu-id="40a76-142">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="40a76-142">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="40a76-143">Hiermee geeft u een unieke naam op die Maven toolook van uw beveiligingsinstellingen worden gebruikt wanneer u uw web-app tooAzure implementeert.</span><span class="sxs-lookup"><span data-stu-id="40a76-143">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="40a76-144">Hallo bevat `appId` waarde van uw service-principal.</span><span class="sxs-lookup"><span data-stu-id="40a76-144">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="40a76-145">Hallo bevat `tenant` waarde van uw service-principal.</span><span class="sxs-lookup"><span data-stu-id="40a76-145">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="40a76-146">Hallo bevat `password` waarde van uw service-principal.</span><span class="sxs-lookup"><span data-stu-id="40a76-146">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="40a76-147">Hallo doel-Azure-cloudomgeving, die definieert `AZURE` in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="40a76-147">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="40a76-148">(Een volledige lijst met omgevingen is beschikbaar in Hallo [Maven-invoegtoepassing voor Azure-Web-Apps] documentatie)</span><span class="sxs-lookup"><span data-stu-id="40a76-148">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="40a76-149">Opslaan en sluiten Hallo *settings.xml* bestand.</span><span class="sxs-lookup"><span data-stu-id="40a76-149">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a><span data-ttu-id="40a76-150">Optioneel: Uw pom.xml aanpassen voordat u uw web-app tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="40a76-150">OPTIONAL: Customize your pom.xml before deploying your web app tooAzure</span></span>

<span data-ttu-id="40a76-151">Open Hallo `pom.xml` bestand voor uw toepassing Spring opstarten in een teksteditor en zoek vervolgens Hallo `<plugin>` element voor `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="40a76-151">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="40a76-152">Dit element moet eruitzien als Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="40a76-152">This element should resemble hello following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="40a76-153">Er zijn verschillende waarden die u voor Hallo Maven-invoegtoepassing wijzigen kunt en een gedetailleerde beschrijving in voor elk van deze elementen is beschikbaar in Hallo [Maven-invoegtoepassing voor Azure-Web-Apps] documentatie.</span><span class="sxs-lookup"><span data-stu-id="40a76-153">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="40a76-154">Die wordt aangegeven, er zijn verschillende waarden die waard markeren in dit artikel zijn:</span><span class="sxs-lookup"><span data-stu-id="40a76-154">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="40a76-155">Element</span><span class="sxs-lookup"><span data-stu-id="40a76-155">Element</span></span> | <span data-ttu-id="40a76-156">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="40a76-156">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="40a76-157">Hiermee geeft u de versie Hallo Hallo [Maven-invoegtoepassing voor Azure-Web-Apps].</span><span class="sxs-lookup"><span data-stu-id="40a76-157">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="40a76-158">Controleer Hallo-versie die worden vermeld in Hallo [Maven centrale opslagplaats](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure die u gebruikt Hallo meest recente versie.</span><span class="sxs-lookup"><span data-stu-id="40a76-158">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="40a76-159">Hiermee geeft u op Hallo verificatie-informatie voor Azure, die in dit voorbeeld bevat een `<serverId>` element met `azure-auth`; Maven maakt gebruik van die waarde toolook hello Azure-service-principal waarden in uw Maven *settings.xml* bestand, dat u hebt gedefinieerd in een eerdere sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="40a76-159">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="40a76-160">Hiermee geeft u op Hallo doelresourcegroep, die `maven-plugin` in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="40a76-160">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="40a76-161">Hallo resourcegroep wordt gemaakt tijdens de implementatie als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="40a76-161">hello resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="40a76-162">Hiermee geeft u de doelnaam Hallo voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="40a76-162">Specifies hello target name for your web app.</span></span> <span data-ttu-id="40a76-163">In dit voorbeeld is de naam van Hallo doel `maven-web-app-${maven.build.timestamp}`, waarbij hello `${maven.build.timestamp}` achtervoegsel wordt toegevoegd in dit voorbeeld tooavoid conflict.</span><span class="sxs-lookup"><span data-stu-id="40a76-163">In this example, hello target name is `maven-web-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="40a76-164">(Hallo tijdstempel is optioneel, kunt u een unieke tekenreeks voor de naam van de app Hallo.)</span><span class="sxs-lookup"><span data-stu-id="40a76-164">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="40a76-165">Hiermee geeft u de doelregio hello, die in dit voorbeeld is `westus`.</span><span class="sxs-lookup"><span data-stu-id="40a76-165">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="40a76-166">(Een volledige lijst is in Hallo [Maven-invoegtoepassing voor Azure-Web-Apps] documentatie.)</span><span class="sxs-lookup"><span data-stu-id="40a76-166">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="40a76-167">Hiermee geeft u Hallo Java runtime-versie voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="40a76-167">Specifies hello Java runtime version for your web app.</span></span> <span data-ttu-id="40a76-168">(Een volledige lijst is in Hallo [Maven-invoegtoepassing voor Azure-Web-Apps] documentatie.)</span><span class="sxs-lookup"><span data-stu-id="40a76-168">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="40a76-169">Hiermee geeft u een implementatietype voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="40a76-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="40a76-170">Op dit moment alleen `ftp` wordt ondersteund, maar ondersteuning voor andere implementatietypen in ontwikkeling is.</span><span class="sxs-lookup"><span data-stu-id="40a76-170">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="40a76-171">Hiermee geeft u resources en doel-doelen die Maven gebruikt bij het implementeren van uw web-app tooAzure.</span><span class="sxs-lookup"><span data-stu-id="40a76-171">Specifies resources and target destinations which Maven uses when deploying your web app tooAzure.</span></span> <span data-ttu-id="40a76-172">In dit voorbeeld twee `<resource>` elementen opgeven dat Maven Hallo JAR-bestand voor uw web-app en het Hallo inzetten *web.config* bestand uit Hallo Spring opstarten project.</span><span class="sxs-lookup"><span data-stu-id="40a76-172">In this example, two `<resource>` elements specify that Maven will deploy hello JAR file for your web app and hello *web.config* file from hello Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-tooazure"></a><span data-ttu-id="40a76-173">Bouw en implementeer uw web-app tooAzure</span><span class="sxs-lookup"><span data-stu-id="40a76-173">Build and deploy your web app tooAzure</span></span>

<span data-ttu-id="40a76-174">Zodra u alle instellingen Hallo in Hallo voorgaande secties in dit artikel hebt geconfigureerd, u bent klaar toodeploy uw web-app tooAzure.</span><span class="sxs-lookup"><span data-stu-id="40a76-174">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your web app tooAzure.</span></span> <span data-ttu-id="40a76-175">toodo gebruik dus Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="40a76-175">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="40a76-176">Opnieuw samenstellen Hallo JAR-bestand met behulp van Maven, als u toohello wijzigingen aangebracht van Hallo-opdrachtprompt of terminalvenster die u eerder gebruikte *pom.xml* bestand; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="40a76-176">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="40a76-177">Uw web-app tooAzure implementeren met behulp van Maven; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="40a76-177">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="40a76-178">Maven implementeert uw web-app tooAzure; Als het Hallo-web-app niet al bestaat, wordt deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="40a76-178">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

<span data-ttu-id="40a76-179">Wanneer uw web-is geïmplementeerd, kunt u zich kunt toomanage deze met behulp van Hallo [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="40a76-179">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="40a76-180">Uw web-app wordt weergegeven in **App Services**:</span><span class="sxs-lookup"><span data-stu-id="40a76-180">Your web app will be listed in **App Services**:</span></span>

   ![Web-app die worden vermeld in Azure-portal App Services][AP01]

* <span data-ttu-id="40a76-182">En Hallo URL voor uw web-app wordt weergegeven in Hallo **overzicht** voor uw web-app:</span><span class="sxs-lookup"><span data-stu-id="40a76-182">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Hallo-URL voor uw web-app te bepalen][AP02]

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

## <a name="next-steps"></a><span data-ttu-id="40a76-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="40a76-184">Next steps</span></span>

<span data-ttu-id="40a76-185">Verschillende technologieën die worden beschreven in dit artikel, Zie voor meer informatie over Hallo Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="40a76-185">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="40a76-186">[Maven-invoegtoepassing voor Azure-Web-Apps]</span><span class="sxs-lookup"><span data-stu-id="40a76-186">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="40a76-187">Meld u bij tooAzure van hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="40a76-187">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="40a76-188">Hoe toouse hello Maven-invoegtoepassing voor Azure Web Apps toodeploy een beperkte app tooAzure voor Spring opstarten</span><span class="sxs-lookup"><span data-stu-id="40a76-188">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="40a76-189">Een Azure-service-principal maken met Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="40a76-189">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="40a76-190">Naslaginformatie over maven</span><span class="sxs-lookup"><span data-stu-id="40a76-190">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure-opdrachtregelinterface (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure-portal]: https://portal.azure.com/
[gratis Azure-account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[voordelen als MSDN-abonnee]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring opstarten aan de slag]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven-invoegtoepassing voor Azure-Web-Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
