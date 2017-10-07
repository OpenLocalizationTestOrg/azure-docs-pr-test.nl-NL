---
title: aaaAccess lokale bronnen in Azure App Service met behulp van hybride verbindingen
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
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="f368c-103">On-premises resources benaderen via hybride verbindingen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f368c-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="f368c-104">U kunt verbinding maken met een Azure App Service-app tooany on-premises resource die gebruikmaakt van een statische TCP-poort, zoals SQL Server, MySQL, HTTP-Web-API's en de meeste aangepaste webservices.</span><span class="sxs-lookup"><span data-stu-id="f368c-104">You can connect an Azure App Service app tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="f368c-105">Dit artikel ziet u hoe toocreate een hybride verbinding tussen de App Service en een on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="f368c-105">This article shows you how toocreate a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="f368c-106">Hallo-Web-Apps-gedeelte van Hallo hybride verbindingen onderdeel is alleen beschikbaar in Hallo [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f368c-106">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="f368c-107">Zie voor een verbinding in BizTalk Services toocreate [hybride verbindingen](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="f368c-107">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="f368c-108">Deze inhoud is ook van toepassing tooMobile Apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f368c-108">This content also applies tooMobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f368c-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f368c-109">Prerequisites</span></span>
* <span data-ttu-id="f368c-110">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f368c-110">An Azure subscription.</span></span> <span data-ttu-id="f368c-111">Zie voor een gratis abonnement [gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f368c-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="f368c-112">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="f368c-112">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f368c-113">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="f368c-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="f368c-114">toouse een lokale SQL Server of SQL Server Express-database met een hybride verbinding, moet TCP/IP toobe ingeschakeld op een statische poort.</span><span class="sxs-lookup"><span data-stu-id="f368c-114">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="f368c-115">Met behulp van een standaardexemplaar van SQL Server wordt aanbevolen omdat deze gebruikmaakt van statische poort 1433.</span><span class="sxs-lookup"><span data-stu-id="f368c-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="f368c-116">Zie voor meer informatie over het installeren en configureren van SQL Server Express voor gebruik met hybride verbindingen [Connect tooan lokale SQL Server uit een Azure-website met behulp van hybride verbindingen](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="f368c-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="f368c-117">Hallo-computer waarop u Hallo op premises hybride Verbindingsbeheer agent beschreven verderop in dit artikel installeert:</span><span class="sxs-lookup"><span data-stu-id="f368c-117">hello computer on which you install hello on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="f368c-118">Moet kunnen tooconnect tooAzure via poort 5671</span><span class="sxs-lookup"><span data-stu-id="f368c-118">Must be able tooconnect tooAzure over port 5671</span></span>
  * <span data-ttu-id="f368c-119">Moet kunnen tooreach hello *hostnaam*:*portnumber* van uw lokale resource.</span><span class="sxs-lookup"><span data-stu-id="f368c-119">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="f368c-120">Hallo stappen in dit artikel wordt ervan uitgegaan dat u gebruikmaakt van Hallo Hallo-computer die als voor agent voor hybride verbinding voor Hallo lokale host fungeert browser.</span><span class="sxs-lookup"><span data-stu-id="f368c-120">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="f368c-121">Een web-app maken in hello Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f368c-121">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="f368c-122">Als u al een web-app of een back-end voor mobiele App in hello Azure-Portal wilt u toouse voor deze zelfstudie hebt gemaakt, kunt u verder gaan te[een hybride verbinding en een BizTalk Service maken](#CreateHC) en van daaruit starten.</span><span class="sxs-lookup"><span data-stu-id="f368c-122">If you have already created a web app or Mobile App backend in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="f368c-123">In Hallo linkerbovenhoek Hallo [Azure Portal](https://portal.azure.com), klikt u op **nieuw** > **Web en mobiel** > **Web-App**.</span><span class="sxs-lookup"><span data-stu-id="f368c-123">In hello upper left corner of hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![Nieuwe web-app][NewWebsite]
2. <span data-ttu-id="f368c-125">Op Hallo **Web-app** blade een URL op en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="f368c-125">On hello **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Websitenaam][WebsiteCreationBlade]
3. <span data-ttu-id="f368c-127">Na enkele ogenblikken Hallo web-app wordt gemaakt en de blade web-app wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f368c-127">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="f368c-128">Hallo-blade is een verticaal schuifbare dashboard waarmee u uw site beheren.</span><span class="sxs-lookup"><span data-stu-id="f368c-128">hello blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Website worden uitgevoerd][WebSiteRunningBlade]
4. <span data-ttu-id="f368c-130">tooverify hello site live is, klikt u op Hallo **Bladeren** pictogram toodisplay Hallo standaardpagina.</span><span class="sxs-lookup"><span data-stu-id="f368c-130">tooverify hello site is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>
   
    ![Klik op Bladeren toosee uw web-app][Browse]
   
    ![App-standaardwebpagina][DefaultWebSitePage]

<span data-ttu-id="f368c-133">Vervolgens maakt u een hybride verbinding en een BizTalk service voor Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="f368c-133">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="f368c-134">Een hybride verbinding en een BizTalk Service maken</span><span class="sxs-lookup"><span data-stu-id="f368c-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="f368c-135">Klik in de blade van uw web-app op **alle instellingen** > **Networking** > **uw hybride-verbindingseindpunten configureren**.</span><span class="sxs-lookup"><span data-stu-id="f368c-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Hybride verbindingen][CreateHCHCIcon]
2. <span data-ttu-id="f368c-137">Klik op Hallo hybride verbindingen blade **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f368c-137">On hello Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="f368c-138">Hallo **toevoegen van een hybride verbinding** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f368c-138">hello **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="f368c-139">Aangezien dit de eerste hybride verbinding, Hallo **nieuwe hybride verbinding** optie vooraf geselecteerd en Hallo **hybride verbinding maken** er wordt een blade geopend voor u.</span><span class="sxs-lookup"><span data-stu-id="f368c-139">Since this is your first hybrid connection, hello **New hybrid connection** option is preselected, and hello **Create hybrid connection** blade opens for you.</span></span>
   
    ![Een hybride verbinding maken][TwinCreateHCBlades]
   
    <span data-ttu-id="f368c-141">Op Hallo **blade voor hybride verbinding maken**:</span><span class="sxs-lookup"><span data-stu-id="f368c-141">On hello **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="f368c-142">Voor **naam**, Geef een naam voor het Hallo-verbinding.</span><span class="sxs-lookup"><span data-stu-id="f368c-142">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="f368c-143">Voor **hostnaam**, voer de naam Hallo van Hallo lokale computer die als host fungeert voor uw resource.</span><span class="sxs-lookup"><span data-stu-id="f368c-143">For **Hostname**, enter hello name of hello on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="f368c-144">Voor **poort**, Voer Hallo-poortnummer dat gebruikmaakt van uw lokale resource (1433 voor een standaardexemplaar van SQL Server).</span><span class="sxs-lookup"><span data-stu-id="f368c-144">For **Port**, enter hello port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="f368c-145">Klik op **Biz Talk Service**</span><span class="sxs-lookup"><span data-stu-id="f368c-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="f368c-146">Hallo **BizTalk Service maken** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f368c-146">hello **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="f368c-147">Voer een naam voor Hallo BizTalk service en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f368c-147">Enter a name for hello BizTalk service, and then click **OK**.</span></span>
   
    ![BizTalk service maken][CreateHCCreateBTS]
   
    <span data-ttu-id="f368c-149">Hallo **BizTalk Service maken** blade wordt gesloten en keert u terug toohello **hybride verbinding maken** blade.</span><span class="sxs-lookup"><span data-stu-id="f368c-149">hello **Create BizTalk Service** blade closes and you are returned toohello **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="f368c-150">Klik op de blade voor Hallo maken hybride verbinding **OK**.</span><span class="sxs-lookup"><span data-stu-id="f368c-150">On hello Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Klik op OK][CreateBTScomplete]
6. <span data-ttu-id="f368c-152">Wanneer het Hallo-proces is voltooid, informeert Hallo meldingengebied in Hallo Portal dat Hallo verbinding is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f368c-152">When hello process completes, hello notifications area in hello Portal informs you that hello connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="f368c-153">Hallo op Hallo van web-app-blade **hybride verbindingen** pictogram nu geeft aan dat er 1 hybride verbinding is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f368c-153">On hello web app's blade, hello **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![Een hybride verbinding is gemaakt][CreateHCOneConnectionCreated]

<span data-ttu-id="f368c-155">U hebt op dit moment een belangrijk onderdeel van hybride Hallo-verbinding cloudinfrastructuur voltooid.</span><span class="sxs-lookup"><span data-stu-id="f368c-155">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="f368c-156">Vervolgens maakt u een bijbehorende lokale apparaat.</span><span class="sxs-lookup"><span data-stu-id="f368c-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="f368c-157">Hallo op premises hybride Verbindingsbeheer toocomplete Hallo verbinding installeren</span><span class="sxs-lookup"><span data-stu-id="f368c-157">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
1. <span data-ttu-id="f368c-158">Klik op Hallo van web-app-blade **alle instellingen** > **Networking** > **uw hybride-verbindingseindpunten configureren**.</span><span class="sxs-lookup"><span data-stu-id="f368c-158">On hello web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Pictogram van hybride verbindingen][HCIcon]
2. <span data-ttu-id="f368c-160">Op Hallo **hybride verbindingen** blade, Hallo **Status** onlangs eindpunt bevat op kolom voor Hallo **niet verbonden**.</span><span class="sxs-lookup"><span data-stu-id="f368c-160">On hello **Hybrid connections** blade, hello **Status** column for hello recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="f368c-161">Klik op Hallo verbinding tooconfigure deze.</span><span class="sxs-lookup"><span data-stu-id="f368c-161">Click hello connection tooconfigure it.</span></span>
   
    ![Niet verbonden][NotConnected]
   
    <span data-ttu-id="f368c-163">Hallo hybride verbinding blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f368c-163">hello Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="f368c-165">Klik op de blade Hallo **Listener Setup**.</span><span class="sxs-lookup"><span data-stu-id="f368c-165">On hello blade, click **Listener Setup**.</span></span>
   
    ![Klik op Listener Setup][ClickListenerSetup]
4. <span data-ttu-id="f368c-167">Hallo **hybride verbindingseigenschappen** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f368c-167">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="f368c-168">Onder **On-premises hybride Verbindingsbeheer**, kies **Klik hier tooinstall**.</span><span class="sxs-lookup"><span data-stu-id="f368c-168">Under **On-premises Hybrid Connection Manager**, choose **Click here tooinstall**.</span></span>
   
    ![Klik hier tooinstall][ClickToInstallHCM]
5. <span data-ttu-id="f368c-170">Kies in het Hallo-toepassing uitgevoerd waarschuwingsvenster, **uitvoeren** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f368c-170">In hello Application Run security warning dialog, choose **Run** toocontinue.</span></span>
   
    ![Kies toocontinue uitvoeren][ApplicationRunWarning]
6. <span data-ttu-id="f368c-172">In Hallo **User Account Control** dialoogvenster kiezen **Ja**.</span><span class="sxs-lookup"><span data-stu-id="f368c-172">In hello **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Klik op Ja][UAC]
7. <span data-ttu-id="f368c-174">Hallo hybride Verbindingsbeheer wordt gedownload en geïnstalleerd voor u.</span><span class="sxs-lookup"><span data-stu-id="f368c-174">hello Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Installeren][HCMInstalling]
8. <span data-ttu-id="f368c-176">Wanneer het Hallo-installatie is voltooid, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="f368c-176">When hello install completes, click **Close**.</span></span>
   
    ![Klik op sluiten][HCMInstallComplete]
   
    <span data-ttu-id="f368c-178">Op Hallo **hybride verbindingen** blade, Hallo **Status** kolom ziet u nu **verbonden**.</span><span class="sxs-lookup"><span data-stu-id="f368c-178">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Status verbonden][HCStatusConnected]

<span data-ttu-id="f368c-180">Nu die infrastructuur Hallo hybride verbinding voltooid is, kunt u een hybride-toepassing die gebruikmaakt van deze.</span><span class="sxs-lookup"><span data-stu-id="f368c-180">Now that hello hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="f368c-181">Hallo volgende secties ziet u hoe toouse een hybride verbinding met een back-end van Mobile Apps .NET project.</span><span class="sxs-lookup"><span data-stu-id="f368c-181">hello following sections show you how toouse a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a><span data-ttu-id="f368c-182">Hallo Mobile App .NET backend project tooconnect toohello SQL Server-database configureren</span><span class="sxs-lookup"><span data-stu-id="f368c-182">Configure hello Mobile App .NET backend project tooconnect toohello SQL Server database</span></span>
<span data-ttu-id="f368c-183">In App Service is een back-end van Mobile Apps .NET project zojuist een ASP.NET web-app met een extra Mobile Apps SDK geïnstalleerd en wordt geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="f368c-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="f368c-184">toouse uw web-app als een back-end van Mobile Apps, moet u [downloaden en te initialiseren Hallo Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="f368c-184">toouse your web app as a Mobile Apps backend, you must [download and initialize hello Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="f368c-185">Voor mobiele Apps, u ook toodefine een verbindingsreeks nodig voor Hallo lokale-database en Hallo back-end toouse wijzigt u deze verbinding.</span><span class="sxs-lookup"><span data-stu-id="f368c-185">For Mobile Apps, you also need toodefine a connection string for hello on-premises database and modify hello backend toouse this connection.</span></span> 

1. <span data-ttu-id="f368c-186">Zoek in Solution Explorer in Visual Studio openen Hallo Web.config-bestand voor uw mobiele App .NET back-end, Hallo **connectionStrings** sectie, het toevoegen van een nieuwe vermelding SqlClient zoals Hallo volgende, welke punten toohello lokale SQL Server-database:</span><span class="sxs-lookup"><span data-stu-id="f368c-186">In Solution Explorer in Visual Studio, open hello Web.config file for your Mobile App .NET backend, locate hello **connectionStrings** section, add a new SqlClient entry like hello following, which points toohello on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="f368c-187">Houd er rekening mee tooreplace `<**secure_password**>` in deze tekenreeks met Hallo wachtwoord die u hebt gemaakt voor *HybridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="f368c-187">Remember tooreplace `<**secure_password**>` in this string with hello password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="f368c-188">Klik op **opslaan** in Visual Studio toosave Hallo Web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="f368c-188">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f368c-189">Deze instelling wordt gebruikt wanneer op de lokale computer Hallo.</span><span class="sxs-lookup"><span data-stu-id="f368c-189">This connection setting is used when running on hello local computer.</span></span> <span data-ttu-id="f368c-190">Wanneer in Azure wordt uitgevoerd, is deze instelling onderdrukt door Hallo verbindingsinstelling gedefinieerd in het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="f368c-190">When running in Azure, this setting is overriden by hello connection setting defined in hello portal.</span></span>
   > 
   > 
3. <span data-ttu-id="f368c-191">Vouw Hallo **modellen** map en open Hallo gegevens modelbestand eindigt in *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="f368c-191">Expand hello **Models** folder and open hello data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="f368c-192">Hallo wijzigen **DbContext** exemplaar-constructor toopass Hallo waarde `OnPremisesDBConnection` toohello base **DbContext** constructor, vergelijkbare toohello codefragment te volgen:</span><span class="sxs-lookup"><span data-stu-id="f368c-192">Modify hello **DbContext** instance constructor toopass hello value `OnPremisesDBConnection` toohello base **DbContext** constructor, similar toohello following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="f368c-193">Hallo-service wordt nu Hallo nieuwe verbinding toohello SQL Server-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f368c-193">hello service will now use hello new connection toohello SQL Server database.</span></span>

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a><span data-ttu-id="f368c-194">Hallo mobiele App back-end toouse Hallo lokale met verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="f368c-194">Update hello Mobile App backend toouse hello on-premises connection string</span></span>
<span data-ttu-id="f368c-195">Vervolgens moet u tooadd een app-instelling voor deze nieuwe verbindingsreeks zodat deze kan worden gebruikt in Azure.</span><span class="sxs-lookup"><span data-stu-id="f368c-195">Next, you need tooadd an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="f368c-196">Terug in Hallo [Azure-portal](https://portal.azure.com) in Hallo web-app back-end-code voor uw mobiele App, klikt u op **alle instellingen**, klikt u vervolgens **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="f368c-196">Back in hello [Azure portal](https://portal.azure.com) in hello web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="f368c-197">In Hallo **Web-appinstellingen** blade Schuif naar beneden te**verbindingsreeksen** en voeg een nieuwe **SQL Server** verbindingstekenreeks met de naam `OnPremisesDBConnection` met een waarde zoals `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="f368c-197">In hello **Web app settings** blade, scroll down too**Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="f368c-198">Vervang `<**secure_password**>` met Hallo beveiligd wachtwoord voor uw lokale-database.</span><span class="sxs-lookup"><span data-stu-id="f368c-198">Replace `<**secure_password**>` with hello secure password for your on-premises database.</span></span>
   
    ![Verbindingsreeks voor on-premises-database](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="f368c-200">Druk op **opslaan** toosave Hallo hybride verbinding en de verbindingsreeks u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f368c-200">Press **Save** toosave hello hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="f368c-201">U kunt op dit moment Hallo serverproject publiceren en testen van Hallo nieuwe verbinding met uw bestaande Mobile Apps-clients.</span><span class="sxs-lookup"><span data-stu-id="f368c-201">At this point you can republish hello server project and test hello new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="f368c-202">Gegevens worden gelezen uit en toohello Hallo hybride verbinding met lokale-database geschreven.</span><span class="sxs-lookup"><span data-stu-id="f368c-202">Data will be read from and written toohello on-premises database using hello hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="f368c-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f368c-203">Next Steps</span></span>
* <span data-ttu-id="f368c-204">Zie voor meer informatie over het maken van een ASP.NET-webtoepassing die gebruikmaakt van een hybride verbinding [Connect tooan lokale SQL Server uit een Azure-website met behulp van hybride verbindingen](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="f368c-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="f368c-205">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="f368c-205">Additional Resources</span></span>
[<span data-ttu-id="f368c-206">Overzicht van hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="f368c-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="f368c-207">Josh Twist introduceert hybride verbindingen (Channel 9 video)</span><span class="sxs-lookup"><span data-stu-id="f368c-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="f368c-208">Hybride verbindingen website</span><span class="sxs-lookup"><span data-stu-id="f368c-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="f368c-209">BizTalk Services: De tabbladen Dashboard, bewaken, schaal, configureren en hybride verbinding</span><span class="sxs-lookup"><span data-stu-id="f368c-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="f368c-210">Het bouwen van een echte hybride Cloud met naadloze toepassing draagbaarheid (Channel 9 video)</span><span class="sxs-lookup"><span data-stu-id="f368c-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="f368c-211">Verbinding maken met tooan lokale SQL-Server van Azure Mobile Services met behulp van hybride verbindingen (Channel 9 video)</span><span class="sxs-lookup"><span data-stu-id="f368c-211">Connect tooan on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="f368c-212">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="f368c-212">What's changed</span></span>
* <span data-ttu-id="f368c-213">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f368c-213">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
