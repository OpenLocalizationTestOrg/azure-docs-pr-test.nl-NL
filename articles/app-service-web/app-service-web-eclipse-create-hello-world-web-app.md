---
title: een eenvoudige Azure-web-app met aaaCreate Eclipse | Microsoft Docs
description: Deze zelfstudie leert u hoe toouse hello Azure Toolkit voor Eclipse toocreate een Hallo wereld-Web-App voor Azure.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="3c9a0-103">Een eenvoudige Azure-web-app met behulp van Eclipse maken</span><span class="sxs-lookup"><span data-stu-id="3c9a0-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="3c9a0-104">Deze zelfstudie laat zien hoe toocreate en een eenvoudige Hallo wereld toepassing tooAzure implementeren als een Web-App met behulp van Hallo [Azure Toolkit voor Eclipse].</span><span class="sxs-lookup"><span data-stu-id="3c9a0-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="3c9a0-105">Een eenvoudige JSP-voorbeeld voor eenvoud wordt weergegeven, maar gelijksoortige stappen zou zijn geschikt voor een servlet Java wat betreft Azure-implementatie is.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="3c9a0-106">Wanneer u deze zelfstudie hebt voltooid, ziet uw toepassing vergelijkbare toohello afbeelding volgen wanneer u deze in een webbrowser bekijken:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Voorbeeld van Hallo wereld-app][01]

## <a name="prerequisites"></a><span data-ttu-id="3c9a0-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3c9a0-108">Prerequisites</span></span>
* <span data-ttu-id="3c9a0-109">Een Java Developer Kit (JDK), v 1.8 of hoger.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="3c9a0-110">Eclipse IDE voor Java EE-ontwikkelaars, standaard of hoger.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-110">Eclipse IDE for Java EE Developers, Luna or later.</span></span> <span data-ttu-id="3c9a0-111">Dit kan worden gedownload vanaf <http://www.eclipse.org/downloads/>.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-111">This can be downloaded from <http://www.eclipse.org/downloads/>.</span></span>
* <span data-ttu-id="3c9a0-112">Een distributiepunt van een Java gebaseerde webserver of toepassingsserver, zoals [Apache Tomcat] of [Jetty].</span><span class="sxs-lookup"><span data-stu-id="3c9a0-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="3c9a0-113">Een Azure-abonnement, die kan worden opgehaald uit <https://azure.microsoft.com/free/> of <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="3c9a0-114">Hallo [Azure Toolkit voor Eclipse].</span><span class="sxs-lookup"><span data-stu-id="3c9a0-114">hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="3c9a0-115">Zie voor meer informatie over het installeren van hello Azure Toolkit [installeren hello Azure Toolkit voor Eclipse].</span><span class="sxs-lookup"><span data-stu-id="3c9a0-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for Eclipse].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="3c9a0-116">een toepassing Hello World toocreate</span><span class="sxs-lookup"><span data-stu-id="3c9a0-116">toocreate a Hello World application</span></span>
<span data-ttu-id="3c9a0-117">Eerst beginnen we uitschakelen met een Java-project maken.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="3c9a0-118">Start Eclipse en op Hallo-menu op **bestand**, klikt u op **nieuw**, en klik vervolgens op **dynamisch webproject**.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-118">Start Eclipse, and at hello menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="3c9a0-119">(Als er geen **dynamisch webproject** vermeld als een project beschikbaar wanneer u op **bestand** en **nieuw**, vervolgens Hallo te volgen: klik op **bestand**, klikt u op **nieuw**, klikt u op **Project...** , vouw **Web**, klikt u op **dynamisch webproject**, en klik op **volgende**.)</span><span class="sxs-lookup"><span data-stu-id="3c9a0-119">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do hello following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>
2. <span data-ttu-id="3c9a0-120">Naam voor deze zelfstudie Hallo project **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-120">For purposes of this tutorial, name hello project **MyWebApp**.</span></span> <span data-ttu-id="3c9a0-121">Het scherm wordt vergelijkbaar toohello volgende weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-121">Your screen will appear similar toohello following:</span></span>
   
    ![Een nieuw Dynamic Web Project maken][02]
3. <span data-ttu-id="3c9a0-123">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-123">Click **Finish**.</span></span>
4. <span data-ttu-id="3c9a0-124">Vouw in de weergave Project Explorer van Eclipse **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-124">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="3c9a0-125">Klik met de rechtermuisknop op **WebContent**(Webinhoud) en klik vervolgens op **New** (Nieuw) en **JSP File** (JSP-bestand).</span><span class="sxs-lookup"><span data-stu-id="3c9a0-125">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
5. <span data-ttu-id="3c9a0-126">In Hallo **nieuw JSP-bestand** in het dialoogvenster, naam Hallo bestand **index.jsp**, houden Hallo bovenliggende map als **MyWebApp/WebContent**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-126">In hello **New JSP File** dialog box, name hello file **index.jsp**, keep hello parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>
6. <span data-ttu-id="3c9a0-127">In Hallo **JSP-sjabloon selecteren** in het dialoogvenster voor de doeleinden van deze zelfstudie geselecteerd **nieuw JSP-bestand (html)**, en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-127">In hello **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
7. <span data-ttu-id="3c9a0-128">Wanneer het bestand index.jsp wordt geopend in Eclipse, toevoegen in toodynamically tekstweergave **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="3c9a0-128">When your index.jsp file opens in Eclipse, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="3c9a0-129">binnen de bestaande Hallo `<body>` element.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-129">within hello existing `<body>` element.</span></span> <span data-ttu-id="3c9a0-130">Uw bijgewerkte `<body>` inhoud moet eruitzien als Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-130">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. <span data-ttu-id="3c9a0-131">Index.jsp opslaan.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-131">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="3c9a0-132">toodeploy uw toepassing tooan Azure Web App-Container</span><span class="sxs-lookup"><span data-stu-id="3c9a0-132">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="3c9a0-133">Er zijn verschillende manieren waarop u een Java web application tooAzure kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-133">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="3c9a0-134">Deze zelfstudie wordt beschreven in een van de eenvoudigste Hallo: uw toepassing worden geïmplementeerde tooan Azure Web App-Container - geen speciale projecttype of extra hulpprogramma's nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-134">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="3c9a0-135">Hallo JDK en Hallo web container software worden geleverd voor u door Azure, zodat er geen noodzaak tooupload uw eigen; u hoeft uw Java-Web-App is.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-135">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="3c9a0-136">Als gevolg hiervan wordt publicatieproces voor uw toepassing hello seconden, niet minuten duren.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-136">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="3c9a0-137">In de Projectverkenner van Eclipse met de rechtermuisknop op **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-137">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>
2. <span data-ttu-id="3c9a0-138">Selecteer in het contextmenu hello, **Azure**, klikt u vervolgens op **publiceren als Azure-Web-App...**</span><span class="sxs-lookup"><span data-stu-id="3c9a0-138">In hello context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
    ![Als Azure-Web-App publiceren][03]
   
    <span data-ttu-id="3c9a0-140">U kunt ook terwijl uw toepassing webproject in Hallo Projectverkenner is geselecteerd, klikt u op Hallo **publiceren** vervolgkeuzeknop op Hallo werkbalk en selecteer **publiceren als Azure-Web-App** van daaruit:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-140">Alternatively, while your web application project is selected in hello Project Explorer, you can click hello **Publish** dropdown button on hello toolbar and select **Publish as Azure Web App** from there:</span></span>
   
    ![Als Azure-Web-App publiceren][14]
3. <span data-ttu-id="3c9a0-142">Als u hebt nog niet aangemeld bij Azure van Eclipse, kunt u zich na vragen aan gebruiker toosign in uw Azure-account:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-142">If you have not already signed into Azure from Eclipse, you will be prompted toosign into your Azure account:</span></span>
   
    ![Azure Sign In het dialoogvenster][04]
   
    <span data-ttu-id="3c9a0-144">Als er meerdere Azure-accounts, aantal Hallo prompts tijdens Hallo aanmelden proces worden mogelijk weergegeven meer dan één keer, zelfs als ze worden weergegeven toobe Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-144">If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="3c9a0-145">Als dit gebeurt, blijven Hallo aanmelden instructies te volgen.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-145">When this happens, continue following hello sign in instructions.</span></span>
4. <span data-ttu-id="3c9a0-146">Nadat u bent aangemeld bij uw Azure-account, Hallo **abonnementen beheren** in het dialoogvenster een lijst met abonnementen die gekoppeld aan uw referenties zijn worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-146">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="3c9a0-147">Als er meerdere abonnementen die worden vermeld en toowork met alleen een specifieke subset ervan gewenste, kan u eventueel Hallo die u wilt dat toouse uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-147">If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello ones you do want toouse.</span></span> <span data-ttu-id="3c9a0-148">Wanneer u uw abonnementen hebt geselecteerd, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-148">When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Dialoogvenster abonnementen beheren][05]
5. <span data-ttu-id="3c9a0-150">Wanneer Hallo **tooAzure Web-App-Container implementeren** dialoogvenster wordt weergegeven, wordt deze in een Web-App-containers die u eerder hebt gemaakt weergegeven; als u geen containers niet gemaakt hebt, Hallo lijst is leeg.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-150">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![Dialoogvenster tooAzure-Web-App-Container implementeren][06]
6. <span data-ttu-id="3c9a0-152">Als u geen hebt gemaakt een Azure-Web-App-Container vóór of als u wilt toopublish uw toepassing tooa nieuwe container, gebruik Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-152">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="3c9a0-153">Anders selecteert u een bestaande Web-App-Container en toostep 7 hieronder overslaan.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-153">Otherwise, select an existing Web App Container and skip toostep 7 below.</span></span>
   
   1. <span data-ttu-id="3c9a0-154">Klik op **nieuwe...**</span><span class="sxs-lookup"><span data-stu-id="3c9a0-154">Click **New...**</span></span>
      
       ![Dialoogvenster tooAzure-Web-App-Container implementeren][15]
   2. <span data-ttu-id="3c9a0-156">Hallo **nieuwe Web-App-Container** in het dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-156">hello **New Web App Container** dialog box will be displayed:</span></span>
      
       ![Dialoogvenster Nieuwe Web-App-Container][07a]
   3. <span data-ttu-id="3c9a0-158">Voer een **DNS-Label** voor uw Web-App-Container; vormt dit Hallo leaf DNS-label van Hallo host-URL voor uw webtoepassing in Azure.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-158">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="3c9a0-159">(Houd er rekening mee dat Hallo-naam moet beschikbaar zijn en voldoen naamgevingsvereisten tooAzure voor Web-App.)</span><span class="sxs-lookup"><span data-stu-id="3c9a0-159">(Note that hello name must be available and conform tooAzure Web App naming requirements.)</span></span>
   4. <span data-ttu-id="3c9a0-160">In Hallo **webcontainer** vervolgkeuzelijst, selecteer Hallo geschikte software voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-160">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="3c9a0-161">U kunt op dit moment van Tomcat-8, 7 Tomcat of Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-161">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="3c9a0-162">Een recente distributie van software Hallo geselecteerd door Azure worden verstrekt en het wordt uitgevoerd op een recente verdeling van JDK 8 gemaakt door Oracle en geleverd door Azure.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-162">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="3c9a0-163">In Hallo **abonnement** vervolgkeuzelijst, selecteer Hallo abonnement gewenste toouse voor deze implementatie.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-163">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="3c9a0-164">In Hallo **resourcegroep** vervolgkeuzelijst, selecteer Hallo resourcegroep waarmee u tooassociate uw Web-App wilt.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-164">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="3c9a0-165">(Azure resourcegroepen kunt u toogroup verwante resources samen zodat bijvoorbeeld ze samen kunnen worden verwijderd.)</span><span class="sxs-lookup"><span data-stu-id="3c9a0-165">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="3c9a0-166">U kunt een bestaande resourcegroep selecteren (als u een hebt) en overslaan toostep g onderstaande of gebruik Hallo na deze stappen een nieuwe resourcegroep toocreate:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-166">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following these steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="3c9a0-167">Klik op **nieuwe...**</span><span class="sxs-lookup"><span data-stu-id="3c9a0-167">Click **New...**</span></span>
      * <span data-ttu-id="3c9a0-168">Hallo **nieuwe resourcegroep** in het dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-168">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Dialoogvenster nieuwe resourcegroep][08]
      * <span data-ttu-id="3c9a0-170">In Hallo Hallo **naam** textbox, Geef een naam voor uw nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-170">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="3c9a0-171">In Hallo Hallo **regio** vervolgkeuzelijst, selecteer Hallo juiste Azure datacentrum locatie voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-171">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="3c9a0-172">Optioneel: Standaard een recente verdeling van Java 8 worden geïmplementeerd door Azure automatisch tooyour webcontainer app als uw JVM.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically tooyour web app container as your JVM.</span></span> <span data-ttu-id="3c9a0-173">U kunt echter een andere versie en de distributie van Hallo JVM opgeven als dit vereist is voor uw Web-App.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-173">However, you can specify a different version and distribution of hello JVM if your Web App requires it.</span></span> <span data-ttu-id="3c9a0-174">toospecify hello JDK voor uw Web-App klikt u op Hallo **JDK** tabblad en selecteer een van Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-174">toospecify hello JDK for your Web App, click hello **JDK** tab, and select one of hello following options:</span></span>
        
        * <span data-ttu-id="3c9a0-175">**Hallo standaard JDK die worden aangeboden door de service Azure Web Apps implementeren**: deze optie wordt een recente verdeling van Java 8 implementeren.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-175">**Deploy hello default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
        * <span data-ttu-id="3c9a0-176">**Een 3e party JDK die beschikbaar zijn in Azure implementeren**: deze optie kunt u toochoose uit Hallo lijst met JDKs die worden geleverd door Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-176">**Deploy a 3rd party JDK available on Azure**: This option allows you toochoose from hello list of JDKs which are provided by Microsoft Azure.</span></span>
        * <span data-ttu-id="3c9a0-177">**Mijn eigen JDK vanaf deze downloadlocatie implementeren**: deze optie kunt u toospecify uw eigen JDK-distributiepunt dat als een ZIP-bestand moet worden verpakt en geüpload tooeither een openbaar downloadlocatie of een Azure storage-account waarvoor u toegang hebben.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-177">**Deploy my own JDK from this download location**: This option allows you toospecify your own JDK distribution, which must be packaged as a ZIP file and uploaded tooeither a publicly available download location or an Azure storage account for which you have access.</span></span>
          
          ![Dialoogvenster Nieuwe Web-App-Container][07b]
   7. <span data-ttu-id="3c9a0-179">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-179">Click **OK**.</span></span>
   8. <span data-ttu-id="3c9a0-180">Hallo **App Service-Plan** vervolgkeuzelijst bevat Hallo-app service-abonnementen die zijn gekoppeld aan Hallo resourcegroep die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-180">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="3c9a0-181">(Informatie zoals Hallo-locatie van uw Web-App Hallo prijscategorie en Hallo compute exemplaargrootte app Service-abonnementen opgeven.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-181">(App Service Plans specify information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="3c9a0-182">Een enkele App Service-Plan kan worden gebruikt voor meerdere Web-Apps, dat is waarom deze afzonderlijk van een specifieke implementatie van Web-App onderhouden.)</span><span class="sxs-lookup"><span data-stu-id="3c9a0-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="3c9a0-183">Selecteer een bestaand App Service-abonnement (als u een hebt) en toostep h onderstaande overslaan of na deze stappen toocreate een nieuwe App Service-Plan hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-183">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following these steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="3c9a0-184">Klik op **nieuwe...**</span><span class="sxs-lookup"><span data-stu-id="3c9a0-184">Click **New...**</span></span>
      * <span data-ttu-id="3c9a0-185">Hallo **nieuwe App Service-Plan** in het dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-185">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Nieuwe App Service-Plan in het dialoogvenster][09]
      * <span data-ttu-id="3c9a0-187">In Hallo Hallo **naam** textbox, Geef een naam voor uw nieuwe App Service-Plan.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-187">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="3c9a0-188">In Hallo Hallo **locatie** vervolgkeuzelijst, selecteer Hallo juiste Azure datacentrum locatie voor Hallo plan.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-188">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="3c9a0-189">In Hallo Hallo **prijscategorie** vervolgkeuzelijst, selecteer Hallo toepasselijke prijzen voor Hallo plan.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-189">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="3c9a0-190">Voor testdoeleinden kunt u **vrije**.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-190">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="3c9a0-191">In Hallo Hallo **Exemplaargrootte** vervolgkeuzelijst, selecteer Hallo juiste exemplaargrootte voor Hallo plan.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-191">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="3c9a0-192">Voor testdoeleinden kunt u **kleine**.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-192">For testing purposes you can choose **Small**.</span></span>
   9. <span data-ttu-id="3c9a0-193">Nadat u alle Hallo bovenstaande stappen hebt voltooid, ziet er Hallo nieuwe Web-App-Container dialoogvenster Hallo volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-193">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![Dialoogvenster Nieuwe Web-App-Container][10]
   10. <span data-ttu-id="3c9a0-195">Klik op **OK** toocomplete Hallo maken van uw nieuwe Web-App-container.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-195">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="3c9a0-196">Wacht een paar seconden voor Hallo lijst met Hallo Web-App containers toobe vernieuwd en de zojuist gemaakte web-app-container moet nu worden geselecteerd in het Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-196">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
7. <span data-ttu-id="3c9a0-197">U bent nu klaar toocomplete Hallo initiële implementatie van uw Web-App-tooAzure:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-197">You are now ready toocomplete hello initial deployment of your Web App tooAzure:</span></span>
   
    ![Dialoogvenster tooAzure-Web-App-Container implementeren][11]
   
    <span data-ttu-id="3c9a0-199">Klik op **OK** toodeploy uw Java-toepassing toohello geselecteerd Web-App-container.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-199">Click **OK** toodeploy your Java application toohello selected Web App container.</span></span>
   
    <span data-ttu-id="3c9a0-200">Standaard wordt uw toepassing wordt geïmplementeerd als een submap van de toepassingsserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-200">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="3c9a0-201">Als u toobe geïmplementeerd als de hoofdtoepassing hello wilt, Controleer Hallo **implementeren tooroot** selectievakje voordat u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-201">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
8. <span data-ttu-id="3c9a0-202">Vervolgens ziet u Hallo **Azure Activity Log** waarmee wordt aangegeven Hallo implementatiestatus van uw Web-App bekijken.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-202">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![Azure Activity Log][12]
   
    <span data-ttu-id="3c9a0-204">Hallo-proces voor het implementeren van uw Web-App tooAzure duurt slechts enkele seconden toocomplete.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-204">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="3c9a0-205">Wanneer uw toepassing ready, ziet u een koppeling met de naam **gepubliceerde** in Hallo **Status** kolom.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-205">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="3c9a0-206">Wanneer u Hallo koppeling klikt, wordt uitgevoerd, u startpagina tooyour geïmplementeerd van Web-App.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-206">When you click hello link, it will take you tooyour deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="3c9a0-207">De web-app beveiligen</span><span class="sxs-lookup"><span data-stu-id="3c9a0-207">Updating your web app</span></span>
<span data-ttu-id="3c9a0-208">Bijwerken van een bestaande Azure-Web-App uitgevoerd is een snelle en eenvoudige proces en hebt u twee opties voor het bijwerken van:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-208">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="3c9a0-209">U kunt Hallo-implementatie van een bestaande Java-Web-App kunt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-209">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="3c9a0-210">U kunt een extra toohello voor Java-toepassing publiceren dezelfde Web-App-Container.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-210">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="3c9a0-211">In beide gevallen Hallo proces identieke en duurt slechts enkele seconden:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-211">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="3c9a0-212">Hallo Eclipse-project explorer met de rechtermuisknop op Hallo Java-toepassing die u wilt dat tooupdate of tooan bestaande Web-App-Container toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-212">In hello Eclipse project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="3c9a0-213">Wanneer het Hallo-contextmenu wordt weergegeven, selecteert u **Azure** en vervolgens **publiceren als Azure-Web-App...**</span><span class="sxs-lookup"><span data-stu-id="3c9a0-213">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="3c9a0-214">Nadat u hebt al aangemeld eerder, ziet u een lijst met uw bestaande Web-App-containers.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-214">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="3c9a0-215">Selecteer een of wilt u toopublish opnieuw publiceren, uw Java-toepassing tooand Klik Hallo **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-215">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="3c9a0-216">Een paar seconden later Hallo **Azure Activity Log** weer uw bijgewerkte implementatie als **gepubliceerde** en u kunt tooverify uw bijgewerkte toepassing in een webbrowser worden.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-216">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="3c9a0-217">Starten, stoppen of opnieuw starten van een bestaande web-app</span><span class="sxs-lookup"><span data-stu-id="3c9a0-217">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="3c9a0-218">toostart of stoppen van een bestaande Azure-Web-App-container (inclusief alle Hallo geïmplementeerd Java-toepassingen in deze), kunt u Hallo **Azure Explorer** weergeven.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-218">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="3c9a0-219">Als hello **Azure Explorer** weergave nog niet is geopend, kunt u deze openen door te klikken op vervolgens **venster** menu in Eclipse, klikt u vervolgens op **weergave tonen**, klikt u vervolgens **andere...** , klikt u vervolgens **Azure**, en klik vervolgens op **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-219">If hello **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="3c9a0-220">Als u eerder niet hebt aangemeld, wordt u gevraagd toodo dus.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-220">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="3c9a0-221">Wanneer Hallo **Azure Explorer** weergave wordt weergegeven, gebruik Volg deze stappen toostart of stoppen van uw Web-App:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-221">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="3c9a0-222">Vouw Hallo **Azure** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-222">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="3c9a0-223">Vouw Hallo **Web-Apps** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-223">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="3c9a0-224">Klik met de rechtermuisknop Hallo gewenste Web-App.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-224">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="3c9a0-225">Wanneer het Hallo-contextmenu wordt weergegeven, klikt u op **Start**, **stoppen**, of **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-225">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="3c9a0-226">Houd er rekening mee dat Hallo menu-Opties contextbewuste, zijn zodat u kunt alleen een actieve WebApp stoppen of starten van een web-app die niet wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3c9a0-226">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Stoppen van een bestaande Web-App][13]

## <a name="next-steps"></a><span data-ttu-id="3c9a0-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3c9a0-228">Next Steps</span></span>
<span data-ttu-id="3c9a0-229">Zie voor meer informatie over hello Azure Toolkits voor IDE voor Java Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3c9a0-229">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="3c9a0-230">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3c9a0-230">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3c9a0-231">[installeren hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3c9a0-231">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3c9a0-232">*Een Hallo wereld Web-App maken voor Azure in Eclipse (in dit artikel)*</span><span class="sxs-lookup"><span data-stu-id="3c9a0-232">*Create a Hello World Web App for Azure in Eclipse (This Article)*</span></span>
  * <span data-ttu-id="3c9a0-233">[Wat is er nieuw in hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3c9a0-233">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="3c9a0-234">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="3c9a0-234">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3c9a0-235">[Hello Azure Toolkit voor IntelliJ installeren]</span><span class="sxs-lookup"><span data-stu-id="3c9a0-235">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3c9a0-236">[Een Hallo wereld Web-App maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3c9a0-236">[Create a Hello World Web App for Azure in IntelliJ]</span></span>
  * <span data-ttu-id="3c9a0-237">[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3c9a0-237">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<span data-ttu-id="3c9a0-238">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="3c9a0-238">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="3c9a0-239">Zie voor meer informatie over het maken van Azure Web Apps Hallo [overzicht van Web Apps].</span><span class="sxs-lookup"><span data-stu-id="3c9a0-239">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld Web-App maken voor Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[installeren hello Azure Toolkit voor Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Hello Azure Toolkit voor IntelliJ installeren]: ../azure-toolkit-for-intellij-installation.md
[Wat is er nieuw in hello Azure Toolkit voor Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[overzicht van Web Apps]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
