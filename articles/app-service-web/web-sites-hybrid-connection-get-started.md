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
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a>On-premises resources benaderen via hybride verbindingen in Azure App Service
U kunt een Azure App Service-app verbinden met een on-premises resource die gebruikmaakt van een statische TCP-poort, zoals SQL Server, MySQL, HTTP-Web-API's en de meeste aangepaste webservices. In dit artikel laat zien hoe een hybride verbinding maken tussen App Service en een on-premises SQL Server database.

> [!NOTE]
> De Web-Apps-gedeelte van de functie hybride verbindingen is alleen beschikbaar in de [Azure Portal](https://portal.azure.com). Zie voor informatie over het maken van een verbinding in BizTalk Services [hybride verbindingen](http://go.microsoft.com/fwlink/p/?LinkID=397274). 
> 
> Deze inhoud geldt ook voor mobiele Apps in Azure App Service. 
> 
> 

## <a name="prerequisites"></a>Vereisten
* Een Azure-abonnement. Zie voor een gratis abonnement [gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/). 
  
    Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
* Als u wilt een on-premises SQL Server of SQL Server Express-database met een hybride verbinding gebruiken, moet TCP/IP moet zijn ingeschakeld op een statische poort. Met behulp van een standaardexemplaar van SQL Server wordt aanbevolen omdat deze gebruikmaakt van statische poort 1433. Zie voor meer informatie over het installeren en configureren van SQL Server Express voor gebruik met hybride verbindingen [verbinding maken met een lokale SQL Server uit een Azure-website met behulp van hybride verbindingen](http://go.microsoft.com/fwlink/?LinkID=397979).
* De computer waarop u de lokale hybride Verbindingsbeheer agent beschreven verderop in dit artikel installeert:
  
  * Moet verbinding maken met Azure via poort 5671
  * Moet kunnen bereiken de *hostnaam*:*portnumber* van uw lokale resource. 

> [!NOTE]
> De stappen in dit artikel wordt ervan uitgegaan dat u gebruikmaakt van de browser van de computer die als host voor de lokale-agent voor hybride verbinding fungeert.
> 
> 

## <a name="create-a-web-app-in-the-azure-portal"></a>Een web-app maken in de Azure-Portal
> [!NOTE]
> Als u al een web-app of een back-end voor mobiele App in de Azure-Portal die u wilt gebruiken voor deze zelfstudie hebt gemaakt, kunt u verder gaan naar [een hybride verbinding en een BizTalk Service maken](#CreateHC) en van daaruit starten.
> 
> 

1. In de linkerbovenhoek van de [Azure Portal](https://portal.azure.com), klikt u op **nieuw** > **Web en mobiel** > **Web-App**.
   
    ![Nieuwe web-app][NewWebsite]
2. Op de **Web-app** blade een URL op en klik op **maken**. 
   
    ![Websitenaam][WebsiteCreationBlade]
3. Na enkele ogenblikken de web-app wordt gemaakt en de blade web-app wordt weergegeven. De blade is een verticaal schuifbare dashboard waarmee u uw site beheren.
   
    ![Website worden uitgevoerd][WebSiteRunningBlade]
4. Om te controleren of de site is live, klikt u op de **Bladeren** pictogram om de standaardpagina weer te geven.
   
    ![Klik op Bladeren als u wilt zien van uw web-app][Browse]
   
    ![App-standaardwebpagina][DefaultWebSitePage]

Vervolgens maakt u een hybride verbinding en een BizTalk service voor de web-app.

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a>Een hybride verbinding en een BizTalk Service maken
1. Klik in de blade van uw web-app op **alle instellingen** > **Networking** > **uw hybride-verbindingseindpunten configureren**.
   
    ![Hybride verbindingen][CreateHCHCIcon]
2. Klik op de blade hybride verbindingen **toevoegen**.
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. De **toevoegen van een hybride verbinding** blade wordt geopend.  Aangezien dit de eerste hybride verbinding de **nieuwe hybride verbinding** optie vooraf geselecteerd, en de **hybride verbinding maken** er wordt een blade geopend voor u.
   
    ![Een hybride verbinding maken][TwinCreateHCBlades]
   
    Op de **blade voor hybride verbinding maken**:
   
   * Voor **naam**, Geef een naam op voor de verbinding.
   * Voor **hostnaam**, voer de naam van de lokale computer die als host fungeert voor uw resource.
   * Voor **poort**, voer het poortnummer dat gebruikmaakt van uw lokale resource (1433 voor een standaardexemplaar van SQL Server).
   * Klik op **Biz Talk Service**
4. De **BizTalk Service maken** blade wordt geopend. Voer een naam voor de BizTalk service en klik vervolgens op **OK**.
   
    ![BizTalk service maken][CreateHCCreateBTS]
   
    De **BizTalk Service maken** blade wordt gesloten en u keert terug naar de **hybride verbinding maken** blade.
5. Klik op de blade maken hybride verbinding **OK**. 
   
    ![Klik op OK][CreateBTScomplete]
6. Wanneer het proces is voltooid, wordt het meldingengebied in de Portal informeert dat de verbinding is gemaakt.
   
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
7. Op de blade web-app en de **hybride verbindingen** pictogram nu geeft aan dat er 1 hybride verbinding is gemaakt.
   
    ![Een hybride verbinding is gemaakt][CreateHCOneConnectionCreated]

U hebt op dit moment een belangrijk onderdeel van de cloudinfrastructuur voor hybride verbinding voltooid. Vervolgens maakt u een bijbehorende lokale apparaat.

<a name="InstallHCM"></a>

## <a name="install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a>Installeren van de lokale hybride Verbindingsbeheer om de verbinding te voltooien
1. Klik op de web-app-blade **alle instellingen** > **Networking** > **uw hybride-verbindingseindpunten configureren**. 
   
    ![Pictogram van hybride verbindingen][HCIcon]
2. Op de **hybride verbindingen** blade de **Status** kolom voor het laatst toegevoegde eindpunt bevat **niet verbonden**. Klik op de verbinding om deze te configureren.
   
    ![Niet verbonden][NotConnected]
   
    De hybride verbinding-blade wordt geopend.
   
    ![NotConnectedBlade][NotConnectedBlade]
3. Klik op de blade **Listener Setup**.
   
    ![Klik op Listener Setup][ClickListenerSetup]
4. De **hybride verbindingseigenschappen** blade wordt geopend. Onder **On-premises hybride Verbindingsbeheer**, kies **Klik hier om te installeren**.
   
    ![Klik hier om te installeren][ClickToInstallHCM]
5. Kies in het dialoogvenster Beveiliging waarschuwing toepassing uitgevoerd **uitvoeren** om door te gaan.
   
    ![Kies uitvoeren om door te gaan][ApplicationRunWarning]
6. In de **User Account Control** dialoogvenster kiezen **Ja**.
   
   ![Klik op Ja][UAC]
7. De hybride Verbindingsbeheer wordt gedownload en geïnstalleerd voor u. 
   
    ![Installeren][HCMInstalling]
8. Wanneer de installatie is voltooid, klikt u op **sluiten**.
   
    ![Klik op sluiten][HCMInstallComplete]
   
    Op de **hybride verbindingen** blade de **Status** kolom ziet u nu **verbonden**. 
   
    ![Status verbonden][HCStatusConnected]

Nu dat de infrastructuur van hybride verbinding voltooid is, kunt u een hybride-toepassing die gebruikmaakt van deze. 

> [!NOTE]
> De volgende secties laten zien hoe een hybride verbinding gebruiken met een back-end van Mobile Apps .NET project.
> 
> 

## <a name="configure-the-mobile-app-net-backend-project-to-connect-to-the-sql-server-database"></a>Het project voor het back-end van Mobile App .NET verbinding maken met de SQL Server-database configureren
In App Service is een back-end van Mobile Apps .NET project zojuist een ASP.NET web-app met een extra Mobile Apps SDK geïnstalleerd en wordt geïnitialiseerd. Voor het gebruik van uw web-app als een back-end van Mobile Apps, moet u [downloaden en het initialiseren van de backend voor mobiele Apps .NET SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).  

Voor mobiele Apps moet u ook een verbindingsreeks voor de lokale database definiëren en wijzigen van de back-end voor het gebruik van deze verbinding. 

1. Open het bestand Web.config voor uw back-end van Mobile App .NET in Solution Explorer in Visual Studio, Ga naar de **connectionStrings** sectie, het toevoegen van een nieuwe vermelding SqlClient als volgt naar de lokale SQL Server-database verwijst:
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    Vervang `<**secure_password**>` in deze tekenreeks met het wachtwoord die u hebt gemaakt voor *HybridConnectionLogin*.
2. Klik op **opslaan** in Visual Studio het Web.config-bestand wilt opslaan.
   
   > [!NOTE]
   > Deze instelling wordt gebruikt wanneer op de lokale computer wordt uitgevoerd. Wanneer in Azure wordt uitgevoerd, is deze instelling overschreven door de instelling voor de gedefinieerd in de portal.
   > 
   > 
3. Vouw de **modellen** map en open het modelbestand gegevens die eindigt in *Context.cs*.
4. Wijzig de **DbContext** exemplaarconstructor voor het doorgeven van de waarde `OnPremisesDBConnection` naar de basistabel **DbContext** constructor, vergelijkbaar met het volgende fragment:
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    De service wordt nu gebruiken voor de nieuwe verbinding met de SQL Server-database.

## <a name="update-the-mobile-app-backend-to-use-the-on-premises-connection-string"></a>De backend voor mobiele Apps voor het gebruik van de lokale verbindingsreeks bijwerken
Vervolgens moet u een app-instelling voor deze nieuwe verbindingsreeks toevoegen zodat deze kan worden gebruikt in Azure.  

1. Terug in de [Azure-portal](https://portal.azure.com) in de web-app back-end-code voor uw mobiele App klikt u op **alle instellingen**, klikt u vervolgens **toepassingsinstellingen**.
2. In de **Web-appinstellingen** blade omlaag naar **verbindingsreeksen** en voeg een nieuwe **SQL Server** verbindingstekenreeks met de naam `OnPremisesDBConnection` met een waarde zoals `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.
   
    Vervang `<**secure_password**>` met het beveiligd wachtwoord voor uw lokale-database.
   
    ![Verbindingsreeks voor on-premises-database](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. Druk op **opslaan** om op te slaan van het hybride verbinding en verbinding string, u zojuist hebt gemaakt.

Op dit moment kunt u het serverproject publiceren en testen van de nieuwe verbinding met uw bestaande Mobile Apps-clients. Gegevens worden gelezen uit en geschreven naar de lokale database met behulp van de hybride verbinding.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over het maken van een ASP.NET-webtoepassing die gebruikmaakt van een hybride verbinding [verbinding maken met een lokale SQL Server uit een Azure-website met behulp van hybride verbindingen](http://go.microsoft.com/fwlink/?LinkID=397979). 

### <a name="additional-resources"></a>Aanvullende resources
[Overzicht van hybride verbindingen](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Josh Twist introduceert hybride verbindingen (Channel 9 video)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Hybride verbindingen website](https://azure.microsoft.com/services/biztalk-services/)

[BizTalk Services: De tabbladen Dashboard, bewaken, schaal, configureren en hybride verbinding](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Het bouwen van een echte hybride Cloud met naadloze toepassing draagbaarheid (Channel 9 video)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Verbinding maken met een lokale SQL Server van Azure Mobile Services met behulp van hybride verbindingen (Channel 9 video)](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a>Wat is er gewijzigd
* Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

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
