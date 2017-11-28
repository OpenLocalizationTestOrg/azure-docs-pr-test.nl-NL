---
title: aaaDeploy een versie die voorjaar opstarten toepassing toohello Azure App Service | Microsoft Docs
description: Deze zelfstudie leidt ontwikkelaars via Hallo stappen toodeploy Hallo Spring opstarten aan de slag web app tooAzure App Service.
services: app-service\web
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
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 69f9c4903fd740125194402cdb4b4db46a1f2773
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a><span data-ttu-id="b5251-103">Een versie die voorjaar opstarten toepassing toohello Azure App Service implementeren</span><span class="sxs-lookup"><span data-stu-id="b5251-103">Deploy a Spring Boot Application toohello Azure App Service</span></span>

<span data-ttu-id="b5251-104">Hallo  **[Spring Framework]**  is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken en een meer populaire Hallo-projecten die is gebaseerd op dat platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b5251-104">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="b5251-105">Deze zelfstudie leert u echter Hallo voorbeeld Spring opstarten aan de slag web-app maken en te implementeren[Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="b5251-105">This tutorial will walk you though creating hello sample Spring Boot Getting Started web app and deploying it too[Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b5251-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b5251-106">Prerequisites</span></span>

<span data-ttu-id="b5251-107">In de volgorde toocomplete Hallo stappen in deze zelfstudie hebt u toohave Hallo volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="b5251-107">In order toocomplete hello steps in this tutorial, you need toohave hello following:</span></span>

* <span data-ttu-id="b5251-108">Een Azure-abonnement; Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee] of zich aanmelden voor een [gratis Azure-account].</span><span class="sxs-lookup"><span data-stu-id="b5251-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="b5251-109">Een up-to-date [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="b5251-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="b5251-110">Apache van [Maven] bouwen tool (versie 3).</span><span class="sxs-lookup"><span data-stu-id="b5251-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="b5251-111">Een [Git] client.</span><span class="sxs-lookup"><span data-stu-id="b5251-111">A [Git] client.</span></span>

## <a name="create-hello-spring-boot-getting-started-web-app"></a><span data-ttu-id="b5251-112">Hallo Spring opstarten aan de slag web-app maken</span><span class="sxs-lookup"><span data-stu-id="b5251-112">Create hello Spring Boot Getting Started web app</span></span>

<span data-ttu-id="b5251-113">Hallo begeleidt volgt u stapsgewijs door Hallo stappen die zijn vereist toocreate een eenvoudige webtoepassing voor Spring opstarten en lokaal testen.</span><span class="sxs-lookup"><span data-stu-id="b5251-113">hello following steps will walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="b5251-114">Open een opdrachtprompt en maken van een lokale map toohold uw toepassing en de wijziging toothat directory; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b5251-114">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="b5251-115">-- of--</span><span class="sxs-lookup"><span data-stu-id="b5251-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="b5251-116">Kloon Hallo [Spring opstarten aan de slag] voorbeeldproject in Hallo directory die u zojuist hebt gemaakt, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b5251-116">Clone hello [Spring Boot Getting Started] sample project into hello directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="b5251-117">Wijzigen van de directory toohello voltooid project. bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b5251-117">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="b5251-118">Hallo JAR-bestand met behulp van Maven; bouwen bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b5251-118">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="b5251-119">Zodra het Hallo-web-app is gemaakt, directory toohello JAR-bestand te wijzigen en Hallo web-app starten bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b5251-119">Once hello web app has been created, change directory toohello JAR file and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="b5251-120">Hallo web-app testen door te bladeren toohttp://localhost:8080 met een webbrowser, of gebruik de syntaxis Hallo zoals Hallo na voorbeeld hebt u curl beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="b5251-120">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="b5251-121">U ziet Hallo volgende bericht wordt weergegeven: **begroetingen vanaf Spring opstart!**</span><span class="sxs-lookup"><span data-stu-id="b5251-121">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Voorbeeld-App bladeren][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="b5251-123">Maken van een Azure-web-app voor gebruik met Java</span><span class="sxs-lookup"><span data-stu-id="b5251-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="b5251-124">Hallo stappen te volgen wordt stapsgewijs Hallo stappen toocreate een Azure-Web-App, Hallo vereiste instellingen configureren voor Java en uw FTP-referenties configureren.</span><span class="sxs-lookup"><span data-stu-id="b5251-124">hello following steps will walk you through hello steps toocreate an Azure Web App, configure hello required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="b5251-125">Blader toohello [Azure-portal] en zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="b5251-125">Browse toohello [Azure portal] and log in.</span></span>

1. <span data-ttu-id="b5251-126">Nadat u hebt geregistreerd bij uw account op Hallo Azure-portal, klikt u op Hallo menupictogram voor **App Services**:</span><span class="sxs-lookup"><span data-stu-id="b5251-126">Once you have logged into your account on hello Azure portal, click hello menu icon for **App Services**:</span></span>
   
   ![Azure Portal][AZ01]

1. <span data-ttu-id="b5251-128">Wanneer Hallo **App Services** pagina wordt weergegeven, klikt u op **+ toevoegen** toocreate een nieuwe App Service.</span><span class="sxs-lookup"><span data-stu-id="b5251-128">When hello **App Services** page is displayed, click **+ Add** toocreate a new App Service.</span></span>

   ![App Service maken][AZ02]

1. <span data-ttu-id="b5251-130">Wanneer Hallo lijst met sjablonen voor web-app wordt weergegeven, klikt u op de koppeling Hallo voor Hallo basic Microsoft Web-App.</span><span class="sxs-lookup"><span data-stu-id="b5251-130">When hello list of web app templates is displayed, click hello link for hello basic Microsoft Web App.</span></span>

   ![Sjablonen voor Web-App][AZ03]

1. <span data-ttu-id="b5251-132">Wanneer Hallo informatiepagina voor Hallo Web-App-sjabloon wordt weergegeven, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="b5251-132">When hello information page for hello Web App template is displayed, click **Create**.</span></span>

   ![Web-app maken][AZ04]

1. <span data-ttu-id="b5251-134">Geef een unieke naam voor uw web-app en geef eventuele aanvullende instellingen en vervolgens **maken**.</span><span class="sxs-lookup"><span data-stu-id="b5251-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Instellingen voor Web-App maken][AZ05]

1. <span data-ttu-id="b5251-136">Nadat uw web-app is gemaakt, klikt u op Hallo menupictogram voor **App Services**, en klik vervolgens op uw nieuwe web-app:</span><span class="sxs-lookup"><span data-stu-id="b5251-136">Once your web app has been created, click hello menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Lijst met Web-Apps][AZ06]

1. <span data-ttu-id="b5251-138">Wanneer uw web-app wordt weergegeven, geeft u Hallo Java-versie via Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b5251-138">When your web app is displayed, specify hello Java version by using hello following steps:</span></span>

   <span data-ttu-id="b5251-139">a.</span><span class="sxs-lookup"><span data-stu-id="b5251-139">a.</span></span> <span data-ttu-id="b5251-140">Klik op Hallo **toepassingsinstellingen** menu-item.</span><span class="sxs-lookup"><span data-stu-id="b5251-140">Click hello **Application Settings** menu item.</span></span>

   <span data-ttu-id="b5251-141">b.</span><span class="sxs-lookup"><span data-stu-id="b5251-141">b.</span></span> <span data-ttu-id="b5251-142">Kies **Java 8** voor Hallo Java-versie.</span><span class="sxs-lookup"><span data-stu-id="b5251-142">Choose **Java 8** for hello Java version.</span></span>

   <span data-ttu-id="b5251-143">c.</span><span class="sxs-lookup"><span data-stu-id="b5251-143">c.</span></span> <span data-ttu-id="b5251-144">Kies **nieuwste** voor Hallo secundaire Java-versie.</span><span class="sxs-lookup"><span data-stu-id="b5251-144">Choose **Newest** for hello minor Java version.</span></span>

   <span data-ttu-id="b5251-145">d.</span><span class="sxs-lookup"><span data-stu-id="b5251-145">d.</span></span> <span data-ttu-id="b5251-146">Kies **nieuwste Tomcat 8.5** voor Hallo webcontainer.</span><span class="sxs-lookup"><span data-stu-id="b5251-146">Choose **Newest Tomcat 8.5** for hello web container.</span></span> <span data-ttu-id="b5251-147">(Deze container niet daadwerkelijk wordt gebruikt; Azure gebruikt Hallo container van uw toepassing Spring opstarten.)</span><span class="sxs-lookup"><span data-stu-id="b5251-147">(This container will not actually be used; Azure will use hello container from your Spring Boot application.)</span></span>

   <span data-ttu-id="b5251-148">e.</span><span class="sxs-lookup"><span data-stu-id="b5251-148">e.</span></span> <span data-ttu-id="b5251-149">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b5251-149">Click **Save**.</span></span>

   ![Toepassingsinstellingen][AZ07]

1. <span data-ttu-id="b5251-151">Geef uw FTP-implementatiereferenties met behulp van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b5251-151">Specify your FTP deployment credentials by using hello following steps:</span></span>

   <span data-ttu-id="b5251-152">a.</span><span class="sxs-lookup"><span data-stu-id="b5251-152">a.</span></span> <span data-ttu-id="b5251-153">Klik op Hallo **Implementatiereferenties** menu-item.</span><span class="sxs-lookup"><span data-stu-id="b5251-153">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="b5251-154">b.</span><span class="sxs-lookup"><span data-stu-id="b5251-154">b.</span></span> <span data-ttu-id="b5251-155">Geef uw gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="b5251-155">Specify your username and password.</span></span>

   <span data-ttu-id="b5251-156">c.</span><span class="sxs-lookup"><span data-stu-id="b5251-156">c.</span></span> <span data-ttu-id="b5251-157">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b5251-157">Click **Save**.</span></span>

   ![Geef referenties voor implementatie][AZ08]

1. <span data-ttu-id="b5251-159">De FTP-verbindingsgegevens ophalen met behulp van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b5251-159">Retrieve your FTP connection information by using hello following steps:</span></span>

   <span data-ttu-id="b5251-160">a.</span><span class="sxs-lookup"><span data-stu-id="b5251-160">a.</span></span> <span data-ttu-id="b5251-161">Klik op Hallo **Implementatiereferenties** menu-item.</span><span class="sxs-lookup"><span data-stu-id="b5251-161">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="b5251-162">b.</span><span class="sxs-lookup"><span data-stu-id="b5251-162">b.</span></span> <span data-ttu-id="b5251-163">Uw volledige FTP-gebruikersnaam en de URL kopiëren en opslaan voor de volgende sectie Hallo van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="b5251-163">Copy your full FTP username and URL and save them for hello next section of this tutorial.</span></span>

   ![FTP-URL en referenties][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a><span data-ttu-id="b5251-165">Uw tooAzure Spring opstarten web-app implementeren</span><span class="sxs-lookup"><span data-stu-id="b5251-165">Deploy your Spring Boot web app tooAzure</span></span>

<span data-ttu-id="b5251-166">Hallo stappen te volgen begeleidt u stapsgewijs door Hallo stappen toodeploy uw tooAzure Spring opstarten web-app.</span><span class="sxs-lookup"><span data-stu-id="b5251-166">hello following steps will walk you through hello steps toodeploy your Spring Boot web app tooAzure.</span></span>

1. <span data-ttu-id="b5251-167">Open een teksteditor zoals Kladblok van Windows op Hallo volgende tekst naar een nieuw document plakken en Hallo bestand opslaan als *web.config*:</span><span class="sxs-lookup"><span data-stu-id="b5251-167">Open a text editor such as Windows Notepad and paste hello following text into a new document, then save hello file as *web.config*:</span></span>
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. <span data-ttu-id="b5251-168">Nadat u hebt opgeslagen Hallo *web.config* tooyour bestandssysteem, tooyour web-app via de FTP-met Hallo-URL, gebruikersnaam en wachtwoord van de voorgaande sectie van deze zelfstudie Hallo verbinden.</span><span class="sxs-lookup"><span data-stu-id="b5251-168">After you have saved hello *web.config* file tooyour system, connect tooyour web app via FTP using hello URL, username, and password from hello preceding section of this tutorial.</span></span> <span data-ttu-id="b5251-169">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b5251-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="b5251-170">Wijziging Hallo externe map toohello hoofdmap van uw web-app (die is op */site/wwwroot*), kopieert u Hallo JAR-bestand van uw toepassing Spring opstarten en Hallo *web.config* van eerder.</span><span class="sxs-lookup"><span data-stu-id="b5251-170">Change hello remote directory toohello root folder of your web app, (which is at */site/wwwroot*), then copy hello JAR file from your Spring Boot application and hello *web.config* from earlier.</span></span> <span data-ttu-id="b5251-171">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b5251-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="b5251-172">Nadat u uw JAR hebt geïmplementeerd en *web.config* bestanden tooyour web-app, moet u toorestart na uw web-app met behulp van hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="b5251-172">After you have deployed your JAR and *web.config* files tooyour web app, you need toorestart your web app using hello Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="b5251-173">Hallo web-app testen door te bladeren tooyour van web-app-URL met een webbrowser, of gebruik de syntaxis Hallo zoals Hallo na voorbeeld hebt u curl beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="b5251-173">Test hello web app by browsing tooyour web app's URL using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="b5251-174">U ziet Hallo volgende bericht wordt weergegeven: **begroetingen vanaf Spring opstart!**</span><span class="sxs-lookup"><span data-stu-id="b5251-174">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Voorbeeld-App bladeren][SB02]

## <a name="next-steps"></a><span data-ttu-id="b5251-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b5251-176">Next steps</span></span>

<span data-ttu-id="b5251-177">Zie voor meer informatie over het gebruik van opstarten Spring toepassingen in Azure Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b5251-177">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="b5251-178">Een toepassing Spring opstarten op Linux in hello Azure Container Service implementeren</span><span class="sxs-lookup"><span data-stu-id="b5251-178">Deploy a Spring Boot Application on Linux in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="b5251-179">Een toepassing Spring opstarten op een Kubernetes Cluster in hello Azure Container Service implementeren</span><span class="sxs-lookup"><span data-stu-id="b5251-179">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="b5251-180">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="b5251-180">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="b5251-181">Zie voor meer informatie over depoying web apps tooAzure met FTP, [implementeren van uw app tooAzure App Service met behulp van FTP/S].</span><span class="sxs-lookup"><span data-stu-id="b5251-181">For additional information about depoying web apps tooAzure using FTP, see [Deploy your app tooAzure App Service using FTP/S].</span></span>

<span data-ttu-id="b5251-182">Zie voor meer informatie over Hallo Spring Boot-voorbeeldproject [Spring opstarten aan de slag].</span><span class="sxs-lookup"><span data-stu-id="b5251-182">For further details about hello Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="b5251-183">Zie voor meer informatie over aan de slag met uw eigen toepassingen Spring opstarten, Hallo **Spring Initializr** op https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="b5251-183">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="b5251-184">Zie voor meer informatie over het configureren van aanvullende instellingen voor uw web-app [web-apps configureren in Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="b5251-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure-portal]: https://portal.azure.com/
[web-apps configureren in Azure App Service]: /azure/app-service-web/web-sites-configure
[implementeren van uw app tooAzure App Service met behulp van FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp
[gratis Azure-account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[voordelen als MSDN-abonnee]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring opstarten aan de slag]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB01.png
[SB02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB02.png

[AZ01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ01.png
[AZ02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ02.png
[AZ03]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ03.png
[AZ04]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ04.png
[AZ05]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ05.png
[AZ06]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ06.png
[AZ07]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ07.png
[AZ08]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ08.png
[AZ09]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ09.png
[AZ10]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ10.png
