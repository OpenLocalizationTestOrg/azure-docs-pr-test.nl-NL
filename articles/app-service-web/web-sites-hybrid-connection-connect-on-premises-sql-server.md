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
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a>Verbinding maken met tooon lokale SQL Server vanuit een web-app in Azure App Service met behulp van hybride verbindingen
Hybride verbindingen kunnen worden aangesloten [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web-Apps tooon lokale bronnen die gebruikmaken van een statische TCP-poort. Ondersteunde resources omvatten Microsoft SQL Server, MySQL, HTTP-Web-API's, App Service en de meeste aangepaste webservices.

In deze zelfstudie leert u hoe toocreate een App Service web-app in Hallo [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715)Hallo web app tooyour lokale lokale SQL Server-database met behulp van de nieuwe functie voor hybride verbinding Hallo verbinding, een eenvoudige ASP.NET maken de toepassing die Hallo hybride verbinding gebruiken en Hallo toepassing toohello App Service-web-app implementeren. Hallo voltooid web-app in Azure worden gebruikersreferenties opgeslagen in een lidmaatschapsdatabase on-premises. Hallo-zelfstudie wordt ervan uitgegaan dat geen ervaring met behulp van Azure of ASP.NET.

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> Hallo-Web-Apps-gedeelte van Hallo hybride verbindingen onderdeel is alleen beschikbaar in Hallo [Azure Portal](https://portal.azure.com). Zie voor een verbinding in BizTalk Services toocreate [hybride verbindingen](http://go.microsoft.com/fwlink/p/?LinkID=397274).  
> 
> 

## <a name="prerequisites"></a>Vereisten
toocomplete in deze zelfstudie, moet u Hallo producten te volgen. Alle zijn beschikbaar in de beschikbare versies zodat u kunt beginnen met het ontwikkelen voor Azure volledig voor gratis.

* **Azure-abonnement** : voor een gratis abonnement, Zie [gratis proefversie van Azure](/pricing/free-trial/).
* **Visual Studio 2013** -toodownload een gratis evaluatieversie van Visual Studio 2013, Zie [Visual Studio-Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs). Installeer dit voordat u doorgaat.
* **Microsoft .NET Framework 3.5 servicepack 1** -als het besturingssysteem Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 of Windows Server 2008 R2 is, kunt u dit inschakelen in het Configuratiescherm > programma's en onderdelen > Windows-onderdelen in- of uitschakelen. Anders, u kunt dit downloaden van Hallo [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).
* **SQL Server 2014 Express met hulpprogramma's voor** -Microsoft SQL Server Express gratis downloaden op Hallo [pagina Microsoft Web Platform Database](http://www.microsoft.com/web/platform/database.aspx). Kies Hallo **Express** (geen LocalDB) versie. Hallo **Express met hulpprogramma's voor** versie SQL Server Management Studio, gaat u in deze zelfstudie bevat.
* **SQL Server Management Studio Express** - dat deel uitmaakt van de SQL Server 2014 Express Hallo met hulpprogramma's downloaden hierboven vermeld, maar als u tooinstall moet deze afzonderlijk, u kunt downloaden en installeren vanaf Hallo [SQL Server Express downloadpagina](http://www.microsoft.com/web/platform/database.aspx).

Hallo-zelfstudie wordt ervan uitgegaan dat u een Azure-abonnement hebt dat u Visual Studio 2013 hebt geïnstalleerd en u hebt geïnstalleerd of .NET Framework 3.5 ingeschakeld. Hallo-zelfstudie laat zien hoe tooinstall SQL Server 2014 Express in een configuratie die goed samen met hello Azure hybride verbindingen werkt functie (een standaardexemplaar met een statische TCP-poort). Voordat u begint Hallo zelfstudie, download SQL Server 2014 Express met hulpprogramma's van Hallo locatie hierboven worden genoemd als u geen SQL Server geïnstalleerd.

### <a name="notes"></a>Opmerkingen
toouse een lokale SQL Server of SQL Server Express-database met een hybride verbinding, moet TCP/IP toobe ingeschakeld op een statische poort. Standaardexemplaren op SQL Server gebruiken statische poort 1433, dat niet het benoemde exemplaren.

Hallo-computer waarop u Hallo op premises hybride Verbindingsbeheer agent installeert:

* Moet uitgaande verbinding tooAzure hebben via:

| Poort | Waarom |
| --- | --- |
| 80 |**Vereist** voor HTTP-poort voor de validatie van het servercertificaat en eventueel voor toegang tot gegevens. |
| 443 |**Optionele** voor toegang tot gegevens. Als uitgaande verbinding too443 niet beschikbaar is, wordt de TCP-poort 80 gebruikt. |
| 5671 en 9352 |**Aanbevolen** maar optioneel voor toegang tot gegevens. Houd er rekening mee dat deze modus levert meestal hogere doorvoer. Als u uitgaande connectiviteit toothese poorten niet beschikbaar is, wordt de TCP-poort 443 gebruikt. |

* Moet kunnen tooreach hello *hostnaam*:*portnumber* van uw lokale resource.

Hallo stappen in dit artikel wordt ervan uitgegaan dat u gebruikmaakt van Hallo Hallo-computer die als voor agent voor hybride verbinding voor Hallo lokale host fungeert browser.

Als u al SQL Server geïnstalleerd in een configuratie en in een omgeving die voldoet aan Hallo voorwaarden die hebt hierboven worden beschreven, kunt u overslaan en beginnen met [maken van een SQL Server-database op de lokale](#CreateSQLDB).

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a>A. SQL Server Express installeren en maken van een SQL Server-database op de lokale TCP/IP inschakelen
Deze sectie leest u hoe tooinstall SQL Server Express TCP/IP inschakelen en een database maken, zodat uw webtoepassing werkt met hello Azure-Portal.

### <a name="install-sql-server-express"></a>SQL Server Express installeren
1. tooinstall SQL Server Express uitvoeren Hallo **SQLEXPRWT_x64_ENU.exe** of **SQLEXPR_x86_ENU.exe** -bestand dat u hebt gedownload. Hallo Installatiecentrum van SQL Server-wizard wordt weergegeven.
   
    ![Installatie van SQL Server][SQLServerInstall]
2. Kies **zelfstandige installatie van nieuwe SQL-Server of bestaande installatie van functies tooan toevoegen**. Volg de aanwijzingen Hallo en accepteren Hallo standaardkeuzes en -instellingen, totdat u toohello **Exemplaarconfiguratie** pagina.
3. Op Hallo **Exemplaarconfiguratie** pagina **standaardexemplaar**.
   
    ![Kies standaardexemplaar][ChooseDefaultInstance]
   
    Standaard luistert Hallo-standaardexemplaar van SQL Server voor aanvragen van SQL Server-clients op statische poort 1433, is welke Hallo hybride verbindingen functie is vereist. Benoemde exemplaren dynamische poorten en UDP, die niet worden ondersteund door hybride verbindingen gebruiken.
4. Accepteer de standaardwaarden Hallo op Hallo **serverconfiguratie** pagina.
5. Op Hallo **Database Engine-configuratie** pagina onder **verificatiemodus**, kies **gemengde modus (SQL Server-verificatie en Windows-verificatie)**, en geef een wachtwoord.
   
    ![Kies in de gemengde modus][ChooseMixedMode]
   
    In deze zelfstudie wordt u SQL Server-verificatie. Worden ervoor tooremember Hallo wachtwoord dat u hebt opgegeven, omdat u deze later hebt.
6. Doorloop rest Hallo van Hallo wizard toocomplete Hallo-installatie.

### <a name="enable-tcpip"></a>TCP/IP inschakelen
tooenable TCP/IP, gebruikt u SQL Server Configuration Manager, die tijdens de installatie van SQL Server Express is geïnstalleerd. Volg de stappen Hallo in [TCP/IP-netwerkprotocol inschakelen voor SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) voordat u doorgaat.

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a>Lokale voor een SQL Server-database maken
Uw Visual Studio-webtoepassing vereist een lidmaatschapsdatabase die toegankelijk zijn voor Azure. Hiervoor moet een SQL Server of SQL Server Express-database (geen Hallo LocalDB-database die Hallo MVC-sjabloon gebruikt standaard), zodat u Hallo lidmaatschapsdatabase naast maken.

1. In SQL Server Management Studio verbinding met toohello SQL-Server die u zojuist hebt geïnstalleerd. (Als hello **verbinding tooServer** dialoogvenster niet automatisch wordt weergegeven, te navigeren**Objectverkenner** in het linkerdeelvenster hello, klikt u op **Connect**, en klik vervolgens op **Database-Engine**.) ![Verbinding maken met tooServer][SSMSConnectToServer]
   
    Voor **servertype**, kies **Database-Engine**. Voor **servernaam**, kunt u **localhost** of Hallo-naam van Hallo-computer die u gebruikt. Kies **SQL Server-verificatie**, en meld u met Hallo sa-gebruikersnaam en wachtwoord op Hallo die u eerder hebt gemaakt.
2. een nieuwe database met behulp van SQL Server Management Studio toocreate met de rechtermuisknop op **Databases** in Object Explorer en klik vervolgens op **nieuwe Database**.
   
    ![Nieuwe database maken][SSMScreateNewDB]
3. In Hallo **nieuwe Database** dialoogvenster MembershipDB voor Hallo databasenaam invoeren en klik vervolgens op **OK**.
   
    ![Databasenaam opgeven][SSMSprovideDBname]
   
    Houd er rekening mee dat u Maak niet alle wijzigingen toohello databases op dit moment. Hallo lidmaatschapsgegevens wordt later automatisch door uw webtoepassing toegevoegd wanneer u het uitvoert.
4. In Object Explorer, als u wilt uitbreiden **Databases**, ziet u dat Hallo lidmaatschap van de database is gemaakt.
   
    ![MembershipDB gemaakt][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a>B. Een web-app maken in hello Azure Portal
> [!NOTE]
> Als u al een web-app in hello Azure-Portal wilt u toouse voor deze zelfstudie hebt gemaakt, kunt u verder gaan te[een hybride verbinding en een BizTalk Service maken](#CreateHC) en van daaruit worden voortgezet.
> 
> 

1. In Hallo [Azure Portal](https://portal.azure.com), klikt u op **nieuw** > **Web en mobiel** > **Web-app**.
   
    ![Knop Nieuw][New]
2. Configureren van uw web-app en klik vervolgens op **maken**.
   
    ![Websitenaam][WebsiteCreationBlade]
3. Na enkele ogenblikken Hallo web-app wordt gemaakt en de blade web-app wordt weergegeven. Hallo-blade is een verticaal schuifbare dashboard waarmee u uw web-app beheren.
   
    ![Website worden uitgevoerd][WebSiteRunningBlade]
   
    tooverify hello web-app live is, kunt u Hallo op **Bladeren** pictogram toodisplay Hallo standaardpagina.

Vervolgens maakt u een hybride verbinding en een BizTalk service voor Hallo web-app.

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a>C. Een hybride verbinding en een BizTalk Service maken
1. Terug in Hallo Portal, Ga toosettings en klik op **Networking** > **uw hybride-verbindingseindpunten configureren**.
   
    ![Hybride verbindingen][CreateHCHCIcon]
2. Klik op Hallo hybride verbindingen blade **toevoegen** > **nieuwe hybride verbinding**.
3. Op Hallo **hybride verbinding maken** blade:
   
   * Voor **naam**, Geef een naam voor het Hallo-verbinding.
   * Voor **hostnaam**, voer de computernaam Hallo van uw SQL Server-hostcomputer.
   * Voor **poort**, voer 1433 (Hallo-standaardpoort voor SQL Server).
   * Klik op **BizTalk Service** > **nieuwe BizTalk Service** en voer een naam voor Hallo BizTalk service.
     
     ![Een hybride verbinding maken][TwinCreateHCBlades]
4. Klik op **OK** twee keer.
   
    Wanneer Hallo-proces is voltooid, hello **meldingen** gebied knippert een groene **geslaagd** en Hallo **hybride verbinding** blade nieuwe hybride verbinding met hello wordt weergegeven Hallo status als **niet verbonden**.
   
    ![Een hybride verbinding is gemaakt][CreateHCOneConnectionCreated]

U hebt op dit moment een belangrijk onderdeel van hybride Hallo-verbinding cloudinfrastructuur voltooid. Vervolgens maakt u een bijbehorende lokale apparaat.

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>D. Hallo op premises hybride Verbindingsbeheer toocomplete Hallo verbinding installeren
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

Nu die infrastructuur Hallo hybride verbinding voltooid is, maakt u een webtoepassing die wordt gebruikt.

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a>E. Een eenvoudige ASP.NET-webproject maakt, Hallo databaseverbindingsreeks bewerken en Hallo-project lokaal uitvoeren
### <a name="create-a-basic-aspnet-project"></a>Een eenvoudige ASP.NET-project maken
1. In Visual Studio op Hallo **bestand** menu, een nieuw Project maken:
   
    ![Nieuw Visual Studio-project][HCVSNewProject]
2. In Hallo **sjablonen** sectie Hallo **nieuw Project** dialoogvenster Selecteer **Web** en kies **ASP.NET-webtoepassing**, en klik vervolgens op  **OK**.
   
    ![Kies ASP.NET-webtoepassing][HCVSChooseASPNET]
3. In Hallo **nieuw ASP.NET-Project** dialoogvenster kiezen **MVC**, en klik vervolgens op **OK**.
   
    ![Kies MVC][HCVSChooseMVC]
4. Als het Hallo-project is gemaakt, weergegeven Hallo toepassing Leesmij pagina. Hallo-webproject niet nog uitgevoerd.
   
    ![Pagina met Leesmij-bestand][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a>Hallo-database-verbindingsreeks voor de toepassing hello bewerken
In deze stap bewerkt u Hallo verbindingsreeks waarin wordt gemeld uw toepassing dat waar toofind uw lokale SQL Server Express database. Hallo-verbindingsreeks is in van de toepassing hello Web.config-bestand configuratiegegevens voor de toepassing hello bevat.

> [!NOTE]
> tooensure die uw toepassing hello-database die u hebt gemaakt in SQL Server Express en niet Hallo een in Visual Studio standaard LocalDB gebruikt, is het belangrijk dat u deze stap hebt voltooid voordat het project wordt uitgevoerd.
> 
> 

1. Dubbelklik in Solution Explorer op Hallo Web.config-bestand.
   
    ![Web.config][HCVSChooseWebConfig]
2. Hallo bewerken **connectionStrings** toopoint toohello SQL Server-database op uw lokale computer, Hallo syntaxis in Hallo voorbeeld van de volgende sectie:
   
    ![Verbindingsreeks][HCVSConnectionString]
   
    Houd er rekening mee Hallo volgende bij samenstellen van de verbindingsreeks Hallo:
   
   * Als u verbinding maakt tooa benoemd exemplaar in plaats van een standaardexemplaar (bijvoorbeeld YourServer\SQLEXPRESS), moet u uw SQL Server-toouse statische poorten configureren. Zie voor meer informatie over het configureren van statische poorten [hoe tooconfigure SQL Server toolisten op een specifieke poort](http://support.microsoft.com/kb/823938). Standaard gebruiken benoemde exemplaren UDP en dynamische poorten die worden niet ondersteund door hybride verbindingen.
   * Het verdient aanbeveling dat u Hallo opgeeft poort (1433 standaard, zoals weergegeven in het voorbeeld Hallo) op Hallo verbindingsreeks zodat u ervoor dat uw lokale SQL Server TCP ingeschakeld is en de juiste poort Hallo wordt gebruikt.
   * Houd er rekening mee toouse SQL Server-verificatie tooconnect, Hallo-gebruikersnaam en wachtwoord opgeven in de verbindingsreeks.
3. Klik op **opslaan** in Visual Studio toosave Hallo Web.config-bestand.

### <a name="run-hello-project-locally-and-register-a-new-user"></a>Hallo-project lokaal uitvoeren en een nieuwe gebruiker registreren
1. Nu uw nieuwe webproject lokaal uitvoeren door te klikken op de knop Bladeren Hallo onder foutopsporing. In dit voorbeeld gebruikt Internet Explorer.
   
    ![Project uitvoeren][HCVSRunProject]
2. Kies op Hallo rechtsboven standaardwebpagina hello, **registreren** tooregister een nieuw account:
   
    ![Registreer een nieuwe account][HCVSRegisterLocally]
3. Voer een gebruikersnaam en wachtwoord:
   
    ![Voer de gebruikersnaam en wachtwoord][HCVSCreateNewAccount]
   
    Dit maakt automatisch een database op de lokale SQL Server die de lidmaatschapsgegevens Hallo voor uw toepassing bevat. Een van de tabellen hello (**dbo. AspNetUsers**) blokkeringen web-app gebruikersreferenties zoals Hallo die u zojuist hebt ingevoerd. Deze tabel ziet u later in de zelfstudie Hallo.
4. Sluit het browservenster Hallo met standaardwebpagina Hallo. Hierdoor wordt voorkomen dat de toepassing hello in Visual Studio.

U bent nu klaar voor de volgende stap hello, namelijk toopublish Hallo toepassing tooAzure en testen.

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a>F. Hallo web application tooAzure publiceren en testen
Nu u uw toepassing tooyour App Service-web-app publiceren en test deze toosee hoe Hallo hybride verbinding die u eerder hebt geconfigureerd is gebruikte tooconnect wordt uw web-app toohello database op uw lokale machine.

### <a name="publish-hello-web-application"></a>Publiceer de webtoepassing Hallo
1. U kunt uw publicatieprofiel voor App Service-web-app in Azure Portal Hallo Hallo downloaden. Klik op de blade voor uw web-app Hallo **Get publicatieprofiel**, en sla Hallo bestand tooyour computer.
   
    ![Publicatieprofiel downloaden][PortalDownloadPublishProfile]
   
    U gaat dit bestand vervolgens importeren in uw Visual Studio-webtoepassing.
2. In Visual Studio met de rechtermuisknop op Hallo projectnaam in Solution Explorer en selecteer **publiceren**.
   
    ![Selecteer publiceren][HCVSRightClickProjectSelectPublish]
3. In Hallo **webpublicatie** dialoogvenster op Hallo **profiel** Kies **importeren**.
   
    ![Importeren][HCVSPublishWebDialogImport]
4. Bladeren tooyour publicatieprofiel gedownload, selecteert u deze en klik vervolgens op **OK**.
   
    ![Tooprofile bladeren][HCVSBrowseToImportPubProfile]
5. De publicatie-informatie is geïmporteerd en geeft weer op Hallo **verbinding** tabblad van Hallo dialoogvenster.
   
    ![Klik op publiceren][HCVSClickPublish]
   
    Klik op **Publish**.
   
    Wanneer publiceren is voltooid, wordt uw browser start en het weergeven van uw ASP.NET-toepassing nu bekend--, behalve dat nu is het live in Azure-cloud Hallo!

Vervolgens wordt u uw live web application toosee de hybride verbinding in te grijpen.

### <a name="test-hello-completed-web-application-on-azure"></a>Test Hallo op Azure-web-App voltooid
1. Hallo bovenaan rechts van de webpagina op Azure, kies **aanmelden**.
   
    ![Test aanmelden][HCTestLogIn]
2. Uw App Service-web-app nu is verbonden tooyour-webtoepassing lidmaatschapsdatabase op uw lokale machine. tooverify deze, meld u aan met van Hallo dezelfde referenties die u hebt opgegeven in de lokale Hallo eerder van de database.
   
    ![Hallo begroeting][HCTestHelloContoso]
3. toofurther uw nieuwe hybride verbinding testen en meld u af bij uw Azure-web-toepassing registreren als een andere gebruiker. Geef een nieuwe gebruikersnaam en wachtwoord en klik vervolgens op **registreren**.
   
    ![Test een andere gebruiker registreren][HCTestRegisterRelecloud]
4. tooverify dat Hallo nieuwe gebruikersreferenties zijn opgeslagen in de lokale database via uw hybride verbinding open SQL Management Studio op uw lokale computer. Vouw in Object Explorer Hallo **MembershipDB** database uit en vouw vervolgens **tabellen**. Klik met de rechtermuisknop Hallo **dbo. AspNetUsers** lidmaatschap tabel en kies **Selecteer Top 1000 rijen** tooview Hallo resultaten.
   
    ![Hallo-resultaten weergeven][HCTestSSMSTree]
5. Uw lidmaatschap van lokale tabel toont nu beide accounts - hello die u lokaal hebt gemaakt en Hallo dat u hebt gemaakt in hello Azure-cloud. Hallo dat u hebt gemaakt in de cloud Hallo is tooyour lokale-database via de Azure-functie voor hybride verbinding opgeslagen.
   
    ![Geregistreerde gebruikers in de lokale database.][HCTestShowMemberDb]

U hebt nu gemaakt en geïmplementeerd ASP.NET-webtoepassing die gebruikmaakt van een hybride verbinding tussen een web-app in Azure-cloud Hallo en een on-premises SQL Server database. Gefeliciteerd.

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
