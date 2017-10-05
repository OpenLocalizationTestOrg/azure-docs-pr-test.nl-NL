---
title: Een zakelijke web-app migreren naar Azure App Service
description: Laat zien hoe u Web Apps migratie Assistant snel bestaande IIS-websites migreren naar Azure App Service Web Apps
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: 
ms.assetid: 2e846fc0-37cc-42e6-ac57-ff442ef16e85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 18d6a8da38b42dcf5c1500f7fc26638aea26a809
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-an-enterprise-web-app-to-azure-app-service"></a>Een zakelijke web-app migreren naar Azure App Service
U kunt eenvoudig uw bestaande websites die worden uitgevoerd op Internet Information Service (IIS) 6 of hoger om te migreren [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). 

> [!IMPORTANT]
> Windows Server 2003 einde van juli 2015 op 14-ondersteuning is bereikt. Als u momenteel de websites op een IIS-server host is Windows Server 2003, Web-Apps is een laag risico, lage kosten en laag wrijving manier om te houden van uw websites online en -assistent migratie van Web Apps kan worden geautomatiseerd het migratieproces voor u. 
> 
> 

[Web-Apps migratie-assistent](https://www.movemetothecloud.net/) kunt analyseren van uw installatie van IIS-server, identificeren welke sites kunnen worden gemigreerd naar App Service, markeer elementen kunnen niet worden gemigreerd of worden niet ondersteund voor het platform en vervolgens uw websites en de bijbehorende databases naar Azure migreren.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a>Elementen die tijdens de analyse van de compatibiliteit is geverifieerd
De migratie-assistent maakt een rapport gereedheid voor het identificeren van alle mogelijke oorzaken voor problemen met blokkeringen waardoor een geslaagde migratie van lokale IIS naar Azure App Service Web Apps. Enkele belangrijke items rekening houden met zijn:

* Poort bindingen – Web Apps ondersteunt alleen poort 80 voor HTTP en poort 443 voor HTTPS-verkeer. Verschillende poortconfiguraties wordt genegeerd en het verkeer wordt doorgestuurd naar 80 of 443. 
* Authenticatie – Web Apps biedt ondersteuning voor anonieme verificatie standaard en formulierverificatie aangegeven door een toepassing. Windows-verificatie kan worden gebruikt door te integreren met Azure Active Directory en AD FS alleen. Alle andere vormen van de verificatie - bijvoorbeeld basisverificatie - worden momenteel niet ondersteund. 
* Globale Assembly-Cache (GAC) – de GAC wordt niet ondersteund in Web-Apps. Als uw toepassing verwijst naar assembly's waarbij u meestal aan de GAC implementeert, moet u de bin-map van de toepassing in de Web-Apps te implementeren. 
* IIS5-Compatibiliteitsmodus: dit wordt niet ondersteund in Web-Apps. 
* Groepen van toepassingen – In Web Apps, elke site en de onderliggende toepassingen worden uitgevoerd in dezelfde groep van toepassingen. Als uw site meerdere onderliggende toepassingen met behulp van meerdere groepen van toepassingen heeft, te consolideren op één groep van toepassingen met algemene instellingen of migreren van elke toepassing een aparte web-app.
* COM-onderdelen, zoals Web Apps is niet toegestaan voor de registratie van COM-onderdelen op het platform. Als uw websites of toepassingen gebruik van een COM-onderdelen maken, moet u ze in beheerde code te herschrijven en implementeren met de website of toepassing.
* ISAPI-extensies – Web Apps kan het gebruik van de ISAPI-extensies ondersteunen. U moet het volgende doen:
  
  * de dll-bestanden met uw web-app implementeren 
  * Registreer het dll-bestanden met [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)
  * Plaats een applicationHost.xdt-bestand in de hoofdmap van de site met de inhoud die worden beschreven in 'Allowing arbitrart ISAPI-extensies worden geladen' [sectie van dit artikel](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples) 
    
  
    
    Zie voor meer voorbeelden van het gebruik van XML-documenttransformaties met uw website [transformatie van uw Microsoft Azure-website](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).
* Andere onderdelen, zoals SharePoint, FrontPage-serverextensies (FPSE), FTP, SSL-certificaten worden niet gemigreerd.

## <a name="how-to-use-the-web-apps-migration-assistant"></a>Het gebruik van de Web-Apps migratie Assistant
Deze sectie stappen via een voorbeeld om te migreren van een paar websites die gebruikmaken van een SQL Server-database en wordt uitgevoerd op een lokale machine, Windows Server 2003 R2 (IIS 6.0):

1. Op de IIS-server of de clientcomputer gaat u naar [https://www.movemetothecloud.net/](https://www.movemetothecloud.net/) 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. Web-Apps migratie Assistant installeren door te klikken op de **IIS-Server toegewezen** knop. Meer opties zijn beschikbaar in de nabije toekomst. 
3. Klik op de **Install-hulpprogramma** knop voor het installeren van Web Apps migratie-assistent op uw computer.
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > U kunt ook klikken op **downloaden voor offline-installatie** een zipbestand voor het installeren op servers die niet is verbonden met internet te downloaden. U kunt ook op **uploaden van een bestaand rapport van de migratie-gereedheid**, dit is een geavanceerde optie voor het werken met een bestaande gereedheid migratierapport die u eerder hebt gegenereerd (dit wordt later).
   > 
   > 
4. In de **toepassing installeert** scherm, klikt u op **installeren** te installeren op uw computer. Het installeert bijbehorende afhankelijkheden, zoals Web Deploy, DacFX en IIS, indien nodig ook. 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   Na de installatie, Web Apps migratie Assistant automatisch gestart.
5. Kies **sites en -databases vanaf een externe server migreren naar Azure**. Voer de beheerdersreferenties voor de externe server en klik op **doorgaan**. 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   U kunt uiteraard voor het migreren van de lokale server. De externe optie is handig wanneer u wilt migreren van websites van een IIS-server voor productie.
   
   Op dit moment het hulpprogramma voor migratie inspecteert de configuratie van de IIS-server, zoals Sites, toepassingen, groepen van toepassingen en afhankelijkheden voor het identificeren van websites kandidaat voor migratie. 
6. De onderstaande schermafbeelding ziet u drie websites – **standaardwebsite**, **TimeTracker**, en **CommerceNet4**. Alle hebben een bijbehorende database die we wilt migreren. Selecteer alle van de sites die u wilt beoordelen en klik vervolgens op **volgende**.
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. Klik op **uploaden** voor het uploaden van het rapport gereedheid. Als u op **bestand lokaal opslaan**, kunt u later opnieuw uitvoeren van het hulpprogramma voor migratie en het rapport opgeslagen gereedheid uploaden als u eerder hebt genoteerd.
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   Zodra u het rapport gereedheid uploadt, wordt Azure voert gereedheid van de analyse en toont u de resultaten. Lees de beoordeling details voor elke website en zorg ervoor dat u begrijpt of alle problemen hebt opgelost voordat u doorgaat. 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. Klik op **beginnen met migratie** voor de migratie te starten. U wordt nu omgeleid naar Azure aan te melden bij uw account. Het is belangrijk dat u aanmelden met een account met een actief Azure-abonnement. Als u een Azure-account niet hebt, dan u zich voor een gratis proefversie aanmelden kunt [hier](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_). 
9. Selecteer de tenantaccount, de Azure-abonnement en de regio waarin u wilt gebruiken voor uw gemigreerde Azure-web-apps en -databases en klik vervolgens op **migratie Start**. U kunt de websites voor het migreren van later selecteren.
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. Op het volgende scherm kunt u wijzigingen op de standaardinstellingen voor migratie, zoals:
    
    * Gebruik een bestaande Azure SQL Database of maak een nieuwe Azure SQL Database en de referenties configureren
    * Selecteer de websites migreren
    * Definieer namen voor de Azure-web-apps en hun gekoppelde SQL-databases
    * de algemene instellingen en het niveau van de site-instellingen aanpassen
    
    De onderstaande schermafbeelding ziet u de websites die zijn geselecteerd voor migratie met de standaardinstellingen.
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > de **Azure Active Directory inschakelen** checkbox in aangepaste instellingen integreert de Azure-web-app met [Azure Active Directory](../active-directory/active-directory-whatis.md) (de **standaarddirectory**). Zie voor meer informatie over het synchroniseren van Azure Active Directory met uw lokale Active Directory [adreslijstintegratie](http://msdn.microsoft.com/library/jj573653).
    > 
    > 
11. Nadat u de gewenste wijzigingen aanbrengt, klikt u op **maken** naar het migratieproces start. Het hulpprogramma voor migratie van de Azure SQL Database en de Azure-web-app maken en publiceren van de website-inhoud en -databases. Voortgang van de migratie wordt duidelijk weergegeven in het hulpprogramma voor migratie en u ziet een scherm Samenvatting aan het einde, welke details van de sites hebt gemigreerd, of het ze gelukt is, koppelingen naar de zojuist gemaakte Azure-web-apps. 
    
    Als er een fout optreedt tijdens de migratie van geeft het hulpprogramma voor migratie duidelijk de fout en het terugdraaien van de wijzigingen. Is ook het foutenrapport rechtstreeks naar het technische team verzenden door te klikken op de **foutrapport verzenden** knop, met de vastgelegde fout call stack en bouwen van de berichttekst. 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    Als migreren is voltooid zonder fouten, u kunt ook klikken op de **Feedback geven** knop rechtstreeks feedback geven. 
12. Klik op de koppelingen aan de Azure-web-apps en controleer of dat de migratie is geslaagd.
13. U kunt nu de gemigreerde web-apps in Azure App Service beheren. Om dit te doen, meld u aan bij de [Azure Portal](https://portal.azure.com).
14. In de Azure-beheerportal, open de blade Web-Apps voor uw gemigreerde websites (weergegeven als de web-apps) en klik vervolgens op een van die beginnen met het beheren van de web-app, zoals het configureren van continue publiceren, het maken van back-ups, automatisch schalen, bewaking gebruik of prestaties.
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u gaat geen verplichtingen aan.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

