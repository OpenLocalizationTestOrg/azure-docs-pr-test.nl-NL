---
title: aaaSecure een app in Azure App Service
description: Meer informatie over hoe toosecure een web-app, back-end voor mobiele app of API-app in Azure App Service.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 5ce560b4-42d7-4b20-935c-0445fd539e39
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: fceef7963b29516f33602dcd50591d14309bf188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-app-in-azure-app-service"></a>Een app beveiligen in Azure App Service
In dit artikel helpt u aan de slag over het beveiligen van uw web-app, back-end voor mobiele app of API-app in Azure App Service. 

Beveiliging in Azure App Service heeft twee niveaus: 

* **Beveiliging van infrastructuur- en platform** -vertrouwensrelatie u Azure toohave Hallo services die u hebt uitgevoerd tooactually dingen veilig in Hallo cloud nodig.
* **Toepassingsbeveiliging** -u toodesign Hallo app zelf veilig nodig hebt. Dit omvat de manier waarop u integreert met Azure Active Directory, hoe u certificaten beheren en hoe u ervoor zorgen dat u veilig toodifferent services kan communiceren. 

#### <a name="infrastructure-and-platform-security"></a>Beveiliging van infrastructuur- en platform
Omdat App Service hello Azure-virtuele machines, opslag, netwerkverbindingen, web frameworks, management en integratiefuncties en nog veel meer onderhoudt is actief beveiligd en gehard en doorloopt krachtige naleving en controleert op een doorlopend toomake zeker die:

* Uw App Service-apps zijn geïsoleerd van beide Hallo Internet en Hallo van andere klanten Azure-resources.
* Communicatie van geheimen (bijvoorbeeld verbindingsreeksen) tussen uw App Service-app en andere Azure-resources (bijvoorbeeld SQL Database) in een resourcegroep blijft in Azure en niet alle netwerkgrenzen cross. Geheimen worden altijd versleuteld.
* Alle communicatie tussen uw App Service-app en externe bronnen, zoals beheer-en PowerShell-opdrachtregelinterface, Azure SDK's, REST-API's en hybride verbindingen zijn juist zijn versleuteld.
* 24-uurs threat management-App Service-bronnen worden beschermd tegen malware, gedistribueerde denial-of-service (DDoS) man-in-the-middle (MITM) en andere dreigingen. 

Zie voor meer informatie over de infrastructuur- en beveiliging in Azure [Azure Vertrouwenscentrum](https://azure.microsoft.com/support/trust-center/security/).

#### <a name="application-security"></a>Toepassingsbeveiliging
Hoewel Azure verantwoordelijk is voor het beveiligen van Hallo-infrastructuur en platform dat op uw toepassing wordt uitgevoerd, is uw verantwoordelijkheid toosecure uw toepassing zelf. Met andere woorden, moet u toodevelop, implementeren en beheren van uw toepassingscode en inhoud op een veilige wijze. Zonder deze kan uw toepassingscode of inhoud nog steeds kwetsbaar toothreats, zoals:

* SQL-injectie
* Sessiehijacking
* Cross-site scripting
* Op toepassingsniveau MITM
* Op toepassingsniveau DDoS

Een volledige beschrijving van de beveiligingsoverwegingen voor het web gebaseerde toepassingen valt buiten bereik Hallo van dit document. Zie als een beginpunt voor verdere informatie over het beveiligen van uw toepassing hello [Open Web Application Security Project (OWASP)](https://www.owasp.org/index.php/Main_Page), speciaal Hallo [top 10 project.](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project), die een lijst met huidige top 10 Hallo kritieke web application beveiligingsfouten, zoals wordt bepaald door OWASP leden.

## <a name="perform-penetration-testing-on-your-app"></a>Binnendringen testen op uw app uitvoeren
Een van de eenvoudigste manieren tooget Hallo gestart met het testen voor beveiligingsproblemen op uw App Service-app is toouse hello [integratie met Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) tooperform één muisklik beveiligingslek scannen van uw app. U kunt de resultaten bekijkt hello weergeven in een rapport gemakkelijk te begrijpen en meer informatie hoe toofix elk beveiligingsprobleem met stapsgewijze instructies.

Als u liever tooperform uw eigen binnendringen test of een andere scanner suite of provider toouse wilt, moet u Hallo volgen [Azure binnendringen goedkeuringsproces testen](https://security-forms.azure.com/penetration-testing/terms) en voorafgaande goedkeuring tooperform Hallo gewenst binnendringen ophalen Test.

## <a name="https"></a>Veilige communicatie met klanten
Als u Hallo  **\*. azurewebsites.net** domeinnaam gemaakt voor uw app in App Service, u kunt onmiddellijk HTTPS, zoals een SSL-certificaat is opgegeven voor alle  **\*. azurewebsites.net** domeinnamen. Als uw site gebruikt een [aangepaste domeinnaam](app-service-web-tutorial-custom-domain.md), kunt u een SSL-certificaat te uploaden[HTTPS inschakelen](app-service-web-tutorial-custom-ssl.md) voor het aangepaste domein Hallo.

Inschakelen van [HTTPS](https://en.wikipedia.org/wiki/HTTPS) kan helpen beschermen tegen MITM-aanvallen op Hallo communicatie tussen uw app en de gebruikers.

## <a name="secure-data-tier"></a>Laag van de beveiligde gegevens
App Service maximaal kan worden geïntegreerd met SQL-Database, zodat alle Hallo-verbindingsreeksen via het mededelingenbord Hallo zijn versleuteld en worden alleen ontsleuteld op Hallo VM die Hallo-app wordt uitgevoerd op *en* alleen wanneer Hallo app wordt uitgevoerd. Daarnaast Azure SQL Database bevat veel beveiliging functies toohelp beveiligen van uw toepassingsgegevens cyberbeveiliging bedreigingen, met inbegrip van [versleuteling in rust](https://msdn.microsoft.com/library/dn948096.aspx), [altijd versleuteld](https://msdn.microsoft.com/library/mt163865.aspx), [ Dynamische Gegevensmaskering](../sql-database/sql-database-dynamic-data-masking-get-started.md), en [Bedreigingendetectie](../sql-database/sql-database-threat-detection.md). Als u gevoelige gegevens of nalevingsvereisten hebt, raadpleegt u [SQL Database beveiligen](../sql-database/sql-database-security-overview.md) voor meer informatie over het toosecure uw gegevens.

Als u een databaseprovider van derden, zoals ClearDB, moet u contact opneemt met de documentatie van de provider van de Hallo rechtstreeks op de best practices voor beveiliging.  

## <a name="develop"></a>Veilige ontwikkeling en implementatie
### <a name="publishing-profiles-and-publish-settings"></a>Publicatie-profielen en publicatie-instellingen
Bij het ontwikkelen van toepassingen-beheertaken uitvoeren of automatiseren met behulp van de hulpprogramma's zoals **Visual Studio**, **Web Matrix**, **Azure PowerShell** of Hallo **Azure-opdrachtregelinterface (Azure CLI)**, kunt u ofwel een *publicatie-instellingen* bestand of een *publiceren profiel*. Beide typen u te verifiëren bij Azure en tooprevent niet-geautoriseerde toegang moeten worden beveiligd.

* Een **publicatie-instellingen** bestand bevat
  
  * Uw Azure-abonnement-ID
  * Een beheercertificaat waarmee u tooperform beheertaken voor uw abonnement *zonder tooprovide een accountnaam of ongeldig wachtwoord*.
* Een **publiceren profiel** bestand bevat
  
  * Informatie voor het publiceren van tooyour app

Als u een hulpprogramma die gebruikmaakt van een bestand met instellingen publiceren of profielbestand publiceren, Hallo-bestand met de Hallo publicatie-instellingen te importeren of profiel naar Hallo hulpprogramma en vervolgens **verwijderen** Hallo-bestand. Als u Hallo-bestand moet houden, tooshare met anderen werkt op Hallo project bijvoorbeeld opslaan op een veilige locatie zoals een *versleutelde* map met beperkte machtigingen.

Bovendien moet u controleren of Hallo geïmporteerd referenties zijn beveiligd. Bijvoorbeeld: **Azure PowerShell** en Hallo **Azure-opdrachtregelinterface (Azure CLI)** beide geïmporteerde gegevens opslaan in uw **basismap** ( *~*  op Linux of OS X-systemen en */gebruikers/uwgebruikersnaam* op Windows-systemen.) Voor extra beveiliging kunt u desgewenst te**versleutelen** deze locaties met behulp van versleuteling hulpprogramma's voor uw besturingssysteem.

### <a name="configuration-settings-and-connection-strings"></a>Configuratie-instellingen en verbindingsreeksen
Het is algemene practice toostore-verbindingsreeksen, referenties voor verificatie en andere gevoelige gegevens in configuratiebestanden. Helaas kunnen deze bestanden worden weergegeven op uw website of ingecheckt in een openbare opslagplaats, wanneer deze gegevens beschikbaar komen. Een eenvoudige zoekopdrachten op [GitHub](https://github.com), bijvoorbeeld kunt onthullen talloze configuratiebestanden met blootgestelde geheimen in openbare Hallo-opslagplaatsen.

Hallo aanbevolen procedure is tookeep deze gegevens buiten de configuratiebestanden van de app. App Service kunt u configuratiegegevens opgeslagen als onderdeel van de runtime-omgeving Hallo als **appinstellingen** en **verbindingsreeksen**. Hallo-waarden zijn blootgestelde tooyour toepassing tijdens runtime via *omgevingsvariabelen* voor de meeste programmeertalen. Voor .NET-toepassingen, worden deze waarden opgenomen in de configuratie van uw .NET tijdens runtime. Naast deze situaties deze configuratie-instellingen wordt blijven versleuteld tenzij u weergeven of ze configureren met behulp van Hallo [Azure Portal](https://portal.azure.com) of -hulpprogramma's zoals PowerShell of Azure CLI Hallo. 

Opslaan van configuratiegegevens in App Service, maakt het mogelijk voor van app Hallo beheerder toolock omlaag gevoelige informatie voor Hallo productie apps. Ontwikkelaars kunnen gebruikmaken van een afzonderlijke set van configuratie-instellingen voor ontwikkeling van Apps en het Hallo-instellingen kunnen automatisch worden vervangen door Hallo-instellingen die zijn geconfigureerd in App Service. Zelfs Hallo ontwikkelaars moeten tooknow Hallo geheimen zijn geconfigureerd voor Hallo productie-app. Zie voor meer informatie over het configureren van app-instellingen en verbindingsreeksen in App Service [web-apps configureren](web-sites-configure.md).

### <a name="ftps"></a>FTPS
Azure App Service biedt veilige FTP-toegang toohello-bestandssysteem voor uw app via **FTPS**. Hiermee kunt u toosecurely toegang Hallo toepassingscode op Hallo web-app, evenals diagnostische logboeken. Het verdient aanbeveling dat u altijd FTPS in plaats van FTP gebruiken. 

Hallo FTPS koppeling voor uw app vindt u Hello stappen te volgen:

1. Open Hallo [Azure Portal](https://portal.azure.com).
2. Selecteer **door alle Bladeren**.
3. Van Hallo **Bladeren** blade Selecteer **App Services**.
4. Van Hallo **App Services** blade, selecteer Hallo gewenste app.
5. Selecteer in het Hallo-app-blade **alle instellingen**.
6. Van Hallo **instellingen** blade Selecteer **eigenschappen**.
7. Hallo FTP en FTPS koppelingen beschikbaar zijn op Hallo **instellingen** blade. 

Zie voor meer informatie over FTPS [File Transfer Protocol](http://en.wikipedia.org/wiki/File_Transfer_Protocol).

## <a name="next-steps"></a>Volgende stappen
Voor meer informatie over beveiliging Hallo Hallo Azure-platform, informatie over het melden van een **veiligheidsincident of misbruik**, of Microsoft die u zult uitvoeren tooinform **binnendringen testen** van uw site, raadpleegt u de Beveiligingssectie Hallo Hallo [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

Voor meer informatie over **web.config** of **applicationhost.config** bestanden in App Service-apps, Zie [configuratieopties ontgrendeld in Azure App Service WebApps](https://azure.microsoft.com/blog/2014/01/28/more-to-explore-configuration-options-unlocked-in-windows-azure-web-sites/).

Zie voor informatie over de logboekinformatie voor App Service-apps, die mogelijk van pas bij het detecteren van aanvallen, [Diagnostische logboekregistratie inschakelen](web-sites-enable-diagnostic-log.md).

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

