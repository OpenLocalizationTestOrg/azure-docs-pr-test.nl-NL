---
title: Verbinding maken met on-premises SQL-Server vanaf een web-app in Azure App Service met behulp van hybride verbindingen
description: Een web-app in Microsoft Azure maken en te verbinden met een lokale SQL Server-database.
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
ms.openlocfilehash: 12456ef3e2aecfa7a03cca97de2ff6ffd9602357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="7dc68-103">Verbinding maken met on-premises SQL-Server vanaf een web-app in Azure App Service met behulp van hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="7dc68-103">Connect to on-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="7dc68-104">Hybride verbindingen kunnen worden aangesloten [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps in de lokale bronnen die een statische TCP-poort gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7dc68-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps to on-premises resources that use a static TCP port.</span></span> <span data-ttu-id="7dc68-105">Ondersteunde resources omvatten Microsoft SQL Server, MySQL, HTTP-Web-API's, App Service en de meeste aangepaste webservices.</span><span class="sxs-lookup"><span data-stu-id="7dc68-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="7dc68-106">In deze zelfstudie leert u het maken van een App Service-web-app in de [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715)de web-app verbinding met uw lokale lokale SQL Server-database met de nieuwe functie voor hybride verbinding, een eenvoudige ASP.NET-toepassing die de hybride verbinding gebruiken en de toepassing implementeren naar de App Service-web-app maken.</span><span class="sxs-lookup"><span data-stu-id="7dc68-106">In this tutorial, you will learn how to create an App Service web app in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect the web app to your local on-premises SQL Server database using the new Hybrid Connection feature, create a simple ASP.NET application that will use the hybrid connection, and deploy the application to the App Service web app.</span></span> <span data-ttu-id="7dc68-107">De voltooide web-app in Azure worden gebruikersreferenties opgeslagen in een lidmaatschapsdatabase on-premises.</span><span class="sxs-lookup"><span data-stu-id="7dc68-107">The completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="7dc68-108">De zelfstudie wordt ervan uitgegaan dat geen ervaring met behulp van Azure of ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7dc68-108">The tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="7dc68-109">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="7dc68-109">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7dc68-110">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="7dc68-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="7dc68-111">De Web-Apps-gedeelte van de functie hybride verbindingen is alleen beschikbaar in de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7dc68-111">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="7dc68-112">Zie voor informatie over het maken van een verbinding in BizTalk Services [hybride verbindingen](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="7dc68-112">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7dc68-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7dc68-113">Prerequisites</span></span>
<span data-ttu-id="7dc68-114">Voor deze zelfstudie hebt voltooid, moet u de volgende producten.</span><span class="sxs-lookup"><span data-stu-id="7dc68-114">To complete this tutorial, you'll need the following products.</span></span> <span data-ttu-id="7dc68-115">Alle zijn beschikbaar in de beschikbare versies zodat u kunt beginnen met het ontwikkelen voor Azure volledig voor gratis.</span><span class="sxs-lookup"><span data-stu-id="7dc68-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="7dc68-116">**Azure-abonnement** : voor een gratis abonnement, Zie [gratis proefversie van Azure](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7dc68-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="7dc68-117">**Visual Studio 2013** : als u wilt een gratis evaluatieversie van Visual Studio 2013 downloaden, Zie [Visual Studio-Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="7dc68-117">**Visual Studio 2013** - To download a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="7dc68-118">Installeer dit voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="7dc68-118">Install this before continuing.</span></span>
* <span data-ttu-id="7dc68-119">**Microsoft .NET Framework 3.5 servicepack 1** -als het besturingssysteem Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 of Windows Server 2008 R2 is, kunt u dit inschakelen in het Configuratiescherm > programma's en onderdelen > Windows-onderdelen in- of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="7dc68-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="7dc68-120">Anders kunt u dit downloaden van de [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="7dc68-120">Otherwise, you can download it from the [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="7dc68-121">**SQL Server 2014 Express met hulpprogramma's voor** -Microsoft SQL Server Express gratis downloaden op de [pagina Microsoft Web Platform Database](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="7dc68-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at the [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="7dc68-122">Kies de **Express** (geen LocalDB) versie.</span><span class="sxs-lookup"><span data-stu-id="7dc68-122">Choose the **Express** (not LocalDB) version.</span></span> <span data-ttu-id="7dc68-123">De **Express met hulpprogramma's voor** versie SQL Server Management Studio, gaat u in deze zelfstudie bevat.</span><span class="sxs-lookup"><span data-stu-id="7dc68-123">The **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="7dc68-124">**SQL Server Management Studio Express** - dat deel uitmaakt van de SQL Server 2014 Express met hulpprogramma's downloaden hierboven vermeld, maar als u moet afzonderlijk te installeren, kunt u downloaden en installeren via de [downloadpagina voor SQL Server Express](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="7dc68-124">**SQL Server Management Studio Express** - This is included with the SQL Server 2014 Express with Tools download mentioned above, but if you need to install it separately, you can download and install it from the [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="7dc68-125">De zelfstudie wordt ervan uitgegaan dat u een Azure-abonnement hebt dat u Visual Studio 2013 hebt geïnstalleerd en u hebt geïnstalleerd of .NET Framework 3.5 ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="7dc68-125">The tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="7dc68-126">De zelfstudie laat zien hoe u SQL Server 2014 Express installeren in een configuratie die goed samen met de functie Azure hybride verbindingen (een standaardexemplaar met een statische TCP-poort werkt).</span><span class="sxs-lookup"><span data-stu-id="7dc68-126">The tutorial shows you how to install SQL Server 2014 Express in a configuration that works well with the Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="7dc68-127">Voordat u de zelfstudie begint, download SQL Server 2014 Express met hulpprogramma's van de locatie die hierboven worden genoemd als u geen SQL Server geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7dc68-127">Before starting the tutorial, download SQL Server 2014 Express with Tools from the location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="7dc68-128">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="7dc68-128">Notes</span></span>
<span data-ttu-id="7dc68-129">Als u wilt een on-premises SQL Server of SQL Server Express-database met een hybride verbinding gebruiken, moet TCP/IP moet zijn ingeschakeld op een statische poort.</span><span class="sxs-lookup"><span data-stu-id="7dc68-129">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="7dc68-130">Standaardexemplaren op SQL Server gebruiken statische poort 1433, dat niet het benoemde exemplaren.</span><span class="sxs-lookup"><span data-stu-id="7dc68-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="7dc68-131">De computer waarop u de hybride Verbindingsbeheer lokale agent installeert:</span><span class="sxs-lookup"><span data-stu-id="7dc68-131">The computer on which you install the on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="7dc68-132">Moet uitgaande verbinding met Azure via:</span><span class="sxs-lookup"><span data-stu-id="7dc68-132">Must have outbound connectivity to Azure over:</span></span>

| <span data-ttu-id="7dc68-133">Poort</span><span class="sxs-lookup"><span data-stu-id="7dc68-133">Port</span></span> | <span data-ttu-id="7dc68-134">Waarom</span><span class="sxs-lookup"><span data-stu-id="7dc68-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="7dc68-135">80</span><span class="sxs-lookup"><span data-stu-id="7dc68-135">80</span></span> |<span data-ttu-id="7dc68-136">**Vereist** voor HTTP-poort voor de validatie van het servercertificaat en eventueel voor toegang tot gegevens.</span><span class="sxs-lookup"><span data-stu-id="7dc68-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="7dc68-137">443</span><span class="sxs-lookup"><span data-stu-id="7dc68-137">443</span></span> |<span data-ttu-id="7dc68-138">**Optionele** voor toegang tot gegevens.</span><span class="sxs-lookup"><span data-stu-id="7dc68-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="7dc68-139">Als uitgaande verbinding met 443 niet beschikbaar is, wordt de TCP-poort 80 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7dc68-139">If outbound connectivity to 443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="7dc68-140">5671 en 9352</span><span class="sxs-lookup"><span data-stu-id="7dc68-140">5671 and 9352</span></span> |<span data-ttu-id="7dc68-141">**Aanbevolen** maar optioneel voor toegang tot gegevens.</span><span class="sxs-lookup"><span data-stu-id="7dc68-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="7dc68-142">Houd er rekening mee dat deze modus levert meestal hogere doorvoer.</span><span class="sxs-lookup"><span data-stu-id="7dc68-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="7dc68-143">Als u uitgaande verbindingen via deze poorten niet beschikbaar is, wordt de TCP-poort 443 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7dc68-143">If outbound connectivity to these ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="7dc68-144">Moet kunnen bereiken de *hostnaam*:*portnumber* van uw lokale resource.</span><span class="sxs-lookup"><span data-stu-id="7dc68-144">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="7dc68-145">De stappen in dit artikel wordt ervan uitgegaan dat u gebruikmaakt van de browser van de computer die als host voor de lokale-agent voor hybride verbinding fungeert.</span><span class="sxs-lookup"><span data-stu-id="7dc68-145">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>

<span data-ttu-id="7dc68-146">Als u al SQL Server geïnstalleerd in een configuratie en in een omgeving die voldoet aan de voorwaarden die hebt hierboven worden beschreven, kunt u overslaan en beginnen met [maken van een SQL Server-database op de lokale](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="7dc68-146">If you already have SQL Server installed in a configuration and in an environment that meets the conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="7dc68-147">A.</span><span class="sxs-lookup"><span data-stu-id="7dc68-147">A.</span></span> <span data-ttu-id="7dc68-148">SQL Server Express installeren en maken van een SQL Server-database op de lokale TCP/IP inschakelen</span><span class="sxs-lookup"><span data-stu-id="7dc68-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="7dc68-149">Deze sectie wordt beschreven hoe u SQL Server Express installeren en een database maken, zodat uw webtoepassing met de Azure Portal werken zullen TCP/IP inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7dc68-149">This section shows you how to install SQL Server Express, enable TCP/IP, and create a database so that your web application will work with the Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="7dc68-150">SQL Server Express installeren</span><span class="sxs-lookup"><span data-stu-id="7dc68-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="7dc68-151">U installeert SQL Server Express door de **SQLEXPRWT_x64_ENU.exe** of **SQLEXPR_x86_ENU.exe** -bestand dat u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="7dc68-151">To install SQL Server Express, run the **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="7dc68-152">Het Installatiecentrum van SQL Server-wizard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7dc68-152">The SQL Server Installation Center wizard appears.</span></span>
   
    ![Installatie van SQL Server][SQLServerInstall]
2. <span data-ttu-id="7dc68-154">Kies **zelfstandige installatie van nieuwe SQL-Server of functies toevoegen aan een bestaande installatie**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-154">Choose **New SQL Server stand-alone installation or add features to an existing installation**.</span></span> <span data-ttu-id="7dc68-155">Volg de instructies, accepteert de standaardwaarden en -instellingen, totdat u de **Exemplaarconfiguratie** pagina.</span><span class="sxs-lookup"><span data-stu-id="7dc68-155">Follow the instructions, accepting the default choices and settings, until you get to the **Instance Configuration** page.</span></span>
3. <span data-ttu-id="7dc68-156">Op de **Exemplaarconfiguratie** pagina **standaardexemplaar**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-156">On the **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Kies standaardexemplaar][ChooseDefaultInstance]
   
    <span data-ttu-id="7dc68-158">Standaard luistert het standaardexemplaar van SQL Server voor aanvragen van SQL Server-clients op statische poort 1433, dit is wat de functie hybride verbindingen is vereist.</span><span class="sxs-lookup"><span data-stu-id="7dc68-158">By default, the default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what the Hybrid Connections feature requires.</span></span> <span data-ttu-id="7dc68-159">Benoemde exemplaren dynamische poorten en UDP, die niet worden ondersteund door hybride verbindingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7dc68-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="7dc68-160">Accepteer de standaardinstellingen op de **serverconfiguratie** pagina.</span><span class="sxs-lookup"><span data-stu-id="7dc68-160">Accept the defaults on the **Server Configuration** page.</span></span>
5. <span data-ttu-id="7dc68-161">Op de **Database Engine-configuratie** pagina onder **verificatiemodus**, kies **gemengde modus (SQL Server-verificatie en Windows-verificatie)**, en een wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="7dc68-161">On the **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Kies in de gemengde modus][ChooseMixedMode]
   
    <span data-ttu-id="7dc68-163">In deze zelfstudie wordt u SQL Server-verificatie.</span><span class="sxs-lookup"><span data-stu-id="7dc68-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="7dc68-164">Zorg ervoor dat het wachtwoord dat u opgeeft, onthoud omdat u deze later hebt.</span><span class="sxs-lookup"><span data-stu-id="7dc68-164">Be sure to remember the password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="7dc68-165">Doorloop de rest van de wizard om de installatie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="7dc68-165">Step through the rest of the wizard to complete the installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="7dc68-166">TCP/IP inschakelen</span><span class="sxs-lookup"><span data-stu-id="7dc68-166">Enable TCP/IP</span></span>
<span data-ttu-id="7dc68-167">Om TCP/IP, gebruikt u SQL Server Configuration Manager, die tijdens de installatie van SQL Server Express is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7dc68-167">To enable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="7dc68-168">Volg de stappen in [TCP/IP-netwerkprotocol inschakelen voor SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="7dc68-168">Follow the steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="7dc68-169">Lokale voor een SQL Server-database maken</span><span class="sxs-lookup"><span data-stu-id="7dc68-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="7dc68-170">Uw Visual Studio-webtoepassing vereist een lidmaatschapsdatabase die toegankelijk zijn voor Azure.</span><span class="sxs-lookup"><span data-stu-id="7dc68-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="7dc68-171">Hiervoor moet een SQL Server of SQL Server Express-database (niet de LocalDB-database die de MVC-sjabloon standaard gebruikt), zodat u de lidmaatschapsdatabase naast gaat maken.</span><span class="sxs-lookup"><span data-stu-id="7dc68-171">This requires a SQL Server or SQL Server Express database (not the LocalDB database that the MVC template uses by default), so you'll create the membership database next.</span></span>

1. <span data-ttu-id="7dc68-172">In SQL Server Management Studio verbinding met de SQL-Server die u zojuist hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7dc68-172">In SQL Server Management Studio, connect to the SQL Server you just installed.</span></span> <span data-ttu-id="7dc68-173">(Als de **verbinding maken met Server** dialoogvenster niet automatisch wordt weergegeven, gaat u naar **Objectverkenner** in het linkerdeelvenster klikt u op **Connect**, en klik vervolgens op **Database-Engine**.) ![Verbinding maken met Server][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="7dc68-173">(If the **Connect to Server** dialog does not appear automatically, navigate to **Object Explorer** in the left pane, click **Connect**, and then click **Database Engine**.) ![Connect to Server][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="7dc68-174">Voor **servertype**, kies **Database-Engine**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="7dc68-175">Voor **servernaam**, kunt u **localhost** of de naam van de computer die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7dc68-175">For **Server name**, you can use **localhost** or the name of the computer that you are using.</span></span> <span data-ttu-id="7dc68-176">Kies **SQL Server-verificatie**, en meld u aan met de sa-gebruikersnaam en het wachtwoord dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7dc68-176">Choose **SQL Server authentication**, and then log in with the sa user name and the password that you created earlier.</span></span>
2. <span data-ttu-id="7dc68-177">Als u wilt een nieuwe database maken met behulp van SQL Server Management Studio, met de rechtermuisknop op **Databases** in Object Explorer en klik vervolgens op **nieuwe Database**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-177">To create a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Nieuwe database maken][SSMScreateNewDB]
3. <span data-ttu-id="7dc68-179">In de **nieuwe Database** dialoogvenster MembershipDB invoeren voor de naam van de database en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-179">In the **New Database** dialog, enter MembershipDB for the database name, and then click **OK**.</span></span>
   
    ![Databasenaam opgeven][SSMSprovideDBname]
   
    <span data-ttu-id="7dc68-181">Houd er rekening mee dat u niet geen wijzigingen in de database op dit moment aanbrengen bent.</span><span class="sxs-lookup"><span data-stu-id="7dc68-181">Note that you do not make any changes to the database at this point.</span></span> <span data-ttu-id="7dc68-182">De lidmaatschapsgegevens wordt later automatisch door uw webtoepassing toegevoegd wanneer u het uitvoert.</span><span class="sxs-lookup"><span data-stu-id="7dc68-182">The membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="7dc68-183">In Object Explorer, als u wilt uitbreiden **Databases**, ziet u dat de lidmaatschapsdatabase is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7dc68-183">In Object Explorer, if you expand **Databases**, you will see that the membership database has been created.</span></span>
   
    ![MembershipDB gemaakt][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="7dc68-185">B.</span><span class="sxs-lookup"><span data-stu-id="7dc68-185">B.</span></span> <span data-ttu-id="7dc68-186">Een web-app maken in de Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="7dc68-186">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="7dc68-187">Als u al een web-app in de Azure-Portal die u wilt gebruiken voor deze zelfstudie hebt gemaakt, kunt u verder gaan naar [een hybride verbinding en een BizTalk Service maken](#CreateHC) en van daaruit worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="7dc68-187">If you have already created a web app in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="7dc68-188">In de [Azure Portal](https://portal.azure.com), klikt u op **nieuw** > **Web en mobiel** > **Web-app**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-188">In the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![Knop Nieuw][New]
2. <span data-ttu-id="7dc68-190">Configureren van uw web-app en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Websitenaam][WebsiteCreationBlade]
3. <span data-ttu-id="7dc68-192">Na enkele ogenblikken de web-app wordt gemaakt en de blade web-app wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7dc68-192">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="7dc68-193">De blade is een verticaal schuifbare dashboard waarmee u uw web-app beheren.</span><span class="sxs-lookup"><span data-stu-id="7dc68-193">The blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Website worden uitgevoerd][WebSiteRunningBlade]
   
    <span data-ttu-id="7dc68-195">Om te controleren of de web-app live, klikt u op de **Bladeren** pictogram om de standaardpagina weer te geven.</span><span class="sxs-lookup"><span data-stu-id="7dc68-195">To verify the web app is live, you can click the **Browse** icon to display the default page.</span></span>

<span data-ttu-id="7dc68-196">Vervolgens maakt u een hybride verbinding en een BizTalk service voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="7dc68-196">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="7dc68-197">C.</span><span class="sxs-lookup"><span data-stu-id="7dc68-197">C.</span></span> <span data-ttu-id="7dc68-198">Een hybride verbinding en een BizTalk Service maken</span><span class="sxs-lookup"><span data-stu-id="7dc68-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="7dc68-199">Terug in de Portal, gaat u naar instellingen en klik op **Networking** > **uw hybride-verbindingseindpunten configureren**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-199">Back in the Portal, go to settings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Hybride verbindingen][CreateHCHCIcon]
2. <span data-ttu-id="7dc68-201">Klik op de blade hybride verbindingen **toevoegen** > **nieuwe hybride verbinding**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-201">On the Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="7dc68-202">Op de **hybride verbinding maken** blade:</span><span class="sxs-lookup"><span data-stu-id="7dc68-202">On the **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="7dc68-203">Voor **naam**, Geef een naam op voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="7dc68-203">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="7dc68-204">Voor **hostnaam**, voer de computernaam van uw SQL Server-hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="7dc68-204">For **Hostname**, enter the computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="7dc68-205">Voor **poort**, voer 1433 (de standaardpoort voor SQL Server).</span><span class="sxs-lookup"><span data-stu-id="7dc68-205">For **Port**, enter 1433 (the default port for SQL Server).</span></span>
   * <span data-ttu-id="7dc68-206">Klik op **BizTalk Service** > **nieuwe BizTalk Service** en voer een naam voor de BizTalk service.</span><span class="sxs-lookup"><span data-stu-id="7dc68-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for the BizTalk service.</span></span>
     
     ![Een hybride verbinding maken][TwinCreateHCBlades]
4. <span data-ttu-id="7dc68-208">Klik op **OK** twee keer.</span><span class="sxs-lookup"><span data-stu-id="7dc68-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="7dc68-209">Wanneer het proces is voltooid, de **meldingen** gebied knippert een groene **geslaagd** en de **hybride verbinding** blade ziet de nieuwe hybride verbinding met de status als **niet verbonden**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-209">When the process completes, the **Notifications** area will flash a green **SUCCESS** and the **Hybrid connection** blade will show the new hybrid connection with the status as **Not connected**.</span></span>
   
    ![Een hybride verbinding is gemaakt][CreateHCOneConnectionCreated]

<span data-ttu-id="7dc68-211">U hebt op dit moment een belangrijk onderdeel van de cloudinfrastructuur voor hybride verbinding voltooid.</span><span class="sxs-lookup"><span data-stu-id="7dc68-211">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="7dc68-212">Vervolgens maakt u een bijbehorende lokale apparaat.</span><span class="sxs-lookup"><span data-stu-id="7dc68-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="7dc68-213">D.</span><span class="sxs-lookup"><span data-stu-id="7dc68-213">D.</span></span> <span data-ttu-id="7dc68-214">Installeren van de lokale hybride Verbindingsbeheer om de verbinding te voltooien</span><span class="sxs-lookup"><span data-stu-id="7dc68-214">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="7dc68-215">Nu dat de infrastructuur van hybride verbinding voltooid is, maakt u een webtoepassing die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7dc68-215">Now that the hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-the-database-connection-string-and-run-the-project-locally"></a><span data-ttu-id="7dc68-216">E.</span><span class="sxs-lookup"><span data-stu-id="7dc68-216">E.</span></span> <span data-ttu-id="7dc68-217">Een eenvoudige ASP.NET-webproject maakt, de verbindingsreeks voor de database en het project lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7dc68-217">Create a basic ASP.NET web project, edit the database connection string, and run the project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="7dc68-218">Een eenvoudige ASP.NET-project maken</span><span class="sxs-lookup"><span data-stu-id="7dc68-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="7dc68-219">In Visual Studio op de **bestand** menu, een nieuw Project maken:</span><span class="sxs-lookup"><span data-stu-id="7dc68-219">In Visual Studio, on the **File** menu, create a new Project:</span></span>
   
    ![Nieuw Visual Studio-project][HCVSNewProject]
2. <span data-ttu-id="7dc68-221">In de **sjablonen** sectie van de **nieuw Project** dialoogvenster Selecteer **Web** en kies **ASP.NET-webtoepassing**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-221">In the **Templates** section of the **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Kies ASP.NET-webtoepassing][HCVSChooseASPNET]
3. <span data-ttu-id="7dc68-223">In de **nieuw ASP.NET-Project** dialoogvenster kiezen **MVC**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-223">In the **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Kies MVC][HCVSChooseMVC]
4. <span data-ttu-id="7dc68-225">Wanneer het project is gemaakt, wordt de pagina met toepassingen Leesmij-bestand weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7dc68-225">When the project has been created, the application readme page appears.</span></span> <span data-ttu-id="7dc68-226">Het webproject niet nog uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7dc68-226">Do not run the web project yet.</span></span>
   
    ![Pagina met Leesmij-bestand][HCVSReadmePage]

### <a name="edit-the-database-connection-string-for-the-application"></a><span data-ttu-id="7dc68-228">De database-verbindingsreeks voor de toepassing bewerken</span><span class="sxs-lookup"><span data-stu-id="7dc68-228">Edit the database connection string for the application</span></span>
<span data-ttu-id="7dc68-229">In deze stap maakt bewerken u de verbindingsreeks waarin wordt gemeld dat uw toepassing waar vind ik de lokale SQL Server Express-database.</span><span class="sxs-lookup"><span data-stu-id="7dc68-229">In this step, you edit the connection string that tells your application where to find your local SQL Server Express database.</span></span> <span data-ttu-id="7dc68-230">De verbindingsreeks is in de toepassing Web.config-bestand configuratiegegevens voor de toepassing bevat.</span><span class="sxs-lookup"><span data-stu-id="7dc68-230">The connection string is in the application's Web.config file, which contains configuration information for the application.</span></span>

> [!NOTE]
> <span data-ttu-id="7dc68-231">Om ervoor te zorgen dat uw toepassing gebruikmaakt van de database die u hebt gemaakt in SQL Server Express en niet het in Visual Studio standaard LocalDB, is het belangrijk dat u deze stap hebt voltooid voordat het project wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7dc68-231">To ensure that your application uses the database that you created in SQL Server Express, and not the one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="7dc68-232">Dubbelklik in Solution Explorer op het bestand Web.config.</span><span class="sxs-lookup"><span data-stu-id="7dc68-232">In Solution Explorer, double-click the Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="7dc68-234">Bewerk de **connectionStrings** sectie om te verwijzen naar de SQL Server-database op uw lokale computer, de syntaxis in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7dc68-234">Edit the **connectionStrings** section to point to the SQL Server database on your local machine, following the syntax in the following example:</span></span>
   
    ![Verbindingsreeks][HCVSConnectionString]
   
    <span data-ttu-id="7dc68-236">Houd bij het samenstellen van de verbindingsreeks rekening met het volgende:</span><span class="sxs-lookup"><span data-stu-id="7dc68-236">When composing the connection string, keep in mind the following:</span></span>
   
   * <span data-ttu-id="7dc68-237">Als u verbinding maakt met een benoemd exemplaar in plaats van een standaardexemplaar (bijvoorbeeld YourServer\SQLEXPRESS), moet u uw SQL Server voor het gebruik van statische poorten configureren.</span><span class="sxs-lookup"><span data-stu-id="7dc68-237">If you are connecting to a named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server to use static ports.</span></span> <span data-ttu-id="7dc68-238">Zie voor meer informatie over het configureren van statische poorten [het configureren van SQL Server om te luisteren op een specifieke poort](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="7dc68-238">For information on configuring static ports, see [How to configure SQL Server to listen on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="7dc68-239">Standaard gebruiken benoemde exemplaren UDP en dynamische poorten die worden niet ondersteund door hybride verbindingen.</span><span class="sxs-lookup"><span data-stu-id="7dc68-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="7dc68-240">Het is raadzaam dat u de poort opgeeft (1433 standaard, zoals wordt weergegeven in het voorbeeld) op de verbindingsreeks zodat u kunt er zeker van dat de lokale SQL-Server heeft TCP ingeschakeld en de juiste poort wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7dc68-240">It is recommended that you specify the port (1433 by default, as shown in the example) on the connection string so that you can be sure that your local SQL Server has TCP enabled and is using the correct port.</span></span>
   * <span data-ttu-id="7dc68-241">Vergeet niet SQL Server-verificatie gebruiken om verbinding te maken voor het opgeven van de gebruikers-ID en het wachtwoord in de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="7dc68-241">Remember to use SQL Server Authentication to connect, specifying the user ID and password in your connection string.</span></span>
3. <span data-ttu-id="7dc68-242">Klik op **opslaan** in Visual Studio het Web.config-bestand wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="7dc68-242">Click **Save** in Visual Studio to save the Web.config file.</span></span>

### <a name="run-the-project-locally-and-register-a-new-user"></a><span data-ttu-id="7dc68-243">Het project lokaal uitvoeren en een nieuwe gebruiker registreren</span><span class="sxs-lookup"><span data-stu-id="7dc68-243">Run the project locally and register a new user</span></span>
1. <span data-ttu-id="7dc68-244">Nu uw nieuwe webproject lokaal uitvoeren door te klikken op de bladerknop onder foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="7dc68-244">Now, run your new web project locally by clicking the browse button under Debug.</span></span> <span data-ttu-id="7dc68-245">In dit voorbeeld gebruikt Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="7dc68-245">This example uses Internet Explorer.</span></span>
   
    ![Project uitvoeren][HCVSRunProject]
2. <span data-ttu-id="7dc68-247">Kies op de rechterbovenhoek van de standaardwebpagina **registreren** registreren van een nieuw account:</span><span class="sxs-lookup"><span data-stu-id="7dc68-247">On the upper right of the default web page, choose **Register** to register a new account:</span></span>
   
    ![Registreer een nieuwe account][HCVSRegisterLocally]
3. <span data-ttu-id="7dc68-249">Voer een gebruikersnaam en wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="7dc68-249">Enter a user name and password:</span></span>
   
    ![Voer de gebruikersnaam en wachtwoord][HCVSCreateNewAccount]
   
    <span data-ttu-id="7dc68-251">Dit maakt automatisch een database op de lokale SQL Server die de lidmaatschapsgegevens voor uw toepassing bevat.</span><span class="sxs-lookup"><span data-stu-id="7dc68-251">This automatically creates a database on your local SQL Server that holds the membership information for your application.</span></span> <span data-ttu-id="7dc68-252">Een van de tabellen (**dbo. AspNetUsers**) blokkeringen web-app gebruikersreferenties zoals de waarden die u zojuist hebt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="7dc68-252">One of the tables (**dbo.AspNetUsers**) holds web app user credentials like the ones that you just entered.</span></span> <span data-ttu-id="7dc68-253">Verderop in de zelfstudie ziet u deze tabel.</span><span class="sxs-lookup"><span data-stu-id="7dc68-253">You will see this table later in the tutorial.</span></span>
4. <span data-ttu-id="7dc68-254">Sluit het browservenster van de standaard-webpagina.</span><span class="sxs-lookup"><span data-stu-id="7dc68-254">Close the browser window of the default web page.</span></span> <span data-ttu-id="7dc68-255">Hierdoor wordt voorkomen dat de toepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7dc68-255">This stops the application in Visual Studio.</span></span>

<span data-ttu-id="7dc68-256">U bent nu klaar voor de volgende stap is het publiceren van de toepassing in Azure en testen.</span><span class="sxs-lookup"><span data-stu-id="7dc68-256">You are now ready for the next step, which is to publish the application to Azure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-the-web-application-to-azure-and-test-it"></a><span data-ttu-id="7dc68-257">F.</span><span class="sxs-lookup"><span data-stu-id="7dc68-257">F.</span></span> <span data-ttu-id="7dc68-258">Publiceer de webtoepassing naar Azure en testen</span><span class="sxs-lookup"><span data-stu-id="7dc68-258">Publish the web application to Azure and test it</span></span>
<span data-ttu-id="7dc68-259">U hebt nu uw toepassing naar uw App Service-web-app publiceren en vervolgens testen om te zien hoe de hybride verbinding die u eerder hebt geconfigureerd voor uw web-app verbinding met de database op uw lokale computer wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7dc68-259">Now, you'll publish your application to your App Service web app and then test it to see how the hybrid connection you configured earlier is being used to connect your web app to the database on your local machine.</span></span>

### <a name="publish-the-web-application"></a><span data-ttu-id="7dc68-260">Publiceer de webtoepassing</span><span class="sxs-lookup"><span data-stu-id="7dc68-260">Publish the web application</span></span>
1. <span data-ttu-id="7dc68-261">U kunt uw publicatieprofiel voor de App Service-web-app in de Azure Portal kunt downloaden.</span><span class="sxs-lookup"><span data-stu-id="7dc68-261">You can download your publishing profile for the App Service web app in the Azure Portal.</span></span> <span data-ttu-id="7dc68-262">Klik op de blade voor uw web-app, **Get publicatieprofiel**, en sla het bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7dc68-262">On the blade for your web app, click **Get publish profile**, and then save the file to your computer.</span></span>
   
    ![Publicatieprofiel downloaden][PortalDownloadPublishProfile]
   
    <span data-ttu-id="7dc68-264">U gaat dit bestand vervolgens importeren in uw Visual Studio-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="7dc68-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="7dc68-265">In Visual Studio met de rechtermuisknop op de projectnaam in Solution Explorer en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-265">In Visual Studio, right-click the project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Selecteer publiceren][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="7dc68-267">In de **webpublicatie** dialoogvenster op de **profiel** Kies **importeren**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-267">In the **Publish Web** dialog, on the **Profile** tab, choose **Import**.</span></span>
   
    ![Importeren][HCVSPublishWebDialogImport]
4. <span data-ttu-id="7dc68-269">Blader naar uw gedownloade publicatieprofiel, selecteert u deze en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-269">Browse to your downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Blader naar profiel][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="7dc68-271">De publicatie-informatie is geïmporteerd en geeft weer op de **verbinding** tabblad van het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7dc68-271">Your publishing information is imported and displays on the **Connection** tab of the dialog.</span></span>
   
    ![Klik op publiceren][HCVSClickPublish]
   
    <span data-ttu-id="7dc68-273">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="7dc68-274">Wanneer publiceren is voltooid, wordt uw browser start en het weergeven van uw ASP.NET-toepassing nu bekend--, behalve dat nu is het live in de Azure-cloud!</span><span class="sxs-lookup"><span data-stu-id="7dc68-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in the Azure cloud!</span></span>

<span data-ttu-id="7dc68-275">Vervolgens gebruikt u uw live webtoepassing voor een overzicht van de hybride verbinding in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="7dc68-275">Next, you will use your live web application to see its Hybrid Connection in action.</span></span>

### <a name="test-the-completed-web-application-on-azure"></a><span data-ttu-id="7dc68-276">Testen van de voltooide webtoepassing op Azure</span><span class="sxs-lookup"><span data-stu-id="7dc68-276">Test the completed web application on Azure</span></span>
1. <span data-ttu-id="7dc68-277">Op de bovenste rechts van de webpagina op Azure, kies **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-277">On the top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Test aanmelden][HCTestLogIn]
2. <span data-ttu-id="7dc68-279">Uw App Service-web-app is nu verbonden met uw webtoepassing lidmaatschapsdatabase op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="7dc68-279">Your App Service web app is now connected to your web application's membership database on your local machine.</span></span> <span data-ttu-id="7dc68-280">U kunt dit controleren aanmelden met dezelfde referenties die u eerder in de lokale database hebt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="7dc68-280">To verify this, log in with the same credentials that you entered in the local database earlier.</span></span>
   
    ![Hallo begroeting][HCTestHelloContoso]
3. <span data-ttu-id="7dc68-282">Meld u af bij uw Azure-webtoepassing verder uw nieuwe hybride om verbinding te testen, en registreren als een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7dc68-282">To further test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="7dc68-283">Geef een nieuwe gebruikersnaam en wachtwoord en klik vervolgens op **registreren**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Test een andere gebruiker registreren][HCTestRegisterRelecloud]
4. <span data-ttu-id="7dc68-285">Om te bevestigen dat de referenties van de nieuwe gebruiker in uw lokale database via de hybride verbinding zijn opgeslagen, open SQL Management Studio op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="7dc68-285">To verify that the new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="7dc68-286">Vouw in Object Explorer het **MembershipDB** database uit en vouw vervolgens **tabellen**.</span><span class="sxs-lookup"><span data-stu-id="7dc68-286">In Object Explorer, expand the **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="7dc68-287">Met de rechtermuisknop op de **dbo. AspNetUsers** lidmaatschap tabel en kies **Selecteer Top 1000 rijen** om de resultaten weer te geven.</span><span class="sxs-lookup"><span data-stu-id="7dc68-287">Right-click the **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** to view the results.</span></span>
   
    ![De resultaten bekijken][HCTestSSMSTree]
5. <span data-ttu-id="7dc68-289">Uw lidmaatschap van lokale tabel toont nu beide accounts - het account waarmee u lokaal hebt gemaakt en die u hebt gemaakt in de Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="7dc68-289">Your local membership table now shows both accounts - the one that you created locally, and the one that you created in the Azure cloud.</span></span> <span data-ttu-id="7dc68-290">De versie die u hebt gemaakt in de cloud is opgeslagen in uw lokale-database via de Azure-functie voor hybride verbinding.</span><span class="sxs-lookup"><span data-stu-id="7dc68-290">The one that you created in the cloud has been saved to your on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Geregistreerde gebruikers in de lokale database.][HCTestShowMemberDb]

<span data-ttu-id="7dc68-292">U hebt nu gemaakt en geïmplementeerd ASP.NET-webtoepassing die gebruikmaakt van een hybride verbinding tussen een web-app in de Azure-cloud en een on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="7dc68-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in the Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="7dc68-293">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="7dc68-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="7dc68-294">Zie ook</span><span class="sxs-lookup"><span data-stu-id="7dc68-294">See Also</span></span>
[<span data-ttu-id="7dc68-295">Overzicht van hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="7dc68-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="7dc68-296">Josh Twist introduceert hybride verbindingen (Channel 9 video)</span><span class="sxs-lookup"><span data-stu-id="7dc68-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="7dc68-297">Overzicht van hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="7dc68-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="7dc68-298">BizTalk Services: De tabbladen Dashboard, bewaken, schaal, configureren en hybride verbinding</span><span class="sxs-lookup"><span data-stu-id="7dc68-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="7dc68-299">Het bouwen van een echte hybride Cloud met naadloze toepassing draagbaarheid (Channel 9 video)</span><span class="sxs-lookup"><span data-stu-id="7dc68-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="7dc68-300">Toegang tot on-premises resources met behulp van hybride verbindingen in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7dc68-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="7dc68-301">Identiteit van de ASP.NET-overzicht</span><span class="sxs-lookup"><span data-stu-id="7dc68-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

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
