---
title: Een app beveiligen in Azure App Service
description: Informatie over het beveiligen van een web-app, back-end voor mobiele app of API-app in Azure App Service.
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
ms.openlocfilehash: b70d74441f3d6d9793ae516b3f04e36e786a9a8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="secure-an-app-in-azure-app-service"></a>Een app beveiligen in Azure App Service
In dit artikel helpt u aan de slag over het beveiligen van uw web-app, back-end voor mobiele app of API-app in Azure App Service. 

Beveiliging in Azure App Service heeft twee niveaus: 

* **Beveiliging van infrastructuur- en platform** -trust van Azure om de services moet u daadwerkelijk uitvoeren dingen veilig in de cloud.
* **Toepassingsbeveiliging** -u moet de app zelf veilig ontwerp. Dit omvat de manier waarop u integreert met Azure Active Directory, hoe u certificaten beheren en hoe u ervoor zorgen dat u veilig contact met andere services opnemen kunt. 

#### <a name="infrastructure-and-platform-security"></a>Beveiliging van infrastructuur- en platform
Omdat App Service de Azure VM's, opslag, netwerkverbindingen, web frameworks, management en integratiefuncties en nog veel meer houdt is actief beveiligd en gehard en doorloopt krachtige naleving en controleert doorlopend om ervoor te zorgen dat:

* Uw App Service-apps zijn geïsoleerd van zowel het Internet en van andere klanten Azure-resources.
* Communicatie van geheimen (bijvoorbeeld verbindingsreeksen) tussen uw App Service-app en andere Azure-resources (bijvoorbeeld SQL Database) in een resourcegroep blijft in Azure en niet alle netwerkgrenzen cross. Geheimen worden altijd versleuteld.
* Alle communicatie tussen uw App Service-app en externe bronnen, zoals beheer-en PowerShell-opdrachtregelinterface, Azure SDK's, REST-API's en hybride verbindingen zijn juist zijn versleuteld.
* 24-uurs threat management-App Service-bronnen worden beschermd tegen malware, gedistribueerde denial-of-service (DDoS) man-in-the-middle (MITM) en andere dreigingen. 

Zie voor meer informatie over de infrastructuur- en beveiliging in Azure [Azure Vertrouwenscentrum](https://azure.microsoft.com/support/trust-center/security/).

#### <a name="application-security"></a>Toepassingsbeveiliging
Hoewel Azure verantwoordelijk is voor het beveiligen van de infrastructuur en het platform dat op uw toepassing wordt uitgevoerd, is uw verantwoordelijkheid voor het beveiligen van uw toepassing zelf. Met andere woorden, wilt u ontwikkelen, implementeren en beheren van uw toepassingscode en inhoud op een veilige wijze. Zonder deze kan uw toepassingscode of inhoud nog steeds kwetsbaar voor aanvallen, zoals:

* SQL-injectie
* Sessiehijacking
* Cross-site scripting
* Op toepassingsniveau MITM
* Op toepassingsniveau DDoS

Er is een volledige beschrijving van de beveiligingsoverwegingen voor het web gebaseerde toepassingen buiten het bereik van dit document. Als een beginpunt voor verdere hulp bij het beveiligen van uw toepassing, Zie de [Open Web Application Security Project (OWASP)](https://www.owasp.org/index.php/Main_Page), specifiek de [top 10 project.](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project), waarin de huidige top 10 kritieke beveiliging van webtoepassingen-fouten, zoals wordt bepaald door OWASP leden.

## <a name="perform-penetration-testing-on-your-app"></a>Binnendringen testen op uw app uitvoeren
Een van de eenvoudigste manieren om aan de slag met het testen op beveiligingsproblemen op uw App Service-app te gebruiken is de [integratie met Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) één muisklik beveiligingslek scannen van uw app uitvoeren. U kunt de resultaten weergeven in een rapport gemakkelijk te begrijpen en informatie over het oplossen van elk beveiligingsprobleem met stapsgewijze instructies.

Als u liever uw eigen tests binnendringen uitvoeren of een andere scanner suite of provider wilt gebruiken, moet u de [Azure binnendringen goedkeuringsproces testen](https://security-forms.azure.com/penetration-testing/terms) en voorafgaande goedkeuring om uit te voeren van de gewenste binnendringen tests verkrijgen.

## <a name="https"></a>Veilige communicatie met klanten
Als u de  **\*. azurewebsites.net** domeinnaam gemaakt voor uw app in App Service, u kunt onmiddellijk HTTPS, zoals een SSL-certificaat is opgegeven voor alle  **\*. azurewebsites.net** domeinnamen. Als uw site gebruikt een [aangepaste domeinnaam](app-service-web-tutorial-custom-domain.md), kunt u een SSL-certificaat te uploaden [HTTPS inschakelen](app-service-web-tutorial-custom-ssl.md) voor het aangepaste domein.

Inschakelen van [HTTPS](https://en.wikipedia.org/wiki/HTTPS) kan helpen beschermen tegen MITM-aanvallen op de communicatie tussen uw app en de gebruikers.

## <a name="secure-data-tier"></a>Laag van de beveiligde gegevens
App Service maximaal kan worden geïntegreerd met SQL-Database, zodat de verbindingsreeksen zijn versleuteld over de hele linie en worden alleen ontsleuteld op de virtuele machine die de app wordt uitgevoerd op *en* alleen wanneer de app wordt uitgevoerd. Bovendien Azure SQL Database bevat veel beveiligingsfuncties om te helpen beveiligen van uw toepassingsgegevens cyberbeveiliging bedreigingen, met inbegrip van [versleuteling in rust](https://msdn.microsoft.com/library/dn948096.aspx), [altijd versleuteld](https://msdn.microsoft.com/library/mt163865.aspx), [dynamische-Gegevensmaskering](../sql-database/sql-database-dynamic-data-masking-get-started.md), en [Bedreigingsdetectie](../sql-database/sql-database-threat-detection.md). Als u gevoelige gegevens of nalevingsvereisten hebt, raadpleegt u [SQL Database beveiligen](../sql-database/sql-database-security-overview.md) voor meer informatie over het beveiligen van uw gegevens.

Als u een databaseprovider van derden, zoals ClearDB, moet u contact opneemt met de documentatie van de provider rechtstreeks op de best practices voor beveiliging.  

## <a name="develop"></a>Veilige ontwikkeling en implementatie
### <a name="publishing-profiles-and-publish-settings"></a>Publicatie-profielen en publicatie-instellingen
Bij het ontwikkelen van toepassingen-beheertaken uitvoeren of automatiseren met behulp van de hulpprogramma's zoals **Visual Studio**, **Web Matrix**, **Azure PowerShell** of de **Azure-opdrachtregelinterface (Azure CLI)**, kunt u ofwel een *publicatie-instellingen* bestand of een *publiceren profiel*. Beide typen u verificatie met Azure en moeten zijn beveiligd om te voorkomen dat onbevoegde toegang.

* Een **publicatie-instellingen** bestand bevat
  
  * Uw Azure-abonnement-ID
  * Een beheercertificaat waarmee u beheertaken uitvoeren voor uw abonnement *zonder te bieden een accountnaam of ongeldig wachtwoord*.
* Een **publiceren profiel** bestand bevat
  
  * Informatie voor publicatie naar uw app

Als u een hulpprogramma die gebruikmaakt van een bestand met instellingen publiceren of publiceren profielbestand gebruikt, importeert u het bestand met publicatie-instellingen of profiel naar het hulpprogramma en vervolgens **verwijderen** het bestand. Als u ervoor dat het bestand zorgen moet om te delen met anderen werkt op het project bijvoorbeeld opslaan op een veilige locatie, zoals een *versleutelde* map met beperkte machtigingen.

Bovendien moet u controleren of dat de ingevoerde referenties zijn beveiligd. Bijvoorbeeld: **Azure PowerShell** en de **Azure-opdrachtregelinterface (Azure CLI)** beide geïmporteerde gegevens opslaan in uw **basismap** ( *~*  op Linux of OS X-systemen en */gebruikers/uwgebruikersnaam* op Windows-systemen.) Voor extra beveiliging, u kunt desgewenst **versleutelen** deze locaties met behulp van versleuteling hulpprogramma's voor uw besturingssysteem.

### <a name="configuration-settings-and-connection-strings"></a>Configuratie-instellingen en verbindingsreeksen
Het is gebruikelijk om voor het opslaan van verbindingsreeksen, referenties voor verificatie en andere gevoelige gegevens in configuratiebestanden. Helaas kunnen deze bestanden worden weergegeven op uw website of ingecheckt in een openbare opslagplaats, wanneer deze gegevens beschikbaar komen. Een eenvoudige zoekopdrachten op [GitHub](https://github.com), bijvoorbeeld kunt onthullen talloze configuratiebestanden met blootgestelde geheimen in de openbare-opslagplaatsen.

De aanbevolen procedure is om deze gegevens buiten de configuratiebestanden van de app. App Service kunt u configuratiegegevens opgeslagen als onderdeel van de runtime-omgeving als **appinstellingen** en **verbindingsreeksen**. De waarden worden blootgesteld aan uw toepassing tijdens runtime via *omgevingsvariabelen* voor de meeste programmeertalen. Voor .NET-toepassingen, worden deze waarden opgenomen in de configuratie van uw .NET tijdens runtime. Naast deze situaties deze configuratie-instellingen wordt blijven versleuteld tenzij u weergeven of ze configureren met behulp van de [Azure Portal](https://portal.azure.com) of -hulpprogramma's zoals PowerShell of Azure CLI. 

Opslaan van configuratiegegevens in App Service, maakt het mogelijk voor de beheerder van de app vergrendelen gevoelige informatie voor de productie-apps. Ontwikkelaars kunnen gebruikmaken van een afzonderlijke set van configuratie-instellingen voor ontwikkeling van Apps en de instellingen kunnen automatisch worden vervangen door de instellingen die in App Service. Ook niet de ontwikkelaars moeten weten wat de geheimen die zijn geconfigureerd voor de productie-app. Zie voor meer informatie over het configureren van app-instellingen en verbindingsreeksen in App Service [web-apps configureren](web-sites-configure.md).

### <a name="ftps"></a>FTPS
Azure App Service biedt veilige FTP-toegang tot het bestandssysteem van uw app via **FTPS**. Hiermee kunt u veilig toegang krijgen tot de toepassingscode die op de web-app evenals diagnostische logboeken. Het verdient aanbeveling dat u altijd FTPS in plaats van FTP gebruiken. 

U vindt de koppeling FTPS voor uw app met de volgende stappen:

1. Open de [Azure-Portal](https://portal.azure.com).
2. Selecteer **door alle Bladeren**.
3. Van de **Bladeren** blade Selecteer **App Services**.
4. Van de **App Services** blade, selecteer de gewenste app.
5. Selecteer in de app-blade **alle instellingen**.
6. Van de **instellingen** blade Selecteer **eigenschappen**.
7. De FTP- en FTPS koppelingen beschikbaar zijn op de **instellingen** blade. 

Zie voor meer informatie over FTPS [File Transfer Protocol](http://en.wikipedia.org/wiki/File_Transfer_Protocol).

## <a name="next-steps"></a>Volgende stappen
Voor meer informatie over de beveiliging van de Azure-platform, informatie over het melden van een **veiligheidsincident of misbruik**, of om u te informeren over Microsoft die u zult uitvoeren **binnendringen testen** van uw site, Zie de Beveiligingssectie van de [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

Voor meer informatie over **web.config** of **applicationhost.config** bestanden in App Service-apps, Zie [configuratieopties ontgrendeld in Azure App Service WebApps](https://azure.microsoft.com/blog/2014/01/28/more-to-explore-configuration-options-unlocked-in-windows-azure-web-sites/).

Zie voor informatie over de logboekinformatie voor App Service-apps, die mogelijk van pas bij het detecteren van aanvallen, [Diagnostische logboekregistratie inschakelen](web-sites-enable-diagnostic-log.md).

> [!NOTE]
> Als u wilt dat aan de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

