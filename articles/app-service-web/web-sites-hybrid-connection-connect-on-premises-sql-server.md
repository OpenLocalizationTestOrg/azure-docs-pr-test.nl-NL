---
title: aaaConnect tooon lokale SQL Server vanuit een web-app in Azure App Service met behulp van hybride verbindingen
description: Een web-app maken in Microsoft Azure en verbindt u deze tooan lokale SQL Server-database.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="1fe6a-103">Verbinding maken met tooon lokale SQL Server vanuit een web-app in Azure App Service met behulp van hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="1fe6a-103">Connect tooon-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="1fe6a-104">Hybride verbindingen kunnen worden aangesloten [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web-Apps tooon lokale bronnen die gebruikmaken van een statische TCP-poort.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps tooon-premises resources that use a static TCP port.</span></span> <span data-ttu-id="1fe6a-105">Ondersteunde resources omvatten Microsoft SQL Server, MySQL, HTTP-Web-API's, App Service en de meeste aangepaste webservices.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="1fe6a-106">In deze zelfstudie leert u hoe toocreate een App Service web-app in Hallo [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715)Hallo web app tooyour lokale lokale SQL Server-database met behulp van de nieuwe functie voor hybride verbinding Hallo verbinding, een eenvoudige ASP.NET maken de toepassing die Hallo hybride verbinding gebruiken en Hallo toepassing toohello App Service-web-app implementeren.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-106">In this tutorial, you will learn how toocreate an App Service web app in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect hello web app tooyour local on-premises SQL Server database using hello new Hybrid Connection feature, create a simple ASP.NET application that will use hello hybrid connection, and deploy hello application toohello App Service web app.</span></span> <span data-ttu-id="1fe6a-107">Hallo voltooid web-app in Azure worden gebruikersreferenties opgeslagen in een lidmaatschapsdatabase on-premises.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-107">hello completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="1fe6a-108">Hallo-zelfstudie wordt ervan uitgegaan dat geen ervaring met behulp van Azure of ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-108">hello tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="1fe6a-109">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-109">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="1fe6a-110">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="1fe6a-111">Hallo-Web-Apps-gedeelte van Hallo hybride verbindingen onderdeel is alleen beschikbaar in Hallo [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1fe6a-111">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="1fe6a-112">Zie voor een verbinding in BizTalk Services toocreate [hybride verbindingen](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="1fe6a-112">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1fe6a-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1fe6a-113">Prerequisites</span></span>
<span data-ttu-id="1fe6a-114">toocomplete in deze zelfstudie, moet u Hallo producten te volgen.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-114">toocomplete this tutorial, you'll need hello following products.</span></span> <span data-ttu-id="1fe6a-115">Alle zijn beschikbaar in de beschikbare versies zodat u kunt beginnen met het ontwikkelen voor Azure volledig voor gratis.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="1fe6a-116">**Azure-abonnement** : voor een gratis abonnement, Zie [gratis proefversie van Azure](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1fe6a-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="1fe6a-117">**Visual Studio 2013** -toodownload een gratis evaluatieversie van Visual Studio 2013, Zie [Visual Studio-Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="1fe6a-117">**Visual Studio 2013** - toodownload a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="1fe6a-118">Installeer dit voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-118">Install this before continuing.</span></span>
* <span data-ttu-id="1fe6a-119">**Microsoft .NET Framework 3.5 servicepack 1** -als het besturingssysteem Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 of Windows Server 2008 R2 is, kunt u dit inschakelen in het Configuratiescherm > programma's en onderdelen > Windows-onderdelen in- of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="1fe6a-120">Anders, u kunt dit downloaden van Hallo [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="1fe6a-120">Otherwise, you can download it from hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="1fe6a-121">**SQL Server 2014 Express met hulpprogramma's voor** -Microsoft SQL Server Express gratis downloaden op Hallo [pagina Microsoft Web Platform Database](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="1fe6a-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at hello [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="1fe6a-122">Kies Hallo **Express** (geen LocalDB) versie.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-122">Choose hello **Express** (not LocalDB) version.</span></span> <span data-ttu-id="1fe6a-123">Hallo **Express met hulpprogramma's voor** versie SQL Server Management Studio, gaat u in deze zelfstudie bevat.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-123">hello **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="1fe6a-124">**SQL Server Management Studio Express** - dat deel uitmaakt van de SQL Server 2014 Express Hallo met hulpprogramma's downloaden hierboven vermeld, maar als u tooinstall moet deze afzonderlijk, u kunt downloaden en installeren vanaf Hallo [SQL Server Express downloadpagina](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="1fe6a-124">**SQL Server Management Studio Express** - This is included with hello SQL Server 2014 Express with Tools download mentioned above, but if you need tooinstall it separately, you can download and install it from hello [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="1fe6a-125">Hallo-zelfstudie wordt ervan uitgegaan dat u een Azure-abonnement hebt dat u Visual Studio 2013 hebt geïnstalleerd en u hebt geïnstalleerd of .NET Framework 3.5 ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-125">hello tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="1fe6a-126">Hallo-zelfstudie laat zien hoe tooinstall SQL Server 2014 Express in een configuratie die goed samen met hello Azure hybride verbindingen werkt functie (een standaardexemplaar met een statische TCP-poort).</span><span class="sxs-lookup"><span data-stu-id="1fe6a-126">hello tutorial shows you how tooinstall SQL Server 2014 Express in a configuration that works well with hello Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="1fe6a-127">Voordat u begint Hallo zelfstudie, download SQL Server 2014 Express met hulpprogramma's van Hallo locatie hierboven worden genoemd als u geen SQL Server geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-127">Before starting hello tutorial, download SQL Server 2014 Express with Tools from hello location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="1fe6a-128">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="1fe6a-128">Notes</span></span>
<span data-ttu-id="1fe6a-129">toouse een lokale SQL Server of SQL Server Express-database met een hybride verbinding, moet TCP/IP toobe ingeschakeld op een statische poort.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-129">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="1fe6a-130">Standaardexemplaren op SQL Server gebruiken statische poort 1433, dat niet het benoemde exemplaren.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="1fe6a-131">Hallo-computer waarop u Hallo op premises hybride Verbindingsbeheer agent installeert:</span><span class="sxs-lookup"><span data-stu-id="1fe6a-131">hello computer on which you install hello on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="1fe6a-132">Moet uitgaande verbinding tooAzure hebben via:</span><span class="sxs-lookup"><span data-stu-id="1fe6a-132">Must have outbound connectivity tooAzure over:</span></span>

| <span data-ttu-id="1fe6a-133">Poort</span><span class="sxs-lookup"><span data-stu-id="1fe6a-133">Port</span></span> | <span data-ttu-id="1fe6a-134">Waarom</span><span class="sxs-lookup"><span data-stu-id="1fe6a-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="1fe6a-135">80</span><span class="sxs-lookup"><span data-stu-id="1fe6a-135">80</span></span> |<span data-ttu-id="1fe6a-136">**Vereist** voor HTTP-poort voor de validatie van het servercertificaat en eventueel voor toegang tot gegevens.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="1fe6a-137">443</span><span class="sxs-lookup"><span data-stu-id="1fe6a-137">443</span></span> |<span data-ttu-id="1fe6a-138">**Optionele** voor toegang tot gegevens.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="1fe6a-139">Als uitgaande verbinding too443 niet beschikbaar is, wordt de TCP-poort 80 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-139">If outbound connectivity too443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="1fe6a-140">5671 en 9352</span><span class="sxs-lookup"><span data-stu-id="1fe6a-140">5671 and 9352</span></span> |<span data-ttu-id="1fe6a-141">**Aanbevolen** maar optioneel voor toegang tot gegevens.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="1fe6a-142">Houd er rekening mee dat deze modus levert meestal hogere doorvoer.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="1fe6a-143">Als u uitgaande connectiviteit toothese poorten niet beschikbaar is, wordt de TCP-poort 443 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-143">If outbound connectivity toothese ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="1fe6a-144">Moet kunnen tooreach hello *hostnaam*:*portnumber* van uw lokale resource.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-144">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="1fe6a-145">Hallo stappen in dit artikel wordt ervan uitgegaan dat u gebruikmaakt van Hallo Hallo-computer die als voor agent voor hybride verbinding voor Hallo lokale host fungeert browser.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-145">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>

<span data-ttu-id="1fe6a-146">Als u al SQL Server geïnstalleerd in een configuratie en in een omgeving die voldoet aan Hallo voorwaarden die hebt hierboven worden beschreven, kunt u overslaan en beginnen met [maken van een SQL Server-database op de lokale](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="1fe6a-146">If you already have SQL Server installed in a configuration and in an environment that meets hello conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="1fe6a-147">A.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-147">A.</span></span> <span data-ttu-id="1fe6a-148">SQL Server Express installeren en maken van een SQL Server-database op de lokale TCP/IP inschakelen</span><span class="sxs-lookup"><span data-stu-id="1fe6a-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="1fe6a-149">Deze sectie leest u hoe tooinstall SQL Server Express TCP/IP inschakelen en een database maken, zodat uw webtoepassing werkt met hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-149">This section shows you how tooinstall SQL Server Express, enable TCP/IP, and create a database so that your web application will work with hello Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="1fe6a-150">SQL Server Express installeren</span><span class="sxs-lookup"><span data-stu-id="1fe6a-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="1fe6a-151">tooinstall SQL Server Express uitvoeren Hallo **SQLEXPRWT_x64_ENU.exe** of **SQLEXPR_x86_ENU.exe** -bestand dat u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-151">tooinstall SQL Server Express, run hello **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="1fe6a-152">Hallo Installatiecentrum van SQL Server-wizard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-152">hello SQL Server Installation Center wizard appears.</span></span>
   
    ![Installatie van SQL Server][SQLServerInstall]
2. <span data-ttu-id="1fe6a-154">Kies **zelfstandige installatie van nieuwe SQL-Server of bestaande installatie van functies tooan toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-154">Choose **New SQL Server stand-alone installation or add features tooan existing installation**.</span></span> <span data-ttu-id="1fe6a-155">Volg de aanwijzingen Hallo en accepteren Hallo standaardkeuzes en -instellingen, totdat u toohello **Exemplaarconfiguratie** pagina.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-155">Follow hello instructions, accepting hello default choices and settings, until you get toohello **Instance Configuration** page.</span></span>
3. <span data-ttu-id="1fe6a-156">Op Hallo **Exemplaarconfiguratie** pagina **standaardexemplaar**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-156">On hello **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Kies standaardexemplaar][ChooseDefaultInstance]
   
    <span data-ttu-id="1fe6a-158">Standaard luistert Hallo-standaardexemplaar van SQL Server voor aanvragen van SQL Server-clients op statische poort 1433, is welke Hallo hybride verbindingen functie is vereist.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-158">By default, hello default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what hello Hybrid Connections feature requires.</span></span> <span data-ttu-id="1fe6a-159">Benoemde exemplaren dynamische poorten en UDP, die niet worden ondersteund door hybride verbindingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="1fe6a-160">Accepteer de standaardwaarden Hallo op Hallo **serverconfiguratie** pagina.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-160">Accept hello defaults on hello **Server Configuration** page.</span></span>
5. <span data-ttu-id="1fe6a-161">Op Hallo **Database Engine-configuratie** pagina onder **verificatiemodus**, kies **gemengde modus (SQL Server-verificatie en Windows-verificatie)**, en geef een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-161">On hello **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Kies in de gemengde modus][ChooseMixedMode]
   
    <span data-ttu-id="1fe6a-163">In deze zelfstudie wordt u SQL Server-verificatie.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="1fe6a-164">Worden ervoor tooremember Hallo wachtwoord dat u hebt opgegeven, omdat u deze later hebt.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-164">Be sure tooremember hello password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="1fe6a-165">Doorloop rest Hallo van Hallo wizard toocomplete Hallo-installatie.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-165">Step through hello rest of hello wizard toocomplete hello installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="1fe6a-166">TCP/IP inschakelen</span><span class="sxs-lookup"><span data-stu-id="1fe6a-166">Enable TCP/IP</span></span>
<span data-ttu-id="1fe6a-167">tooenable TCP/IP, gebruikt u SQL Server Configuration Manager, die tijdens de installatie van SQL Server Express is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-167">tooenable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="1fe6a-168">Volg de stappen Hallo in [TCP/IP-netwerkprotocol inschakelen voor SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-168">Follow hello steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="1fe6a-169">Lokale voor een SQL Server-database maken</span><span class="sxs-lookup"><span data-stu-id="1fe6a-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="1fe6a-170">Uw Visual Studio-webtoepassing vereist een lidmaatschapsdatabase die toegankelijk zijn voor Azure.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="1fe6a-171">Hiervoor moet een SQL Server of SQL Server Express-database (geen Hallo LocalDB-database die Hallo MVC-sjabloon gebruikt standaard), zodat u Hallo lidmaatschapsdatabase naast maken.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-171">This requires a SQL Server or SQL Server Express database (not hello LocalDB database that hello MVC template uses by default), so you'll create hello membership database next.</span></span>

1. <span data-ttu-id="1fe6a-172">In SQL Server Management Studio verbinding met toohello SQL-Server die u zojuist hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-172">In SQL Server Management Studio, connect toohello SQL Server you just installed.</span></span> <span data-ttu-id="1fe6a-173">(Als hello **verbinding tooServer** dialoogvenster niet automatisch wordt weergegeven, te navigeren**Objectverkenner** in het linkerdeelvenster hello, klikt u op **Connect**, en klik vervolgens op **Database-Engine**.) ![Verbinding maken met tooServer][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="1fe6a-173">(If hello **Connect tooServer** dialog does not appear automatically, navigate too**Object Explorer** in hello left pane, click **Connect**, and then click **Database Engine**.) ![Connect tooServer][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="1fe6a-174">Voor **servertype**, kies **Database-Engine**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="1fe6a-175">Voor **servernaam**, kunt u **localhost** of Hallo-naam van Hallo-computer die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-175">For **Server name**, you can use **localhost** or hello name of hello computer that you are using.</span></span> <span data-ttu-id="1fe6a-176">Kies **SQL Server-verificatie**, en meld u met Hallo sa-gebruikersnaam en wachtwoord op Hallo die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-176">Choose **SQL Server authentication**, and then log in with hello sa user name and hello password that you created earlier.</span></span>
2. <span data-ttu-id="1fe6a-177">een nieuwe database met behulp van SQL Server Management Studio toocreate met de rechtermuisknop op **Databases** in Object Explorer en klik vervolgens op **nieuwe Database**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-177">toocreate a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Nieuwe database maken][SSMScreateNewDB]
3. <span data-ttu-id="1fe6a-179">In Hallo **nieuwe Database** dialoogvenster MembershipDB voor Hallo databasenaam invoeren en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-179">In hello **New Database** dialog, enter MembershipDB for hello database name, and then click **OK**.</span></span>
   
    ![Databasenaam opgeven][SSMSprovideDBname]
   
    <span data-ttu-id="1fe6a-181">Houd er rekening mee dat u Maak niet alle wijzigingen toohello databases op dit moment.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-181">Note that you do not make any changes toohello database at this point.</span></span> <span data-ttu-id="1fe6a-182">Hallo lidmaatschapsgegevens wordt later automatisch door uw webtoepassing toegevoegd wanneer u het uitvoert.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-182">hello membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="1fe6a-183">In Object Explorer, als u wilt uitbreiden **Databases**, ziet u dat Hallo lidmaatschap van de database is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-183">In Object Explorer, if you expand **Databases**, you will see that hello membership database has been created.</span></span>
   
    ![MembershipDB gemaakt][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="1fe6a-185">B.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-185">B.</span></span> <span data-ttu-id="1fe6a-186">Een web-app maken in hello Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1fe6a-186">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="1fe6a-187">Als u al een web-app in hello Azure-Portal wilt u toouse voor deze zelfstudie hebt gemaakt, kunt u verder gaan te[een hybride verbinding en een BizTalk Service maken](#CreateHC) en van daaruit worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-187">If you have already created a web app in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="1fe6a-188">In Hallo [Azure Portal](https://portal.azure.com), klikt u op **nieuw** > **Web en mobiel** > **Web-app**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-188">In hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![Knop Nieuw][New]
2. <span data-ttu-id="1fe6a-190">Configureren van uw web-app en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Websitenaam][WebsiteCreationBlade]
3. <span data-ttu-id="1fe6a-192">Na enkele ogenblikken Hallo web-app wordt gemaakt en de blade web-app wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-192">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="1fe6a-193">Hallo-blade is een verticaal schuifbare dashboard waarmee u uw web-app beheren.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-193">hello blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Website worden uitgevoerd][WebSiteRunningBlade]
   
    <span data-ttu-id="1fe6a-195">tooverify hello web-app live is, kunt u Hallo op **Bladeren** pictogram toodisplay Hallo standaardpagina.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-195">tooverify hello web app is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>

<span data-ttu-id="1fe6a-196">Vervolgens maakt u een hybride verbinding en een BizTalk service voor Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-196">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="1fe6a-197">C.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-197">C.</span></span> <span data-ttu-id="1fe6a-198">Een hybride verbinding en een BizTalk Service maken</span><span class="sxs-lookup"><span data-stu-id="1fe6a-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="1fe6a-199">Terug in Hallo Portal, Ga toosettings en klik op **Networking** > **uw hybride-verbindingseindpunten configureren**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-199">Back in hello Portal, go toosettings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Hybride verbindingen][CreateHCHCIcon]
2. <span data-ttu-id="1fe6a-201">Klik op Hallo hybride verbindingen blade **toevoegen** > **nieuwe hybride verbinding**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-201">On hello Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="1fe6a-202">Op Hallo **hybride verbinding maken** blade:</span><span class="sxs-lookup"><span data-stu-id="1fe6a-202">On hello **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="1fe6a-203">Voor **naam**, Geef een naam voor het Hallo-verbinding.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-203">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="1fe6a-204">Voor **hostnaam**, voer de computernaam Hallo van uw SQL Server-hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-204">For **Hostname**, enter hello computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="1fe6a-205">Voor **poort**, voer 1433 (Hallo-standaardpoort voor SQL Server).</span><span class="sxs-lookup"><span data-stu-id="1fe6a-205">For **Port**, enter 1433 (hello default port for SQL Server).</span></span>
   * <span data-ttu-id="1fe6a-206">Klik op **BizTalk Service** > **nieuwe BizTalk Service** en voer een naam voor Hallo BizTalk service.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for hello BizTalk service.</span></span>
     
     ![Een hybride verbinding maken][TwinCreateHCBlades]
4. <span data-ttu-id="1fe6a-208">Klik op **OK** twee keer.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="1fe6a-209">Wanneer Hallo-proces is voltooid, hello **meldingen** gebied knippert een groene **geslaagd** en Hallo **hybride verbinding** blade nieuwe hybride verbinding met hello wordt weergegeven Hallo status als **niet verbonden**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-209">When hello process completes, hello **Notifications** area will flash a green **SUCCESS** and hello **Hybrid connection** blade will show hello new hybrid connection with hello status as **Not connected**.</span></span>
   
    ![Een hybride verbinding is gemaakt][CreateHCOneConnectionCreated]

<span data-ttu-id="1fe6a-211">U hebt op dit moment een belangrijk onderdeel van hybride Hallo-verbinding cloudinfrastructuur voltooid.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-211">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="1fe6a-212">Vervolgens maakt u een bijbehorende lokale apparaat.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="1fe6a-213">D.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-213">D.</span></span> <span data-ttu-id="1fe6a-214">Hallo op premises hybride Verbindingsbeheer toocomplete Hallo verbinding installeren</span><span class="sxs-lookup"><span data-stu-id="1fe6a-214">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="1fe6a-215">Nu die infrastructuur Hallo hybride verbinding voltooid is, maakt u een webtoepassing die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-215">Now that hello hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a><span data-ttu-id="1fe6a-216">E.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-216">E.</span></span> <span data-ttu-id="1fe6a-217">Een eenvoudige ASP.NET-webproject maakt, Hallo databaseverbindingsreeks bewerken en Hallo-project lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1fe6a-217">Create a basic ASP.NET web project, edit hello database connection string, and run hello project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="1fe6a-218">Een eenvoudige ASP.NET-project maken</span><span class="sxs-lookup"><span data-stu-id="1fe6a-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="1fe6a-219">In Visual Studio op Hallo **bestand** menu, een nieuw Project maken:</span><span class="sxs-lookup"><span data-stu-id="1fe6a-219">In Visual Studio, on hello **File** menu, create a new Project:</span></span>
   
    ![Nieuw Visual Studio-project][HCVSNewProject]
2. <span data-ttu-id="1fe6a-221">In Hallo **sjablonen** sectie Hallo **nieuw Project** dialoogvenster Selecteer **Web** en kies **ASP.NET-webtoepassing**, en klik vervolgens op  **OK**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-221">In hello **Templates** section of hello **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Kies ASP.NET-webtoepassing][HCVSChooseASPNET]
3. <span data-ttu-id="1fe6a-223">In Hallo **nieuw ASP.NET-Project** dialoogvenster kiezen **MVC**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-223">In hello **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Kies MVC][HCVSChooseMVC]
4. <span data-ttu-id="1fe6a-225">Als het Hallo-project is gemaakt, weergegeven Hallo toepassing Leesmij pagina.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-225">When hello project has been created, hello application readme page appears.</span></span> <span data-ttu-id="1fe6a-226">Hallo-webproject niet nog uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-226">Do not run hello web project yet.</span></span>
   
    ![Pagina met Leesmij-bestand][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a><span data-ttu-id="1fe6a-228">Hallo-database-verbindingsreeks voor de toepassing hello bewerken</span><span class="sxs-lookup"><span data-stu-id="1fe6a-228">Edit hello database connection string for hello application</span></span>
<span data-ttu-id="1fe6a-229">In deze stap bewerkt u Hallo verbindingsreeks waarin wordt gemeld uw toepassing dat waar toofind uw lokale SQL Server Express database.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-229">In this step, you edit hello connection string that tells your application where toofind your local SQL Server Express database.</span></span> <span data-ttu-id="1fe6a-230">Hallo-verbindingsreeks is in van de toepassing hello Web.config-bestand configuratiegegevens voor de toepassing hello bevat.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-230">hello connection string is in hello application's Web.config file, which contains configuration information for hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="1fe6a-231">tooensure die uw toepassing hello-database die u hebt gemaakt in SQL Server Express en niet Hallo een in Visual Studio standaard LocalDB gebruikt, is het belangrijk dat u deze stap hebt voltooid voordat het project wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-231">tooensure that your application uses hello database that you created in SQL Server Express, and not hello one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="1fe6a-232">Dubbelklik in Solution Explorer op Hallo Web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-232">In Solution Explorer, double-click hello Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="1fe6a-234">Hallo bewerken **connectionStrings** toopoint toohello SQL Server-database op uw lokale computer, Hallo syntaxis in Hallo voorbeeld van de volgende sectie:</span><span class="sxs-lookup"><span data-stu-id="1fe6a-234">Edit hello **connectionStrings** section toopoint toohello SQL Server database on your local machine, following hello syntax in hello following example:</span></span>
   
    ![Verbindingsreeks][HCVSConnectionString]
   
    <span data-ttu-id="1fe6a-236">Houd er rekening mee Hallo volgende bij samenstellen van de verbindingsreeks Hallo:</span><span class="sxs-lookup"><span data-stu-id="1fe6a-236">When composing hello connection string, keep in mind hello following:</span></span>
   
   * <span data-ttu-id="1fe6a-237">Als u verbinding maakt tooa benoemd exemplaar in plaats van een standaardexemplaar (bijvoorbeeld YourServer\SQLEXPRESS), moet u uw SQL Server-toouse statische poorten configureren.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-237">If you are connecting tooa named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server toouse static ports.</span></span> <span data-ttu-id="1fe6a-238">Zie voor meer informatie over het configureren van statische poorten [hoe tooconfigure SQL Server toolisten op een specifieke poort](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="1fe6a-238">For information on configuring static ports, see [How tooconfigure SQL Server toolisten on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="1fe6a-239">Standaard gebruiken benoemde exemplaren UDP en dynamische poorten die worden niet ondersteund door hybride verbindingen.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="1fe6a-240">Het verdient aanbeveling dat u Hallo opgeeft poort (1433 standaard, zoals weergegeven in het voorbeeld Hallo) op Hallo verbindingsreeks zodat u ervoor dat uw lokale SQL Server TCP ingeschakeld is en de juiste poort Hallo wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-240">It is recommended that you specify hello port (1433 by default, as shown in hello example) on hello connection string so that you can be sure that your local SQL Server has TCP enabled and is using hello correct port.</span></span>
   * <span data-ttu-id="1fe6a-241">Houd er rekening mee toouse SQL Server-verificatie tooconnect, Hallo-gebruikersnaam en wachtwoord opgeven in de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-241">Remember toouse SQL Server Authentication tooconnect, specifying hello user ID and password in your connection string.</span></span>
3. <span data-ttu-id="1fe6a-242">Klik op **opslaan** in Visual Studio toosave Hallo Web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-242">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>

### <a name="run-hello-project-locally-and-register-a-new-user"></a><span data-ttu-id="1fe6a-243">Hallo-project lokaal uitvoeren en een nieuwe gebruiker registreren</span><span class="sxs-lookup"><span data-stu-id="1fe6a-243">Run hello project locally and register a new user</span></span>
1. <span data-ttu-id="1fe6a-244">Nu uw nieuwe webproject lokaal uitvoeren door te klikken op de knop Bladeren Hallo onder foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-244">Now, run your new web project locally by clicking hello browse button under Debug.</span></span> <span data-ttu-id="1fe6a-245">In dit voorbeeld gebruikt Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-245">This example uses Internet Explorer.</span></span>
   
    ![Project uitvoeren][HCVSRunProject]
2. <span data-ttu-id="1fe6a-247">Kies op Hallo rechtsboven standaardwebpagina hello, **registreren** tooregister een nieuw account:</span><span class="sxs-lookup"><span data-stu-id="1fe6a-247">On hello upper right of hello default web page, choose **Register** tooregister a new account:</span></span>
   
    ![Registreer een nieuwe account][HCVSRegisterLocally]
3. <span data-ttu-id="1fe6a-249">Voer een gebruikersnaam en wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="1fe6a-249">Enter a user name and password:</span></span>
   
    ![Voer de gebruikersnaam en wachtwoord][HCVSCreateNewAccount]
   
    <span data-ttu-id="1fe6a-251">Dit maakt automatisch een database op de lokale SQL Server die de lidmaatschapsgegevens Hallo voor uw toepassing bevat.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-251">This automatically creates a database on your local SQL Server that holds hello membership information for your application.</span></span> <span data-ttu-id="1fe6a-252">Een van de tabellen hello (**dbo. AspNetUsers**) blokkeringen web-app gebruikersreferenties zoals Hallo die u zojuist hebt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-252">One of hello tables (**dbo.AspNetUsers**) holds web app user credentials like hello ones that you just entered.</span></span> <span data-ttu-id="1fe6a-253">Deze tabel ziet u later in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-253">You will see this table later in hello tutorial.</span></span>
4. <span data-ttu-id="1fe6a-254">Sluit het browservenster Hallo met standaardwebpagina Hallo.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-254">Close hello browser window of hello default web page.</span></span> <span data-ttu-id="1fe6a-255">Hierdoor wordt voorkomen dat de toepassing hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-255">This stops hello application in Visual Studio.</span></span>

<span data-ttu-id="1fe6a-256">U bent nu klaar voor de volgende stap hello, namelijk toopublish Hallo toepassing tooAzure en testen.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-256">You are now ready for hello next step, which is toopublish hello application tooAzure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a><span data-ttu-id="1fe6a-257">F.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-257">F.</span></span> <span data-ttu-id="1fe6a-258">Hallo web application tooAzure publiceren en testen</span><span class="sxs-lookup"><span data-stu-id="1fe6a-258">Publish hello web application tooAzure and test it</span></span>
<span data-ttu-id="1fe6a-259">Nu u uw toepassing tooyour App Service-web-app publiceren en test deze toosee hoe Hallo hybride verbinding die u eerder hebt geconfigureerd is gebruikte tooconnect wordt uw web-app toohello database op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-259">Now, you'll publish your application tooyour App Service web app and then test it toosee how hello hybrid connection you configured earlier is being used tooconnect your web app toohello database on your local machine.</span></span>

### <a name="publish-hello-web-application"></a><span data-ttu-id="1fe6a-260">Publiceer de webtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="1fe6a-260">Publish hello web application</span></span>
1. <span data-ttu-id="1fe6a-261">U kunt uw publicatieprofiel voor App Service-web-app in Azure Portal Hallo Hallo downloaden.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-261">You can download your publishing profile for hello App Service web app in hello Azure Portal.</span></span> <span data-ttu-id="1fe6a-262">Klik op de blade voor uw web-app Hallo **Get publicatieprofiel**, en sla Hallo bestand tooyour computer.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-262">On hello blade for your web app, click **Get publish profile**, and then save hello file tooyour computer.</span></span>
   
    ![Publicatieprofiel downloaden][PortalDownloadPublishProfile]
   
    <span data-ttu-id="1fe6a-264">U gaat dit bestand vervolgens importeren in uw Visual Studio-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="1fe6a-265">In Visual Studio met de rechtermuisknop op Hallo projectnaam in Solution Explorer en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-265">In Visual Studio, right-click hello project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Selecteer publiceren][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="1fe6a-267">In Hallo **webpublicatie** dialoogvenster op Hallo **profiel** Kies **importeren**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-267">In hello **Publish Web** dialog, on hello **Profile** tab, choose **Import**.</span></span>
   
    ![Importeren][HCVSPublishWebDialogImport]
4. <span data-ttu-id="1fe6a-269">Bladeren tooyour publicatieprofiel gedownload, selecteert u deze en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-269">Browse tooyour downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Tooprofile bladeren][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="1fe6a-271">De publicatie-informatie is geïmporteerd en geeft weer op Hallo **verbinding** tabblad van Hallo dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-271">Your publishing information is imported and displays on hello **Connection** tab of hello dialog.</span></span>
   
    ![Klik op publiceren][HCVSClickPublish]
   
    <span data-ttu-id="1fe6a-273">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="1fe6a-274">Wanneer publiceren is voltooid, wordt uw browser start en het weergeven van uw ASP.NET-toepassing nu bekend--, behalve dat nu is het live in Azure-cloud Hallo!</span><span class="sxs-lookup"><span data-stu-id="1fe6a-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in hello Azure cloud!</span></span>

<span data-ttu-id="1fe6a-275">Vervolgens wordt u uw live web application toosee de hybride verbinding in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-275">Next, you will use your live web application toosee its Hybrid Connection in action.</span></span>

### <a name="test-hello-completed-web-application-on-azure"></a><span data-ttu-id="1fe6a-276">Test Hallo op Azure-web-App voltooid</span><span class="sxs-lookup"><span data-stu-id="1fe6a-276">Test hello completed web application on Azure</span></span>
1. <span data-ttu-id="1fe6a-277">Hallo bovenaan rechts van de webpagina op Azure, kies **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-277">On hello top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Test aanmelden][HCTestLogIn]
2. <span data-ttu-id="1fe6a-279">Uw App Service-web-app nu is verbonden tooyour-webtoepassing lidmaatschapsdatabase op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-279">Your App Service web app is now connected tooyour web application's membership database on your local machine.</span></span> <span data-ttu-id="1fe6a-280">tooverify deze, meld u aan met van Hallo dezelfde referenties die u hebt opgegeven in de lokale Hallo eerder van de database.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-280">tooverify this, log in with hello same credentials that you entered in hello local database earlier.</span></span>
   
    ![Hallo begroeting][HCTestHelloContoso]
3. <span data-ttu-id="1fe6a-282">toofurther uw nieuwe hybride verbinding testen en meld u af bij uw Azure-web-toepassing registreren als een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-282">toofurther test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="1fe6a-283">Geef een nieuwe gebruikersnaam en wachtwoord en klik vervolgens op **registreren**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Test een andere gebruiker registreren][HCTestRegisterRelecloud]
4. <span data-ttu-id="1fe6a-285">tooverify dat Hallo nieuwe gebruikersreferenties zijn opgeslagen in de lokale database via uw hybride verbinding open SQL Management Studio op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-285">tooverify that hello new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="1fe6a-286">Vouw in Object Explorer Hallo **MembershipDB** database uit en vouw vervolgens **tabellen**.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-286">In Object Explorer, expand hello **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="1fe6a-287">Klik met de rechtermuisknop Hallo **dbo. AspNetUsers** lidmaatschap tabel en kies **Selecteer Top 1000 rijen** tooview Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-287">Right-click hello **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** tooview hello results.</span></span>
   
    ![Hallo-resultaten weergeven][HCTestSSMSTree]
5. <span data-ttu-id="1fe6a-289">Uw lidmaatschap van lokale tabel toont nu beide accounts - hello die u lokaal hebt gemaakt en Hallo dat u hebt gemaakt in hello Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-289">Your local membership table now shows both accounts - hello one that you created locally, and hello one that you created in hello Azure cloud.</span></span> <span data-ttu-id="1fe6a-290">Hallo dat u hebt gemaakt in de cloud Hallo is tooyour lokale-database via de Azure-functie voor hybride verbinding opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-290">hello one that you created in hello cloud has been saved tooyour on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Geregistreerde gebruikers in de lokale database.][HCTestShowMemberDb]

<span data-ttu-id="1fe6a-292">U hebt nu gemaakt en geïmplementeerd ASP.NET-webtoepassing die gebruikmaakt van een hybride verbinding tussen een web-app in Azure-cloud Hallo en een on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in hello Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="1fe6a-293">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="1fe6a-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="1fe6a-294">Zie ook</span><span class="sxs-lookup"><span data-stu-id="1fe6a-294">See Also</span></span>
[<span data-ttu-id="1fe6a-295">Overzicht van hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="1fe6a-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="1fe6a-296">Josh Twist introduceert hybride verbindingen (Channel 9 video)</span><span class="sxs-lookup"><span data-stu-id="1fe6a-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="1fe6a-297">Overzicht van hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="1fe6a-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="1fe6a-298">BizTalk Services: De tabbladen Dashboard, bewaken, schaal, configureren en hybride verbinding</span><span class="sxs-lookup"><span data-stu-id="1fe6a-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="1fe6a-299">Het bouwen van een echte hybride Cloud met naadloze toepassing draagbaarheid (Channel 9 video)</span><span class="sxs-lookup"><span data-stu-id="1fe6a-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="1fe6a-300">Toegang tot on-premises resources met behulp van hybride verbindingen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1fe6a-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="1fe6a-301">Identiteit van de ASP.NET-overzicht</span><span class="sxs-lookup"><span data-stu-id="1fe6a-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
