---
title: On-premises resources benaderen via hybride verbindingen in Azure App Service
description: Maak een verbinding tussen een web-app in Azure App Service en een on-premises resource die gebruikmaakt van een statische TCP-poort
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: fbd22e6e285c5ddaef2a473671d4a06a97384b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="a3249-103">On-premises resources benaderen via hybride verbindingen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a3249-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="a3249-104">U kunt een Azure App Service-app verbinden met een on-premises resource die gebruikmaakt van een statische TCP-poort, zoals SQL Server, MySQL, HTTP-Web-API's en de meeste aangepaste webservices.</span><span class="sxs-lookup"><span data-stu-id="a3249-104">You can connect an Azure App Service app to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="a3249-105">In dit artikel laat zien hoe een hybride verbinding maken tussen App Service en een on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="a3249-105">This article shows you how to create a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="a3249-106">De Web-Apps-gedeelte van de functie hybride verbindingen is alleen beschikbaar in de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3249-106">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="a3249-107">Zie voor informatie over het maken van een verbinding in BizTalk Services [hybride verbindingen](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="a3249-107">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="a3249-108">Deze inhoud geldt ook voor mobiele Apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a3249-108">This content also applies to Mobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a3249-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a3249-109">Prerequisites</span></span>
* <span data-ttu-id="a3249-110">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a3249-110">An Azure subscription.</span></span> <span data-ttu-id="a3249-111">Zie voor een gratis abonnement [gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3249-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="a3249-112">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="a3249-112">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a3249-113">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="a3249-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="a3249-114">Als u wilt een on-premises SQL Server of SQL Server Express-database met een hybride verbinding gebruiken, moet TCP/IP moet zijn ingeschakeld op een statische poort.</span><span class="sxs-lookup"><span data-stu-id="a3249-114">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="a3249-115">Met behulp van een standaardexemplaar van SQL Server wordt aanbevolen omdat deze gebruikmaakt van statische poort 1433.</span><span class="sxs-lookup"><span data-stu-id="a3249-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="a3249-116">Zie voor meer informatie over het installeren en configureren van SQL Server Express voor gebruik met hybride verbindingen [verbinding maken met een lokale SQL Server uit een Azure-website met behulp van hybride verbindingen](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="a3249-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="a3249-117">De computer waarop u de lokale hybride Verbindingsbeheer agent beschreven verderop in dit artikel installeert:</span><span class="sxs-lookup"><span data-stu-id="a3249-117">The computer on which you install the on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="a3249-118">Moet verbinding maken met Azure via poort 5671</span><span class="sxs-lookup"><span data-stu-id="a3249-118">Must be able to connect to Azure over port 5671</span></span>
  * <span data-ttu-id="a3249-119">Moet kunnen bereiken de *hostnaam*:*portnumber* van uw lokale resource.</span><span class="sxs-lookup"><span data-stu-id="a3249-119">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="a3249-120">De stappen in dit artikel wordt ervan uitgegaan dat u gebruikmaakt van de browser van de computer die als host voor de lokale-agent voor hybride verbinding fungeert.</span><span class="sxs-lookup"><span data-stu-id="a3249-120">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="a3249-121">Een web-app maken in de Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="a3249-121">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="a3249-122">Als u al een web-app of een back-end voor mobiele App in de Azure-Portal die u wilt gebruiken voor deze zelfstudie hebt gemaakt, kunt u verder gaan naar [een hybride verbinding en een BizTalk Service maken](#CreateHC) en van daaruit starten.</span><span class="sxs-lookup"><span data-stu-id="a3249-122">If you have already created a web app or Mobile App backend in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="a3249-123">In de linkerbovenhoek van de [Azure Portal](https://portal.azure.com), klikt u op **nieuw** > **Web en mobiel** > **Web-App**.</span><span class="sxs-lookup"><span data-stu-id="a3249-123">In the upper left corner of the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![Nieuwe web-app][NewWebsite]
2. <span data-ttu-id="a3249-125">Op de **Web-app** blade een URL op en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="a3249-125">On the **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Websitenaam][WebsiteCreationBlade]
3. <span data-ttu-id="a3249-127">Na enkele ogenblikken de web-app wordt gemaakt en de blade web-app wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a3249-127">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="a3249-128">De blade is een verticaal schuifbare dashboard waarmee u uw site beheren.</span><span class="sxs-lookup"><span data-stu-id="a3249-128">The blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Website worden uitgevoerd][WebSiteRunningBlade]
4. <span data-ttu-id="a3249-130">Om te controleren of de site is live, klikt u op de **Bladeren** pictogram om de standaardpagina weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a3249-130">To verify the site is live, you can click the **Browse** icon to display the default page.</span></span>
   
    ![Klik op Bladeren als u wilt zien van uw web-app][Browse]
   
    ![App-standaardwebpagina][DefaultWebSitePage]

<span data-ttu-id="a3249-133">Vervolgens maakt u een hybride verbinding en een BizTalk service voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="a3249-133">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="a3249-134">Een hybride verbinding en een BizTalk Service maken</span><span class="sxs-lookup"><span data-stu-id="a3249-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="a3249-135">Klik in de blade van uw web-app op **alle instellingen** > **Networking** > **uw hybride-verbindingseindpunten configureren**.</span><span class="sxs-lookup"><span data-stu-id="a3249-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Hybride verbindingen][CreateHCHCIcon]
2. <span data-ttu-id="a3249-137">Klik op de blade hybride verbindingen **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a3249-137">On the Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="a3249-138">De **toevoegen van een hybride verbinding** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="a3249-138">The **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="a3249-139">Aangezien dit de eerste hybride verbinding de **nieuwe hybride verbinding** optie vooraf geselecteerd, en de **hybride verbinding maken** er wordt een blade geopend voor u.</span><span class="sxs-lookup"><span data-stu-id="a3249-139">Since this is your first hybrid connection, the **New hybrid connection** option is preselected, and the **Create hybrid connection** blade opens for you.</span></span>
   
    ![Een hybride verbinding maken][TwinCreateHCBlades]
   
    <span data-ttu-id="a3249-141">Op de **blade voor hybride verbinding maken**:</span><span class="sxs-lookup"><span data-stu-id="a3249-141">On the **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="a3249-142">Voor **naam**, Geef een naam op voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="a3249-142">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="a3249-143">Voor **hostnaam**, voer de naam van de lokale computer die als host fungeert voor uw resource.</span><span class="sxs-lookup"><span data-stu-id="a3249-143">For **Hostname**, enter the name of the on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="a3249-144">Voor **poort**, voer het poortnummer dat gebruikmaakt van uw lokale resource (1433 voor een standaardexemplaar van SQL Server).</span><span class="sxs-lookup"><span data-stu-id="a3249-144">For **Port**, enter the port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="a3249-145">Klik op **Biz Talk Service**</span><span class="sxs-lookup"><span data-stu-id="a3249-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="a3249-146">De **BizTalk Service maken** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="a3249-146">The **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="a3249-147">Voer een naam voor de BizTalk service en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a3249-147">Enter a name for the BizTalk service, and then click **OK**.</span></span>
   
    ![BizTalk service maken][CreateHCCreateBTS]
   
    <span data-ttu-id="a3249-149">De **BizTalk Service maken** blade wordt gesloten en u keert terug naar de **hybride verbinding maken** blade.</span><span class="sxs-lookup"><span data-stu-id="a3249-149">The **Create BizTalk Service** blade closes and you are returned to the **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="a3249-150">Klik op de blade maken hybride verbinding **OK**.</span><span class="sxs-lookup"><span data-stu-id="a3249-150">On the Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Klik op OK][CreateBTScomplete]
6. <span data-ttu-id="a3249-152">Wanneer het proces is voltooid, wordt het meldingengebied in de Portal informeert dat de verbinding is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a3249-152">When the process completes, the notifications area in the Portal informs you that the connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in the dogfood portal. I switch to the classic portal
    (full portal) and created the BizTalk service but it doesn't seem to let you connnect them - When you finish the
    Create hybrid conn step, you get the following error
    Failed to create hybrid connection RelecIoudHC. The 
    resource type could not be found in the namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    The error indicates it couldn't find the type, not the instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="a3249-153">Op de blade web-app en de **hybride verbindingen** pictogram nu geeft aan dat er 1 hybride verbinding is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a3249-153">On the web app's blade, the **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![Een hybride verbinding is gemaakt][CreateHCOneConnectionCreated]

<span data-ttu-id="a3249-155">U hebt op dit moment een belangrijk onderdeel van de cloudinfrastructuur voor hybride verbinding voltooid.</span><span class="sxs-lookup"><span data-stu-id="a3249-155">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="a3249-156">Vervolgens maakt u een bijbehorende lokale apparaat.</span><span class="sxs-lookup"><span data-stu-id="a3249-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="a3249-157">Installeren van de lokale hybride Verbindingsbeheer om de verbinding te voltooien</span><span class="sxs-lookup"><span data-stu-id="a3249-157">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
1. <span data-ttu-id="a3249-158">Klik op de web-app-blade **alle instellingen** > **Networking** > **uw hybride-verbindingseindpunten configureren**.</span><span class="sxs-lookup"><span data-stu-id="a3249-158">On the web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Pictogram van hybride verbindingen][HCIcon]
2. <span data-ttu-id="a3249-160">Op de **hybride verbindingen** blade de **Status** kolom voor het laatst toegevoegde eindpunt bevat **niet verbonden**.</span><span class="sxs-lookup"><span data-stu-id="a3249-160">On the **Hybrid connections** blade, the **Status** column for the recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="a3249-161">Klik op de verbinding om deze te configureren.</span><span class="sxs-lookup"><span data-stu-id="a3249-161">Click the connection to configure it.</span></span>
   
    ![Niet verbonden][NotConnected]
   
    <span data-ttu-id="a3249-163">De hybride verbinding-blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="a3249-163">The Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="a3249-165">Klik op de blade **Listener Setup**.</span><span class="sxs-lookup"><span data-stu-id="a3249-165">On the blade, click **Listener Setup**.</span></span>
   
    ![Klik op Listener Setup][ClickListenerSetup]
4. <span data-ttu-id="a3249-167">De **hybride verbindingseigenschappen** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="a3249-167">The **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="a3249-168">Onder **On-premises hybride Verbindingsbeheer**, kies **Klik hier om te installeren**.</span><span class="sxs-lookup"><span data-stu-id="a3249-168">Under **On-premises Hybrid Connection Manager**, choose **Click here to install**.</span></span>
   
    ![Klik hier om te installeren][ClickToInstallHCM]
5. <span data-ttu-id="a3249-170">Kies in het dialoogvenster Beveiliging waarschuwing toepassing uitgevoerd **uitvoeren** om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="a3249-170">In the Application Run security warning dialog, choose **Run** to continue.</span></span>
   
    ![Kies uitvoeren om door te gaan][ApplicationRunWarning]
6. <span data-ttu-id="a3249-172">In de **User Account Control** dialoogvenster kiezen **Ja**.</span><span class="sxs-lookup"><span data-stu-id="a3249-172">In the **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Klik op Ja][UAC]
7. <span data-ttu-id="a3249-174">De hybride Verbindingsbeheer wordt gedownload en geïnstalleerd voor u.</span><span class="sxs-lookup"><span data-stu-id="a3249-174">The Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Installeren][HCMInstalling]
8. <span data-ttu-id="a3249-176">Wanneer de installatie is voltooid, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="a3249-176">When the install completes, click **Close**.</span></span>
   
    ![Klik op sluiten][HCMInstallComplete]
   
    <span data-ttu-id="a3249-178">Op de **hybride verbindingen** blade de **Status** kolom ziet u nu **verbonden**.</span><span class="sxs-lookup"><span data-stu-id="a3249-178">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span></span> 
   
    ![Status verbonden][HCStatusConnected]

<span data-ttu-id="a3249-180">Nu dat de infrastructuur van hybride verbinding voltooid is, kunt u een hybride-toepassing die gebruikmaakt van deze.</span><span class="sxs-lookup"><span data-stu-id="a3249-180">Now that the hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="a3249-181">De volgende secties laten zien hoe een hybride verbinding gebruiken met een back-end van Mobile Apps .NET project.</span><span class="sxs-lookup"><span data-stu-id="a3249-181">The following sections show you how to use a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-the-mobile-app-net-backend-project-to-connect-to-the-sql-server-database"></a><span data-ttu-id="a3249-182">Het project voor het back-end van Mobile App .NET verbinding maken met de SQL Server-database configureren</span><span class="sxs-lookup"><span data-stu-id="a3249-182">Configure the Mobile App .NET backend project to connect to the SQL Server database</span></span>
<span data-ttu-id="a3249-183">In App Service is een back-end van Mobile Apps .NET project zojuist een ASP.NET web-app met een extra Mobile Apps SDK geïnstalleerd en wordt geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="a3249-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="a3249-184">Voor het gebruik van uw web-app als een back-end van Mobile Apps, moet u [downloaden en het initialiseren van de backend voor mobiele Apps .NET SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="a3249-184">To use your web app as a Mobile Apps backend, you must [download and initialize the Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="a3249-185">Voor mobiele Apps moet u ook een verbindingsreeks voor de lokale database definiëren en wijzigen van de back-end voor het gebruik van deze verbinding.</span><span class="sxs-lookup"><span data-stu-id="a3249-185">For Mobile Apps, you also need to define a connection string for the on-premises database and modify the backend to use this connection.</span></span> 

1. <span data-ttu-id="a3249-186">Open het bestand Web.config voor uw back-end van Mobile App .NET in Solution Explorer in Visual Studio, Ga naar de **connectionStrings** sectie, het toevoegen van een nieuwe vermelding SqlClient als volgt naar de lokale SQL Server-database verwijst:</span><span class="sxs-lookup"><span data-stu-id="a3249-186">In Solution Explorer in Visual Studio, open the Web.config file for your Mobile App .NET backend, locate the **connectionStrings** section, add a new SqlClient entry like the following, which points to the on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="a3249-187">Vervang `<**secure_password**>` in deze tekenreeks met het wachtwoord die u hebt gemaakt voor *HybridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="a3249-187">Remember to replace `<**secure_password**>` in this string with the password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="a3249-188">Klik op **opslaan** in Visual Studio het Web.config-bestand wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="a3249-188">Click **Save** in Visual Studio to save the Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a3249-189">Deze instelling wordt gebruikt wanneer op de lokale computer wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a3249-189">This connection setting is used when running on the local computer.</span></span> <span data-ttu-id="a3249-190">Wanneer in Azure wordt uitgevoerd, is deze instelling overschreven door de instelling voor de gedefinieerd in de portal.</span><span class="sxs-lookup"><span data-stu-id="a3249-190">When running in Azure, this setting is overriden by the connection setting defined in the portal.</span></span>
   > 
   > 
3. <span data-ttu-id="a3249-191">Vouw de **modellen** map en open het modelbestand gegevens die eindigt in *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="a3249-191">Expand the **Models** folder and open the data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="a3249-192">Wijzig de **DbContext** exemplaarconstructor voor het doorgeven van de waarde `OnPremisesDBConnection` naar de basistabel **DbContext** constructor, vergelijkbaar met het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="a3249-192">Modify the **DbContext** instance constructor to pass the value `OnPremisesDBConnection` to the base **DbContext** constructor, similar to the following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="a3249-193">De service wordt nu gebruiken voor de nieuwe verbinding met de SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="a3249-193">The service will now use the new connection to the SQL Server database.</span></span>

## <a name="update-the-mobile-app-backend-to-use-the-on-premises-connection-string"></a><span data-ttu-id="a3249-194">De backend voor mobiele Apps voor het gebruik van de lokale verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="a3249-194">Update the Mobile App backend to use the on-premises connection string</span></span>
<span data-ttu-id="a3249-195">Vervolgens moet u een app-instelling voor deze nieuwe verbindingsreeks toevoegen zodat deze kan worden gebruikt in Azure.</span><span class="sxs-lookup"><span data-stu-id="a3249-195">Next, you need to add an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="a3249-196">Terug in de [Azure-portal](https://portal.azure.com) in de web-app back-end-code voor uw mobiele App klikt u op **alle instellingen**, klikt u vervolgens **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="a3249-196">Back in the [Azure portal](https://portal.azure.com) in the web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="a3249-197">In de **Web-appinstellingen** blade omlaag naar **verbindingsreeksen** en voeg een nieuwe **SQL Server** verbindingstekenreeks met de naam `OnPremisesDBConnection` met een waarde zoals `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="a3249-197">In the **Web app settings** blade, scroll down to **Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="a3249-198">Vervang `<**secure_password**>` met het beveiligd wachtwoord voor uw lokale-database.</span><span class="sxs-lookup"><span data-stu-id="a3249-198">Replace `<**secure_password**>` with the secure password for your on-premises database.</span></span>
   
    ![Verbindingsreeks voor on-premises-database](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="a3249-200">Druk op **opslaan** om op te slaan van het hybride verbinding en verbinding string, u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a3249-200">Press **Save** to save the hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="a3249-201">Op dit moment kunt u het serverproject publiceren en testen van de nieuwe verbinding met uw bestaande Mobile Apps-clients.</span><span class="sxs-lookup"><span data-stu-id="a3249-201">At this point you can republish the server project and test the new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="a3249-202">Gegevens worden gelezen uit en geschreven naar de lokale database met behulp van de hybride verbinding.</span><span class="sxs-lookup"><span data-stu-id="a3249-202">Data will be read from and written to the on-premises database using the hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="a3249-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a3249-203">Next Steps</span></span>
* <span data-ttu-id="a3249-204">Zie voor meer informatie over het maken van een ASP.NET-webtoepassing die gebruikmaakt van een hybride verbinding [verbinding maken met een lokale SQL Server uit een Azure-website met behulp van hybride verbindingen](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="a3249-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="a3249-205">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="a3249-205">Additional Resources</span></span>
[<span data-ttu-id="a3249-206">Overzicht van hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="a3249-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="a3249-207">Josh Twist introduceert hybride verbindingen (Channel 9 video)</span><span class="sxs-lookup"><span data-stu-id="a3249-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="a3249-208">Hybride verbindingen website</span><span class="sxs-lookup"><span data-stu-id="a3249-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="a3249-209">BizTalk Services: De tabbladen Dashboard, bewaken, schaal, configureren en hybride verbinding</span><span class="sxs-lookup"><span data-stu-id="a3249-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="a3249-210">Het bouwen van een echte hybride Cloud met naadloze toepassing draagbaarheid (Channel 9 video)</span><span class="sxs-lookup"><span data-stu-id="a3249-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="a3249-211">Verbinding maken met een lokale SQL Server van Azure Mobile Services met behulp van hybride verbindingen (Channel 9 video)</span><span class="sxs-lookup"><span data-stu-id="a3249-211">Connect to an on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="a3249-212">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="a3249-212">What's changed</span></span>
* <span data-ttu-id="a3249-213">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a3249-213">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
