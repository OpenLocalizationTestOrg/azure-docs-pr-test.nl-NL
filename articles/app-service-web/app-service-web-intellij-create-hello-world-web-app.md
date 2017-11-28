---
title: een eenvoudige Azure-web-app in IntelliJ aaaCreate | Microsoft Docs
description: Deze zelfstudie leert u hoe toouse hello Azure Toolkit voor IntelliJ toocreate een Hallo wereld-Web-App voor Azure.
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="32621-103">Een eenvoudige Azure-web-app maken in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="32621-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="32621-104">Deze zelfstudie laat zien hoe toocreate en een eenvoudige Hallo wereld toepassing tooAzure implementeren als een Web-App met behulp van Hallo [Azure Toolkit voor IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="32621-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="32621-105">Een eenvoudige JSP-voorbeeld voor eenvoud wordt weergegeven, maar gelijksoortige stappen zou zijn geschikt voor een servlet Java wat betreft Azure-implementatie is.</span><span class="sxs-lookup"><span data-stu-id="32621-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="32621-106">Wanneer u deze zelfstudie hebt voltooid, ziet uw toepassing vergelijkbare toohello afbeelding volgen wanneer u deze in een webbrowser bekijken:</span><span class="sxs-lookup"><span data-stu-id="32621-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Voorbeeldwebpagina][01]

## <a name="prerequisites"></a><span data-ttu-id="32621-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="32621-108">Prerequisites</span></span>
* <span data-ttu-id="32621-109">Een Java Developer Kit (JDK), v 1.8 of hoger.</span><span class="sxs-lookup"><span data-stu-id="32621-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="32621-110">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="32621-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="32621-111">Dit kan worden gedownload vanaf <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="32621-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="32621-112">Een distributiepunt van een Java gebaseerde webserver of toepassingsserver, zoals [Apache Tomcat] of [Jetty].</span><span class="sxs-lookup"><span data-stu-id="32621-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="32621-113">Een Azure-abonnement, die kan worden opgehaald uit <https://azure.microsoft.com/free/> of <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="32621-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="32621-114">Hallo [Azure Toolkit voor IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="32621-114">hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="32621-115">Zie voor meer informatie over het installeren van hello Azure Toolkit [installeren hello Azure Toolkit voor IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="32621-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="32621-116">een toepassing Hello World toocreate</span><span class="sxs-lookup"><span data-stu-id="32621-116">toocreate a Hello World application</span></span>
<span data-ttu-id="32621-117">Eerst beginnen we uitschakelen met een Java-project maken.</span><span class="sxs-lookup"><span data-stu-id="32621-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="32621-118">IntelliJ Start en klik op Hallo **bestand** menu, klikt u vervolgens op **nieuw**, en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="32621-118">Start IntelliJ and click hello **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![Bestand Nieuw Project][02]
2. <span data-ttu-id="32621-120">Selecteer in het dialoogvenster Nieuw Project hello, **Java**, klikt u vervolgens **webtoepassing**, en klik vervolgens op **nieuw** tooadd een SDK-Project.</span><span class="sxs-lookup"><span data-stu-id="32621-120">In hello New Project dialog box, select **Java**, then **Web Application**, and then click **New** tooadd a Project SDK.</span></span>
   
    ![Het dialoogvenster Nieuw project][03a]
   
3. <span data-ttu-id="32621-122">In Hallo basismap selecteren voor het dialoogvenster JDK, selecteer map waarin uw JDK is geïnstalleerd en klik vervolgens op Hallo **OK**.</span><span class="sxs-lookup"><span data-stu-id="32621-122">In hello Select Home Directory for JDK dialog box, select hello folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="32621-123">Klik op **volgende** in Hallo nieuw Project dialoogvenster vak toocontinue.</span><span class="sxs-lookup"><span data-stu-id="32621-123">Click **Next** in hello New Project dialog box toocontinue.</span></span>
   
    ![Basismap van de JDK opgeven][03b]
4. <span data-ttu-id="32621-125">Naam voor deze zelfstudie Hallo project **Java-Web-App-op-Azure**, en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="32621-125">For purposes of this tutorial, name hello project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Het dialoogvenster Nieuw project][04]
5. <span data-ttu-id="32621-127">Vouw in de weergave Project Explorer van IntelliJ **Java-Web-App-op-Azure**, vouw vervolgens **web**, en dubbelklik vervolgens op **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="32621-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Open indexpagina][05c]
6. <span data-ttu-id="32621-129">Wanneer het bestand index.jsp wordt geopend in IntelliJ, toevoegen in toodynamically tekstweergave **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="32621-129">When your index.jsp file opens in IntelliJ, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="32621-130">binnen de bestaande Hallo `<body>` element.</span><span class="sxs-lookup"><span data-stu-id="32621-130">within hello existing `<body>` element.</span></span> <span data-ttu-id="32621-131">Uw bijgewerkte `<body>` inhoud moet eruitzien als Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="32621-131">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="32621-132">Index.jsp opslaan.</span><span class="sxs-lookup"><span data-stu-id="32621-132">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="32621-133">toodeploy uw toepassing tooan Azure Web App-Container</span><span class="sxs-lookup"><span data-stu-id="32621-133">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="32621-134">Er zijn verschillende manieren waarop u een Java web application tooAzure kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="32621-134">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="32621-135">Deze zelfstudie wordt beschreven in een van de eenvoudigste Hallo: uw toepassing worden geïmplementeerde tooan Azure Web App-Container - geen speciale projecttype of extra hulpprogramma's nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="32621-135">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="32621-136">Hallo JDK en Hallo web container software worden geleverd voor u door Azure, zodat er geen noodzaak tooupload uw eigen; u hoeft uw Java-Web-App is.</span><span class="sxs-lookup"><span data-stu-id="32621-136">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="32621-137">Als gevolg hiervan wordt publicatieproces voor uw toepassing hello seconden, niet minuten duren.</span><span class="sxs-lookup"><span data-stu-id="32621-137">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="32621-138">Voordat u uw toepassing publiceren, moet u eerst tooconfigure module-instellingen.</span><span class="sxs-lookup"><span data-stu-id="32621-138">Before you publish your application, you first need tooconfigure your module settings.</span></span> <span data-ttu-id="32621-139">toodo gebruik dus Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="32621-139">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="32621-140">In de IntelliJ Projectverkenner met de rechtermuisknop op Hallo **Java-Web-App-op-Azure** project.</span><span class="sxs-lookup"><span data-stu-id="32621-140">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="32621-141">Wanneer het Hallo-contextmenu wordt weergegeven, klikt u op **Open Module-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="32621-141">When hello context menu appears, click **Open Module Settings**.</span></span>

    ![Open de Module-instellingen][05a]
2. <span data-ttu-id="32621-143">Wanneer de Hallo structuur Project dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="32621-143">When hello Project Structure dialog box appears:</span></span>

   <span data-ttu-id="32621-144">a.</span><span class="sxs-lookup"><span data-stu-id="32621-144">a.</span></span> <span data-ttu-id="32621-145">Klik op **artefacten** in de lijst met Hallo **projectinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="32621-145">Click **Artifacts** in hello list of **Project Settings**.</span></span>
   <span data-ttu-id="32621-146">b.</span><span class="sxs-lookup"><span data-stu-id="32621-146">b.</span></span> <span data-ttu-id="32621-147">Naam van wijzigen Hallo artefacten in Hallo **naam** vak zodat het geen spaties of speciale tekens bevat; dit is nodig omdat het Hallo-naam wordt gebruikt in Hallo Uniform Resource Identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="32621-147">Change hello artifact name in hello **Name** box so that it doesn't contain whitespace or special characters; this is necessary since hello name will be used in hello Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="32621-148">c.</span><span class="sxs-lookup"><span data-stu-id="32621-148">c.</span></span> <span data-ttu-id="32621-149">Wijziging Hallo **Type** te**webtoepassing: archief**.</span><span class="sxs-lookup"><span data-stu-id="32621-149">Change hello **Type** too**Web Application: Archive**.</span></span>
   <span data-ttu-id="32621-150">d.</span><span class="sxs-lookup"><span data-stu-id="32621-150">d.</span></span> <span data-ttu-id="32621-151">Klik op **OK** tooclose Hallo structuur Project dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="32621-151">Click **OK** tooclose hello Project Structure dialog box.</span></span>

    ![Open de Module-instellingen][05b]

<span data-ttu-id="32621-153">Wanneer u uw module-instellingen hebt geconfigureerd, kunt u uw toepassing tooAzure publiceren met behulp van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="32621-153">When you have configured your module settings, you can publish your application tooAzure by using hello following steps:</span></span>

1. <span data-ttu-id="32621-154">In de IntelliJ Projectverkenner met de rechtermuisknop op Hallo **Java-Web-App-op-Azure** project.</span><span class="sxs-lookup"><span data-stu-id="32621-154">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="32621-155">Wanneer het Hallo-contextmenu wordt weergegeven, selecteert u **Azure**, en klik vervolgens op **publiceren als Azure-Web-App...**</span><span class="sxs-lookup"><span data-stu-id="32621-155">When hello context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Azure contextmenu publiceren][06]
2. <span data-ttu-id="32621-157">Als u hebt nog niet aangemeld bij Azure van IntelliJ, kunt u zich na vragen aan gebruiker toosign in uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="32621-157">If you have not already signed into Azure from IntelliJ, you will be prompted toosign into your Azure account.</span></span> <span data-ttu-id="32621-158">(Als er meerdere Azure-accounts, aantal Hallo prompts tijdens de aanmelding Hallo in proces worden mogelijk weergegeven meer dan één keer zelfs als ze worden weergegeven toobe Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="32621-158">(If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="32621-159">Als dit gebeurt, blijven toofollow Hallo aanmelding instructies.)</span><span class="sxs-lookup"><span data-stu-id="32621-159">When this happens, continue toofollow hello sign in instructions.)</span></span>
   
    ![Azure-logboekanalyse In het dialoogvenster][07]
3. <span data-ttu-id="32621-161">Nadat u bent aangemeld bij uw Azure-account, Hallo **abonnementen beheren** in het dialoogvenster een lijst met abonnementen die gekoppeld aan uw referenties zijn worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="32621-161">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="32621-162">(Als er meerdere abonnementen die worden vermeld en toowork met alleen een specifieke subset van deze gewenste, u kan desgewenst uitschakelen Hallo-abonnementen die u niet wilt dat toouse.) Wanneer u uw abonnementen hebt geselecteerd, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="32621-162">(If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello subscriptions you don't want toouse.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Abonnementen beheren][08]
4. <span data-ttu-id="32621-164">Wanneer Hallo **tooAzure Web-App-Container implementeren** dialoogvenster wordt weergegeven, wordt deze in een Web-App-containers die u eerder hebt gemaakt weergegeven; als u geen containers niet gemaakt hebt, Hallo lijst is leeg.</span><span class="sxs-lookup"><span data-stu-id="32621-164">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![App-Containers][09]
5. <span data-ttu-id="32621-166">Als u geen hebt gemaakt een Azure-Web-App-Container vóór of als u wilt toopublish uw toepassing tooa nieuwe container, gebruik Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="32621-166">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="32621-167">Anders selecteert u een bestaande Web-App-Container en skip-toostep 6 hieronder.</span><span class="sxs-lookup"><span data-stu-id="32621-167">Otherwise, select an existing Web App Container and skip toostep 6 below.</span></span>
   
   1. <span data-ttu-id="32621-168">Klik op**+**</span><span class="sxs-lookup"><span data-stu-id="32621-168">Click **+**</span></span>
      
       ![App-Container toevoegen][10]
   2. <span data-ttu-id="32621-170">Hallo **nieuwe Web-App-Container** in het dialoogvenster wordt weergegeven, die worden gebruikt voor Hallo naast verschillende stappen.</span><span class="sxs-lookup"><span data-stu-id="32621-170">hello **New Web App Container** dialog box will be displayed, which will be used for hello next several steps.</span></span>
      
       ![Nieuwe App-Container][11a]
   3. <span data-ttu-id="32621-172">Voer een **DNS-Label** voor uw Web-App-Container; vormt dit Hallo leaf DNS-label van Hallo host-URL voor uw webtoepassing in Azure.</span><span class="sxs-lookup"><span data-stu-id="32621-172">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="32621-173">Houd er rekening mee dat Hallo-naam moet beschikbaar zijn en voldoen naamgevingsvereisten tooAzure voor Web-App.</span><span class="sxs-lookup"><span data-stu-id="32621-173">Note that hello name must be available and conform tooAzure Web App naming requirements.</span></span>
   4. <span data-ttu-id="32621-174">In Hallo **webcontainer** vervolgkeuzelijst, selecteer Hallo geschikte software voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="32621-174">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="32621-175">U kunt op dit moment van Tomcat-8, 7 Tomcat of Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="32621-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="32621-176">Een recente distributie van software Hallo geselecteerd door Azure worden verstrekt en het wordt uitgevoerd op een recente verdeling van JDK 8 gemaakt door Oracle en geleverd door Azure.</span><span class="sxs-lookup"><span data-stu-id="32621-176">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="32621-177">In Hallo **abonnement** vervolgkeuzelijst, selecteer Hallo abonnement gewenste toouse voor deze implementatie.</span><span class="sxs-lookup"><span data-stu-id="32621-177">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="32621-178">In Hallo **resourcegroep** vervolgkeuzelijst, selecteer Hallo resourcegroep waarmee u tooassociate uw Web-App wilt.</span><span class="sxs-lookup"><span data-stu-id="32621-178">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="32621-179">(Azure resourcegroepen kunt u toogroup verwante resources samen zodat bijvoorbeeld ze samen kunnen worden verwijderd.)</span><span class="sxs-lookup"><span data-stu-id="32621-179">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="32621-180">U kunt een bestaande resourcegroep selecteren (als u een hebt) en overslaan toostep g onderstaande of gebruik Hallo volgende stappen toocreate een nieuwe resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="32621-180">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="32621-181">Selecteer  **&lt; &lt; nieuwe resourcegroep maken &gt; &gt;**  in Hallo **resourcegroep** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="32621-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in hello **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="32621-182">Hallo **nieuwe resourcegroep** in het dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="32621-182">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Nieuwe resourcegroep][12]
      * <span data-ttu-id="32621-184">In Hallo Hallo **naam** textbox, Geef een naam voor uw nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="32621-184">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="32621-185">In Hallo Hallo **regio** vervolgkeuzelijst, selecteer Hallo juiste Azure datacentrum locatie voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="32621-185">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="32621-186">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="32621-186">Click **OK**.</span></span>
   7. <span data-ttu-id="32621-187">Hallo **App Service-Plan** vervolgkeuzelijst bevat Hallo-app service-abonnementen die zijn gekoppeld aan Hallo resourcegroep die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="32621-187">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="32621-188">(Een App Service-Plan bevat informatie zoals Hallo-locatie van uw Web-App Hallo prijscategorie en Hallo compute exemplaargrootte.</span><span class="sxs-lookup"><span data-stu-id="32621-188">(An App Service Plan specifies information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="32621-189">Een enkele App Service-Plan kan worden gebruikt voor meerdere Web-Apps, dat is waarom deze afzonderlijk van een specifieke implementatie van Web-App onderhouden.)</span><span class="sxs-lookup"><span data-stu-id="32621-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="32621-190">Selecteer een bestaand App Service-abonnement (als u een hebt) en toostep h onderstaande overslaan of gebruik een Hallo stappen toocreate een nieuwe App Service-Plan te volgen:</span><span class="sxs-lookup"><span data-stu-id="32621-190">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="32621-191">Selecteer  **&lt; &lt; maken nieuwe App Service-Plan &gt; &gt;**  in Hallo **App Service-Plan** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="32621-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in hello **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="32621-192">Hallo **nieuwe App Service-Plan** in het dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="32621-192">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Nieuwe App Service-abonnement][13]
      * <span data-ttu-id="32621-194">In Hallo Hallo **naam** textbox, Geef een naam voor uw nieuwe App Service-Plan.</span><span class="sxs-lookup"><span data-stu-id="32621-194">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="32621-195">In Hallo Hallo **locatie** vervolgkeuzelijst, selecteer Hallo juiste Azure datacentrum locatie voor Hallo plan.</span><span class="sxs-lookup"><span data-stu-id="32621-195">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="32621-196">In Hallo Hallo **prijscategorie** vervolgkeuzelijst, selecteer Hallo toepasselijke prijzen voor Hallo plan.</span><span class="sxs-lookup"><span data-stu-id="32621-196">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="32621-197">Voor testdoeleinden kunt u **vrije**.</span><span class="sxs-lookup"><span data-stu-id="32621-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="32621-198">In Hallo Hallo **Exemplaargrootte** vervolgkeuzelijst, selecteer Hallo juiste exemplaargrootte voor Hallo plan.</span><span class="sxs-lookup"><span data-stu-id="32621-198">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="32621-199">Voor testdoeleinden kunt u **kleine**.</span><span class="sxs-lookup"><span data-stu-id="32621-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="32621-200">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="32621-200">Click **OK**.</span></span>
   8. <span data-ttu-id="32621-201">(Optioneel) Standaard worden een recente verdeling van Java 8 automatisch geïmplementeerd als uw JVM door Azure tooyour web-app-container.</span><span class="sxs-lookup"><span data-stu-id="32621-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure tooyour web app container.</span></span> <span data-ttu-id="32621-202">U kunt echter een andere versie en de distributie van Hallo JVM selecteren.</span><span class="sxs-lookup"><span data-stu-id="32621-202">However, you can select a different version and distribution of hello JVM.</span></span> <span data-ttu-id="32621-203">toodo gebruik dus Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="32621-203">toodo so, use hello following steps:</span></span>
      
      * <span data-ttu-id="32621-204">Klik op Hallo **JDK** tabblad in Hallo **nieuwe Web-App-Container** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="32621-204">Click hello **JDK** tab in hello **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="32621-205">U kunt kiezen uit een Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="32621-205">You can choose from one of hello following options:</span></span>
        
        * <span data-ttu-id="32621-206">Hallo standaard JDK die wordt aangeboden door Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="32621-206">Deploy hello default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="32621-207">Een 3e party JDK uit een vervolgkeuzelijst van aanvullende JDKs die beschikbaar op Azure zijn implementeren</span><span class="sxs-lookup"><span data-stu-id="32621-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="32621-208">Implementeren van een aangepaste JDK die moet worden opgenomen als een ZIP-bestand en een openbaar of in uw Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="32621-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Nieuw App-Container JDK tabblad][11b]
   9. <span data-ttu-id="32621-210">Nadat u alle Hallo bovenstaande stappen hebt voltooid, ziet er Hallo nieuwe Web-App-Container dialoogvenster Hallo volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="32621-210">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![Nieuwe App-Container][14]
   10. <span data-ttu-id="32621-212">Klik op **OK** toocomplete Hallo maken van uw nieuwe Web-App-container.</span><span class="sxs-lookup"><span data-stu-id="32621-212">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="32621-213">Wacht een paar seconden voor Hallo lijst met Hallo Web-App containers toobe vernieuwd en de zojuist gemaakte web-app-container moet nu worden geselecteerd in het Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="32621-213">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
6. <span data-ttu-id="32621-214">U bent nu klaar toocomplete Hallo initiële implementatie van uw Web-App tooAzure; Klik op **OK** toodeploy uw Java-toepassing toohello geselecteerd Web-App-container.</span><span class="sxs-lookup"><span data-stu-id="32621-214">You are now ready toocomplete hello initial deployment of your Web App tooAzure; click **OK** toodeploy your Java application toohello selected Web App container.</span></span> <span data-ttu-id="32621-215">Standaard wordt uw toepassing wordt geïmplementeerd als een submap van de toepassingsserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="32621-215">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="32621-216">Als u toobe geïmplementeerd als de hoofdtoepassing hello wilt, Controleer Hallo **implementeren tooroot** selectievakje voordat u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="32621-216">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
   
    ![TooAzure implementeren][15]
7. <span data-ttu-id="32621-218">Vervolgens ziet u Hallo **Azure Activity Log** waarmee wordt aangegeven Hallo implementatiestatus van uw Web-App bekijken.</span><span class="sxs-lookup"><span data-stu-id="32621-218">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![Voortgangsindicator][16]
   
    <span data-ttu-id="32621-220">Hallo-proces voor het implementeren van uw Web-App tooAzure duurt slechts enkele seconden toocomplete.</span><span class="sxs-lookup"><span data-stu-id="32621-220">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="32621-221">Wanneer uw toepassing ready, ziet u een koppeling met de naam **gepubliceerde** in Hallo **Status** kolom.</span><span class="sxs-lookup"><span data-stu-id="32621-221">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="32621-222">Wanneer u Hallo koppeling klikt, duurt het u startpagina tooyour geïmplementeerd van Web-App of kunt u Hallo stappen in de volgende sectie toobrowse tooyour web-app Hallo.</span><span class="sxs-lookup"><span data-stu-id="32621-222">When you click hello link, it will take you tooyour deployed Web App's home page, or you can use hello steps in hello following section toobrowse tooyour web app.</span></span>

## <a name="browsing-tooyour-web-app-on-azure"></a><span data-ttu-id="32621-223">Bladeren door tooyour Web-App in Azure</span><span class="sxs-lookup"><span data-stu-id="32621-223">Browsing tooyour Web App on Azure</span></span>
<span data-ttu-id="32621-224">toobrowse tooyour Web-App in Azure, kunt u Hallo **Azure Explorer** weergeven.</span><span class="sxs-lookup"><span data-stu-id="32621-224">toobrowse tooyour Web App on Azure, you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="32621-225">Als hello **Azure Explorer** weergave nog niet is geopend, kunt u deze openen door te klikken op vervolgens **weergave** menu in IntelliJ, klikt u vervolgens op **hulpprogramma Windows**, en klik vervolgens op  **Service-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="32621-225">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="32621-226">Als u eerder niet hebt aangemeld, wordt u gevraagd toodo dus.</span><span class="sxs-lookup"><span data-stu-id="32621-226">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="32621-227">Wanneer Hallo **Azure Explorer** weergave wordt weergegeven, gebruik Volg deze stappen toobrowse tooyour Web-App:</span><span class="sxs-lookup"><span data-stu-id="32621-227">When hello **Azure Explorer** view is displayed, use follow these steps toobrowse tooyour Web App:</span></span> 

1. <span data-ttu-id="32621-228">Vouw Hallo **Azure** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="32621-228">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="32621-229">Vouw Hallo **Web-Apps** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="32621-229">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="32621-230">Klik met de rechtermuisknop Hallo gewenste Web-App.</span><span class="sxs-lookup"><span data-stu-id="32621-230">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="32621-231">Wanneer het Hallo-contextmenu wordt weergegeven, klikt u op **openen in Browser**.</span><span class="sxs-lookup"><span data-stu-id="32621-231">When hello context menu appears, click **Open in Browser**.</span></span>
   
    ![Web-App bladeren][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="32621-233">De web-app beveiligen</span><span class="sxs-lookup"><span data-stu-id="32621-233">Updating your web app</span></span>
<span data-ttu-id="32621-234">Bijwerken van een bestaande Azure-Web-App uitgevoerd is een snelle en eenvoudige proces en hebt u twee opties voor het bijwerken van:</span><span class="sxs-lookup"><span data-stu-id="32621-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="32621-235">U kunt Hallo-implementatie van een bestaande Java-Web-App kunt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="32621-235">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="32621-236">U kunt een extra toohello voor Java-toepassing publiceren dezelfde Web-App-Container.</span><span class="sxs-lookup"><span data-stu-id="32621-236">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="32621-237">In beide gevallen Hallo proces identieke en duurt slechts enkele seconden:</span><span class="sxs-lookup"><span data-stu-id="32621-237">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="32621-238">Hallo IntelliJ Projectverkenner met de rechtermuisknop op Hallo Java-toepassing die u wilt dat tooupdate of tooan bestaande Web-App-Container toevoegen.</span><span class="sxs-lookup"><span data-stu-id="32621-238">In hello IntelliJ project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="32621-239">Wanneer het Hallo-contextmenu wordt weergegeven, selecteert u **Azure** en vervolgens **publiceren als Azure-Web-App...**</span><span class="sxs-lookup"><span data-stu-id="32621-239">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="32621-240">Nadat u hebt al aangemeld eerder, ziet u een lijst met uw bestaande Web-App-containers.</span><span class="sxs-lookup"><span data-stu-id="32621-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="32621-241">Selecteer een of wilt u toopublish opnieuw publiceren, uw Java-toepassing tooand Klik Hallo **OK**.</span><span class="sxs-lookup"><span data-stu-id="32621-241">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="32621-242">Een paar seconden later Hallo **Azure Activity Log** weer uw bijgewerkte implementatie als **gepubliceerde** en u kunt tooverify uw bijgewerkte toepassing in een webbrowser worden.</span><span class="sxs-lookup"><span data-stu-id="32621-242">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="32621-243">Starten, stoppen of opnieuw starten van een bestaande web-app</span><span class="sxs-lookup"><span data-stu-id="32621-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="32621-244">toostart of stoppen van een bestaande Azure-Web-App-container (inclusief alle Hallo geïmplementeerd Java-toepassingen in deze), kunt u Hallo **Azure Explorer** weergeven.</span><span class="sxs-lookup"><span data-stu-id="32621-244">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="32621-245">Als hello **Azure Explorer** weergave nog niet is geopend, kunt u deze openen door te klikken op vervolgens **weergave** menu in IntelliJ, klikt u vervolgens op **hulpprogramma Windows**, en klik vervolgens op  **Service-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="32621-245">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="32621-246">Als u eerder niet hebt aangemeld, wordt u gevraagd toodo dus.</span><span class="sxs-lookup"><span data-stu-id="32621-246">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="32621-247">Wanneer Hallo **Azure Explorer** weergave wordt weergegeven, gebruik Volg deze stappen toostart of stoppen van uw Web-App:</span><span class="sxs-lookup"><span data-stu-id="32621-247">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="32621-248">Vouw Hallo **Azure** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="32621-248">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="32621-249">Vouw Hallo **Web-Apps** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="32621-249">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="32621-250">Klik met de rechtermuisknop Hallo gewenste Web-App.</span><span class="sxs-lookup"><span data-stu-id="32621-250">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="32621-251">Wanneer het Hallo-contextmenu wordt weergegeven, klikt u op **Start**, **stoppen**, of **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="32621-251">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="32621-252">Houd er rekening mee dat Hallo menu-Opties contextbewuste, zijn zodat u kunt alleen een actieve WebApp stoppen of starten van een web-app die niet wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="32621-252">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Web-App stoppen][18]

## <a name="next-steps"></a><span data-ttu-id="32621-254">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="32621-254">Next Steps</span></span>
<span data-ttu-id="32621-255">Zie voor meer informatie over hello Azure Toolkits voor IDE voor Java Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="32621-255">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="32621-256">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="32621-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="32621-257">[Hello Azure Toolkit voor Eclipse installeren]</span><span class="sxs-lookup"><span data-stu-id="32621-257">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="32621-258">[Een Hallo wereld Web-App maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="32621-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="32621-259">[Wat is er nieuw in hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="32621-259">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="32621-260">[Azure Toolkit voor IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="32621-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="32621-261">[installeren hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="32621-261">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="32621-262">*Een Hallo wereld Web-App maken voor Azure in IntelliJ (in dit artikel)*</span><span class="sxs-lookup"><span data-stu-id="32621-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="32621-263">[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="32621-263">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="32621-264">Zie ook</span><span class="sxs-lookup"><span data-stu-id="32621-264">See Also</span></span>
<span data-ttu-id="32621-265">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="32621-265">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="32621-266">Zie voor meer informatie over het maken van Azure Web Apps Hallo [overzicht van Web Apps].</span><span class="sxs-lookup"><span data-stu-id="32621-266">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit voor IntelliJ]: ../azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld Web-App maken voor Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Hello Azure Toolkit voor Eclipse installeren]: ../azure-toolkit-for-eclipse-installation.md
[installeren hello Azure Toolkit voor IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Wat is er nieuw in hello Azure Toolkit voor Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[overzicht van Web Apps]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
