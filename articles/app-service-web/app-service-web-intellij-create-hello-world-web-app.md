---
title: Een eenvoudige Azure-web-app maken in IntelliJ | Microsoft Docs
description: Deze zelfstudie laat zien hoe de Azure-werkset voor IntelliJ gebruiken voor het maken van een Hello World Web-App voor Azure.
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
ms.openlocfilehash: 20b2c3d86f5bde9302647f345aa99b030d78613a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="5ea0b-103">Een eenvoudige Azure-web-app maken in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5ea0b-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="5ea0b-104">Deze zelfstudie laat zien hoe maken en implementeren van een eenvoudige toepassing van Hallo wereld naar Azure als een Web-App met behulp van de [Azure Toolkit voor IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="5ea0b-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="5ea0b-105">Een eenvoudige JSP-voorbeeld voor eenvoud wordt weergegeven, maar gelijksoortige stappen zou zijn geschikt voor een servlet Java wat betreft Azure-implementatie is.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="5ea0b-106">Wanneer u deze zelfstudie hebt voltooid, ziet uw toepassing er ongeveer als de volgende afbeelding wanneer u deze in een webbrowser bekijken:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Voorbeeldwebpagina][01]

## <a name="prerequisites"></a><span data-ttu-id="5ea0b-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5ea0b-108">Prerequisites</span></span>
* <span data-ttu-id="5ea0b-109">Een Java Developer Kit (JDK), v 1.8 of hoger.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="5ea0b-110">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="5ea0b-111">Dit kan worden gedownload vanaf <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="5ea0b-112">Een distributiepunt van een Java gebaseerde webserver of toepassingsserver, zoals [Apache Tomcat] of [Jetty].</span><span class="sxs-lookup"><span data-stu-id="5ea0b-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="5ea0b-113">Een Azure-abonnement, die kan worden opgehaald uit <https://azure.microsoft.com/free/> of <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="5ea0b-114">De [Azure Toolkit voor IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="5ea0b-114">The [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="5ea0b-115">Zie voor meer informatie over het installeren van de Azure-Toolkit [Toolkit Azure installeren voor IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="5ea0b-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ].</span></span>

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="5ea0b-116">Een toepassing Hello World maken</span><span class="sxs-lookup"><span data-stu-id="5ea0b-116">To create a Hello World application</span></span>
<span data-ttu-id="5ea0b-117">Eerst beginnen we uitschakelen met een Java-project maken.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="5ea0b-118">IntelliJ Start en klik op de **bestand** menu, klikt u vervolgens op **nieuw**, en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-118">Start IntelliJ and click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![Bestand Nieuw Project][02]
2. <span data-ttu-id="5ea0b-120">Selecteer in het dialoogvenster Nieuw Project **Java**, klikt u vervolgens **webtoepassing**, en klik vervolgens op **nieuw** toevoegen van een Project-SDK.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-120">In the New Project dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
    ![Het dialoogvenster Nieuw project][03a]
   
3. <span data-ttu-id="5ea0b-122">Selecteer de map waarin uw JDK is geïnstalleerd en klik vervolgens op in de basismap selecteren voor het dialoogvenster JDK, **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-122">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="5ea0b-123">Klik op **volgende** in het dialoogvenster Nieuw Project om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-123">Click **Next** in the New Project dialog box to continue.</span></span>
   
    ![Basismap van de JDK opgeven][03b]
4. <span data-ttu-id="5ea0b-125">Noem het project voor deze zelfstudie **Java-Web-App-op-Azure**, en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-125">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Het dialoogvenster Nieuw project][04]
5. <span data-ttu-id="5ea0b-127">Vouw in de weergave Project Explorer van IntelliJ **Java-Web-App-op-Azure**, vouw vervolgens **web**, en dubbelklik vervolgens op **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Open indexpagina][05c]
6. <span data-ttu-id="5ea0b-129">Wanneer het bestand index.jsp wordt geopend in IntelliJ, toevoegen in de tekst die moet dynamisch weergeven **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="5ea0b-129">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="5ea0b-130">in het bestaande `<body>`-element.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-130">within the existing `<body>` element.</span></span> <span data-ttu-id="5ea0b-131">Uw bijgewerkte `<body>` inhoud moet eruitzien als in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-131">Your updated `<body>` content should resemble the following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="5ea0b-132">Index.jsp opslaan.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-132">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="5ea0b-133">Voor het implementeren van uw toepassing in een Azure-Web-App-Container</span><span class="sxs-lookup"><span data-stu-id="5ea0b-133">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="5ea0b-134">Er zijn verschillende manieren waarop u een Java-webtoepassing naar Azure kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-134">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="5ea0b-135">Deze zelfstudie wordt beschreven in een van de eenvoudigste: uw toepassing wordt geïmplementeerd op een Azure-Web-App-Container - geen speciale projecttype of extra hulpprogramma's nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-135">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="5ea0b-136">De JDK en de software van de container web worden geleverd voor u door Azure, zodat er geen nodig is voor het uploaden van uw eigen; u hoeft uw Java-Web-App is.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-136">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="5ea0b-137">Als gevolg hiervan wordt het publicatieproces voor uw toepassing seconden, niet minuten duren.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-137">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="5ea0b-138">Voordat u uw toepassing publiceren, moet u eerst uw module-instellingen configureren.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-138">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="5ea0b-139">Volg hiervoor de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-139">To do so, use the following steps:</span></span>

1. <span data-ttu-id="5ea0b-140">In de IntelliJ Projectverkenner met de rechtermuisknop op de **Java-Web-App-op-Azure** project.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-140">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="5ea0b-141">Wanneer het contextmenu wordt weergegeven, klikt u op **Open Module-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-141">When the context menu appears, click **Open Module Settings**.</span></span>

    ![Open de Module-instellingen][05a]
2. <span data-ttu-id="5ea0b-143">Wanneer het projectstructuur dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-143">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="5ea0b-144">a.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-144">a.</span></span> <span data-ttu-id="5ea0b-145">Klik op **artefacten** in de lijst met **projectinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-145">Click **Artifacts** in the list of **Project Settings**.</span></span>
   <span data-ttu-id="5ea0b-146">b.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-146">b.</span></span> <span data-ttu-id="5ea0b-147">Wijzig de naam van het artefact in de **naam** vak zodat het geen spaties of speciale tekens bevat; dit is nodig omdat de naam wordt gebruikt in de Uniform Resource Identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="5ea0b-147">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="5ea0b-148">c.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-148">c.</span></span> <span data-ttu-id="5ea0b-149">Wijzig de **Type** naar **webtoepassing: archief**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-149">Change the **Type** to **Web Application: Archive**.</span></span>
   <span data-ttu-id="5ea0b-150">d.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-150">d.</span></span> <span data-ttu-id="5ea0b-151">Klik op **OK** om het projectstructuur dialoogvenster te sluiten.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-151">Click **OK** to close the Project Structure dialog box.</span></span>

    ![Open de Module-instellingen][05b]

<span data-ttu-id="5ea0b-153">Wanneer u uw module-instellingen hebt geconfigureerd, kunt u uw toepassing in Azure publiceren met behulp van de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-153">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="5ea0b-154">In de IntelliJ Projectverkenner met de rechtermuisknop op de **Java-Web-App-op-Azure** project.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-154">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="5ea0b-155">Wanneer het contextmenu wordt weergegeven, selecteert u **Azure**, en klik vervolgens op **publiceren als Azure-Web-App...**</span><span class="sxs-lookup"><span data-stu-id="5ea0b-155">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Azure contextmenu publiceren][06]
2. <span data-ttu-id="5ea0b-157">Als u hebt nog niet aangemeld bij Azure van IntelliJ, wordt u gevraagd om aan te melden bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-157">If you have not already signed into Azure from IntelliJ, you will be prompted to sign into your Azure account.</span></span> <span data-ttu-id="5ea0b-158">(Als er meerdere Azure-accounts, enkele van de prompts tijdens de aanmelding in proces worden mogelijk weergegeven meer dan één keer, zelfs als ze niet dezelfde worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-158">(If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="5ea0b-159">Als dit gebeurt, blijven de aanmeldingspagina instructies te volgen.)</span><span class="sxs-lookup"><span data-stu-id="5ea0b-159">When this happens, continue to follow the sign in instructions.)</span></span>
   
    ![Azure-logboekanalyse In het dialoogvenster][07]
3. <span data-ttu-id="5ea0b-161">Nadat u zich heeft aangemeld bij uw Azure-account, de **abonnementen beheren** in het dialoogvenster een lijst met abonnementen die gekoppeld aan uw referenties zijn worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-161">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="5ea0b-162">(Als er zijn meerdere abonnementen weergegeven en u wilt werken met alleen een specifieke subset van deze, u kunt desgewenst uitschakelen de abonnementen die u niet wilt gebruiken.) Wanneer u uw abonnementen hebt geselecteerd, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-162">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Abonnementen beheren][08]
4. <span data-ttu-id="5ea0b-164">Wanneer de **implementeren in Azure Web App-Container** dialoogvenster wordt weergegeven, wordt deze in een Web-App-containers die u eerder hebt gemaakt weergegeven; als u geen containers niet gemaakt hebt, wordt de lijst leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-164">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
    ![App-Containers][09]
5. <span data-ttu-id="5ea0b-166">Als u een Azure Web App-Container voordat niet hebt gemaakt, of als u uw toepassing naar een nieuwe container publiceren, gebruikt u de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-166">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="5ea0b-167">Anders selecteert u een bestaande Web-App-Container en gaat u verder met stap 6 hieronder.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-167">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   1. <span data-ttu-id="5ea0b-168">Klik op**+**</span><span class="sxs-lookup"><span data-stu-id="5ea0b-168">Click **+**</span></span>
      
       ![App-Container toevoegen][10]
   2. <span data-ttu-id="5ea0b-170">De **nieuwe Web-App-Container** in het dialoogvenster wordt weergegeven, die wordt gebruikt voor de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-170">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
       ![Nieuwe App-Container][11a]
   3. <span data-ttu-id="5ea0b-172">Voer een **DNS-Label** voor uw Web-App-Container; vormt dit het leaf DNS-label van de host-URL voor uw webtoepassing in Azure.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-172">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="5ea0b-173">Houd er rekening mee dat de naam moet beschikbaar zijn en voldoen aan de naamgeving van de vereisten voor Azure-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-173">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>
   4. <span data-ttu-id="5ea0b-174">In de **webcontainer** vervolgkeuzelijst, selecteer de juiste software voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-174">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
       <span data-ttu-id="5ea0b-175">U kunt op dit moment van Tomcat-8, 7 Tomcat of Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="5ea0b-176">Een recente distributie van de geselecteerde software door Azure worden verstrekt en het wordt uitgevoerd op een recente verdeling van JDK 8 gemaakt door Oracle en geleverd door Azure.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-176">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="5ea0b-177">In de **abonnement** vervolgkeuzelijst, selecteer het abonnement dat u wilt gebruiken voor deze implementatie.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>
   6. <span data-ttu-id="5ea0b-178">In de **resourcegroep** vervolgkeuzelijst, selecteer de resourcegroep die u wilt koppelen van uw Web-App.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-178">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="5ea0b-179">(Azure resourcegroepen kunt u voor het groeperen van gerelateerde resources samen zodat bijvoorbeeld ze samen kunnen worden verwijderd.)</span><span class="sxs-lookup"><span data-stu-id="5ea0b-179">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="5ea0b-180">U kunt Selecteer een bestaande resourcegroep (als u een hebt) en overslaan naar stap g onderstaande of gebruik de volgende stappen om een nieuwe resourcegroep te maken:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-180">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="5ea0b-181">Selecteer  **&lt; &lt; nieuwe resourcegroep maken &gt; &gt;**  in de **resourcegroep** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="5ea0b-182">De **nieuwe resourcegroep** in het dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-182">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Nieuwe resourcegroep][12]
      * <span data-ttu-id="5ea0b-184">In de de **naam** textbox, Geef een naam voor uw nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-184">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="5ea0b-185">In de de **regio** vervolgkeuzelijst, selecteer de juiste Azure datacentrum locatie voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-185">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="5ea0b-186">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-186">Click **OK**.</span></span>
   7. <span data-ttu-id="5ea0b-187">De **App Service-Plan** vervolgkeuzelijst geeft een lijst van de app service-abonnementen die zijn gekoppeld aan de resourcegroep die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-187">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="5ea0b-188">(Een App Service-Plan bevat informatie zoals de locatie van uw Web-App, de prijscategorie en de grootte van de compute-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-188">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="5ea0b-189">Een enkele App Service-Plan kan worden gebruikt voor meerdere Web-Apps, dat is waarom deze afzonderlijk van een specifieke implementatie van Web-App onderhouden.)</span><span class="sxs-lookup"><span data-stu-id="5ea0b-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="5ea0b-190">U kunt een bestaand App Service-abonnement (als u een hebt) en overslaan voor selecteren h onderstaande stap of gebruik de volgende stappen voor het maken van een nieuwe App Service-Plan:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-190">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="5ea0b-191">Selecteer  **&lt; &lt; maken nieuwe App Service-Plan &gt; &gt;**  in de **App Service-Plan** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="5ea0b-192">De **nieuwe App Service-Plan** in het dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-192">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Nieuwe App Service-abonnement][13]
      * <span data-ttu-id="5ea0b-194">In de de **naam** textbox, Geef een naam voor uw nieuwe App Service-Plan.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-194">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="5ea0b-195">In de de **locatie** vervolgkeuzelijst, selecteer de juiste Azure datacentrum locatie voor het plan.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-195">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="5ea0b-196">In de de **prijscategorie** vervolgkeuzelijst, selecteer de juiste prijs voor het plan.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-196">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="5ea0b-197">Voor testdoeleinden kunt u **vrije**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="5ea0b-198">In de de **Exemplaargrootte** vervolgkeuzelijst, selecteer het juiste exemplaar grootte voor het plan.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-198">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="5ea0b-199">Voor testdoeleinden kunt u **kleine**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="5ea0b-200">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-200">Click **OK**.</span></span>
   8. <span data-ttu-id="5ea0b-201">(Optioneel) Standaard worden een recente verdeling van Java 8 automatisch geïmplementeerd als uw JVM door Azure voor uw web-app-container.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="5ea0b-202">U kunt echter een andere versie en de distributie van de JVM selecteren.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-202">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="5ea0b-203">Volg hiervoor de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-203">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="5ea0b-204">Klik op de **JDK** tabblad de **nieuwe Web-App-Container** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-204">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="5ea0b-205">U kunt kiezen uit een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-205">You can choose from one of the following options:</span></span>
        
        * <span data-ttu-id="5ea0b-206">De standaardwaarde JDK die wordt aangeboden door Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="5ea0b-206">Deploy the default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="5ea0b-207">Een 3e party JDK uit een vervolgkeuzelijst van aanvullende JDKs die beschikbaar op Azure zijn implementeren</span><span class="sxs-lookup"><span data-stu-id="5ea0b-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="5ea0b-208">Implementeren van een aangepaste JDK die moet worden opgenomen als een ZIP-bestand en een openbaar of in uw Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="5ea0b-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Nieuw App-Container JDK tabblad][11b]
   9. <span data-ttu-id="5ea0b-210">Nadat u alle bovenstaande stappen hebt voltooid, moet het dialoogvenster Nieuwe Web-App-Container zijn vergelijkbaar met de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-210">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
       ![Nieuwe App-Container][14]
   10. <span data-ttu-id="5ea0b-212">Klik op **OK** voor het maken van uw nieuwe Web-App-container niet voltooien.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-212">Click **OK** to complete the creation of your new Web App container.</span></span>
       
        <span data-ttu-id="5ea0b-213">Wacht een paar seconden voor een overzicht van de Web-App-containers worden vernieuwd en de zojuist gemaakte web-app-container moet nu worden geselecteerd in de lijst.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-213">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>
6. <span data-ttu-id="5ea0b-214">U bent nu klaar voor het uitvoeren van de eerste implementatie van uw Web-App in Azure; Klik op **OK** voor het implementeren van uw Java-toepassing aan de geselecteerde container van Web-App.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-214">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="5ea0b-215">Standaard wordt uw toepassing wordt geïmplementeerd als een submap van de toepassingsserver.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-215">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="5ea0b-216">Als u wilt dat deze worden geïmplementeerd als de hoofdtoepassing, controleert u de **implementeren in de hoofdmap** selectievakje voordat u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-216">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
    ![Implementeren in Azure][15]
7. <span data-ttu-id="5ea0b-218">Vervolgens ziet u de **Azure Activity Log** weergave, die de status van de implementatie van uw Web-App wordt aangegeven.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-218">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
    ![Voortgangsindicator][16]
   
    <span data-ttu-id="5ea0b-220">Het proces voor het implementeren van uw Web-App naar Azure duren slechts een paar seconden.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-220">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="5ea0b-221">Wanneer uw toepassing ready, ziet u een koppeling met de naam **gepubliceerde** in de **Status** kolom.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-221">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="5ea0b-222">Wanneer u de koppeling klikt, wordt deze gaat u naar de startpagina van de geïmplementeerde Web-App of kunt u de stappen in de volgende sectie om te bladeren naar uw web-app.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-222">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

## <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="5ea0b-223">Bladeren naar uw Web-App in Azure</span><span class="sxs-lookup"><span data-stu-id="5ea0b-223">Browsing to your Web App on Azure</span></span>
<span data-ttu-id="5ea0b-224">Om te bladeren naar uw Web-App in Azure, kunt u de **Azure Explorer** weergeven.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-224">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="5ea0b-225">Als de **Azure Explorer** weergave nog niet is geopend, kunt u deze openen door te klikken op vervolgens **weergave** menu in IntelliJ, klikt u vervolgens op **hulpprogramma Windows**, en klik vervolgens op  **Service-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-225">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="5ea0b-226">Als u eerder niet hebt aangemeld, wordt u gevraagd.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-226">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="5ea0b-227">Wanneer de **Azure Explorer** weergave wordt weergegeven, gebruik als volgt te werk om te bladeren naar uw Web-App:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-227">When the **Azure Explorer** view is displayed, use follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="5ea0b-228">Vouw de **Azure** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-228">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="5ea0b-229">Vouw de **Web-Apps** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-229">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="5ea0b-230">Met de rechtermuisknop op de gewenste Web-App.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-230">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="5ea0b-231">Wanneer het contextmenu wordt weergegeven, klikt u op **openen in Browser**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-231">When the context menu appears, click **Open in Browser**.</span></span>
   
    ![Web-App bladeren][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="5ea0b-233">De web-app beveiligen</span><span class="sxs-lookup"><span data-stu-id="5ea0b-233">Updating your web app</span></span>
<span data-ttu-id="5ea0b-234">Bijwerken van een bestaande Azure-Web-App uitgevoerd is een snelle en eenvoudige proces en hebt u twee opties voor het bijwerken van:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="5ea0b-235">U kunt de implementatie van een bestaande Java-Web-App kunt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-235">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="5ea0b-236">U kunt een extra Java-toepassing tot dezelfde Container voor de Web-App publiceren.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-236">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="5ea0b-237">In beide gevallen is het proces identieke en duurt slechts enkele seconden:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-237">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="5ea0b-238">In de Projectverkenner IntelliJ met de rechtermuisknop op de Java-toepassing die u wilt bijwerken of toevoegen aan een bestaande Web-App-Container.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-238">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="5ea0b-239">Wanneer het contextmenu wordt weergegeven, selecteert u **Azure** en vervolgens **publiceren als Azure-Web-App...**</span><span class="sxs-lookup"><span data-stu-id="5ea0b-239">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="5ea0b-240">Nadat u hebt al aangemeld eerder, ziet u een lijst met uw bestaande Web-App-containers.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="5ea0b-241">Selecteer de gewenste publiceren of uw Java-toepassing opnieuw te publiceren en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-241">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="5ea0b-242">Een paar seconden later, de **Azure Activity Log** weer uw bijgewerkte implementatie als **gepubliceerde** en u kunt controleren of uw bijgewerkte toepassing in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-242">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="5ea0b-243">Starten, stoppen of opnieuw starten van een bestaande web-app</span><span class="sxs-lookup"><span data-stu-id="5ea0b-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="5ea0b-244">Om te starten of stoppen van een bestaande Azure-Web-App-container (en alle geïmplementeerde Java-toepassingen erin), kunt u de **Azure Explorer** weergeven.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-244">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="5ea0b-245">Als de **Azure Explorer** weergave nog niet is geopend, kunt u deze openen door te klikken op vervolgens **weergave** menu in IntelliJ, klikt u vervolgens op **hulpprogramma Windows**, en klik vervolgens op  **Service-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-245">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="5ea0b-246">Als u eerder niet hebt aangemeld, wordt u gevraagd.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-246">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="5ea0b-247">Wanneer de **Azure Explorer** weergave wordt weergegeven, gebruik als volgt te werk om te starten of stoppen van uw Web-App:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-247">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="5ea0b-248">Vouw de **Azure** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-248">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="5ea0b-249">Vouw de **Web-Apps** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-249">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="5ea0b-250">Met de rechtermuisknop op de gewenste Web-App.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-250">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="5ea0b-251">Wanneer het contextmenu wordt weergegeven, klikt u op **Start**, **stoppen**, of **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-251">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="5ea0b-252">Houd er rekening mee dat de menu-Opties contextbewuste, zijn zodat u kunt alleen een actieve WebApp stoppen of starten van een web-app die niet wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-252">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Web-App stoppen][18]

## <a name="next-steps"></a><span data-ttu-id="5ea0b-254">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5ea0b-254">Next Steps</span></span>
<span data-ttu-id="5ea0b-255">Voor meer informatie over de Azure Toolkits voor Java-IDE's klikt u op de volgende koppelingen:</span><span class="sxs-lookup"><span data-stu-id="5ea0b-255">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="5ea0b-256">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5ea0b-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5ea0b-257">[Installing the Azure Toolkit for Eclipse] (De Azure Toolkit voor Eclipse installeren)</span><span class="sxs-lookup"><span data-stu-id="5ea0b-257">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5ea0b-258">[Een Hallo wereld Web-App maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5ea0b-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="5ea0b-259">[What's New in the Azure Toolkit for Eclipse] (Nieuw in de Azure Toolkit voor Eclipse)</span><span class="sxs-lookup"><span data-stu-id="5ea0b-259">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="5ea0b-260">[Azure Toolkit voor IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="5ea0b-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5ea0b-261">[Toolkit Azure installeren voor IntelliJ] (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="5ea0b-261">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5ea0b-262">*Een Hallo wereld Web-App maken voor Azure in IntelliJ (in dit artikel)*</span><span class="sxs-lookup"><span data-stu-id="5ea0b-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="5ea0b-263">[What's New in the Azure Toolkit for IntelliJ] (Nieuw in de Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="5ea0b-263">[What's New in the Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="5ea0b-264">Zie ook</span><span class="sxs-lookup"><span data-stu-id="5ea0b-264">See Also</span></span>
<span data-ttu-id="5ea0b-265">In het [Azure Java Developer Center] vindt u meer informatie over het gebruik van Azure met Java.</span><span class="sxs-lookup"><span data-stu-id="5ea0b-265">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="5ea0b-266">Zie voor meer informatie over het maken van Azure Web Apps, de [overzicht van Web Apps].</span><span class="sxs-lookup"><span data-stu-id="5ea0b-266">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit voor IntelliJ]: ../azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld Web-App maken voor Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)
[Toolkit Azure installeren voor IntelliJ]: ../azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)
[What's New in the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md (Nieuw in de Azure Toolkit voor Eclipse)
[What's New in the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md (Nieuw in de Azure Toolkit voor IntelliJ)

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
