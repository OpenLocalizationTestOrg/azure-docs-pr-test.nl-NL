---
title: aaaManage een web-app in Azure App Service
description: Koppelingen tooresources voor het beheren van een web-app in Azure App Service.
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a>Een web-app in Azure App Service beheren
Dit onderwerp vindt u koppelingen tooresources voor het beheren van een web-app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Beheer omvat alle Hallo-taken die uw web-app probleemloos houden. 

Gedurende de levensduur van de Hallo van een web-app, wordt u verschillende beheertaken uitvoeren tijdens het verplaatsen van de initiële implementatie toonormal bewerking, onderhoud en updates.

Veel beheertaken voor web-app kunnen worden uitgevoerd in hello Azure-Portal.

## <a name="before-you-deploy-your-web-app-tooproduction"></a>Voordat u uw web-app tooproduction implementeren
### <a name="choose-a-tier"></a>Kies een laag
Azure App Service wordt aangeboden in vijf categorieën: vrijmaken, gedeelde, Basic, Standard en Premium. Zie voor meer informatie over het Hallo-functies en prijzen voor elke laag [prijsinformatie](https://azure.microsoft.com/pricing/details/app-service/). 

* [App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) kunt u meerdere web-apps onder Hallo groep dezelfde categorie.
* U kunt altijd [overschakelen lagen](web-sites-scale.md) nadat u uw web-app hebt gemaakt.

### <a name="configuration"></a>Configuratie
Gebruik Hallo [Azure Portal](https://portal.azure.com/) tooset verschillende configuratieopties. Zie voor meer informatie [web-apps configureren in Azure App Service](web-sites-configure.md). Dit is een snelle Controlelijst:

* Selecteer **runtime versies** voor .NET, PHP, Java of Python, indien nodig.
* Schakel **WebSockets** als Hallo WebSocket-protocol maakt gebruik van uw web-app. (Dit omvat apps die gebruikmaken van [ASP.NET SignalR](http://www.asp.net/signalr) of [socket.io](web-sites-nodejs-chat-app-socketio.md).)
* Voert u doorlopende webtaken? Zo ja, inschakelen **altijd op**.
* Set Hallo **standaarddocument**, zoals index.html.

U kunt in toevoeging toothese basic configuratie-instellingen, tooconfigure Hallo volgende:

* **Secure Socket Layer (SSL)** versleuteling. toouse SSL met een aangepaste domeinnaam, moet u een SSL-certificaat en het configureren van uw web-app toouse deze. Zie [HTTPS inschakelen voor een web-app in Azure App Service](app-service-web-tutorial-custom-ssl.md).
* **Aangepaste domeinnaam.** Uw web-app wordt automatisch een subdomein onder azurewebsites.net heeft. U kunt een aangepaste domeinnaam bijvoorbeeld contoso.com koppelen. Zie [een aangepaste domeinnaam configureren in Azure App Service](app-service-web-tutorial-custom-domain.md).

Taalspecifieke configuratie:

* **PHP**: [PHP configureren in Azure App Service WebApps](web-sites-php-configure.md).
* **Python**: [Python configureren met Azure App Service Web-Apps](web-sites-python-configure.md)

## <a name="while-your-web-app-is-running"></a>Terwijl uw web-app wordt uitgevoerd
Terwijl uw web-app wordt uitgevoerd, wilt u ervoor dat deze beschikbaar is en dat het gebruikersverkeer toomeet schalen toomake. U moet mogelijk ook tootroubleshoot fouten.

### <a name="monitoring"></a>Bewaking
* Met hello Azure Portal, kunt u [toevoegen maatstaven voor prestaties](web-sites-monitor.md) zoals CPU-gebruik en het aantal aanvragen van clients.
* [Schalen van uw web-app](web-sites-scale.md) in antwoord tootraffic. Afhankelijk van de laag, kunt u Hallo aantal VM's en/of Hallo grootte van de VM-instanties Hallo schalen. In Hallo Standard en Premium-categorieën, kunt u ook instellen automatisch schalen, zodat uw web-app automatisch wordt geschaald op basis van een vaste planning, of in antwoord tooload.  

### <a name="backups"></a>Back-ups
* Stel [automatische back-ups](web-sites-backup.md) van uw web-app. Meer informatie over back-ups in [in deze video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).
* Meer informatie over opties voor Hallo [databases herstellen](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.

### <a name="troubleshooting"></a>Problemen oplossen
* Als er iets mis gaat, kunt u [in Visual Studio oplossen](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), met behulp van diagnostische logboeken en foutopsporing in de cloud Hallo live. 
* Buiten Visual Studio zijn er verschillende manieren toocollect diagnostische logboeken. Zie [logboekregistratie van diagnostische gegevens van web-apps in Azure App Service](web-sites-enable-diagnostic-log.md).
* Zie voor Node.js-toepassingen [hoe toodebug een Node.js web-app in Azure App Service](web-sites-nodejs-debug.md).

### <a name="restoring-data"></a>Gegevens terugzetten
* [Herstellen](web-sites-restore.md) een web-app die u eerder een back-up.

## <a name="when-you-update-your-web-app"></a>Wanneer u uw web-app bijwerken
Als u automatische back-ups niet hebt ingeschakeld, kunt u een [handmatige back-up](web-sites-backup.md).

Overweeg het gebruik van [gefaseerde implementatie](web-sites-staged-publishing.md). Deze optie kunt u updates tooa staging-implementatie die naast elkaar uitvoert publiceren met uw productie-implementatie. 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


