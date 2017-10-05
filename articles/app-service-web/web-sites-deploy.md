---
title: Implementeer uw app in Azure App Service | Microsoft Docs
description: Informatie over het implementeren van uw app in Azure App Service.
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
ms.openlocfilehash: f41be4e00a9250b07ca260c2858e5fc45143f746
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-app-to-azure-app-service"></a>Implementeer uw app in Azure App Service
Dit artikel helpt u de beste optie voor het implementeren van de bestanden voor uw web-app, back-end voor mobiele app of API-app om te bepalen [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), en leidt u naar de juiste resources met instructies die specifiek zijn voor uw voorkeursoptie.

## <a name="overview"></a>Overzicht van Azure App Service-implementatie
Application framework onderhoudt-Azure App Service voor u (ASP.NET, PHP, Node.js, enzovoort). Sommige frameworks standaard terwijl anderen, zoals Java en Python zijn ingeschakeld, moet mogelijk een eenvoudige vinkje configuratie in te schakelen. Bovendien kunt u uw toepassingsframework, zoals de PHP-versie of de bitness van uw runtime aanpassen. Zie voor meer informatie [configureren van uw app in Azure App Service](web-sites-configure.md).

Omdat u geen zorgen te hoeven maken over de web server of toepassing framework, het implementeren van uw app in App Service is een kwestie van het implementeren van uw code, binaire bestanden, bestanden en hun respectieve mapstructuur op de [ **/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (of de **/site/wwwroot/App_Data/taken/** map voor WebJobs). App Service ondersteunt drie verschillende implementatieprocessen. De implementatiemethoden in dit artikel gebruik een van de volgende processen: 

* [FTP- of FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol): gebruik uw favoriete FTP of FTPS ingeschakeld hulpprogramma voor het verplaatsen van bestanden naar Azure van [FileZilla](https://filezilla-project.org) naar complete IDE zoals [NetBeans](https://netbeans.org). Dit is uitsluitend een uploadproces. Er zijn geen extra services worden geleverd door App Service, zoals versiebeheer, structuur bestandsbeheer, enz. 
* [Kudu (Git/volgt of OneDrive/Dropbox)](https://github.com/projectkudu/kudu/wiki/Deployment): Kudu is de [implementatie-engine](https://github.com/projectkudu/kudu/wiki) in App Service. Uw code naar Kudu rechtstreeks vanuit een opslagplaats forceren. Kudu biedt ook extra services wanneer code wordt doorgeschoven, zoals versiebeheer, pakket herstellen, MSBuild, en [web hooks](https://github.com/projectkudu/kudu/wiki/Web-hooks) voor continue implementatie en andere automatiseringstaken. De implementatie-engine Kudu ondersteunt 3 soorten implementatie bronnen:   
  
  * Inhoud synchroniseren vanuit OneDrive en Dropbox   
  * Doorlopende implementatie op basis van een opslagplaats met automatische synchronisatie van GitHub en Bitbucket Visual Studio Team Services  
  * Implementatie met handmatige synchronisatie uit lokale Git-opslagplaats gebaseerde  
* [Web Deploy](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy): code implementeren in App Service rechtstreeks van uw favoriete tools zoals Visual Studio met behulp van dezelfde tooling die automatiseert implementatie naar IIS-servers. Dit hulpprogramma ondersteunt diff-implementatie, het maken van de database, transformaties van verbindingsreeksen, enzovoort. Web Deploy verschilt van Kudu binaire bestanden van toepassingen voordat ze worden geïmplementeerd in Azure zijn ingebouwd. Net zoals bij FTP, er zijn geen extra services worden geleverd door App Service.

Populaire web ontwikkelingsprogramma's ondersteuning voor een of meer van deze van implementatieprocessen. Terwijl het hulpprogramma dat u kiest, de implementatieprocessen die u gebruikmaken van bepaalt kunt, afhankelijk van de werkelijke DevOps-functionaliteit tot uw beschikking staan de combinatie van het implementatieproces en de specifieke hulpprogramma's die u kiest. Bijvoorbeeld, als u Web Deploy uit uitvoeren [Visual Studio met Azure SDK](#vspros), zelfs als u geen automatisering van kudu Bovendien krijgt, u krijgt pakket herstellen en MSBuild-automatisering in Visual Studio. 

> [!NOTE]
> Deze implementatieprocessen niet daadwerkelijk [de Azure-resources inrichten](../azure-resource-manager/resource-group-template-deploy-portal.md) die uw app mogelijk nodig heeft. Echter de meeste van de gekoppelde artikelen met procedures laten zien hoe u de app inrichten en implementeren van uw code voor het end-to-end. U vindt ook aanvullende opties voor het inrichten van Azure-resources in de [implementatie automatiseren met behulp van de opdrachtregelprogramma's](#automate) sectie.
> 
> 

## <a name="ftp"></a>Handmatig implementeren door het uploaden van bestanden met FTP
Als u worden gebruikt om de inhoud van uw website handmatig kopiëren naar een webserver, kunt u een [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) hulpprogramma voor het kopiëren van bestanden, zoals Windows Verkenner of [FileZilla](https://filezilla-project.org/).

De professionals van handmatig kopiëren van bestanden zijn:

* Bekend zijn en de minimale complexiteit voor FTP-tooling. 
* Weten precies waar uw bestanden gaat.
* Extra beveiliging met FTPS.

De nadelen van het handmatig kopiëren van bestanden zijn:

* Hoeven weten hoe bestanden op de juiste mappen in App Service implementeren. 
* Er is geen versiebeheer voor terugdraaien als er fouten optreden.
* Er is geen ingebouwde implementatiegeschiedenis voor het oplossen van problemen bij de implementatie.
* Mogelijke lang implementatie tijden omdat veel FTP-hulpprogramma's niet diff-alleen kunnen worden gekopieerd en kopieer alle bestanden.  

### <a name="howtoftp"></a>Het uploaden van bestanden met FTP
De [Azure Portal](https://portal.azure.com) biedt u de informatie die u wilt verbinding maken met uw app adreslijsten met FTP- of FTPS.

* [Uw app implementeren in Azure App Service met FTP](app-service-deploy-ftp.md)

## <a name="dropbox"></a>Implementeren door te synchroniseren met een cloud-map
Een goed alternatief voor [u bestanden handmatig kopieert](#ftp) wordt gesynchroniseerd bestanden en mappen in App Service uit een cloud-opslagservice, zoals OneDrive en Dropbox. Synchroniseren met een map cloud maakt gebruik van de Kudu-proces voor de implementatie (Zie [overzicht van implementatieprocessen](#overview)).

De professionals van de synchronisatie met een cloud-map zijn:

* Eenvoud van implementatie. Services zoals OneDrive en Dropbox bieden bureaublad sync-clients, zodat uw lokale werkmap ook de directory van uw implementatie is.
* Implementatie met één klik.
* Alle functionaliteit in de implementatie-engine Kudu beschikbaar is (bijvoorbeeld pakket herstellen, automatisering).

De nadelen van de synchronisatie met een cloud-map zijn:

* Er is geen versiebeheer voor terugdraaien als er fouten optreden.
* Er is geen geautomatiseerde implementatie handmatig synchroniseren is vereist.

### <a name="howtodropbox"></a>Implementeren door te synchroniseren met een cloud-map
In de [Azure Portal](https://portal.azure.com), kunt u een map voor synchronisatie van inhoud in de cloudopslag OneDrive of Dropbox, werken met uw app-code en de inhoud in de map en synchroniseren in App Service met de op een knop te klikken.

* [Synchroniseren van de inhoud van een cloud-map in Azure App Service](app-service-deploy-content-sync.md). 

## <a name="continuousdeployment"></a>Continu implementeren vanuit een cloud-gebaseerde source control-service
Als uw ontwikkelteam gebruikmaakt van een cloud-gebaseerde source code management (SCM) service, zoals [Visual Studio Team Services](http://www.visualstudio.com/), [GitHub](https://www.github.com), of [BitBucket](https://bitbucket.org/), kunt u App Service voor het integreren in uw opslagplaats en continu implementeren. 

De professionals voor het implementeren van een cloud-gebaseerde source control-service zijn:

* Versiebeheer terugdraaien inschakelen.
* Mogelijkheid voor het configureren van continue implementatie voor Git (en volgt indien van toepassing) opslagplaatsen. 
* Implementatie van branchespecifieke verschillende filialen kunt implementeren naar andere [sleuven](web-sites-staged-publishing.md).
* Alle functionaliteit in de implementatie-engine Kudu beschikbaar is (bijvoorbeeld implementatie versiebeheer, terugdraaien, pakket herstellen, automatisering).

De con voor het implementeren van een cloud-gebaseerde source control-service is:

* Enige kennis van de respectieve SCM-service vereist.

### <a name="vsts"></a>Continu implementeren van een cloud-gebaseerde source control-service
In de [Azure Portal](https://portal.azure.com), kunt u continue implementatie van GitHub en Bitbucket Visual Studio Team Services configureren.

* [Continue implementatie in Azure App Service](app-service-continuous-deployment.md). 

Voor informatie over het configureren van continue implementatie handmatig van een cloud-opslagplaats niet vermeld in de Azure-Portal (zoals [GitLab](https://gitlab.com/)), Zie [instellen van continue implementatie met handmatige stappen](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="localgitdeployment"></a>Implementeren vanaf de lokale Git
Als uw ontwikkelteam gebruikmaakt van een lokale lokale bron code management (SCM) service op basis van Git, kunt u dit configureren als een implementatiebron in App Service. 

Professionals voor het implementeren van lokale Git zijn:

* Versiebeheer terugdraaien inschakelen.
* Implementatie van branchespecifieke verschillende filialen kunt implementeren naar andere [sleuven](web-sites-staged-publishing.md).
* Alle functionaliteit in de implementatie-engine Kudu beschikbaar is (bijvoorbeeld implementatie versiebeheer, terugdraaien, pakket herstellen, automatisering).

Nadelen van het implementeren van het lokale Git is:

* Enige kennis van het respectieve SCM-systeem vereist.
* Er zijn geen directe oplossingen voor continue implementatie. 

### <a name="vsts"></a>Het implementeren van lokale Git
In de [Azure Portal](https://portal.azure.com), kunt u lokale Git-implementatie.

* [Lokale Git-implementatie in Azure App Service](app-service-deploy-local-git.md). 
* [Publiceren op Web-Apps uit elke hg-git-opslagplaats](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html).  

## <a name="deploy-using-an-ide"></a>Implementeren met behulp van een IDE
Als u al [Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) met een [Azure SDK](https://azure.microsoft.com/downloads/), of andere IDE-pakketten zoals [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org), en [IntelliJ IDEA](https://www.jetbrains.com/idea/), u kunt implementeren naar Azure rechtstreeks vanuit uw IDE. Deze optie is ideaal voor een afzonderlijke ontwikkelaar.

Visual Studio ondersteunt alle drie implementatieprocessen (FTP, Git en Web Deploy), afhankelijk van uw voorkeur, terwijl andere IDE in App Service implementeren kunt als ze FTP of Git-integratie hebben (Zie [overzicht van implementatieprocessen](#overview)).

De professionals van implementatie met behulp van een IDE zijn:

* Mogelijk minimaliseert de tooling voor uw toepassing end-to-end-levenscyclus. Ontwikkelen, foutopsporing, volgen en een app implementeren in Azure alle zonder het verplaatsen van buiten uw IDE. 

De nadelen van de implementatie met behulp van een IDE zijn:

* Extra complexiteit in tooling.
* Een bronbeheersysteem nog steeds vereist voor een teamproject.

<a name="vspros"></a>Er zijn aanvullende professionals implementeren met Visual Studio met Azure SDK:

* Azure SDK maakt Azure-resources klas burgers in Visual Studio. Maken, verwijderen, bewerken, starten, en apps stoppen, zoeken in de back-end SQL-database, de Azure-app en nog veel meer live-debug. 
* Live codebestanden in Azure worden bewerkt.
* Live foutopsporing van apps in Azure.
* Geïntegreerde Azure explorer.
* Diff-implementatie. 

### <a name="vs"></a>Het rechtstreeks vanuit Visual Studio implementeren
* [Aan de slag met Azure en ASP.NET](app-service-web-get-started-dotnet.md). Het maken en een eenvoudige ASP.NET MVC-webproject implementeren met behulp van Visual Studio en Web Deploy.
* [Hoe Azure WebJobs implementeren met Visual Studio](websites-dotnet-deploy-webjobs.md). Klik hier voor meer informatie over het consoletoepassing projecten zodanig configureren dat ze als WebJobs implementeren.  
* [ASP.NET Web Deployment met Visual Studio](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction). Een zelfstudie 12-onderdeel-serie die betrekking heeft op een uitgebreidere bereik implementatietaken dan de andere in deze lijst. Sommige functies van Azure-implementatie zijn toegevoegd sinds de zelfstudie is geschreven, maar later toegevoegd opmerkingen wordt uitgelegd wat ontbreekt.
* [Implementeren van een ASP.NET-Website naar Azure in Visual Studio 2012 van een Git-opslagplaats rechtstreeks](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881). Legt uit hoe voor het implementeren van een ASP.NET-webproject in Visual Studio met behulp van de invoegtoepassing Git doorvoeren van de code aan Git en verbindende Azure aan de Git-opslagplaats. U start in Visual Studio 2013, Git-ondersteuning is ingebouwd en u hoeft de installatie van een invoegtoepassing.

### <a name="aztk"></a>Het implementeren van de Azure-Toolkits voor Eclipse en IntelliJ IDEA gebruiken
Microsoft maakt het mogelijk voor de implementatie van Web-Apps naar Azure rechtstreeks vanaf Eclipse en IntelliJ via de [Azure Toolkit voor Eclipse](../azure-toolkit-for-eclipse.md) en [Azure Toolkit voor IntelliJ](../azure-toolkit-for-intellij.md). De volgende zelfstudies ziet u de stappen die betrokken zijn bij het implementeren van eenvoudige een 'Hallo' wereld Web-App in Azure maken met beide IDE:

* [Een Hallo wereld Web-App maken voor Azure in Eclipse](app-service-web-eclipse-create-hello-world-web-app.md). Deze zelfstudie laat zien hoe u met de Azure-werkset voor Eclipse maken en implementeren van een Hello World Web-App voor Azure.
* [Een Hallo wereld Web-App maken voor Azure in IntelliJ](app-service-web-intellij-create-hello-world-web-app.md). Deze zelfstudie laat zien hoe de Azure-werkset voor IntelliJ gebruiken voor het maken en implementeren van een Hello World Web-App voor Azure.

## <a name="automate"></a>Implementatie automatiseren met behulp van de opdrachtregelprogramma 's
Als u de opdrachtregeloptie terminal liever als ontwikkelomgeving naar keuze, kunt u een script implementatietaken voor uw App Service-app met opdrachtregelprogramma's. 

Professionals implementeren met behulp van de opdrachtregelprogramma's zijn:

* Kan een script vastgelegd implementatiescenario's.
* Integreren met het inrichten van de Azure-resources en code-implementatie.
* Azure-implementatie integreren met bestaande continue integratie scripts.

Nadelen van de implementatie met behulp van de opdrachtregelprogramma's zijn:

* Niet voor ontwikkelaars GUI voorkeur.

### <a name="automatehow"></a>Implementatie met de opdrachtregelprogramma's automatiseren

Zie [implementatie van uw app in Azure met opdrachtregelprogramma's automatiseren](app-service-deploy-command-line.md) voor een lijst met de opdrachtregelprogramma's en koppelingen naar zelfstudies. 

## <a name="nextsteps"></a>Volgende stappen
In sommige gevallen is het raadzaam kunnen eenvoudig heen en weer schakelen tussen een faserings- en een productieversie van uw app. Zie voor meer informatie [gefaseerde implementatie op Web-Apps](web-sites-staged-publishing.md).

Als een plan voor back-up en herstel op plek is een belangrijk onderdeel van de werkstroom voor de implementatie. Voor informatie over de App Service back-up en herstellen van de functie, Zie [back-ups van Web Apps](web-sites-backup.md).  

Zie voor meer informatie over het gebruik van Azure op rollen gebaseerde toegangsbeheer voor het beheren van toegang tot de App Service-implementatie [RBAC en Web-App Publishing](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/).

