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
# <a name="connect-to-on-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a>Verbinding maken met on-premises SQL-Server vanaf een web-app in Azure App Service met behulp van hybride verbindingen
Hybride verbindingen kunnen worden aangesloten [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps in de lokale bronnen die een statische TCP-poort gebruiken. Ondersteunde resources omvatten Microsoft SQL Server, MySQL, HTTP-Web-API's, App Service en de meeste aangepaste webservices.

In deze zelfstudie leert u het maken van een App Service-web-app in de [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715)de web-app verbinding met uw lokale lokale SQL Server-database met de nieuwe functie voor hybride verbinding, een eenvoudige ASP.NET-toepassing die de hybride verbinding gebruiken en de toepassing implementeren naar de App Service-web-app maken. De voltooide web-app in Azure worden gebruikersreferenties opgeslagen in een lidmaatschapsdatabase on-premises. De zelfstudie wordt ervan uitgegaan dat geen ervaring met behulp van Azure of ASP.NET.

> [!NOTE]
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> De Web-Apps-gedeelte van de functie hybride verbindingen is alleen beschikbaar in de [Azure Portal](https://portal.azure.com). Zie voor informatie over het maken van een verbinding in BizTalk Services [hybride verbindingen](http://go.microsoft.com/fwlink/p/?LinkID=397274).  
> 
> 

## <a name="prerequisites"></a>Vereisten
Voor deze zelfstudie hebt voltooid, moet u de volgende producten. Alle zijn beschikbaar in de beschikbare versies zodat u kunt beginnen met het ontwikkelen voor Azure volledig voor gratis.

* **Azure-abonnement** : voor een gratis abonnement, Zie [gratis proefversie van Azure](/pricing/free-trial/).
* **Visual Studio 2013** : als u wilt een gratis evaluatieversie van Visual Studio 2013 downloaden, Zie [Visual Studio-Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs). Installeer dit voordat u doorgaat.
* **Microsoft .NET Framework 3.5 servicepack 1** -als het besturingssysteem Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 of Windows Server 2008 R2 is, kunt u dit inschakelen in het Configuratiescherm > programma's en onderdelen > Windows-onderdelen in- of uitschakelen. Anders kunt u dit downloaden van de [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).
* **SQL Server 2014 Express met hulpprogramma's voor** -Microsoft SQL Server Express gratis downloaden op de [pagina Microsoft Web Platform Database](http://www.microsoft.com/web/platform/database.aspx). Kies de **Express** (geen LocalDB) versie. De **Express met hulpprogramma's voor** versie SQL Server Management Studio, gaat u in deze zelfstudie bevat.
* **SQL Server Management Studio Express** - dat deel uitmaakt van de SQL Server 2014 Express met hulpprogramma's downloaden hierboven vermeld, maar als u moet afzonderlijk te installeren, kunt u downloaden en installeren via de [downloadpagina voor SQL Server Express](http://www.microsoft.com/web/platform/database.aspx).

De zelfstudie wordt ervan uitgegaan dat u een Azure-abonnement hebt dat u Visual Studio 2013 hebt geïnstalleerd en u hebt geïnstalleerd of .NET Framework 3.5 ingeschakeld. De zelfstudie laat zien hoe u SQL Server 2014 Express installeren in een configuratie die goed samen met de functie Azure hybride verbindingen (een standaardexemplaar met een statische TCP-poort werkt). Voordat u de zelfstudie begint, download SQL Server 2014 Express met hulpprogramma's van de locatie die hierboven worden genoemd als u geen SQL Server geïnstalleerd.

### <a name="notes"></a>Opmerkingen
Als u wilt een on-premises SQL Server of SQL Server Express-database met een hybride verbinding gebruiken, moet TCP/IP moet zijn ingeschakeld op een statische poort. Standaardexemplaren op SQL Server gebruiken statische poort 1433, dat niet het benoemde exemplaren.

De computer waarop u de hybride Verbindingsbeheer lokale agent installeert:

* Moet uitgaande verbinding met Azure via:

| Poort | Waarom |
| --- | --- |
| 80 |**Vereist** voor HTTP-poort voor de validatie van het servercertificaat en eventueel voor toegang tot gegevens. |
| 443 |**Optionele** voor toegang tot gegevens. Als uitgaande verbinding met 443 niet beschikbaar is, wordt de TCP-poort 80 gebruikt. |
| 5671 en 9352 |**Aanbevolen** maar optioneel voor toegang tot gegevens. Houd er rekening mee dat deze modus levert meestal hogere doorvoer. Als u uitgaande verbindingen via deze poorten niet beschikbaar is, wordt de TCP-poort 443 gebruikt. |

* Moet kunnen bereiken de *hostnaam*:*portnumber* van uw lokale resource.

De stappen in dit artikel wordt ervan uitgegaan dat u gebruikmaakt van de browser van de computer die als host voor de lokale-agent voor hybride verbinding fungeert.

Als u al SQL Server geïnstalleerd in een configuratie en in een omgeving die voldoet aan de voorwaarden die hebt hierboven worden beschreven, kunt u overslaan en beginnen met [maken van een SQL Server-database op de lokale](#CreateSQLDB).

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a>A. SQL Server Express installeren en maken van een SQL Server-database op de lokale TCP/IP inschakelen
Deze sectie wordt beschreven hoe u SQL Server Express installeren en een database maken, zodat uw webtoepassing met de Azure Portal werken zullen TCP/IP inschakelen.

### <a name="install-sql-server-express"></a>SQL Server Express installeren
1. U installeert SQL Server Express door de **SQLEXPRWT_x64_ENU.exe** of **SQLEXPR_x86_ENU.exe** -bestand dat u hebt gedownload. Het Installatiecentrum van SQL Server-wizard wordt weergegeven.
   
    ![Installatie van SQL Server][SQLServerInstall]
2. Kies **zelfstandige installatie van nieuwe SQL-Server of functies toevoegen aan een bestaande installatie**. Volg de instructies, accepteert de standaardwaarden en -instellingen, totdat u de **Exemplaarconfiguratie** pagina.
3. Op de **Exemplaarconfiguratie** pagina **standaardexemplaar**.
   
    ![Kies standaardexemplaar][ChooseDefaultInstance]
   
    Standaard luistert het standaardexemplaar van SQL Server voor aanvragen van SQL Server-clients op statische poort 1433, dit is wat de functie hybride verbindingen is vereist. Benoemde exemplaren dynamische poorten en UDP, die niet worden ondersteund door hybride verbindingen gebruiken.
4. Accepteer de standaardinstellingen op de **serverconfiguratie** pagina.
5. Op de **Database Engine-configuratie** pagina onder **verificatiemodus**, kies **gemengde modus (SQL Server-verificatie en Windows-verificatie)**, en een wachtwoord opgeven.
   
    ![Kies in de gemengde modus][ChooseMixedMode]
   
    In deze zelfstudie wordt u SQL Server-verificatie. Zorg ervoor dat het wachtwoord dat u opgeeft, onthoud omdat u deze later hebt.
6. Doorloop de rest van de wizard om de installatie te voltooien.

### <a name="enable-tcpip"></a>TCP/IP inschakelen
Om TCP/IP, gebruikt u SQL Server Configuration Manager, die tijdens de installatie van SQL Server Express is geïnstalleerd. Volg de stappen in [TCP/IP-netwerkprotocol inschakelen voor SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) voordat u doorgaat.

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a>Lokale voor een SQL Server-database maken
Uw Visual Studio-webtoepassing vereist een lidmaatschapsdatabase die toegankelijk zijn voor Azure. Hiervoor moet een SQL Server of SQL Server Express-database (niet de LocalDB-database die de MVC-sjabloon standaard gebruikt), zodat u de lidmaatschapsdatabase naast gaat maken.

1. In SQL Server Management Studio verbinding met de SQL-Server die u zojuist hebt geïnstalleerd. (Als de **verbinding maken met Server** dialoogvenster niet automatisch wordt weergegeven, gaat u naar **Objectverkenner** in het linkerdeelvenster klikt u op **Connect**, en klik vervolgens op **Database-Engine**.) ![Verbinding maken met Server][SSMSConnectToServer]
   
    Voor **servertype**, kies **Database-Engine**. Voor **servernaam**, kunt u **localhost** of de naam van de computer die u gebruikt. Kies **SQL Server-verificatie**, en meld u aan met de sa-gebruikersnaam en het wachtwoord dat u eerder hebt gemaakt.
2. Als u wilt een nieuwe database maken met behulp van SQL Server Management Studio, met de rechtermuisknop op **Databases** in Object Explorer en klik vervolgens op **nieuwe Database**.
   
    ![Nieuwe database maken][SSMScreateNewDB]
3. In de **nieuwe Database** dialoogvenster MembershipDB invoeren voor de naam van de database en klik vervolgens op **OK**.
   
    ![Databasenaam opgeven][SSMSprovideDBname]
   
    Houd er rekening mee dat u niet geen wijzigingen in de database op dit moment aanbrengen bent. De lidmaatschapsgegevens wordt later automatisch door uw webtoepassing toegevoegd wanneer u het uitvoert.
4. In Object Explorer, als u wilt uitbreiden **Databases**, ziet u dat de lidmaatschapsdatabase is gemaakt.
   
    ![MembershipDB gemaakt][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-the-azure-portal"></a>B. Een web-app maken in de Azure-Portal
> [!NOTE]
> Als u al een web-app in de Azure-Portal die u wilt gebruiken voor deze zelfstudie hebt gemaakt, kunt u verder gaan naar [een hybride verbinding en een BizTalk Service maken](#CreateHC) en van daaruit worden voortgezet.
> 
> 

1. In de [Azure Portal](https://portal.azure.com), klikt u op **nieuw** > **Web en mobiel** > **Web-app**.
   
    ![Knop Nieuw][New]
2. Configureren van uw web-app en klik vervolgens op **maken**.
   
    ![Websitenaam][WebsiteCreationBlade]
3. Na enkele ogenblikken de web-app wordt gemaakt en de blade web-app wordt weergegeven. De blade is een verticaal schuifbare dashboard waarmee u uw web-app beheren.
   
    ![Website worden uitgevoerd][WebSiteRunningBlade]
   
    Om te controleren of de web-app live, klikt u op de **Bladeren** pictogram om de standaardpagina weer te geven.

Vervolgens maakt u een hybride verbinding en een BizTalk service voor de web-app.

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a>C. Een hybride verbinding en een BizTalk Service maken
1. Terug in de Portal, gaat u naar instellingen en klik op **Networking** > **uw hybride-verbindingseindpunten configureren**.
   
    ![Hybride verbindingen][CreateHCHCIcon]
2. Klik op de blade hybride verbindingen **toevoegen** > **nieuwe hybride verbinding**.
3. Op de **hybride verbinding maken** blade:
   
   * Voor **naam**, Geef een naam op voor de verbinding.
   * Voor **hostnaam**, voer de computernaam van uw SQL Server-hostcomputer.
   * Voor **poort**, voer 1433 (de standaardpoort voor SQL Server).
   * Klik op **BizTalk Service** > **nieuwe BizTalk Service** en voer een naam voor de BizTalk service.
     
     ![Een hybride verbinding maken][TwinCreateHCBlades]
4. Klik op **OK** twee keer.
   
    Wanneer het proces is voltooid, de **meldingen** gebied knippert een groene **geslaagd** en de **hybride verbinding** blade ziet de nieuwe hybride verbinding met de status als **niet verbonden**.
   
    ![Een hybride verbinding is gemaakt][CreateHCOneConnectionCreated]

U hebt op dit moment een belangrijk onderdeel van de cloudinfrastructuur voor hybride verbinding voltooid. Vervolgens maakt u een bijbehorende lokale apparaat.

<a name="InstallHCM"></a>

## <a name="d-install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a>D. Installeren van de lokale hybride Verbindingsbeheer om de verbinding te voltooien
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

Nu dat de infrastructuur van hybride verbinding voltooid is, maakt u een webtoepassing die wordt gebruikt.

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-the-database-connection-string-and-run-the-project-locally"></a>E. Een eenvoudige ASP.NET-webproject maakt, de verbindingsreeks voor de database en het project lokaal uitvoeren
### <a name="create-a-basic-aspnet-project"></a>Een eenvoudige ASP.NET-project maken
1. In Visual Studio op de **bestand** menu, een nieuw Project maken:
   
    ![Nieuw Visual Studio-project][HCVSNewProject]
2. In de **sjablonen** sectie van de **nieuw Project** dialoogvenster Selecteer **Web** en kies **ASP.NET-webtoepassing**, en klik vervolgens op **OK**.
   
    ![Kies ASP.NET-webtoepassing][HCVSChooseASPNET]
3. In de **nieuw ASP.NET-Project** dialoogvenster kiezen **MVC**, en klik vervolgens op **OK**.
   
    ![Kies MVC][HCVSChooseMVC]
4. Wanneer het project is gemaakt, wordt de pagina met toepassingen Leesmij-bestand weergegeven. Het webproject niet nog uitgevoerd.
   
    ![Pagina met Leesmij-bestand][HCVSReadmePage]

### <a name="edit-the-database-connection-string-for-the-application"></a>De database-verbindingsreeks voor de toepassing bewerken
In deze stap maakt bewerken u de verbindingsreeks waarin wordt gemeld dat uw toepassing waar vind ik de lokale SQL Server Express-database. De verbindingsreeks is in de toepassing Web.config-bestand configuratiegegevens voor de toepassing bevat.

> [!NOTE]
> Om ervoor te zorgen dat uw toepassing gebruikmaakt van de database die u hebt gemaakt in SQL Server Express en niet het in Visual Studio standaard LocalDB, is het belangrijk dat u deze stap hebt voltooid voordat het project wordt uitgevoerd.
> 
> 

1. Dubbelklik in Solution Explorer op het bestand Web.config.
   
    ![Web.config][HCVSChooseWebConfig]
2. Bewerk de **connectionStrings** sectie om te verwijzen naar de SQL Server-database op uw lokale computer, de syntaxis in het volgende voorbeeld:
   
    ![Verbindingsreeks][HCVSConnectionString]
   
    Houd bij het samenstellen van de verbindingsreeks rekening met het volgende:
   
   * Als u verbinding maakt met een benoemd exemplaar in plaats van een standaardexemplaar (bijvoorbeeld YourServer\SQLEXPRESS), moet u uw SQL Server voor het gebruik van statische poorten configureren. Zie voor meer informatie over het configureren van statische poorten [het configureren van SQL Server om te luisteren op een specifieke poort](http://support.microsoft.com/kb/823938). Standaard gebruiken benoemde exemplaren UDP en dynamische poorten die worden niet ondersteund door hybride verbindingen.
   * Het is raadzaam dat u de poort opgeeft (1433 standaard, zoals wordt weergegeven in het voorbeeld) op de verbindingsreeks zodat u kunt er zeker van dat de lokale SQL-Server heeft TCP ingeschakeld en de juiste poort wordt gebruikt.
   * Vergeet niet SQL Server-verificatie gebruiken om verbinding te maken voor het opgeven van de gebruikers-ID en het wachtwoord in de verbindingsreeks.
3. Klik op **opslaan** in Visual Studio het Web.config-bestand wilt opslaan.

### <a name="run-the-project-locally-and-register-a-new-user"></a>Het project lokaal uitvoeren en een nieuwe gebruiker registreren
1. Nu uw nieuwe webproject lokaal uitvoeren door te klikken op de bladerknop onder foutopsporing. In dit voorbeeld gebruikt Internet Explorer.
   
    ![Project uitvoeren][HCVSRunProject]
2. Kies op de rechterbovenhoek van de standaardwebpagina **registreren** registreren van een nieuw account:
   
    ![Registreer een nieuwe account][HCVSRegisterLocally]
3. Voer een gebruikersnaam en wachtwoord:
   
    ![Voer de gebruikersnaam en wachtwoord][HCVSCreateNewAccount]
   
    Dit maakt automatisch een database op de lokale SQL Server die de lidmaatschapsgegevens voor uw toepassing bevat. Een van de tabellen (**dbo. AspNetUsers**) blokkeringen web-app gebruikersreferenties zoals de waarden die u zojuist hebt ingevoerd. Verderop in de zelfstudie ziet u deze tabel.
4. Sluit het browservenster van de standaard-webpagina. Hierdoor wordt voorkomen dat de toepassing in Visual Studio.

U bent nu klaar voor de volgende stap is het publiceren van de toepassing in Azure en testen.

<a name="PubNTest"></a>

## <a name="f-publish-the-web-application-to-azure-and-test-it"></a>F. Publiceer de webtoepassing naar Azure en testen
U hebt nu uw toepassing naar uw App Service-web-app publiceren en vervolgens testen om te zien hoe de hybride verbinding die u eerder hebt geconfigureerd voor uw web-app verbinding met de database op uw lokale computer wordt gebruikt.

### <a name="publish-the-web-application"></a>Publiceer de webtoepassing
1. U kunt uw publicatieprofiel voor de App Service-web-app in de Azure Portal kunt downloaden. Klik op de blade voor uw web-app, **Get publicatieprofiel**, en sla het bestand op uw computer.
   
    ![Publicatieprofiel downloaden][PortalDownloadPublishProfile]
   
    U gaat dit bestand vervolgens importeren in uw Visual Studio-webtoepassing.
2. In Visual Studio met de rechtermuisknop op de projectnaam in Solution Explorer en selecteer **publiceren**.
   
    ![Selecteer publiceren][HCVSRightClickProjectSelectPublish]
3. In de **webpublicatie** dialoogvenster op de **profiel** Kies **importeren**.
   
    ![Importeren][HCVSPublishWebDialogImport]
4. Blader naar uw gedownloade publicatieprofiel, selecteert u deze en klik vervolgens op **OK**.
   
    ![Blader naar profiel][HCVSBrowseToImportPubProfile]
5. De publicatie-informatie is geïmporteerd en geeft weer op de **verbinding** tabblad van het dialoogvenster.
   
    ![Klik op publiceren][HCVSClickPublish]
   
    Klik op **Publish**.
   
    Wanneer publiceren is voltooid, wordt uw browser start en het weergeven van uw ASP.NET-toepassing nu bekend--, behalve dat nu is het live in de Azure-cloud!

Vervolgens gebruikt u uw live webtoepassing voor een overzicht van de hybride verbinding in te grijpen.

### <a name="test-the-completed-web-application-on-azure"></a>Testen van de voltooide webtoepassing op Azure
1. Op de bovenste rechts van de webpagina op Azure, kies **aanmelden**.
   
    ![Test aanmelden][HCTestLogIn]
2. Uw App Service-web-app is nu verbonden met uw webtoepassing lidmaatschapsdatabase op uw lokale machine. U kunt dit controleren aanmelden met dezelfde referenties die u eerder in de lokale database hebt ingevoerd.
   
    ![Hallo begroeting][HCTestHelloContoso]
3. Meld u af bij uw Azure-webtoepassing verder uw nieuwe hybride om verbinding te testen, en registreren als een andere gebruiker. Geef een nieuwe gebruikersnaam en wachtwoord en klik vervolgens op **registreren**.
   
    ![Test een andere gebruiker registreren][HCTestRegisterRelecloud]
4. Om te bevestigen dat de referenties van de nieuwe gebruiker in uw lokale database via de hybride verbinding zijn opgeslagen, open SQL Management Studio op uw lokale computer. Vouw in Object Explorer het **MembershipDB** database uit en vouw vervolgens **tabellen**. Met de rechtermuisknop op de **dbo. AspNetUsers** lidmaatschap tabel en kies **Selecteer Top 1000 rijen** om de resultaten weer te geven.
   
    ![De resultaten bekijken][HCTestSSMSTree]
5. Uw lidmaatschap van lokale tabel toont nu beide accounts - het account waarmee u lokaal hebt gemaakt en die u hebt gemaakt in de Azure-cloud. De versie die u hebt gemaakt in de cloud is opgeslagen in uw lokale-database via de Azure-functie voor hybride verbinding.
   
    ![Geregistreerde gebruikers in de lokale database.][HCTestShowMemberDb]

U hebt nu gemaakt en geïmplementeerd ASP.NET-webtoepassing die gebruikmaakt van een hybride verbinding tussen een web-app in de Azure-cloud en een on-premises SQL Server database. Gefeliciteerd.

## <a name="see-also"></a>Zie ook
[Overzicht van hybride verbindingen](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Josh Twist introduceert hybride verbindingen (Channel 9 video)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Overzicht van hybride verbindingen](/services/biztalk-services/)

[BizTalk Services: De tabbladen Dashboard, bewaken, schaal, configureren en hybride verbinding](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Het bouwen van een echte hybride Cloud met naadloze toepassing draagbaarheid (Channel 9 video)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Toegang tot on-premises resources met behulp van hybride verbindingen in Azure App Service](web-sites-hybrid-connection-get-started.md)

[Identiteit van de ASP.NET-overzicht](http://www.asp.net/identity)

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
