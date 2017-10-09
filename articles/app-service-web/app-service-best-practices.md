---
title: aaaBest procedures voor Azure App Service
description: Informatie over aanbevolen procedures en probleemoplossing voor Azure App Service.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: f3359464-fa44-4f4a-9ea6-7821060e8d0d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: dariagrigoriu
ms.openlocfilehash: a1d3127f5a746aa43f7b56b45f17c45df9087bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-app-service"></a>Aanbevolen procedures voor Azure App Service
In dit artikel bevat een overzicht van aanbevolen procedures voor het gebruik van [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). 

## <a name="colocation"></a>Plaatsing
Wanneer Azure-resources voor het samenstellen van een oplossing zoals een web-app en een database bevinden zich in verschillende regio's Hallo effecten kunt Hallo volgende zijn:

* Wachttijd in de communicatie tussen bronnen
* Financieel kosten voor uitgaande gegevens overbrengen regio-overschrijdende zoals aangegeven op Hallo [Azure pagina met prijzen](https://azure.microsoft.com/pricing/details/data-transfers).

Collocatie in Hallo dezelfde regio wordt aanbevolen voor Azure-resources voor het samenstellen van een oplossing zoals een web-app en een database of opslaggroep-account gebruikt toohold inhoud of gegevens. Wanneer Hallo maken van resources moet u controleren of dat ze zich in dezelfde Azure-regio tenzij u specifieke zakelijke hebt of reden voor deze niet toobe ontwerpen. U kunt een App Service-app toohello verplaatsen dezelfde regio bevinden als uw database dankzij het gebruik van Hallo [App Service-functie voor het klonen](app-service-web-app-cloning-portal.md) momenteel beschikbaar voor Premium-App Service-Plan apps.   

## <a name="memoryresources"></a>Wanneer de meer geheugen hebben dan verwacht voor het gebruiken van apps
Wanneer u een app verbruikt meer geheugen hebben dan verwacht, omdat aangegeven via bewaking of serviceaanbevelingen rekening houden met Hallo merkt [functie-App Service automatisch herstel](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites). Een van de opties voor Hallo automatisch herstel functie Hallo duurt aangepaste acties op basis van een drempelwaarde voor geheugen. Acties omvatten Hallo spectrum van e-mailmeldingen tooinvestigation via memory dump tooon plaatse risicobeperking door Hallo werkproces wordt gerecycled. Automatisch herstel kan worden geconfigureerd via web.config en via een beschrijvende gebruikersinterface zoals beschreven op in dit blogbericht voor Hallo [Appuitbreiding Service ondersteuning Site](https://azure.microsoft.com/blog/additional-updates-to-support-site-extension-for-azure-app-service-web-apps).   

## <a name="CPUresources"></a>Wanneer de meer CPU dan verwacht voor het gebruiken van apps
Wanneer er dat een app verbruikt meer CPU dan verwacht of optreedt herhaald CPU, pieken aangegeven via bewaking of serviceaanbevelingen rekening houden met omhoog schalen of uitbreiden Hallo App Service-abonnement. Als uw toepassing statefull, is omhoog schalen Hallo enige optie, terwijl als de toepassing is staatloze, scaling out u meer flexibiliteit en hogere schaal potentieel krijgt. 

Voor meer informatie over 'statefull' vs 'stateless' toepassingen kunt Bekijk deze video: [Planning van een toepassing met meerdere lagen schaalbare End-to-End voor Microsoft Azure Web App](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/DEV-B414#fbid=?hashlink=fbid). Lees voor meer informatie over App Service-opties voor schaalbaarheid en automatisch schalen: [schalen van een Web-App in Azure App Service](web-sites-scale.md).  

## <a name="socketresources"></a>Wanneer de socket-resources zijn uitgeput
Een veelvoorkomende reden voor put uitgaande TCP-verbindingen is Hallo gebruik van clientbibliotheken die niet zijn geïmplementeerd tooreuse TCP-verbindingen of in Hallo geval van een hoger niveau protocol zoals HTTP - keepalive-niet gebruikt. Controleer het Hallo-documentatie voor elk Hallo-bibliotheken waarnaar wordt verwezen door Hallo apps in uw App Service-Plan tooensure ze zijn geconfigureerd of toegankelijk is in uw code voor efficiënte hergebruik van uitgaande verbindingen. U volgt tevens Hallo bibliotheek documentatie richtlijnen voor het maken van een juiste en release of opschoning tooavoid verbindingen lekken. Terwijl deze client bibliotheken onderzoeken in mogelijk gevolgen uitgevoerd worden verminderd door toomultiple exemplaren uitbreiden.  

## <a name="appbackup"></a>Wanneer uw app back-up begint mislukt
Hallo twee meest voorkomende redenen waarom app back-up mislukt zijn: instellingen van het opslagaccount is ongeldig en ongeldige database-configuratie. Deze fouten worden gewoonlijk gebeuren wanneer er wijzigingen toostorage of bronnen van de database of wijzigingen voor het tooaccess deze resources (bijvoorbeeld referenties voor geselecteerde in de back-upinstellingen Hallo Hallo-database bijgewerkt). Back-ups worden doorgaans volgens een planning wordt uitgevoerd en vereisen toegang toostorage (voor het uitvoeren van back-up bestanden Hallo) en databases (voor het kopiëren en lezen inhoud toobe in Hallo back-up). Hallo resultaat tooaccess een van deze resources zijn niet consistent back-upfouten. 

Wanneer er back-fouten optreden, Raadpleeg de meest recente resultaten toounderstand welk type van de fout zich heeft voorgedaan. In geval van toegang Opslagfouten Hallo bekijken en Opslaginstellingen Hallo gebruikt in de back-upconfiguratie Hallo bijwerken. In geval van toegang databasefouten Hallo Bekijk en uw verbindingen tekenreeksen werken als onderdeel van de appinstellingen van de. Ga verder tooupdate uw back-upconfiguratie tooproperly Hallo vereist databases bevatten. Zie voor meer informatie over back-up app Hallo [Back-up van een web-app in Azure App Service](web-sites-backup.md) documentatie.

## <a name="nodejs"></a>Wanneer nieuwe Node.js-apps zijn geïmplementeerd tooAzure App Service
Azure App Service-standaardconfiguratie voor Node.js-apps is bedoeld toobest gesorteerde Hallo behoeften van de meest voorkomende apps. Als de configuratie voor uw Node.js-app of zou kunnen profiteren van persoonlijke afstemmen tooimprove prestaties optimaliseren Resourcegebruik voor CPU/geheugen/netwerkbronnen, kunt u de aanbevolen procedures en stappen voor probleemoplossing kan bekijken. Deze documentatie wordt beschreven Hallo iisnode instellingen moet u mogelijk tooconfigure voor uw Node.js-app beschrijft Hallo verschillende scenario's of problemen die kan worden aangesloten op uw app en toont hoe tooaddress deze problemen: [aanbevolen procedures en gids voor probleemoplossing voor knooppunt toepassingen in Azure App Service](app-service-web-nodejs-best-practices-and-troubleshoot-guide.md).   

