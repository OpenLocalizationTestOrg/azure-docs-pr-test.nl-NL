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
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a>On-premises resources benaderen via hybride verbindingen in Azure App Service
U kunt verbinding maken met een Azure App Service-app tooany on-premises resource die gebruikmaakt van een statische TCP-poort, zoals SQL Server, MySQL, HTTP-Web-API's en de meeste aangepaste webservices. Dit artikel ziet u hoe toocreate een hybride verbinding tussen de App Service en een on-premises SQL Server database.

> [!NOTE]
> Hallo-Web-Apps-gedeelte van Hallo hybride verbindingen onderdeel is alleen beschikbaar in Hallo [Azure Portal](https://portal.azure.com). Zie voor een verbinding in BizTalk Services toocreate [hybride verbindingen](http://go.microsoft.com/fwlink/p/?LinkID=397274). 
> 
> Deze inhoud is ook van toepassing tooMobile Apps in Azure App Service. 
> 
> 

## <a name="prerequisites"></a>Vereisten
* Een Azure-abonnement. Zie voor een gratis abonnement [gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/). 
  
    Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
* toouse een lokale SQL Server of SQL Server Express-database met een hybride verbinding, moet TCP/IP toobe ingeschakeld op een statische poort. Met behulp van een standaardexemplaar van SQL Server wordt aanbevolen omdat deze gebruikmaakt van statische poort 1433. Zie voor meer informatie over het installeren en configureren van SQL Server Express voor gebruik met hybride verbindingen [Connect tooan lokale SQL Server uit een Azure-website met behulp van hybride verbindingen](http://go.microsoft.com/fwlink/?LinkID=397979).
* Hallo-computer waarop u Hallo op premises hybride Verbindingsbeheer agent beschreven verderop in dit artikel installeert:
  
  * Moet kunnen tooconnect tooAzure via poort 5671
  * Moet kunnen tooreach hello *hostnaam*:*portnumber* van uw lokale resource. 

> [!NOTE]
> Hallo stappen in dit artikel wordt ervan uitgegaan dat u gebruikmaakt van Hallo Hallo-computer die als voor agent voor hybride verbinding voor Hallo lokale host fungeert browser.
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Een web-app maken in hello Azure Portal
> [!NOTE]
> Als u al een web-app of een back-end voor mobiele App in hello Azure-Portal wilt u toouse voor deze zelfstudie hebt gemaakt, kunt u verder gaan te[een hybride verbinding en een BizTalk Service maken](#CreateHC) en van daaruit starten.
> 
> 

1. In Hallo linkerbovenhoek Hallo [Azure Portal](https://portal.azure.com), klikt u op **nieuw** > **Web en mobiel** > **Web-App**.
   
    ![Nieuwe web-app][NewWebsite]
2. Op Hallo **Web-app** blade een URL op en klik op **maken**. 
   
    ![Websitenaam][WebsiteCreationBlade]
3. Na enkele ogenblikken Hallo web-app wordt gemaakt en de blade web-app wordt weergegeven. Hallo-blade is een verticaal schuifbare dashboard waarmee u uw site beheren.
   
    ![Website worden uitgevoerd][WebSiteRunningBlade]
4. tooverify hello site live is, klikt u op Hallo **Bladeren** pictogram toodisplay Hallo standaardpagina.
   
    ![Klik op Bladeren toosee uw web-app][Browse]
   
    ![App-standaardwebpagina][DefaultWebSitePage]

Vervolgens maakt u een hybride verbinding en een BizTalk service voor Hallo web-app.

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a>Een hybride verbinding en een BizTalk Service maken
1. Klik in de blade van uw web-app op **alle instellingen** > **Networking** > **uw hybride-verbindingseindpunten configureren**.
   
    ![Hybride verbindingen][CreateHCHCIcon]
2. Klik op Hallo hybride verbindingen blade **toevoegen**.
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. Hallo **toevoegen van een hybride verbinding** blade wordt geopend.  Aangezien dit de eerste hybride verbinding, Hallo **nieuwe hybride verbinding** optie vooraf geselecteerd en Hallo **hybride verbinding maken** er wordt een blade geopend voor u.
   
    ![Een hybride verbinding maken][TwinCreateHCBlades]
   
    Op Hallo **blade voor hybride verbinding maken**:
   
   * Voor **naam**, Geef een naam voor het Hallo-verbinding.
   * Voor **hostnaam**, voer de naam Hallo van Hallo lokale computer die als host fungeert voor uw resource.
   * Voor **poort**, Voer Hallo-poortnummer dat gebruikmaakt van uw lokale resource (1433 voor een standaardexemplaar van SQL Server).
   * Klik op **Biz Talk Service**
4. Hallo **BizTalk Service maken** blade wordt geopend. Voer een naam voor Hallo BizTalk service en klik vervolgens op **OK**.
   
    ![BizTalk service maken][CreateHCCreateBTS]
   
    Hallo **BizTalk Service maken** blade wordt gesloten en keert u terug toohello **hybride verbinding maken** blade.
5. Klik op de blade voor Hallo maken hybride verbinding **OK**. 
   
    ![Klik op OK][CreateBTScomplete]
6. Wanneer het Hallo-proces is voltooid, informeert Hallo meldingengebied in Hallo Portal dat Hallo verbinding is gemaakt.
   
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
7. Hallo op Hallo van web-app-blade **hybride verbindingen** pictogram nu geeft aan dat er 1 hybride verbinding is gemaakt.
   
    ![Een hybride verbinding is gemaakt][CreateHCOneConnectionCreated]

U hebt op dit moment een belangrijk onderdeel van hybride Hallo-verbinding cloudinfrastructuur voltooid. Vervolgens maakt u een bijbehorende lokale apparaat.

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>Hallo op premises hybride Verbindingsbeheer toocomplete Hallo verbinding installeren
1. Klik op Hallo van web-app-blade **alle instellingen** > **Networking** > **uw hybride-verbindingseindpunten configureren**. 
   
    ![Pictogram van hybride verbindingen][HCIcon]
2. Op Hallo **hybride verbindingen** blade, Hallo **Status** onlangs eindpunt bevat op kolom voor Hallo **niet verbonden**. Klik op Hallo verbinding tooconfigure deze.
   
    ![Niet verbonden][NotConnected]
   
    Hallo hybride verbinding blade wordt geopend.
   
    ![NotConnectedBlade][NotConnectedBlade]
3. Klik op de blade Hallo **Listener Setup**.
   
    ![Klik op Listener Setup][ClickListenerSetup]
4. Hallo **hybride verbindingseigenschappen** blade wordt geopend. Onder **On-premises hybride Verbindingsbeheer**, kies **Klik hier tooinstall**.
   
    ![Klik hier tooinstall][ClickToInstallHCM]
5. Kies in het Hallo-toepassing uitgevoerd waarschuwingsvenster, **uitvoeren** toocontinue.
   
    ![Kies toocontinue uitvoeren][ApplicationRunWarning]
6. In Hallo **User Account Control** dialoogvenster kiezen **Ja**.
   
   ![Klik op Ja][UAC]
7. Hallo hybride Verbindingsbeheer wordt gedownload en geïnstalleerd voor u. 
   
    ![Installeren][HCMInstalling]
8. Wanneer het Hallo-installatie is voltooid, klikt u op **sluiten**.
   
    ![Klik op sluiten][HCMInstallComplete]
   
    Op Hallo **hybride verbindingen** blade, Hallo **Status** kolom ziet u nu **verbonden**. 
   
    ![Status verbonden][HCStatusConnected]

Nu die infrastructuur Hallo hybride verbinding voltooid is, kunt u een hybride-toepassing die gebruikmaakt van deze. 

> [!NOTE]
> Hallo volgende secties ziet u hoe toouse een hybride verbinding met een back-end van Mobile Apps .NET project.
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a>Hallo Mobile App .NET backend project tooconnect toohello SQL Server-database configureren
In App Service is een back-end van Mobile Apps .NET project zojuist een ASP.NET web-app met een extra Mobile Apps SDK geïnstalleerd en wordt geïnitialiseerd. toouse uw web-app als een back-end van Mobile Apps, moet u [downloaden en te initialiseren Hallo Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).  

Voor mobiele Apps, u ook toodefine een verbindingsreeks nodig voor Hallo lokale-database en Hallo back-end toouse wijzigt u deze verbinding. 

1. Zoek in Solution Explorer in Visual Studio openen Hallo Web.config-bestand voor uw mobiele App .NET back-end, Hallo **connectionStrings** sectie, het toevoegen van een nieuwe vermelding SqlClient zoals Hallo volgende, welke punten toohello lokale SQL Server-database:
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    Houd er rekening mee tooreplace `<**secure_password**>` in deze tekenreeks met Hallo wachtwoord die u hebt gemaakt voor *HybridConnectionLogin*.
2. Klik op **opslaan** in Visual Studio toosave Hallo Web.config-bestand.
   
   > [!NOTE]
   > Deze instelling wordt gebruikt wanneer op de lokale computer Hallo. Wanneer in Azure wordt uitgevoerd, is deze instelling onderdrukt door Hallo verbindingsinstelling gedefinieerd in het Hallo-portal.
   > 
   > 
3. Vouw Hallo **modellen** map en open Hallo gegevens modelbestand eindigt in *Context.cs*.
4. Hallo wijzigen **DbContext** exemplaar-constructor toopass Hallo waarde `OnPremisesDBConnection` toohello base **DbContext** constructor, vergelijkbare toohello codefragment te volgen:
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    Hallo-service wordt nu Hallo nieuwe verbinding toohello SQL Server-database gebruiken.

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a>Hallo mobiele App back-end toouse Hallo lokale met verbindingsreeks bijwerken
Vervolgens moet u tooadd een app-instelling voor deze nieuwe verbindingsreeks zodat deze kan worden gebruikt in Azure.  

1. Terug in Hallo [Azure-portal](https://portal.azure.com) in Hallo web-app back-end-code voor uw mobiele App, klikt u op **alle instellingen**, klikt u vervolgens **toepassingsinstellingen**.
2. In Hallo **Web-appinstellingen** blade Schuif naar beneden te**verbindingsreeksen** en voeg een nieuwe **SQL Server** verbindingstekenreeks met de naam `OnPremisesDBConnection` met een waarde zoals `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.
   
    Vervang `<**secure_password**>` met Hallo beveiligd wachtwoord voor uw lokale-database.
   
    ![Verbindingsreeks voor on-premises-database](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. Druk op **opslaan** toosave Hallo hybride verbinding en de verbindingsreeks u zojuist hebt gemaakt.

U kunt op dit moment Hallo serverproject publiceren en testen van Hallo nieuwe verbinding met uw bestaande Mobile Apps-clients. Gegevens worden gelezen uit en toohello Hallo hybride verbinding met lokale-database geschreven.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over het maken van een ASP.NET-webtoepassing die gebruikmaakt van een hybride verbinding [Connect tooan lokale SQL Server uit een Azure-website met behulp van hybride verbindingen](http://go.microsoft.com/fwlink/?LinkID=397979). 

### <a name="additional-resources"></a>Aanvullende resources
[Overzicht van hybride verbindingen](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Josh Twist introduceert hybride verbindingen (Channel 9 video)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Hybride verbindingen website](https://azure.microsoft.com/services/biztalk-services/)

[BizTalk Services: De tabbladen Dashboard, bewaken, schaal, configureren en hybride verbinding](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Het bouwen van een echte hybride Cloud met naadloze toepassing draagbaarheid (Channel 9 video)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Verbinding maken met tooan lokale SQL-Server van Azure Mobile Services met behulp van hybride verbindingen (Channel 9 video)](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

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
