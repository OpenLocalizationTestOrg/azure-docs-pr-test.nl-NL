---
title: aaaMigrate een enterprise web app tooAzure App Service
description: Toont hoe de bestaande IIS-websites tooAzure App Service Web Apps voor het migreren van Web Apps migratie Assistant tooquickly toouse
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
ms.openlocfilehash: 7d66c5b799f0eefe85cbd9ba596ee0a05167f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-enterprise-web-app-tooazure-app-service"></a>Migreren van een onderneming web app tooAzure App Service
U kunt eenvoudig uw bestaande websites die worden uitgevoerd op Internet Information Service (IIS) 6 of hoger migreren te[App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). 

> [!IMPORTANT]
> Windows Server 2003 einde van juli 2015 op 14-ondersteuning is bereikt. Als u momenteel uw websites op een IIS-server van Windows Server 2003 host, is Web-Apps een laag risico, lage kosten en laag wrijving tookeep uw online websites en Web-Apps migratie Assistant kunt automatiseren Hallo migratieproces voor u. 
> 
> 

[Web-Apps migratie-assistent](https://www.movemetothecloud.net/) kunt analyseren van uw installatie van IIS-server, identificeren welke sites worden gemigreerde tooApp Service, markeer elementen kunnen niet worden gemigreerd of worden niet ondersteund op Hallo-platform en Migreer uw websites en gekoppelde databases tooAzure.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a>Elementen die tijdens de analyse van de compatibiliteit is geverifieerd
Migratie-assistent Hallo maakt een gereedheid rapport tooidentify alle mogelijke oorzaken voor problemen met blokkeringen waardoor een geslaagde migratie van lokale IIS tooAzure App Service Web Apps. Aantal Hallo essentiële items toobe op de hoogte van zijn:

* Poort bindingen – Web Apps ondersteunt alleen poort 80 voor HTTP en poort 443 voor HTTPS-verkeer. Andere poortconfiguraties worden genegeerd en verkeer worden gerouteerd too80 of 443. 
* Authenticatie – Web Apps biedt ondersteuning voor anonieme verificatie standaard en formulierverificatie aangegeven door een toepassing. Windows-verificatie kan worden gebruikt door te integreren met Azure Active Directory en AD FS alleen. Alle andere vormen van de verificatie - bijvoorbeeld basisverificatie - worden momenteel niet ondersteund. 
* Globale Assembly-Cache (GAC) – Hallo GAC wordt niet ondersteund in Web-Apps. Als uw toepassing verwijst naar assembly's die u normaal gesproken toohello GAC implementeert, moet u toodeploy toohello toepassing bin-map in de Web-Apps. 
* IIS5-Compatibiliteitsmodus: dit wordt niet ondersteund in Web-Apps. 
* Groepen van toepassingen – In Web Apps, elke site en de onderliggende toepassingen worden uitgevoerd in Hallo dezelfde groep van toepassingen. Als uw site meerdere onderliggende toepassingen met behulp van meerdere groepen van toepassingen heeft, te tooa één groep van toepassingen met algemene instellingen consolideren of migreren van elke toepassing tooa afzonderlijke web-app.
* COM-onderdelen, zoals Web Apps kan geen Hallo registratie van COM-onderdelen op Hallo-platform. Als uw websites of toepassingen gebruik van een COM-onderdelen maken, moet u ze in beheerde code te herschrijven en implementeren met Hallo website of toepassing.
* ISAPI-extensies – Web Apps kan Hallo gebruik van de ISAPI-extensies ondersteunen. U hebt toodo Hallo volgende nodig:
  
  * Hallo dll-bestanden met uw web-app implementeren 
  * Hallo-dll's met behulp van registreren [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)
  * Plaats een applicationHost.xdt-bestand in de hoofdmap van site Hallo met Hallo inhoud die worden beschreven in 'Zodat arbitrart ISAPI-extensies toobe geladen' [sectie van dit artikel](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples) 
    
  
    
    Voor meer voorbeelden van het XML-documenttransformaties toouse met uw website, Zie [transformatie van uw Microsoft Azure-website](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).
* Andere onderdelen, zoals SharePoint, FrontPage-serverextensies (FPSE), FTP, SSL-certificaten worden niet gemigreerd.

## <a name="how-toouse-hello-web-apps-migration-assistant"></a>Hoe toouse Hallo-assistent migratie van Web-Apps
Deze sectie stappen via een tootoomigrate voorbeeld enkele websites die gebruikmaken van een SQL Server-database en wordt uitgevoerd op een lokale machine, Windows Server 2003 R2 (IIS 6.0):

1. Hallo IIS-server of de clientcomputer Navigeer op te[https://www.movemetothecloud.net/](https://www.movemetothecloud.net/) 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. Web-Apps migratie Assistant installeren door te klikken op Hallo **IIS-Server toegewezen** knop. Meer opties zijn opties in Hallo nabije toekomst. 
3. Klik op Hallo **Install-hulpprogramma** knop tooinstall Web Apps migratie-assistent op uw computer.
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > U kunt ook klikken op **downloaden voor offline-installatie** toodownload een ZIP-bestand niet installeren op servers verbonden toohello internet. U kunt ook op **uploaden van een bestaand rapport van de migratie-gereedheid**, dit is een geavanceerde optie toowork met een bestaande gereedheid migratierapport die u eerder hebt gegenereerd (dit wordt later).
   > 
   > 
4. In Hallo **toepassing installeert** scherm, klikt u op **installeren** tooinstall op uw computer. Het installeert bijbehorende afhankelijkheden, zoals Web Deploy, DacFX en IIS, indien nodig ook. 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   Na de installatie, Web Apps migratie Assistant automatisch gestart.
5. Kies **sites en -databases migreren vanaf een externe server tooAzure**. Voer Hallo beheerdersreferenties voor de externe server Hallo en klik op **doorgaan**. 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   U kunt uiteraard toomigrate van Hallo lokale server. Hallo externe optie is handig als u wilt dat toomigrate websites uit een productie-IIS-server.
   
   Op dit moment hulpprogramma voor migratie van Hallo inspecteert Hallo van de configuratie van de IIS-server, zoals Sites, toepassingen, toepassingen en afhankelijkheden tooidentify candidate websites voor de migratie. 
6. Hallo schermafbeelding hieronder ziet u drie websites – **standaardwebsite**, **TimeTracker**, en **CommerceNet4**. Alle hebben een bijbehorende database willen we toomigrate. Selecteer alle sites op Hallo zou u zoals tooassess en klik vervolgens op **volgende**.
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. Klik op **uploaden** tooupload Hallo gereedheid rapport. Als u op **bestand lokaal opslaan**, kunt u het hulpprogramma voor migratie van hello later opnieuw uitvoeren en uploaden Hallo gereedheid voor het rapport opgeslagen zoals eerder opgemerkt.
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   Zodra u Hallo gereedheid rapport uploadt, voert Azure de gereedheid van de analyses en het Hallo van resultaten wordt weergegeven. Hallo assessment details voor elke website lezen en zorg ervoor dat u begrijpt of alle problemen hebt opgelost voordat u doorgaat. 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. Klik op **beginnen met migratie** toostart Hallo migratie. U zult omgeleid tooAzure toolog nu toegang tot je account. Het is belangrijk dat u aanmelden met een account met een actief Azure-abonnement. Als u een Azure-account niet hebt, dan u zich voor een gratis proefversie aanmelden kunt [hier](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_). 
9. Hallo tenantaccount, Azure-abonnement en toouse regio voor uw gemigreerde Azure-web-apps en -databases selecteren en klik vervolgens op **migratie Start**. U kunt later Hallo websites toomigrate selecteren.
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. Op het volgende scherm Hallo kunt u wijzigingen aanbrengen toohello standaard migratie-instellingen, zoals:
    
    * Gebruik een bestaande Azure SQL Database of maak een nieuwe Azure SQL Database en de referenties configureren
    * Hallo websites toomigrate selecteren
    * namen voor hello Azure-web-apps en hun gekoppelde SQL-databases definiëren
    * Hallo globale instellingen en het niveau van de site-instellingen aanpassen
    
    Hallo onderstaande schermafbeelding ziet u alle Hallo websites geselecteerd om te migreren met de standaardinstellingen Hallo.
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > Hallo **Azure Active Directory inschakelen** checkbox in aangepaste instellingen integreert hello Azure-web-app met [Azure Active Directory](../active-directory/active-directory-whatis.md) (Hallo **standaarddirectory**). Zie voor meer informatie over het synchroniseren van Azure Active Directory met uw lokale Active Directory [adreslijstintegratie](http://msdn.microsoft.com/library/jj573653).
    > 
    > 
11. Nadat u alle gewenste Hallo wijzigingen aanbrengt, klikt u op **maken** toostart Hallo-migratieproces. hulpprogramma voor migratie van Hallo hello Azure SQL Database en Azure web-app maken en vervolgens publiceren Hallo website-inhoud en -databases. voortgang van de migratie Hello wordt duidelijk weergegeven in Hallo-hulpprogramma voor migratie en u ziet een scherm Samenvatting op Hallo end, welke details Hallo sites gemigreerd, of dit is gelukt, koppelingen toohello gemaakte Azure-web-apps. 
    
    Als een fout optreedt tijdens de migratie migratie hulpprogramma wordt duidelijk Hallo duiden op Hallo fout en terugdraaien Hallo wijzigingen. U zult ook kunnen toosend Hallo foutenrapport rechtstreeks toohello engineering team door te klikken op Hallo **foutrapport verzenden** knop met de Hallo vastgelegde fout aanroepstack en bouwen van de berichttekst. 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    Als migreren is voltooid zonder fouten, u kunt ook klikken op Hallo **Feedback geven** tooprovide rechtstreeks feedback knop. 
12. Klik op Hallo koppelingen toohello Azure-web-apps en controleer of dat Hallo migratie is geslaagd.
13. U kunt nu beheren Hallo gemigreerd web-apps in Azure App Service. toodo deze, meld u aan bij Hallo [Azure Portal](https://portal.azure.com).
14. Open in hello Azure Portal, Hallo Web-Apps blade toosee gemigreerde website (weergegeven als de web-apps) en klik vervolgens op een van deze toostart Hallo web-app, zoals het configureren van continue publiceren, het maken van back-ups, automatisch schalen, en gebruik controleren beheren of de prestaties.
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

