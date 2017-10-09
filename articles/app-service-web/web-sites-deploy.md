---
title: aaaDeploy uw app tooAzure App Service | Microsoft Docs
description: Meer informatie over hoe toodeploy uw app tooAzure App Service.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: f1464f71-2624-400e-86a2-e687e385804f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 5c84e4ca502874209d750c94efeb86a59aa71a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service"></a>Uw app tooAzure App Service implementeren
Dit artikel helpt u Hallo aanbevolen optie toodeploy Hallo bestanden voor uw web-app, back-end voor mobiele app of API-app te bepalen[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), en leidt u tooappropriate resources met specifieke tooyour instructies voorkeursoptie.

## <a name="overview"></a>Overzicht van Azure App Service-implementatie
Azure App Service onderhoudt Hallo toepassingsframework voor u (ASP.NET, PHP, Node.js, enzovoort). Sommige frameworks standaard terwijl anderen, zoals Java en Python zijn ingeschakeld, moet een eenvoudige vinkje configuratie tooenable mogelijk deze. Bovendien kunt u uw toepassingsframework, zoals PHP-versie van Hallo of Hallo bitness van uw runtime aanpassen. Zie voor meer informatie [configureren van uw app in Azure App Service](web-sites-configure.md).

Omdat er geen tooworry over Hallo web server of toepassing framework, het implementeren van uw app tooApp Service is een kwestie van het implementeren van uw code, binaire bestanden, bestanden en hun respectieve mapstructuur toohello [   **/siteconfiguratie /wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (of Hallo **/site/wwwroot/App_Data/taken/** map voor WebJobs). App Service ondersteunt drie verschillende implementatieprocessen. Alle Hallo implementatiemethoden in dit artikel gebruik een van de volgende processen Hallo: 

* [FTP- of FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol): uw favoriete FTP of FTPS ingeschakeld hulpprogramma toomove uw tooAzure bestanden vanuit [FileZilla](https://filezilla-project.org) toofull aanbevolen IDE zoals [NetBeans](https://netbeans.org). Dit is uitsluitend een uploadproces. Er zijn geen extra services worden geleverd door App Service, zoals versiebeheer, structuur bestandsbeheer, enz. 
* [Kudu (Git/volgt of OneDrive/Dropbox)](https://github.com/projectkudu/kudu/wiki/Deployment): Kudu is Hallo [implementatie-engine](https://github.com/projectkudu/kudu/wiki) in App Service. Uw tooKudu code rechtstreeks vanuit een opslagplaats pushen. Kudu biedt ook extra services wanneer tooit, zoals versiebeheer, pakket herstellen, MSBuild, wordt doorgeschoven, code en [web hooks](https://github.com/projectkudu/kudu/wiki/Web-hooks) voor continue implementatie en andere automatiseringstaken. implementatie-engine Kudu Hallo ondersteunt 3 soorten implementatie bronnen:   
  
  * Inhoud synchroniseren vanuit OneDrive en Dropbox   
  * Doorlopende implementatie op basis van een opslagplaats met automatische synchronisatie van GitHub en Bitbucket Visual Studio Team Services  
  * Implementatie met handmatige synchronisatie uit lokale Git-opslagplaats gebaseerde  
* [Web Deploy](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy): implementeren code tooApp Service rechtstreeks van uw favoriete tools zoals met behulp van Visual Studio Hallo dezelfde tooling waarmee implementatie tooIIS servers worden geautomatiseerd. Dit hulpprogramma ondersteunt diff-implementatie, het maken van de database, transformaties van verbindingsreeksen, enzovoort. Web Deploy verschilt van Kudu toepassing binaire bestanden zijn ingebouwd voordat ze worden geïmplementeerd tooAzure. Vergelijkbare tooFTP geen extra services worden geleverd door App Service.

Populaire web ontwikkelingsprogramma's ondersteuning voor een of meer van deze van implementatieprocessen. Terwijl hello u ervoor kiezen hulpprogramma Hallo implementatieprocessen bepaalt kunt u gebruikmaken van, hello werkelijke DevOps-functionaliteit tot uw beschikking staan afhankelijk Hallo combinatie van het implementatieproces Hallo en hello specifieke hulpprogramma's u kiest. Bijvoorbeeld, als u Web Deploy uit uitvoeren [Visual Studio met Azure SDK](#vspros), zelfs als u geen automatisering van kudu Bovendien krijgt, u krijgt pakket herstellen en MSBuild-automatisering in Visual Studio. 

> [!NOTE]
> Deze implementatieprocessen niet daadwerkelijk [inrichten hello Azure-resources](../azure-resource-manager/resource-group-template-deploy-portal.md) die uw app mogelijk nodig heeft. Echter de meeste Hallo gekoppeld hoe-tooarticles wordt uitgelegd hoe tooprovision Hallo app en implementeren van uw code tooit end-to-end. U kunt ook aanvullende opties voor het inrichten van Azure-resources in Hallo vinden [implementatie automatiseren met behulp van de opdrachtregelprogramma's](#automate) sectie.
> 
> 

## <a name="ftp"></a>Handmatig implementeren door het uploaden van bestanden met FTP
Als u de gebruikte toomanually kopiëren van de webserver van de web content tooa bent, kunt u een [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) hulpprogramma toocopy bestanden, zoals Windows Verkenner of [FileZilla](https://filezilla-project.org/).

Hallo-professionals van handmatig kopiëren van bestanden zijn:

* Bekend zijn en de minimale complexiteit voor FTP-tooling. 
* Weten precies waar uw bestanden gaat.
* Extra beveiliging met FTPS.

Hallo nadelen van het handmatig kopiëren van bestanden zijn:

* Met tooknow hoe toodeploy toohello juiste mappen in App Service-bestanden. 
* Er is geen versiebeheer voor terugdraaien als er fouten optreden.
* Er is geen ingebouwde implementatiegeschiedenis voor het oplossen van problemen bij de implementatie.
* Mogelijke lang implementatie tijden omdat veel FTP-hulpprogramma's niet diff-alleen kunnen worden gekopieerd en gewoon alle Hallo-bestanden te kopiëren.  

### <a name="howtoftp"></a>Hoe tooupload bestanden met FTP
Hallo [Azure Portal](https://portal.azure.com) biedt u alle benodigde tooconnect tooyour app mappen met FTP- of FTPS Hallo-gegevens.

* [Uw app tooAzure App Service implementeren met FTP](app-service-deploy-ftp.md)

## <a name="dropbox"></a>Implementeren door te synchroniseren met een cloud-map
Een goed alternatief te[u bestanden handmatig kopieert](#ftp) bestanden en mappen tooApp Service van een cloudopslagservice zoals OneDrive en Dropbox wordt gesynchroniseerd. Hallo Kudu proces voor de implementatie maakt gebruik van synchroniseren met een cloud-map (Zie [overzicht van implementatieprocessen](#overview)).

Hallo-professionals van de synchronisatie met een cloud-map zijn:

* Eenvoud van implementatie. Services zoals OneDrive en Dropbox bieden bureaublad sync-clients, zodat uw lokale werkmap ook de directory van uw implementatie is.
* Implementatie met één klik.
* Alle implementatie-engine Kudu Hallo-functionaliteit is beschikbaar (bijvoorbeeld pakket herstellen, automatisering).

Hallo nadelen van de synchronisatie met een cloud-map zijn:

* Er is geen versiebeheer voor terugdraaien als er fouten optreden.
* Er is geen geautomatiseerde implementatie handmatig synchroniseren is vereist.

### <a name="howtodropbox"></a>Hoe toodeploy door synchroniseren met een cloud-map
In Hallo [Azure Portal](https://portal.azure.com), kunt u een map voor synchronisatie van inhoud in de cloudopslag OneDrive of Dropbox, werken met uw app-code en de inhoud in de map en sync tooApp Service Hello op een knop.

* [Synchroniseren van de inhoud van een map tooAzure voor cloud-App Service](app-service-deploy-content-sync.md). 

## <a name="continuousdeployment"></a>Continu implementeren vanuit een cloud-gebaseerde source control-service
Als uw ontwikkelteam gebruikmaakt van een cloud-gebaseerde source code management (SCM) service, zoals [Visual Studio Team Services](http://www.visualstudio.com/), [GitHub](https://www.github.com), of [BitBucket](https://bitbucket.org/), kunt u een App configureren Service-toointegrate met uw opslagplaats en continu implementeren. 

Hallo-professionals voor het implementeren van een cloud-gebaseerde source control-service zijn:

* Versie besturingselement tooenable ongedaan maken.
* Mogelijkheid tooconfigure continue implementatie voor Git (en volgt indien van toepassing) opslagplaatsen. 
* Branchespecifieke implementatie, kunt implementeren verschillende filialen toodifferent [sleuven](web-sites-staged-publishing.md).
* Alle implementatie-engine Kudu Hallo-functionaliteit is beschikbaar (bijvoorbeeld implementatie versiebeheer, terugdraaien, pakket herstellen, automatisering).

Hallo con voor het implementeren van een cloud-gebaseerde source control-service is:

* Enige kennis van Hallo respectieve SCM-service vereist.

### <a name="vsts"></a>Hoe toodeploy continu van een bron cloud-gebaseerde service beheren
In Hallo [Azure Portal](https://portal.azure.com), kunt u continue implementatie van GitHub en Bitbucket Visual Studio Team Services configureren.

* [Continue implementatie tooAzure App Service](app-service-continuous-deployment.md). 

toofind uit hoe tooconfigure continue implementatie handmatig van een cloud-opslagplaats niet vermeld in Azure Portal Hallo (zoals [GitLab](https://gitlab.com/)), Zie [instellen van continue implementatie met handmatige stappen](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="localgitdeployment"></a>Implementeren vanaf de lokale Git
Als uw ontwikkelteam gebruikmaakt van een lokale lokale bron code management (SCM) service op basis van Git, kunt u dit configureren als een implementatie bron tooApp Service. 

Professionals voor het implementeren van lokale Git zijn:

* Versie besturingselement tooenable ongedaan maken.
* Branchespecifieke implementatie, kunt implementeren verschillende filialen toodifferent [sleuven](web-sites-staged-publishing.md).
* Alle implementatie-engine Kudu Hallo-functionaliteit is beschikbaar (bijvoorbeeld implementatie versiebeheer, terugdraaien, pakket herstellen, automatisering).

Nadelen van het implementeren van het lokale Git is:

* Enige kennis van Hallo respectieve SCM-systeem vereist.
* Er zijn geen directe oplossingen voor continue implementatie. 

### <a name="vsts"></a>Hoe toodeploy van lokale Git
In Hallo [Azure Portal](https://portal.azure.com), kunt u lokale Git-implementatie.

* [Lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md). 
* [Publiceren van Apps uit elke hg-git-opslagplaats tooWeb](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html).  

## <a name="deploy-using-an-ide"></a>Implementeren met behulp van een IDE
Als u al [Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) met een [Azure SDK](https://azure.microsoft.com/downloads/), of andere IDE-pakketten zoals [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org), en [ IntelliJ IDEA](https://www.jetbrains.com/idea/), kunt u tooAzure rechtstreeks vanuit uw IDE implementeren. Deze optie is ideaal voor een afzonderlijke ontwikkelaar.

Visual Studio ondersteunt alle drie implementatieprocessen (FTP, Git en Web Deploy), afhankelijk van uw voorkeur, terwijl andere IDE tooApp Service implementeren kunt, als ze FTP of Git-integratie hebben (Zie [overzicht van implementatieprocessen](#overview)).

Hallo-professionals van implementatie met behulp van een IDE zijn:

* Hallo tooling voor uw toepassing end-to-end-levenscyclus mogelijk minimaliseren. Ontwikkelen, foutopsporing, bijhouden en uw tooAzure app implementeren zonder het verplaatsen van buiten uw IDE. 

Hallo-nadelen van de implementatie met behulp van een IDE zijn:

* Extra complexiteit in tooling.
* Een bronbeheersysteem nog steeds vereist voor een teamproject.

<a name="vspros"></a>Er zijn aanvullende professionals implementeren met Visual Studio met Azure SDK:

* Azure SDK maakt Azure-resources klas burgers in Visual Studio. Maken, verwijderen, bewerken, starten en stoppen van apps, query Hallo back-end SQL-database, live-debug hello Azure-app en nog veel meer. 
* Live codebestanden in Azure worden bewerkt.
* Live foutopsporing van apps in Azure.
* Geïntegreerde Azure explorer.
* Diff-implementatie. 

### <a name="vs"></a>Hoe rechtstreeks toodeploy vanuit Visual Studio
* [Aan de slag met Azure en ASP.NET](app-service-web-get-started-dotnet.md). Hoe toocreate en een eenvoudige ASP.NET MVC-webproject implementeren met behulp van Visual Studio en Web Deploy.
* [Hoe tooDeploy met Visual Studio voor Azure WebJobs](websites-dotnet-deploy-webjobs.md). Hoe projecteert tooconfigure consoletoepassing zodat ze als WebJobs implementeren.  
* [ASP.NET Web Deployment met Visual Studio](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction). Een zelfstudie 12-onderdeel-serie die betrekking heeft op een uitgebreidere bereik implementatietaken dan Hallo anderen in deze lijst. Sommige functies van Azure-implementatie zijn toegevoegd sinds het Hallo-zelfstudie is geschreven, maar later toegevoegd opmerkingen wordt uitgelegd wat ontbreekt.
* [Een ASP.NET-Website tooAzure in Visual Studio 2012 uit een Git-opslagplaats rechtstreeks implementeren](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881). Legt uit hoe toodeploy een ASP.NET-web project in Visual Studio met Hallo Git invoegtoepassing toocommit Hallo code tooGit en verbinding maken met Azure toohello Git-opslagplaats. U start in Visual Studio 2013, Git-ondersteuning is ingebouwd en u hoeft de installatie van een invoegtoepassing.

### <a name="aztk"></a>Hoe Azure Toolkits met behulp van toodeploy Hallo voor Eclipse en IntelliJ IDEA
Microsoft maakt het mogelijk toodeploy Web-Apps tooAzure rechtstreeks vanuit de Eclipse en IntelliJ via Hallo [Azure Toolkit voor Eclipse](../azure-toolkit-for-eclipse.md) en [Azure Toolkit voor IntelliJ](../azure-toolkit-for-intellij.md). Hallo illustreren volgende zelfstudies Hallo stappen die betrokken zijn bij het implementeren van eenvoudige een 'Hallo' wereld Web-App tooAzure IDE met:

* [Een Hallo wereld Web-App maken voor Azure in Eclipse](app-service-web-eclipse-create-hello-world-web-app.md). Deze zelfstudie leert u hoe toouse hello Azure Toolkit voor Eclipse toocreate en implementeren van een Hallo wereld-Web-App voor Azure.
* [Een Hallo wereld Web-App maken voor Azure in IntelliJ](app-service-web-intellij-create-hello-world-web-app.md). Deze zelfstudie leert u hoe toouse hello Azure Toolkit voor IntelliJ toocreate en implementeren van een Hallo wereld-Web-App voor Azure.

## <a name="automate"></a>Implementatie automatiseren met behulp van de opdrachtregelprogramma 's
Als u liever Hallo opdrachtregelprogramma terminal als ontwikkelomgeving Hallo naar keuze, kunt u een script implementatietaken voor uw App Service-app met opdrachtregelprogramma's. 

Professionals implementeren met behulp van de opdrachtregelprogramma's zijn:

* Kan een script vastgelegd implementatiescenario's.
* Integreren met het inrichten van de Azure-resources en code-implementatie.
* Azure-implementatie integreren met bestaande continue integratie scripts.

Nadelen van de implementatie met behulp van de opdrachtregelprogramma's zijn:

* Niet voor ontwikkelaars GUI voorkeur.

### <a name="automatehow"></a>Hoe tooautomate implementatie met de opdrachtregelprogramma's

Zie [implementatie van uw app in Azure met opdrachtregelprogramma's automatiseren](app-service-deploy-command-line.md) voor een lijst met opdrachtregelprogramma tootutorials in hulpprogramma's en koppelingen. 

## <a name="nextsteps"></a>Volgende stappen
In sommige gevallen kunt u toobe kunnen tooeasily switch heen en weer tussen een faserings- en een productieversie van uw app. Zie voor meer informatie [gefaseerde implementatie op Web-Apps](web-sites-staged-publishing.md).

Als een plan voor back-up en herstel op plek is een belangrijk onderdeel van de werkstroom voor de implementatie. Zie voor meer informatie over het Hallo-App Service back-up en herstelfunctie [back-ups van Web Apps](web-sites-backup.md).  

Zie voor meer informatie over hoe toouse Azure toegangsbeheer op basis van rollen toomanage toegang krijgen tot de Service-implementatie tooApp [RBAC en Web-App Publishing](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/).

