---
title: aaaIntroduction tooAzure beveiliging | Microsoft Docs
description: Meer informatie over Azure-beveiliging, de services en hoe het werkt.
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/03/2017
ms.author: TomSh
ms.openlocfilehash: 2d42057e9586a0b6ce16a1582db3b3af842297af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security"></a>Inleiding tooAzure beveiliging
## <a name="overview"></a>Overzicht
We weten dat beveiliging taak in de cloud Hallo en het is belangrijk dat u tijdig en informatie over Azure-beveiliging. Een van de Hallo beste redenen-toouse Azure voor uw toepassingen en services is tootake profiteren van de breed scala aan mogelijkheden en hulpprogramma's voor beveiliging. Deze hulpprogramma's en mogelijkheden helpen mogelijke toocreate veilige oplossingen maken op Hallo beveiligde Azure-platform. Microsoft Azure biedt vertrouwelijkheid, integriteit en beschikbaarheid van klantgegevens, maar ook transparante accountability.

Hallo-verzameling van beveiligingsmechanismen geïmplementeerd in Microsoft Azure vanuit Microsoft bewerkingen en Hallo klant perspectieven, deze witboek 'Inleiding tooAzure beveiliging', beter te begrijpen toohelp tooprovide wordt geschreven een uitgebreide bekijkt hello beveiliging met Microsoft Azure.

### <a name="azure-platform"></a>Azure-Platform
Azure is een openbare cloud service-platform die ondersteuning biedt voor een brede selectie van besturingssystemen, programmeertalen, frameworks, hulpprogramma's, databases, en apparaten. Linux-containers kan worden uitgevoerd met Docker-integratie; bouwen van apps met JavaScript, Python, .NET, PHP, Java en Node.js; Build back-ends voor iOS, Android en Windows apparaten.

Hallo van dezelfde technologieën miljoenen van ontwikkelaars en IT-professionals al zijn afhankelijk van en vertrouwen wordt ondersteund door Azure openbare cloud-services. Wanneer u bouwen op of IT-activa te migreren, een openbare cloud serviceprovider u zijn afhankelijk te zijn van die organisatie mogelijkheden tooprotect uw toepassingen en gegevens met Hallo services en Hallo besturingselementen ze bieden toomanage Hallo beveiliging van uw cloud-gebaseerde activa.

Azure infrastructuur is speciaal ontworpen van faciliteit tooapplications voor het hosten van miljoenen klanten tegelijkertijd en biedt een betrouwbare basis waarop bedrijven kunnen voldoen aan de beveiligingsvereisten.

Bovendien Azure biedt u een breed scala aan configureerbare beveiliging opties en Hallo mogelijkheid toocontrol ze zodat u beveiliging toomeet Hallo unieke vereisten van uw organisatie implementaties kunt aanpassen. Dit document helpt u begrijpen hoe Azure-beveiliging mogelijkheden kunt u aan deze vereisten voldoen.

> [!Note]
> Hallo dit document richt zich voornamelijk op klantgerichte besturingselementen toocustomize gebruiken en betere beveiliging voor uw toepassingen en services.
>
> We bieden sommige overzichtsinformatie, maar Azure-platform zelf, Zie voor gedetailleerde informatie over hoe Microsoft hello beveiligt informatie in Hallo [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/default.aspx).

### <a name="abstract"></a>Abstracte
Openbare Clouds migraties zijn in eerste instantie wordt aangestuurd door kosten besparen en aanpassingsvermogen tooinnovate. Beveiliging wordt beschouwd als een groot belang voor enige tijd en zelfs een weergeven Stop voor migratie van de openbare cloud. Echter, openbare cloud security is overgegaan van een primaire problematisch tooone Hallo stuurprogramma's voor cloudmigratie. Hallo logica achter dit is Hallo bovenliggende mogelijkheid van grote openbare cloud serviceproviders tooprotect toepassingen en gegevens Hallo van cloud-gebaseerde activa.

Azure infrastructuur is speciaal ontworpen van Hallo faciliteit tooapplications voor het hosten van miljoenen klanten tegelijkertijd en biedt een betrouwbare basis waarop bedrijven hun beveiliging behoeften kunnen. Bovendien Azure biedt u een breed scala aan configureerbare beveiliging opties en Hallo mogelijkheid toocontrol ze zodat u kunt aanpassen toomeet Hallo unieke beveiligingsvereisten van uw implementaties toomeet uw IT-afdeling toegangsbeheerbeleid en tooexternal voldoen voorschriften.

Dit artikel bevat een overzicht van Microsoft benadering toosecurity binnen Hallo Microsoft Azure cloud-platform:
* Beveiligingsfuncties die zijn geïmplementeerd door Microsoft toosecure hello Azure-infrastructuur, klantgegevens en toepassingen.
* Azure-services en beveiliging functies beschikbaar tooyou toomanage hello beveiliging van Hallo Services en uw gegevens in uw Azure-abonnementen.

## <a name="summary-azure-security-capabilities"></a>Overzicht Azure beveiligingsmogelijkheden
Hallo tabel hieronder bieden een korte beschrijving van beveiligingsfuncties Hallo geïmplementeerd door Microsoft toosecure hello Azure-infrastructuur, klantgegevens en beveiligde toepassingen.
### <a name="security-features-implemented-toosecure-hello-azure-platform"></a>Beveiliging functies geïmplementeerd tooSecure hello Azure-Platform:
Hallo functies vermeld na zijn mogelijkheden die kunt u tooprovide Hallo zekerheid dat hello die Azure-Platform wordt beheerd op een veilige manier bekijken. Koppelingen zijn opgegeven voor verdere Inzoomen op hoe Microsoft vragen van klanten vertrouwen in vier gebieden adressen: Secure Platform, Privacy en besturingselementen, naleving en transparantie.


| [Veilig Platform](https://www.microsoft.com/en-us/trustcenter/Security/default.aspx)  | [Privacy en besturingselementen](https://www.microsoft.com/en-us/trustcenter/Privacy/default.aspx)  |[Naleving](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)   | [Transparantie](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| :-- | :-- | :-- | :-- |
| [Beveiligingsontwikkeling opstellen](https://www.microsoft.com/en-us/sdl/), interne controles | [Alle Hallo-tijd van uw gegevens beheren](https://www.microsoft.com/en-us/trustcenter/Privacy/You-own-your-data) | [Vertrouwenscentrum](https://www.microsoft.com/en-us/trustcenter/default.aspx) |[Hoe Microsoft beveiligt de gegevens van de klant in de Azure-services](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| [Verplichte beveiligingstraining, achtergrond controles](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc) |  [Op de locatie van gegevens beheren](https://www.microsoft.com/en-us/trustcenter/Privacy/Where-your-data-is-located) |  [Algemene besturingselementen Hub](https://www.microsoft.com/en-us/trustcenter/Common-Controls-Hub) |[Hoe de locatie van gegevens in Azure-services voor het beheren van Microsoft](http://azuredatacentermap.azurewebsites.net/)|
| [Testen van binnendringen](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc), [inbraakdetectie, DDoS](https://www.microsoft.com/en-us/trustcenter/Security/ThreatManagemen), [Audits & logboekregistratie](https://www.microsoft.com/en-us/trustcenter/Security/AuditingAndLogging) | [Gegevenstoegang bieden op uw eigen voorwaarden](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms) |  [Hallo Cloud-Services vanwege toewijding inzetten controlelijst](https://www.microsoft.com/en-us/trustcenter/Compliance/Due-Diligence-Checklist) |[Wie in Microsoft kan toegang tot uw gegevens op welke voorwaarden](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms)|
| [Status van de illustraties Datacenter](https://www.microsoft.com/en-us/cloud-platform/global-datacenters), fysieke beveiliging [beveiligd netwerk](https://docs.microsoft.com/en-us/azure/security/security-network-overview) | [Reageert toolaw afdwingen](https://www.microsoft.com/en-us/trustcenter/Privacy/Responding-to-govt-agency-requests-for-customer-data) |  [Naleving door service, de locatie en de branche](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx) |[Hoe Microsoft beveiligt de gegevens van de klant in de Azure-services](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx)|
|  [Security Incident response](http://aka.ms/SecurityResponsepaper), [verantwoordelijkheid gedeeld](http://aka.ms/sharedresponsibility) |[Strikte privacystandaarden](https://www.microsoft.com/en-us/TrustCenter/Privacy/We-set-and-adhere-to-stringent-standards) |  | [Certificeringsinstantie voor Azure-services, transparantie hub controleren](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)|



### <a name="security-features-offered-by-azure-toosecure-data-and-application"></a>Beveiliging functies die worden aangeboden door Azure tooSecure gegevens en toepassingen
Afhankelijk van Hallo cloudservicemodel is het er variabele verantwoordelijk is voor wie verantwoordelijk is voor het beheren van Hallo beveiliging van Hallo toepassing of service. Er zijn mogelijkheden beschikbaar in hello Azure-Platform tooassist u voor het voldoen aan deze verantwoordelijkheden via ingebouwde functies en via partneroplossingen die kan worden geïmplementeerd in een Azure-abonnement.

Hallo ingebouwde mogelijkheden zijn georganiseerd in functiegebieden zes (6): bewerkingen, toepassingen, opslag, netwerken, berekening en identiteit. Via samenvattende informatie vindt u aanvullende details over Hallo functies en mogelijkheden beschikbaar in hello Azure-Platform op deze gebieden zes (6).

## <a name="operations"></a>Bewerkingen
Deze sectie bevat overzichtsinformatie over deze mogelijkheden en aanvullende informatie met betrekking tot belangrijke functies in beveiligingsbewerkingen.

### <a name="operations-management-suite-security-and-audit-dashboard"></a>Beveiliging van operations Management Suite en Audit-Dashboard
Hallo [OMS beveiligings- en Audit oplossing](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) biedt een uitgebreid overzicht van uw organisatie IT beveiligingspostuur met [ingebouwde zoekquery's](https://blogs.technet.microsoft.com/msoms/2016/01/21/easy-microsoft-operations-management-suite-search-queries/) voor problemen die aandacht vereisen die uw aandacht vereisen. Hallo [beveiligings- en Audit](https://technet.microsoft.com/library/mt484091.aspx) dashboard is Hallo startscherm voor van alles aan elkaar gerelateerd toosecurity in OMS. Het biedt op hoog niveau inzicht in de Hallo beveiligingsstatus van uw computers. Dit omvat ook Hallo mogelijkheid tooview alle gebeurtenissen uit Hallo afgelopen 24 uur, 7 dagen of een andere aangepaste tijdsbestek.

Bovendien kunt u configureren OMS-beveiliging en naleving te[automatisch bepaalde acties uitvoeren](https://blogs.technet.microsoft.com/robdavies/2016/04/20/simple-look-at-oms-alert-remediation-with-runbooks-part-1/) wanneer een bepaalde gebeurtenis wordt gedetecteerd.

### <a name="azure-resource-manager"></a>Azure Resource Manager
[Azure Resource Manager ](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model) kunt u toowork met Hallo resources in uw oplossing als een groep. U kunt implementeren, bijwerken of verwijderen van alle Hallo resources voor uw oplossing in een enkele, gecoördineerde bewerking. U gebruikt een [Azure Resource Manager-sjabloon](https://blogs.technet.microsoft.com/canitpro/2015/06/29/devops-basics-infrastructure-as-code-arm-templates/) voor implementatie en dat de sjabloon voor verschillende omgevingen zoals testen, Faseren en productie werken kunnen. Resource Manager biedt beveiliging, controle en functies toohelp tagging u uw resources beheren na implementatie.

Azure implementaties van Resource Manager-sjabloon gebaseerde beveiliging te verbeteren Hallo van oplossingen die zijn geïmplementeerd in Azure, omdat de standaardbeveiliging-instellingen beheren en kan worden geïntegreerd in implementaties van gestandaardiseerde op basis van een sjabloon. Dit vermindert het risico van Hallo beveiligingsfouten configuratie die tijdens handmatige-implementaties kan plaatsvinden.

### <a name="application-insights"></a>Application Insights
[Application Insights](https://docs.microsoft.com/azure/application-insights/) is een uitbreidbaar Management APM (Application Performance)-service voor webontwikkelaars. Met Application Insights kunt u uw live webtoepassingen bewaken en afwijkingen automatisch detecteren. Dit omvat krachtige analytics extra toohelp onderzoeken van problemen en toounderstand wat gebruikers daadwerkelijk met uw apps doen. Het bewaakt uw toepassing alle Hallo tijd uitgevoerd, zowel tijdens het testen en nadat u hebt gepubliceerd of geïmplementeerd.

Application Insights grafieken en tabellen die u maakt, bijvoorbeeld welke tijdstippen ophalen van de meeste gebruikers hoe responsief Hallo-app is en hoe deze in behandeling is genomen door een externe bron services waar deze afhankelijk is van.

Als er crashes, fouten of prestatieproblemen, kunt u zoeken via Hallo telemetrische gegevens in detail toodiagnose Hallo oorzaak. En Hallo-service stuurt u e-mailberichten als er wijzigingen in Hallo beschikbaarheid en prestaties van uw app. Toepassing inzicht wordt dus een waardevolle beveiligingsprogramma omdat hiermee met Hallo beschikbaarheid in Hallo vertrouwelijkheid, integriteit en beschikbaarheid beveiliging drie vakken.

### <a name="azure-monitor"></a>Azure Monitor
[Monitor voor Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) biedt visualisatie, query routering, waarschuwingen, automatisch schalen en automatisering van gegevens, zowel van hello Azure-infrastructuur ([activiteitenlogboek](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)) en elke afzonderlijke Azure-resource ([ Diagnostische logboeken](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)). U kunt Azure Monitor tooalert u van beveiliging gerelateerde gebeurtenissen die worden gegenereerd in Logboeken op Azure.

### <a name="log-analytics"></a>Log Analytics
[Meld u Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) deel uit van [Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite) – vindt u een oplossing voor IT-beheer voor zowel on-premises en cloud-gebaseerde infrastructuur hebben van derden (zoals AWS) bovendien tooAzure bronnen. Gegevens uit Azure Monitor kan worden gerouteerd rechtstreeks tooLog Analytics zodat u Logboeken en metrische gegevens voor uw hele omgeving op één plek kunt zien.

Log Analytics zijn een handig hulpmiddel in forensische en andere beveiligingsanalyse Hallo hulpprogramma kunt u tooquickly zoeken door grote hoeveelheden beveiliging gerelateerde vermeldingen met een flexibele queryfunctionaliteit benadering. Bovendien lokale [firewall en proxy-logboeken kunnen worden geëxporteerd naar Azure en beschikbaar gesteld voor analyse met behulp van logboekanalyse.](https://docs.microsoft.com/azure/log-analytics/log-analytics-proxy-firewall)

### <a name="azure-advisor"></a>Azure Advisor
[Azure Advisor](https://docs.microsoft.com/azure/advisor/) is een persoonlijke cloud-consultant waarmee u toooptimize uw Azure-implementaties. Advisor analyseert de configuratie van uw resources en de gebruiksgerelateerde telemetrie. Het oplossingen vervolgens beveelt toohelp verbeteren Hallo [prestaties](https://docs.microsoft.com/azure/advisor/advisor-performance-recommendations), [beveiliging](https://docs.microsoft.com/azure/advisor/advisor-security-recommendations), en [hoge beschikbaarheid](https://docs.microsoft.com/azure/advisor/advisor-high-availability-recommendations) van uw resources tijdens het zoeken naar mogelijkheden te[reduceren uw algehele Azure besteden](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations). Azure Advisor bevat aanbevelingen voor beveiliging, aanzienlijk kan verbeteren de algehele beveiligingsstatus voor oplossingen die u in Azure implementeren. Deze aanbevelingen zijn afkomstig van beveiligingsanalyse uitgevoerd door [Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-intro)

### <a name="azure-security-center"></a>Azure Security Center
[Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) helpt u te voorkomen, detecteren, en toothreats reageren met een verhoogde zichtbaarheid van en controle over Hallo beveiliging van uw Azure-resources. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt bedreigingen te detecteren die anders onopgemerkt zouden blijven, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.

Bovendien Azure Security Center helpt met beveiligingsbewerkingen doordat u een dashboard dat verwerkingsinformatie waarschuwingen en aanbevelingen die kunnen worden gereageerd onmiddellijk. U kunt vaak problemen met een enkele klik binnen hello Azure Security Center-console herstellen.
## <a name="applications"></a>Toepassingen
Hallo gedeelte bevat aanvullende informatie met betrekking tot belangrijke functies in de toepassing beveiligings- en samenvatting informatie over deze mogelijkheden.

### <a name="web-application-vulnerability-scanning"></a>Web Application beveiligingslek scannen
Een van de eenvoudigste manieren tooget Hallo gestart met het testen op beveiligingsproblemen op uw [App Service-app](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is) toouse Hallo is [integratie met Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) tooperform één muisklik beveiligingslek scannen op uw app. U kunt de resultaten bekijkt hello weergeven in een rapport gemakkelijk te begrijpen en meer informatie hoe toofix elk beveiligingsprobleem met stapsgewijze instructies.

### <a name="penetration-testing"></a>Indringingstests
Als u liever tooperform uw eigen binnendringen test of een andere scanner suite of provider toouse wilt, moet u Hallo volgen [Azure binnendringen goedkeuringsproces testen](https://security-forms.azure.com/penetration-testing/terms) en voorafgaande goedkeuring tooperform Hallo gewenst binnendringen ophalen Test.

### <a name="web-application-firewall"></a>Web Application firewall
web application firewall (WAF) in Hallo [Azure Application Gateway](https://azure.microsoft.com/services/application-gateway/) helpt webtoepassingen te beschermen tegen veelvoorkomende web gebaseerde aanvallen zoals SQL-injectie, cross-site scripting aanvallen en sessiehijacking. Het is vooraf geconfigureerd met beveiliging tegen bedreigingen die zijn geïdentificeerd door Hallo [Open Web Application Security Project (OWASP) als Hallo top 10 veelvoorkomende beveiligingslekken](https://msdn.microsoft.com/library/).

### <a name="authentication-and-authorization-in-azure-app-service"></a>Verificatie en autorisatie in Azure App Service
[App Service-verificatie / autorisatie](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) is een functie die een manier voor uw toepassing toosign in gebruikers, biedt zodat u geen toochange code op Hallo app back-end hebt. Het biedt een eenvoudige manier tooprotect uw toepassing en werk gegevens per gebruiker.

### <a name="layered-security-architecture"></a>Gelaagde beveiligingsarchitectuur
Aangezien [App Service-omgevingen](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-intro) voorziet in een geïsoleerde runtime-omgeving geïmplementeerd in een [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview), kunnen ontwikkelaars een gelaagd beveiligingsarchitectuur bieden verschillende niveaus van toegang tot het netwerk voor elke toepassingslaag maken. Een algemene streven toohide API-back-ends van algemene toegang tot het Internet is en dat alleen API's toobe aangeroepen door de upstream-web-apps. [Netwerkbeveiligingsgroepen (nsg's)](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/) op Azure Virtual Network subnetten met App Service-omgevingen toorestrict openbare toegang tooAPI toepassingen kunnen worden gebruikt.

### <a name="web-server-diagnostics-and-application-diagnostics"></a>Web server diagnostics en application diagnostics
App Service-web-apps bieden diagnostische functionaliteit voor logboekinformatie van zowel Hallo-webserver en Hallo-webtoepassing. Deze logisch zijn verdeeld in [web server diagnostische](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) en [application diagnostics](https://technet.microsoft.com/library/hh530058(v=sc.12).aspx). Webserver bevat twee belangrijke ontwikkelingen bij het opsporen en oplossen van sites en toepassingen.

de eerste nieuwe functie Hallo is realtime statusinformatie over groepen van toepassingen, werkprocessen, sites, toepassingsdomeinen en uitvoeren van aanvragen. Hallo tweede nieuwe voordelen zijn Hallo Gedetailleerde traceringsgebeurtenissen die een aanvraag tijdens de volledige aanvraag / antwoord-proces Hallo bijhouden.

IIS 7 mag tooenable Hallo-verzameling van deze traceringsgebeurtenissen, geconfigureerde tooautomatically vastleggen volledige traceerlogboeken in XML-indeling voor een bepaalde aanvraag op basis van de verstreken tijd of fout responscodes.

#### <a name="web-server-diagnostics"></a>Web server diagnostische gegevens
U kunt in- of uitschakelen van Hallo soorten logboeken te volgen:

-   Gedetailleerde foutregistratie - gedetailleerde informatie over de fout voor HTTP-statuscodes die wijzen op mislukte (statuscode 400 of hoger). Dit kan bevatten informatie om te bepalen waarom Hallo server Hallo foutcode geretourneerd.

-   Tracering van mislukte aanvragen - gedetailleerde informatie over de mislukte aanvragen, met inbegrip van een tracering van Hallo IIS componenten gebruikt tooprocess Hallo aanvraag en Hallo-tijd benodigd in elk onderdeel. Dit is handig als u de siteprestaties tooincrease probeert of isoleren wat de oorzaak van een specifieke HTTP-fout toobe geretourneerd.

-   Web Server-logboekregistratie - informatie over HTTP transacties met uitgebreide Hallo W3C-logboekindeling. Dit is handig bij het bepalen van de algemene site metrische gegevens zoals het aantal aanvragen dat is verwerkt Hallo of hoeveel aanvragen van een specifiek IP-adres.

#### <a name="application-diagnostics"></a>Application diagnostics
[Application diagnostics](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) kunt u toocapture informatie die wordt geproduceerd door een webtoepassing. ASP.NET-toepassingen kunnen gebruikmaken van Hallo [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) klasse toolog informatie toohello application diagnostics melden. In Application Diagnostics, er zijn twee belangrijke gebeurtenistypen, die verband houden met tooapplication prestaties en gerelateerde tooapplication storingen en fouten. Hallo storingen en fouten kunnen worden onderverdeeld in connectiviteit, beveiliging en fout-problemen. Systeemfouten worden doorgaans gerelateerde tooa probleem met de toepassingscode Hallo.

In Application Diagnostics, kunt u gebeurtenissen gegroepeerd op de volgende manieren weergeven:

-   Alle (alle gebeurtenissen weergegeven)
-   Toepassingsfouten (uitzonderingsgebeurtenissen worden weergegeven)
-   Prestaties (prestatiegebeurtenissen worden weergegeven)

## <a name="storage"></a>Storage
Hallo gedeelte bevat aanvullende informatie met betrekking tot belangrijke functies in Azure storage beveiligings- en samenvatting informatie over deze mogelijkheden.

### <a name="role-based-access-control-rbac"></a>RBAC (op rollen gebaseerd toegangsbeheer)
U kunt uw storage-account met op rollen gebaseerde toegangsbeheer (RBAC) beveiligen. De toegang beperken op basis van Hallo [moet tooknow](https://en.wikipedia.org/wiki/Need_to_know) en [minimale bevoegdheden](https://en.wikipedia.org/wiki/Principle_of_least_privilege) beveiligingsprincipes is van cruciaal belang voor organisaties die tooenforce beveiligingsbeleid voor toegang tot gegevens willen. Deze toegangsrechten worden verleend door Hallo juiste RBAC-rol toogroups en toepassingen op een bepaalde scope. U kunt [ingebouwde RBAC-rollen](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles), zoals opslag Account Inzender, tooassign toousers bevoegdheden. Toegangssleutels toohello opslag voor een opslagaccount met Hallo [Azure Resource Manager](https://docs.microsoft.com/azure/storage/storage-security-guide) model kan worden beheerd via op rollen gebaseerde toegangsbeheer (RBAC).

### <a name="shared-access-signature"></a>Shared Access Signature
Een [shared access signature (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) tooresources gedelegeerde toegang in uw opslagaccount biedt. Hallo SAS betekent dat u een client beperkte machtigingen tooobjects in uw storage-account voor een opgegeven periode en met een opgegeven set machtigingen kunt verlenen. U kunt deze beperkte rechten verlenen zonder tooshare de toegangssleutels van uw account.

### <a name="encryption-in-transit"></a>Codering in Transit
Versleuteling onderweg is een mechanisme om gegevens te beveiligen wanneer deze worden verzonden via netwerken. U kunt beveiligen met behulp van gegevens met Azure Storage:
-   [Versleuteling transportniveau](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit), zoals HTTPS wanneer u gegevens van of naar Azure Storage overbrengen.

-   [Versleuteling Wire](https://docs.microsoft.com/azure/storage/storage-security-guide#using-encryption-during-transit-with-azure-file-shares), zoals [versleuteling door SMB 3.0](https://docs.microsoft.com/azure/storage/storage-security-guide) voor [Azure-bestandsshares](https://docs.microsoft.com/azure/storage/storage-dotnet-how-to-use-files).

-   Versleuteling aan clientzijde, tooencrypt Hallo gegevens voordat deze worden overgedragen naar de opslag en toodecrypt Hallo gegevens nadat deze zijn overgebracht buiten-opslag.

### <a name="encryption-at-rest"></a>Versleuteling 'at rest'
Gegevensversleuteling in rust is voor veel organisaties een verplichte stap naar de privacy van gegevens, naleving en onafhankelijkheid van gegevens. Er zijn drie Azure storage-beveiligingsfuncties die versleuteling van gegevens die zich 'in rust' bieden:

-   [Versleuteling van de opslagruimte](https://docs.microsoft.com/azure/storage/storage-service-encryption) kunt u toorequest dat Hallo storage-service automatisch coderen van gegevens bij het schrijven van tooAzure opslag.

-   [Versleuteling aan clientzijde](https://docs.microsoft.com/azure/storage/storage-client-side-encryption) biedt ook de functie Hallo van versleuteling in rust.

-   [Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) kunt u tooencrypt Hallo OS schijven en gegevensschijven die wordt gebruikt door een virtuele machine voor IaaS.

### <a name="storage-analytics"></a>Storage Analytics
[Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) voert logboekregistratie en voorziet in metrische gegevens voor een opslagaccount. U kunt deze gegevensaanvragen tootrace gebruiken, trends in gebruik analyseren en vaststellen van problemen met uw opslagaccount. Storage Analytics registreert gedetailleerde informatie over geslaagde en mislukte aanvragen tooa storage-service. Deze informatie kan worden gebruikt toomonitor afzonderlijke aanvragen en toodiagnose problemen met de storage-service. Aanvragen worden geregistreerd op basis van best-effort. Hallo volgende typen geverifieerde aanvragen worden geregistreerd:
-   Geslaagde aanvragen.

-   Mislukte aanvragen, met inbegrip van de time-outperiode, beperking, netwerk, autorisatie en andere fouten.

-   -Aanvragen via een Shared Access Signature (SAS), met inbegrip van mislukte en geslaagde aanvragen.

-   Aanvragen tooanalytics gegevens.

### <a name="enabling-browser-based-clients-using-cors"></a>Browser gebaseerde Clients met behulp van CORS inschakelen
[Cross-Origin-Resource delen (CORS)](https://docs.microsoft.com/rest/api/storageservices/fileservices/cross-origin-resource-sharing--cors--support-for-the-azure-storage-services) is een mechanisme waarmee domeinen toogive elkaar machtiging voor toegang tot elkaars bronnen. Hallo gebruikersagent verzendt extra headers tooensure dat is toegestaan Hallo JavaScript-code geladen vanaf een bepaald domein tooaccess bronnen op een ander domein. Hallo laatstgenoemde domein beantwoordt vervolgens met extra kopteksten toegang verlenen of weigeren Hallo oorspronkelijke domein tooits resources.

Azure storage-services bieden nu ondersteuning voor CORS zodat zodra u Hallo CORS-regels voor Hallo service hebt ingesteld, een correct geverifieerde aanvraag tegen Hallo-service uit een ander domein geëvalueerde toodetermine of het is toegestaan op basis van toohello regels die u hebt opgegeven.
## <a name="networking"></a>Netwerken
Hallo gedeelte bevat aanvullende informatie met betrekking tot belangrijke functies in Azure-netwerk beveiligings- en samenvatting informatie over deze mogelijkheden.

### <a name="network-layer-controls"></a>Laag netwerkfuncties
Netwerktoegangsbeheer wordt Hallo van de beperkende connectiviteit tooand van specifieke apparaten of subnetten en vertegenwoordigt Hallo core van netwerkbeveiliging. Hallo-doel van netwerktoegangsbeheer is toomake ervoor dat uw virtuele machines en services toegankelijk tooonly gebruikers zijn en apparaten toowhich u wilt dat ze toegankelijk zijn.

#### <a name="network-security-groups"></a>Netwerkbeveiligingsgroepen
Een [Netwerkbeveiligingsgroep (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) is een eenvoudige filterregels voor pakketten firewall en kunt u toocontrol toegang op basis van een [5-tuple](https://www.techopedia.com/definition/28190/5-tuple). Nsg's bieden geen application layer inspectie of geverifieerde toegangsbeheer. Ze kunnen worden gebruikt toocontrol verkeer tussen subnetten binnen een Azure-netwerk en het verkeer tussen een Azure-netwerk en Internet Hallo verplaatsen.

#### <a name="route-control-and-forced-tunneling"></a>Route besturingselement en geforceerde Tunneling
Hallo mogelijkheid toocontrol routeringsgedrag op uw virtuele Azure-netwerken is een kritieke beveiliging en toegang besturingselement mogelijkheid via het netwerk. Bijvoorbeeld, als u ervoor dat alle verkeer tooand van uw Azure Virtual Network dat toestel virtuele beveiliging doorloopt toomake wilt, u moet toobe kunnen toocontrol en aanpassen routeringsgedrag. U kunt dit doen door zelfgedefinieerde Routes configureren in Azure.

[De gebruiker gedefinieerde Routes](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) kunt u toocustomize binnenkomende en uitgaande paden voor verkeer van en naar afzonderlijke virtuele machines of subnetten tooinsure Hallo veiligste route mogelijk. [Geforceerde tunneling](https://www.petri.com/azure-forced-tunneling) is een mechanisme kunt u tooensure die uw services niet zijn toegestaan tooinitiate een toodevices verbinding op Hallo Internet.

Dit verschilt van binnenkomende verbindingen kunnen tooaccept worden en vervolgens reageert toothem. Front-end-webservers moeten toorespond toorequests via Internet-hosts, en dus Internet afkomstig verkeer is toegestaan inkomende toothese webservers en Hallo-webservers kunnen reageren.

Geforceerde tunneling is vaak gebruikte tooforce uitgaand verkeer toohello Internet toogo via lokale beveiliging proxy's en firewalls.

#### <a name="virtual-network-security-appliances"></a>Virtueel netwerk beveiligingsapparaten
Terwijl Netwerkbeveiligingsgroepen, door de gebruiker gedefinieerde Routes en geforceerde tunneling u een niveau van beveiliging op de netwerk- en lagen Hallo Hallo bieden [OSI-model](https://en.wikipedia.org/wiki/OSI_model), het kan gebeuren als u wilt dat tooenable hogere niveaus van beveiliging Hallo-stack. U kunt toegang tot deze beveiligingsfuncties verbeterde netwerk met behulp van een Azure-partner toestel oplossing voor netwerkbeveiliging. U vindt Hallo meest recente Azure network security partneroplossingen Hallo [Azure Marketplace](https://azure.microsoft.com/marketplace/) en zoeken naar 'beveiliging' en "netwerkbeveiliging."

### <a name="azure-virtual-network"></a>Azure Virtual Network

Een Azure-netwerk (VNet) is een weergave van uw eigen netwerk in Hallo cloud. Het is een logische isolatie van hello Azure-netwerk fabric toegewezen tooyour abonnement. U kunt volledig Hallo IP-adresblokken, DNS-instellingen, beveiligingsbeleidsregels en routetabellen binnen dit netwerk beheren. U kunt uw VNet onderverdelen in subnetten en Azure IaaS virtuele machines (VM's) te plaatsen en/of [Cloudservices (PaaS-rolexemplaren)](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) op Azure Virtual Networks.

Bovendien kunt u Hallo virtueel netwerk tooyour on-premises netwerk via een Hallo [connectiviteitsopties](https://docs.microsoft.com/azure/vpn-gateway/) beschikbaar in Azure. U kunt uw netwerk tooAzure, met volledige controle over IP-adresblokken met Hallo voordeel van het enterprise scale die Azure biedt in wezen kunt uitbreiden.

Azure-netwerken ondersteunt verschillende scenario's voor veilige externe toegang. Enkele van de volgende:

-   [Verbinding maken met afzonderlijke werkstations tooan Azure Virtual Network](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

-   [Lokale netwerk tooan Azure Virtual Network bij een VPN-verbinding](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

-   [Lokale netwerk tooan Azure Virtual Network verbinden met een specifieke WAN-verbinding](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)

-   [Verbinding maken met Azure Virtual Networks tooeach andere](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps)

### <a name="vpn-gateway"></a>VPN Gateway
toosend netwerkverkeer tussen uw Azure Virtual Network en uw on-premises site, moet u een VPN-gateway maken voor uw Azure Virtual Network. Een [VPN-gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) is een soort virtuele netwerkgateway die versleuteld verkeer via een openbare verbinding verzonden. Ook kunt u VPN-gateways toosend verkeer tussen virtuele netwerken van Azure via hello Azure-netwerk fabric.

### <a name="express-route"></a>ExpressRoute
Microsoft Azure [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) is een speciale WAN-koppeling waarmee u uw on-premises netwerken in Hallo Microsoft cloud uitbreiden via een speciale persoonlijke verbinding die wordt gefaciliteerd door een connectiviteitsprovider.

![ExpressRoute](./media/azure-security/azure-security-fig1.png)

Met ExpressRoute kunt kunt u verbindingen tooMicrosoft cloudservices, zoals Microsoft Azure, Office 365 en CRM Online maken. Via een connectiviteitsprovider in een co-locatiefaciliteit is connectiviteit mogelijk vanuit een any-to-any (IP VPN) netwerk, een point-to-point Ethernet-netwerk of een virtuele overlappende verbinding.

ExpressRoute-verbindingen gaan niet via openbaar Internet Hallo en dus kan worden beschouwd als veiliger dan een VPN-oplossingen. ExpressRoute-verbindingen toooffer kan dit meer betrouwbaarheid, sneller en hebben ze lagere latenties en betere beveiliging dan gewone verbindingen via Internet Hallo.


### <a name="application-gateway"></a>Application Gateway
Microsoft [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) biedt een [toepassing levering Controller (ADC)](https://en.wikipedia.org/wiki/Application_delivery_controller) als een service, biedt verschillende laag 7 taakverdeling mogelijkheden voor uw toepassing.

![Application Gateway](./media/azure-security/azure-security-fig2.png)

Hiermee kunt u toooptimize web farm productiviteit door het offloaden van CPU intensief SSL-beëindiging toohello Application Gateway (ook wel bekend als 'SSL-offload' of 'SSL-bridging'). Het bevat ook andere laag 7 routering mogelijkheden, waaronder round-robin distributie van inkomend verkeer, sessie cookies gebaseerde affiniteit URL-pad gebaseerde routering en Hallo mogelijkheid toohost meerdere websites achter een enkele Gateway van de toepassing. Azure Application Gateway is een load balancer in laag 7.

Het biedt failover, HTTP-aanvragen routeren tussen verschillende servers, ongeacht of deze op Hallo cloud of on-premises.

Toepassing biedt veel toepassing levering Controller (ADC)-functies, zoals HTTP laden taakverdeling, cookies gebaseerde affiniteit van sessie, [Secure Sockets Layer (SSL)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-powershell) -offload, aangepaste statuscontroles, ondersteuning voor meerdere locaties en vele andere.

### <a name="web-application-firewall"></a>Web Application Firewall
Web Application Firewall is een functie van [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) die beveiliging biedt tooweb toepassingen die gebruikmaken van toepassingsgateway voor standaardfuncties toepassing levering besturingselement (ADC). Web application firewall doet dit door deze op basis van de meeste Hallo OWASP bovenste 10 veelvoorkomende web beveiligingslekken te beschermen.

![Web Application Firewall](./media/azure-security/azure-security-fig1.png)

-   Beveiliging tegen SQL-injecties

-   Beveiliging tegen veelvoorkomende aanvallen via internet, zoals opdrachtinjectie, het smokkelen van HTTP-aanvragen, het uitsplitsen van HTTP-antwoorden en aanvallen waarbij een extern bestand wordt ingesloten

-   Beveiliging tegen schendingen van het HTTP-protocol

-   Beveiliging tegen afwijkingen van het HTTP-protocol, zoals een gebruikersagent voor de host en Accept-headers die ontbreken

-   Beveiliging tegen bots, crawlers en scanners

-   Detectie van veelvoorkomende onvolkomenheden in toepassing (dat wil zeggen, Apache, IIS, enz.)


Een gecentraliseerde web application firewall tooprotect tegen aanvallen via Internet maakt beveiligingsbeheer veel eenvoudiger en biedt betere zekerheid toohello toepassing tegen Hallo bedreigingen van indringers. Een WAF oplossing kan ook beveiligingsrisico tooa sneller reageren door een bekend beveiligingsprobleem met een centrale locatie en beveiliging van elk van de afzonderlijke webtoepassingen patchen. Bestaande toepassing gateways kunnen worden geconverteerd tooan toepassingsgateway met web application firewall eenvoudig.
### <a name="traffic-manager"></a>Traffic Manager
Microsoft [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) kunt u toocontrol Hallo distributie van gebruikersverkeer voor service-eindpunten in verschillende datacenters. Ondersteund door Traffic Manager-service-eindpunten zijn virtuele Azure-machines, Web-Apps en cloudservices. U kunt Traffic Manager ook gebruiken met externe eindpunten die niet van Azure zijn. Traffic Manager gebruikt Hallo System DNS (Domain Name) toodirect toohello van de meest geschikte eindpunt op basis clientaanvragen van een [verkeersroutering methode](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) en Hallo-status van het Hallo-eindpunten.

Traffic Manager biedt een reeks verkeersroutering methoden toosuit verschillende groepen van toepassingen behoeften, eindpunt health [bewaking](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring), en automatische failover. Traffic Manager is een robuuste toofailure, met inbegrip van Hallo falen van een volledige Azure-regio.
### <a name="azure-load-balancer"></a>Azure Load Balancer
[Azure Load Balancer](https://docs.microsoft.com/azure/load-balancer/load-balancer-overview) tooyour toepassingen voor hoge beschikbaarheid en netwerk prestaties levert. Het is een laag 4 (TCP, UDP) load balancer die binnenkomend verkeer over orde exemplaren van services gedefinieerd in een set met gelijke taakverdeling distribueert. Azure Load Balancer kan worden geconfigureerd voor:

-   Taakverdeling saldo binnenkomende Internet verkeer toovirtual machines. Deze configuratie wordt ook wel [internetgerichte taakverdeling](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview).

-   Load balance verkeer tussen virtuele machines in een virtueel netwerk, tussen virtuele machines in de cloud-services of tussen virtuele machines in een virtueel netwerk met cross-premises en lokale computers. Deze configuratie wordt ook wel [interne load balancing](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview). 

- Doorsturen van verkeer van externe tooa specifieke virtuele machine

### <a name="internal-dns"></a>Interne DNS
Hallo-lijst met DNS-servers in een VNet in Hallo-beheerportal of in het configuratiebestand voor Hallo netwerk gebruikt, kunt u beheren. De klant kunt u too12 DNS-servers toevoegen voor elk VNet. Wanneer u DNS-servers opgeeft, is het belangrijk tooverify weer te geven die van de klant DNS-servers in de juiste volgorde Hallo voor de omgeving van de klant. Een lijst met DNS-server werkt niet round robin. Ze worden gebruikt in Hallo volgorde waarin ze worden opgegeven. Als eerste DNS-server op Hallo lijst Hallo kunnen toobe bereikt, wordt in het Hallo-client die DNS-server, ongeacht of Hallo DNS-server niet de juiste wijze of functioneert gebruikt. toochange hello volgorde van de DNS-server voor het virtuele netwerk van de klant, Hallo DNS-servers verwijderen uit lijst Hallo en toe te voegen terug in de volgorde van de Hallo die klant wil. DNS ondersteunt Hallo beschikbaarheid aspect van drie vakken Hallo 'Correctspell(tm)' beveiliging.

### <a name="azure-dns"></a>Azure DNS
Hallo [Domain Name System](https://technet.microsoft.com/library/bb629410.aspx), of DNS, is verantwoordelijk voor het omzetten van (of het oplossen van) een website of service name tooits IP-adres. [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview) is een hosting service voor DNS-domeinen, omzetten van namen met behulp van Microsoft Azure-infrastructuur. U kunt uw DNS beheren door het hosten van uw Azure-domeinen records met dezelfde referenties, API's, hulpprogramma's en facturering Hallo als uw andere Azure-services. DNS ondersteunt Hallo beschikbaarheid aspect van drie vakken Hallo 'Correctspell(tm)' beveiliging.
### <a name="log-analytics-nsgs"></a>Log Analytics nsg 's
Hallo diagnostische logboeken categorieën voor het nsg's te volgen, kunt u inschakelen:
-   Gebeurtenis: Bevat vermeldingen voor welke NSG regels toegepaste tooVMs en de exemplaar-rollen op basis van MAC-adres zijn. Hallo-status voor deze regels worden verzameld om de 60 seconden.

-   Regels teller: bevat vermeldingen voor het aantal keren dat elke NSG-regel is toegepast toodeny of verkeer toestaan.

### <a name="azure-security-center"></a>Azure Security Center
Security Center helpt u bij het detecteren, voorkomen van en reageren toothreats en vindt u meer zichtbaarheid van en controle over de beveiliging van uw Azure-resources Hallo. Het biedt geïntegreerde Beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt detecteren bedreigingen die anders onopgemerkt, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen. Aanbevelingen Netwerkcentrum rond firewalls, Netwerkbeveiligingsgroepen en regels voor binnenkomend verkeer op configureren.

Aanbevelingen voor netwerken beschikbaar zijn als volgt:

-   [Next Generation Firewall toevoegen](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall) raadt aan dat u, een volgende generatie Firewall (NGFW) van een Microsoft-partner tooincrease uw beveiligingsinstellingen toevoegt

-   [Alleen via NGFW verkeer routeren](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall#route-traffic-through-ngfw-only) raadt die u configureert netwerk groep (NSG) regels voor binnenkomend verkeer tooyour VM via uw NGFW afdwingen.

-   [Inschakelen van Netwerkbeveiligingsgroepen op subnetten of virtuele machines](https://docs.microsoft.com/azure/security-center/security-center-enable-network-security-groups) raadt aan om het nsg's op subnetten of VM's in te schakelen.

-   [Beperken van toegang via Internetgericht eindpunt](https://docs.microsoft.com/azure/security-center/security-center-restrict-access-through-internet-facing-endpoints) raadt aan dat u regels voor binnenkomend verkeer voor het nsg's configureren.


## <a name="compute"></a>Compute

Hallo gedeelte bevat aanvullende informatie met betrekking tot belangrijke functies in dit gedeelte en samenvatting informatie over deze mogelijkheden.

### <a name="antimalware--antivirus"></a>Antimalware & Antivirus
Met Azure IaaS, kunt u antimalware-software van beveiliging leveranciers zoals Microsoft, Symantec, Trend Micro, McAfee en Kaspersky tooprotect uw virtuele machines van schadelijke bestanden, adware en andere dreigingen. [Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) voor Azure Cloud Services en virtuele Machines is een beveiliging-functie waarmee identificeren en virussen, spyware en andere schadelijke software verwijderen. Microsoft Antimalware biedt configureerbare waarschuwingen wanneer bekende schadelijke of ongewenste software probeert tooinstall zelf of uit te op uw Azure-systemen voeren. Microsoft Antimalware kan ook worden geïmplementeerd met Azure Security Center

### <a name="hardware-security-module"></a>Hardware Security Module
Versleuteling en authenticatie verbetert niet beveiliging tenzij Hallo sleutels zelf worden beveiligd. Kunt u Hallo-beheer en beveiliging van uw kritieke geheimen en sleutels vereenvoudigen doordat ze op in [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis). Sleutelkluis biedt Hallo optie toostore uw sleutels in hardware Security modules (HSM's) gecertificeerde tooFIPS 140-2 Level 2-standaarden. De versleutelingssleutels SQL Server voor back-up of [transparante gegevensversleuteling](https://msdn.microsoft.com/library/bb934049.aspx) kunnen alle worden opgeslagen in de Sleutelkluis met alle sleutels of geheimen van uw toepassingen. Machtigingen en toegang toothese beveiligde items worden beheerd via [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).

### <a name="virtual-machine-backup"></a>Back-up van virtuele machine
[Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) is een oplossing die uw toepassingsgegevens met nul investeringen en minimale beschermt bedrijfskosten. Toepassingsfouten kunnen uw gegevens beschadigd raken en menselijke fouten fouten in uw toepassingen die toosecurity problemen leiden kunnen kunnen veroorzaken. Uw virtuele machines met Windows en Linux zijn beveiligd met Azure Backup.

### <a name="azure-site-recovery"></a>Azure Site Recovery
Een belangrijk onderdeel van uw organisatie [zakelijke continuïteit en herstel in noodgevallen (BCDR)](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) strategie uitzoeken hoe tookeep zakelijke workloads en apps up en wordt uitgevoerd als geplande en niet-geplande storingen optreden. [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) helpt bij het indelen replicatie, failovers en herstel van workloads en apps, zodat ze beschikbaar vanaf een secundaire locatie zijn als uw primaire locatie uitvalt.

### <a name="sql-vm-tde"></a>SQL VM TDE
[Transparante gegevensversleuteling (TDE)](https://docs.microsoft.com/azure/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-ps-sql-keyvault) en kolom: versleuteling op bestandsniveau (wissen) zijn functies van SQL server-versleuteling. Deze vorm van versleuteling vereist klanten toomanage en store Hallo cryptografische sleutels die u voor versleuteling gebruikt.

Hello Azure Key Vault (Azure Sleutelkluis)-service is ontworpen tooimprove Hallo beveiliging en beheer van deze sleutels op een locatie met veilige en maximaal beschikbaar. Hallo SQL Server-Connector kunt SQL Server-toouse deze sleutels van Azure Sleutelkluis.

Als u SQL Server met lokale virtuele machines uitvoert, zijn er stappen kunt u tooaccess Azure Key Vault volgen uit uw on-premises SQL Server-machine. Maar voor SQL Server in Azure VM's, kunt u tijd besparen met hello Azure Sleutelkluis-integratie-functie. Met een paar Azure PowerShell-cmdlets tooenable deze functie kunt u automatiseren Hallo configuratie nodig is voor een SQL VM tooaccess de sleutelkluis.

### <a name="vm-disk-encryption"></a>VM-schijfversleuteling
[Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) is een nieuwe functie waarmee u uw Windows- en Linux IaaS-schijven voor virtuele machine versleutelen. Van toepassing hello bedrijfstak standaard BitLocker-functie van Windows hello DM-Crypt functie en van Linux tooprovide volumeversleuteling voor Hallo OS en Hallo gegevensschijven. Hallo-oplossing is geïntegreerd met Azure Key Vault toohelp u controleren en beheren van Hallo schijfversleuteling sleutels en geheimen in uw abonnement Sleutelkluis. Hallo oplossing zorgt er ook voor dat alle gegevens op schijven van de virtuele machine Hallo zijn versleuteld in rust in uw Azure-opslag.

### <a name="virtual-networking"></a>Virtuele netwerken
Verbinding met het netwerk, moeten virtuele machines. toosupport is vereist dat dit vereiste, Azure virtuele machines toobe verbonden tooan Azure Virtual Network. Een Azure-netwerk is een logische constructie die is gebouwd op Hallo fysieke netwerk van Azure-infrastructuur. Elke logische [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) wordt geïsoleerd van alle andere virtuele netwerken van Azure. Deze isolatie kunt zorgen dat het netwerkverkeer in uw implementaties is niet toegankelijk tooother Microsoft Azure-klanten.

### <a name="patch-updates"></a>Patchupdates
Patch Updates vormen Hallo basis voor het opsporen en oplossen van problemen en vereenvoudigen Hallo software update management, zowel Hallo aantal software-updates die u in uw onderneming implementeren moet te verminderen en door te verhogen van de mogelijkheid toomonitor naleving.

### <a name="security-policy-management-and-reporting"></a>Beheer van beveiligingsbeleid en rapportage
[Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) helpt u bij het detecteren, voorkomen van en reageren toothreats en biedt u grotere zichtbaarheid van, en controle over, Hallo beveiliging van uw Azure-resources. Het biedt geïntegreerde Beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt detecteren bedreigingen die anders onopgemerkt, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.

### <a name="azure-security-center"></a>Azure Security Center
Security Center helpt u bij het detecteren, voorkomen van en reageren toothreats met verhoogde zichtbaarheid van en controle over Hallo beveiliging van uw Azure-resources. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt bedreigingen te detecteren die anders onopgemerkt zouden blijven, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.

## <a name="identify-and-access-management"></a>Identificatie en toegang beheren

Systemen, toepassingen en gegevens beveiligen begint met toegangsbeheer op basis van identiteit. Hallo identiteits- en toegangsbeheer beheerfuncties die zijn ingebouwd in zakelijke Microsoft-producten en services te beveiligen van uw organisatie en persoonlijke gegevens tegen onbevoegde toegang tijdens het maken van het beschikbare toolegitimate gebruikers wanneer en waar ze moeten deze.

### <a name="secure-identity"></a>Beveiligde identiteit
Microsoft maakt gebruik van meerdere procedures voor beveiliging en technologieën via Microsoft-producten en services toomanage identiteit en toegang.
-   [Multi-Factor Authentication](https://azure.microsoft.com/services/multi-factor-authentication/) vereist dat gebruikers toouse meerdere methoden om toegang te krijgen, lokaal en in Hallo cloud. Het biedt geavanceerde verificatie met tal van opties voor eenvoudige verificatie tijdens kunnen voldoen aan gebruikers met een eenvoudig proces aanmelden.

-   [Microsoft Authenticator](https://aka.ms/authenticator) biedt een gebruiksvriendelijke multi-factor Authentication-ervaring die werkt met Microsoft Azure Active Directory en Microsoft-accounts en biedt ondersteuning voor wearables en goedkeuringen op basis van een vingerafdruk.

-   [Wachtwoord-beleidsafdwinging](https://azure.microsoft.com/documentation/articles/active-directory-passwords-policy/) toeneemt Hallo beveiliging van traditionele wachtwoorden door wachtwoordlengte en complexiteitsvereisten vereisten, periodieke rotatie gedwongen om op te leggen en accountvergrendeling na mislukte verificatie probeert.

-   [Verificatie op basis van tokens](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/) Hiermee schakelt u verificatie via Active Directory Federation Services (AD FS) of secure token systemen van derden.

-   [Op rollen gebaseerde toegangsbeheer (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/) schakelt u toogrant toegang op basis van Hallo van de gebruiker toegewezen rol, zodat u eenvoudig toogive gebruikers alleen Hallo hoeveelheid toegang moeten deze tooperform hun taken. U kunt RBAC per bedrijfsmodel van uw organisatie en risicotolerantie aanpassen.

-   [Geïntegreerd identiteitsbeheer (hybride identiteit)](https://azure.microsoft.com/documentation/articles/active-directory-hybrid-identity-design-considerations-overview/) kunt u toomaintain beheer van toegang van gebruikers voor interne datacenters en cloudservices platforms, maken de identiteit van een enkele gebruiker voor verificatie en autorisatie tooall resources.

### <a name="secure-apps-and-data"></a>Apps en gegevens beveiligen
[Azure Active Directory](https://azure.microsoft.com/services/active-directory/), een uitgebreide identiteits- en toegangsbeheer cloud beheeroplossing voor beveiligde toegang toodata in toepassingen op de site en Hallo cloud helpt en vereenvoudigt het beheer van gebruikers en groepen Hallo. Het combineert core directoryservices, geavanceerde identiteit governance, beveiliging en toegang van Toepassingsbeheer, en maakt het eenvoudig voor ontwikkelaars toobuild op basis van beleid identiteitsbeheer in hun apps. tooenhance uw Azure Active Directory, kunt u betaald mogelijkheden met behulp van de edities Azure Active Directory Basic, Premium P1 en Premium-P2 Hallo toevoegen.

| Gratis / algemene functies     | Basisfuncties    |Premium P1-functies |Premium P2-functies | Azure Active Directory Join – alleen gerelateerde functies van Windows 10|
| :------------- | :------------- |:------------- |:------------- |:------------- |
|   [Directory-objecten](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#directory-objects), [gebruiker of groep Management (toevoegen, bijwerken, verwijderen) / op basis van gebruikers inrichten, apparaatregistratie](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#usergroup-management-addupdatedelete-user-based-provisioning-device-registration), [eenmalige aanmelding (SSO)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#single-sign-on-sso), [Self-service Wijzigen van wachtwoorden voor cloudgebruikers](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-change-for-cloud-users), [Connect (Sync engine die uitgebreider is dan lokale mappen tooAzure Active Directory)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-sync-engine-that-extends-on-premises-directories-to-azure-active-directory), [beveiliging / gebruiksrapporten](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#securityusage-reports)       |     [Toegangsbeheer op basis van een groep / inrichting](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#group-based-access-managementprovisioning), [selfservice voor wachtwoordherstel voor cloudgebruikers](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-reset-for-cloud-users), [bedrijf huisstijl (aanmelden pagina's / Toegangsvenster aanpassing)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#company-branding-logon-pagesaccess-panel-customization), [toepassingsproxy](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#application-proxy), [SLA 99,9%](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#sla-999) |  [Self-Service groep en app Management/zelfstandige verkeer toepassing toevoegingen/dynamische groepen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-group), [Self-Service wachtwoord opnieuw instellen/wijzigen/ontgrendelen met lokale terugschrijven](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-resetchangeunlock-with-on-premises-write-back), [multi-factor Authentication (Cloud en On-premises (MFA-Server))](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#multi-factor-authentication-cloud-and-on-premises-mfa-server), [MIM CAL + MIM-Server](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mim-cal-mim-server), [Cloud App Discovery](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#cloud-app-discovery), [Connect Health](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-health), [rollover van de automatische wachtwoord voor groepsaccounts](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#automatic-password-rollover-for-group-accounts)|     [Identity Protection](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-identityprotection), [Privileged Identity Management](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-privileged-identity-management-configure)|    [Lid worden van een apparaat tooAzure AD, bureaublad SSO, Microsoft Passport voor Azure AD, beheerder Bitlocker-herstel](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#join-a-device-to-azure-ad-desktop-sso-microsoft-passport-for-azure-ad-administrator-bitlocker-recovery), [MDM automatische inschrijving, Self-Service Bitlocker-herstel, extra lokale beheerders tooWindows 10-apparaten via Azure AD Join](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mdm-auto-enrollment)|


- [Cloud App Discovery](https://docs.microsoft.com/azure/active-directory/active-directory-cloudappdiscovery-whatis) is een premium-functie van Azure Active Directory waarmee u tooidentify cloud-toepassingen die worden gebruikt door Hallo werknemers in uw organisatie.

- [Azure Active Directory: Identity Protection](https://azure.microsoft.com/documentation/articles/active-directory-identityprotection/) is een security-service die gebruikmaakt van Azure Active Directory afwijkingsdetectie detectie mogelijkheden tooprovide een geconsolideerde weergave risicogebeurtenissen en mogelijke beveiligingsproblemen die invloed kunnen zijn op uw de identiteiten van de organisatie.

- [Azure Active Directory Domain Services](https://azure.microsoft.com/services/active-directory-ds/) kunt u toojoin Azure Virtual machines tooa domein zonder Hallo toodeploy domeincontrollers nodig. Gebruikers toothese VMs aanmelden met hun zakelijke Active Directory-referenties en naadloos toegang tot bronnen.

- [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) is een maximaal beschikbare, wereldwijde identity management-service voor consumentgerichte-apps die u kunt schalen toohundreds miljoenen identiteiten en geïntegreerd in mobiele en web-platforms. Uw klanten kunnen aanmelden tooall met uw apps via aanpasbare die gebruikmaken van bestaande accounts van sociale media, of u kunt nieuwe zelfstandige referenties maken.

- [Azure Active Directory B2B-samenwerking](https://aka.ms/aad-b2b-collaboration) is een beveiligde integratie partneroplossing die ondersteuning biedt voor uw externe bedrijfsrelaties door in te schakelen partners tooaccess uw zakelijke toepassingen en gegevens selectief met behulp van hun zelfbeheerde identiteiten.

- [Azure Active Directory Join](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-overview/) kunt u tooextend cloud mogelijkheden tooWindows 10-apparaten voor gecentraliseerd beheer. Dit maakt het mogelijk voor gebruikers tooconnect toohello bedrijf of organisatie-cloud via Azure Active Directory en vereenvoudigt toegang tooapps en bronnen.

- [Azure Active Directory-toepassingsproxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/) biedt eenmalige aanmelding en veilige externe toegang voor webtoepassingen die lokaal worden gehost.

## <a name="next-steps"></a>Volgende stappen
- [Aan de slag met Microsoft Azure-beveiliging](https://docs.microsoft.com/azure/security/azure-security-getting-started)

Azure-services en functies toohelp kunt u beveiligen uw services en de gegevens in Azure

- [Azure Security Center](https://azure.microsoft.com/services/security-center/)

Detecteren, voorkomen van en reageren toothreats met verhoogde zichtbaarheid en controle over Hallo beveiliging van uw Azure-resources

- [Beveiligingsstatus bewaken in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-monitoring)

Hallo bewakingsmogelijkheden in Azure Security Center toomonitor naleving van beleid.
