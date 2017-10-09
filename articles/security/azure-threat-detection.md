---
title: aaaAzure detectie van dreigingen geavanceerde | Microsoft Docs
description: Meer informatie over Identity Protection en de mogelijkheden ervan.
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
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 63e2c541fd4ce2c571af9d5845c9a9bd4b03b2a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-advanced-threat-detection"></a>Azure Advanced Threat detectie
## <a name="introduction"></a>Inleiding

### <a name="overview"></a>Overzicht

Er is een reeks whitepapers, overzichten van de beveiliging, aanbevolen procedures en controlelijsten tooassist Azure ontwikkeld klanten over Hallo verschillende mogelijkheden beschikbaar zijn in betrekking hebben op beveiliging en omringende hello Azure-Platform. bereik van de onderwerpen in termen van breedte en diepte Hallo en regelmatig worden bijgewerkt. Dit document is onderdeel van de reeks zoals samengevat in Hallo abstracte sectie volgen.

### <a name="azure-platform"></a>Azure-Platform

Azure is een openbare cloud service-platform dat ondersteuning Hallo breedste selectie van besturingssystemen biedt, programmeertalen, frameworks, hulpprogramma's, databases, en apparaten.
Het ondersteunt Hallo programmeertalen te volgen:
-   Linux-containers worden uitgevoerd met Docker-integratie.
-   Met JavaScript, Python, .NET, PHP, Java en Node.js-apps bouwen
-   Build back-ends voor iOS, Android en Windows apparaten.

Hallo van dezelfde technologieën miljoenen van ontwikkelaars en IT-professionals al zijn afhankelijk van en vertrouwen wordt ondersteund door Azure openbare cloud-services.

Wanneer u de openbare cloud tooa met een organisatie migreert, wordt die organisatie is verantwoordelijk tooprotect uw gegevens en bieden beveiliging en beheeracties rond Hallo-systeem.

Azure infrastructuur is speciaal ontworpen van Hallo faciliteit tooapplications voor het hosten van miljoenen klanten tegelijkertijd en biedt een betrouwbare basis waarop bedrijven hun beveiliging behoeften kunnen. Azure biedt een breed scala aan opties tooconfigure en aanpassen van toomeet Hallo beveiligingsvereisten van uw app-implementaties. Dit document helpt u aan deze vereisten voldoet.

### <a name="abstract"></a>Abstracte

Microsoft Azure-aanbiedingen die zijn ingebouwd in de functie voor de detectie geavanceerde threat via services, zoals Azure Active Directory, Azure Operations Management Suite (OMS) en Azure Security Center. Deze verzameling beveiligingsservices en mogelijkheden bevat een eenvoudig en snel toounderstand wat gebeurt er in uw Azure-implementaties.

In dit artikel begeleidt u Hallo "Microsoft Azure benaderingen' naar threat beveiligingslek diagnostische en analyse van Hallo risico's die zijn gekoppeld aan Hallo schadelijke activiteiten die gericht is op basis van servers en andere Azure-resources. Dit helpt u tooidentify Hallo methoden voor identificatie en beveiligingslek management met geoptimaliseerd oplossingen per hello Azure-platform en klantgerichte beveiligingsservices en -technologieën.

Dit document is gericht op het Hallo-technologie van Azure-platform en klantgerichte besturingselementen en probeert niet tooaddress Sla's, prijzen modellen en DevOps practice overwegingen.

## <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Identity Protection

![Azure Active Directory Identity Protection](./media/azure-threat-detection/azure-threat-detection-fig1.png)


[Azure Active Directory: Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) is een functie van Hallo [Azure AD Premium-P2](https://docs.microsoft.com/azure/active-directory/active-directory-editions) edition waarmee u een overzicht van Hallo risicogebeurtenissen en mogelijke beveiligingsproblemen die invloed hebben op uw organisatie identiteiten. Microsoft heeft identiteiten voor een cloud-gebaseerde is beveiligen via een tien jaar en met Azure AD Identity Protection Microsoft aan te brengen deze dezelfde beveiliging systemen beschikbaar tooenterprise klanten. Identity Protection gebruikmaakt van bestaande Azure AD afwijkingsdetectie detectiemogelijkheden beschikbaar via [Azure AD-rapporten voor afwijkende activiteiten](https://docs.microsoft.com/azure/active-directory/active-directory-view-access-usage-reports#anomalous-activity-reports), en introduceert nieuwe risico gebeurtenistypen dat realtime afwijkingen kunnen detecteren.

Identity Protection maakt gebruik van geavanceerde machine learning-algoritmen en methodiek toodetect afwijkingen en risico's die aangeven mogelijk dat een identiteit is aangetast. Met deze gegevens Identity Protection genereert rapporten en waarschuwingen die u in staat tooinvestigate stellen deze risicogebeurtenissen en onderneem gepaste actie voor herstel of afname.

Maar Azure Active Directory: Identity Protection is meer dan een hulpprogramma voor bewaking en rapportage. Op basis van de risico's, Identity Protection berekent het risiconiveau van een gebruiker voor elke gebruiker, zodat u tooconfigure risico beleid op basis van tooautomatically beveiligen Hallo identiteiten van uw organisatie.

Deze beleidsregels risico gebaseerde in toevoeging tooother [voorwaardelijk toegangsbeheer](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) verstrekt door Azure Active Directory en [EMS](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access), kunnen automatisch blokkeren of bieden adaptieve herstelacties die bevatten wachtwoord opnieuw instellen en afdwingen van multi-factor authentication-server.

### <a name="identity-protections-capabilities"></a>De mogelijkheden van Identity Protection

Azure Active Directory: Identity Protection is meer dan een controle en rapportage. tooprotect identiteiten van uw organisatie, kunt u risico-beleidsregels die automatisch toodetected problemen reageren als een opgegeven risiconiveau is bereikt. Deze beleidsregels bovendien tooother voorwaardelijke toegang tot de besturingselementen die worden geleverd door Azure Active Directory en EMS, kunnen automatisch blokkeren of initiëren adaptieve herstelacties met inbegrip van wachtwoorden en afdwingen van multi-factor authentication-server.

Voorbeelden van een aantal manieren waarop hello Azure Identity Protection kunt beveiligen van uw accounts en identiteiten omvatten:

[Risico's en riskant accounts te detecteren:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#detection)
-   Zes risico gebeurtenistypen met machine learning en heuristische regels detecteren
-   Gebruiker risiconiveaus berekenen
-   Aangepaste aanbevelingen tooimprove bieden algehele beveiligingsstatus beveiligingslekken markeert

[Bezig met het onderzoeken van risico's:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#investigation)
-   Verzenden van meldingen voor risico 's
-   Het onderzoeken van risico's met behulp van de relevante en contextuele informatie
-   Biedt eenvoudige werkstromen tootrack onderzoeken
-   Eenvoudige toegang bieden tooremediation acties zoals het wachtwoord opnieuw instellen

[Beleid voor voorwaardelijke toegang op basis van risico's:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#risky-sign-ins)
-   Beleid toomitigate riskant aanmeldingen door aanmeldingen blokkeren of uitdagingen voor meervoudige verificatie vereisen.
-   Beleid tooblock of beveiligde riskant gebruikersaccounts
-   Beleid toorequire gebruikers tooregister voor multi-factor authentication

### <a name="azure-ad-privileged-identity-management-pim"></a>Azure AD Privileged Identity Management (PIM)

Met [Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure),

![Azure AD Privileged Identity Management](./media/azure-threat-detection/azure-threat-detection-fig2.png)

u kunt beheren, bepalen en controleren van toegang binnen uw organisatie. Dit omvat toegang tooresources in Azure AD en andere Microsoft online services zoals Office 365 of Microsoft Intune.

Azure AD Privileged Identity Management kunt u:

-   Een waarschuwing en rapporteren over Azure AD-beheerders en 'just in time' beheerderstoegang tooMicrosoft Online Services, zoals Office 365 en Intune

-   Rapporten over beheerder toegang tot geschiedenis en wijzigingen in beheerderstoewijzingen ophalen

-   Ontvang waarschuwingen over toegang tooa bevoorrechte rol

## <a name="microsoft-operations-management-suite-oms"></a>Microsoft Operations Management Suite (OMS)

[Microsoft Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) van Microsoft cloud-gebaseerde IT beheeroplossing waarmee u beheren kunt en beveiligen van uw on-premises en cloud-infrastructuur. Aangezien OMS wordt geïmplementeerd als een cloudservice, kunt u er al snel mee aan de slag, en dat met minimale investeringen in infrastructuurservices. Nieuwe beveiligingsfuncties automatisch worden geleverd voor het opslaan van uw voortdurend onderhoud en kosten te upgraden.

Bovendien tooproviding waardevolle services op een eigen, OMS kunnen worden geïntegreerd met System Center-onderdelen, zoals [System Center Operations Manager](https://blogs.technet.microsoft.com/cbernier/2013/10/23/monitoring-windows-azure-with-system-center-operations-manager-2012-get-me-started/) tooextend uw bestaande security management investeringen in Hallo cloud. System Center en OMS kunnen samenwerken tooprovide beheer van een volledige hybride-ervaring.

### <a name="holistic-security-and-compliance-posture"></a>Holistische beveiliging en naleving houding

Hallo [OMS beveiligings- en Audit dashboard](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) biedt een uitgebreid overzicht van uw organisatie IT beveiligingspostuur met ingebouwde zoekquery's voor problemen die aandacht vereisen die uw aandacht vereisen. Hallo beveiligings- en Audit dashboard is het startscherm voor van alles Hallo toosecurity in OMS. Het biedt op hoog niveau inzicht in de Hallo beveiligingsstatus van uw computers. Dit omvat ook Hallo mogelijkheid tooview alle gebeurtenissen uit Hallo afgelopen 24 uur, 7 dagen of een andere aangepaste tijdsbestek.

OMS dashboards help u snel en eenvoudig begrijpt Hallo algehele beveiligingsstatus van de omgeving, allemaal binnen Hallo context van de IT-bewerkingen, inclusief: software-update-evaluatie, antimalware beoordeling en configuratiebasislijnen. Bovendien beveiliging logboekgegevens gemakkelijk toegankelijk is toostreamline Hallo beveiliging en naleving controleren processen.

Hallo OMS beveiligings- en Audit dashboard is onderverdeeld in vier hoofdcategorieën:

![OMS-dashboard Beveiliging en controle](./media/azure-threat-detection/azure-threat-detection-fig3.jpg)

-   **Beveiligingsdomeinen:** op dit gebied kunt u zich kunt toofurther beveiligingsrecord verkennen gedurende een bepaalde periode, toegang tot de evaluatie van schadelijke software, bijwerken assessment, netwerkbeveiliging, informatie over identiteit en toegang, computers met beveiligingsgebeurtenissen en snel hebben toegang tooAzure Security Center-dashboard.

-   **Problemen die aandacht vereisen:** deze optie kunt u tooquickly Hallo aantal actieve problemen identificeren en Hallo ernst van deze problemen.

-   **Detecties (Preview):** kunt u tooidentify aanvalspatronen met beveiligingswaarschuwingen visualiseren als zij op basis van uw resources plaatsvinden.

-   **Dreigingen:** kunt u tooidentify aanvalspatronen door het totale aantal servers met uitgaand schadelijk IP-verkeer, Hallo schadelijke threat type en een kaart die laat waar deze IP-adressen afkomstig zijn zien van Hallo visualiseren.

-   **Algemene beveiliging query's:** deze optie biedt u een lijst met de meest voorkomende beveiliging Hallo query's waarmee u toomonitor uw omgeving kunt. Wanneer u op een van de query's klikt, wordt Hallo Search-blade geopend met de Hallo resultaten van deze query.

### <a name="insight-and-analytics"></a>Inzicht en analyses
Hallo midden van [logboekanalyse](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) Hallo OMS-opslagplaats, die wordt gehost in hello Azure-cloud is.

![Inzicht en analyses](./media/azure-threat-detection/azure-threat-detection-fig4.png)

Gegevens worden verzameld in Hallo opslagplaats van verbonden bronnen door configureren gegevensbronnen en toe te voegen oplossingen tooyour abonnement.

![abonnement](./media/azure-threat-detection/azure-threat-detection-fig5.png)

Gegevensbronnen en oplossingen maakt elk verschillende recordtypen die hun eigen set eigenschappen, maar nog steeds in query's toohello opslagplaats samen kunnen worden geanalyseerd. Hiermee kunt u toouse Hallo dezelfde toowork in hulpprogramma's en -methoden met verschillende soorten gegevens verzameld door verschillende bronnen.


De meeste van uw interactie met logboekanalyse is via Hallo OMS-portal, die wordt uitgevoerd in een browser en biedt u toegang tooconfiguration instellingen en meerdere tooanalyze in hulpprogramma's en act van verzamelde gegevens. Vanuit de portal hello, kunt u [Meld zoekopdrachten](https://docs.microsoft.com/azure/log-analytics/log-analytics-log-searches) wanneer u query's tooanalyze verzamelde gegevens, samenstellen [dashboards](https://docs.microsoft.com/azure/log-analytics/log-analytics-dashboards), die u kunt aanpassen met grafische weergave van uw waardevolste zoekopdrachten en [oplossingen](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions), die aanvullende functionaliteit en analyse hulpprogramma's bieden.

![analyseprogramma 's](./media/azure-threat-detection/azure-threat-detection-fig6.png)

Oplossingen toevoegen functionaliteit tooLog Analytics. Ze voornamelijk uitgevoerd in de cloud Hallo en analyse van de verzamelde gegevens in de OMS-opslagplaats Hallo bieden. Ze kunnen ook nieuwe recordtypen toobe verzameld die kan worden geanalyseerd met logboek zoekopdrachten of door aanvullende gebruikersinterface van de oplossing in de OMS-dashboard Hallo Hallo definiëren.
Hallo beveiliging en controle is een voorbeeld van deze typen oplossingen.



### <a name="automation--control-alert-on-security-configuration-drifts"></a>Automation en Control: waarschuwing voor beveiligingsconfiguratie drifts

Azure Automation automatiseert administratieve processen met runbooks die zijn gebaseerd op PowerShell en uitvoeren in hello Azure-cloud. Runbooks kunnen ook worden uitgevoerd op een server in uw lokale toomanage lokale bronnen in een datacenter. Azure Automation biedt Configuratiebeheer met PowerShell DSC (Desired State Configuration).

![Azure Automation](./media/azure-threat-detection/azure-threat-detection-fig7.png)

U kunt maken en beheren DSC-resources gehost in Azure en ze toocloud en on-premises systemen toodefine toepassen en automatisch afdwingen van de configuratie of rapporten op afwijking toohelp ervoor zorgen dat beveiligingsconfiguraties blijven binnen beleid.

## <a name="azure-security-center"></a>Azure Security Center

Azure Security Center beschermt u uw Azure-resources. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen. Binnen het Hallo-service, u zich kunt toodefine beleidsregels niet alleen op basis van uw Azure-abonnementen, maar ook tegen [resourcegroepen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal), zodat u gedetailleerder worden uitgevoerd kunt.

![Azure Security Center](./media/azure-threat-detection/azure-threat-detection-fig8.png)

Beveiligingsonderzoekers van Microsoft zijn voortdurend op Hallo lookout voor bedreigingen. Ze hebben toegang tot tooan uitbreidbare set telemetrie verkregen van wereldwijde aanwezigheid van Microsoft in Hallo cloud en on-premises. In deze verzameling wide bereiken en diverse gegevenssets kan Microsoft toodiscover nieuwe aanvalspatronen en trends in de lokale producten voor consumenten en bedrijven, evenals de bijbehorende online services.

Security Center kunt dus snel de detectiealgoritmen bijwerken als aanvallers release nieuwe en steeds meer geavanceerde aanvallen. Deze aanpak kunt u blijven met een bedreiging snel bewegende omgeving.

![Security Center](./media/azure-threat-detection/azure-threat-detection-fig9.jpg)

Detectie van dreigingen Security Center werkt door het automatisch verzamelen van gegevens van de beveiliging van uw Azure-resources, het Hallo-netwerk en de verbonden partneroplossingen.  Deze informatie kunt correleren van gegevens uit meerdere bronnen, tooidentify bedreigingen wordt geanalyseerd.
Beveiligingswaarschuwingen worden samen met aanbevelingen voor hoe tooremediate threat Hallo prioriteit in Security Center.

Security Center maakt gebruik van geavanceerde beveiligingsanalyses die veel verder gaan dan op handtekeningen gebaseerde benaderingen. Doorbraken in big data en [machine learning](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) technologieën zijn gebruikte tooevaluate gebeurtenissen op Hallo gehele cloud-infrastructuurresources – bedreigingen die onmogelijk tooidentify handmatige benaderingen en het voorspellen van Hallo detecteren evolutie van aanvallen. Deze beveiligingsanalyse omvat Hallo volgende.

### <a name="threat-intelligence"></a>Bedreigingsinformatie

Microsoft heeft een gigantische hoeveelheid informatie over wereldwijde bedreigingen.
Telemetrie stroomt in uit meerdere bronnen, zoals Azure, Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com, MSN.com, Hallo Microsoft Digital Crimes Unit (DCU) en Microsoft Security Response Center (MSRC).

![Bedreigingsinformatie](./media/azure-threat-detection/azure-threat-detection-fig10.jpg)

Onderzoekers ook ontvangen threat intelligence-informatie die wordt gedeeld door grote cloudserviceproviders en toothreat intelligence feeds is lid van een derde partij. Azure Security Center kunt gebruiken deze informatie tooalert u toothreats van bekende ongewenste actoren. Voorbeelden zijn:

-   **Energiebeheer van Machine Learning - harnessing Hallo** Azure Security Center heeft toegang tot tooa enorme hoeveelheid gegevens over de netwerkactiviteit cloud, die kan worden gebruikt toodetect bedreigingen die gericht is op uw Azure-implementaties. Bijvoorbeeld:

-   **Brute Force detecties -** Machine learning-gebruikte toocreate is een historische patroon van externe toegangspogingen, waardoor toodetect beveiligingsaanvallen tegen SSH, RDP en SQL-poorten.

-   **Uitgaande DDoS Botnet en de detectie en** -een algemene doelstelling van aanvallen die gericht is op cloud-bronnen is toouse Hallo rekencapaciteit van deze resources tooexecute andere aanvallen.

-   **Nieuwe gebruikersgedrag Analytics-Servers en virtuele machines -** wanneer een server of de virtuele machine is geknoeid, tijdens detectie vermijden, gezorgd persistentie en waardoor aanvallers gebruikmaken van met tal van technieken tooexecute schadelijke code op dat systeem beveiligingsmechanismen.

-   **Azure SQL Database-Bedreigingsdetectie -** detectie van dreigingen voor Azure SQL Database, waarmee wordt aangegeven afwijkende databaseactiviteiten die aangeeft ongebruikelijke en potentieel schadelijke probeert tooaccess of misbruik databases.

### <a name="behavioral-analytics"></a>Gedragsanalyse

Behavior analytics is een techniek die geanalyseerd en vergeleken tooa gegevensverzameling van bekende patronen. Deze patronen zijn echter geen eenvoudige handtekeningen. Deze zijn bepaald door middel van complexe machine learning-algoritmen die toegepast toomassive gegevenssets zijn.

![Gedragsanalyse](./media/azure-threat-detection/azure-threat-detection-fig11.jpg)


Ze worden ook vastgesteld via de zorgvuldige analyse van schadelijk gedrag door deskundige analisten. Azure Security Center kunnen gedragsanalyse tooidentify geknoeid met resources op basis van de analyse van Logboeken van de virtuele machine, apparaatlogboeken virtueel netwerk, infrastructuur Logboeken, crashdumps en andere bronnen gebruiken.

Daarnaast is de correlatie met andere signalen toocheck voor ondersteunend bewijs van een wijdverbreid campagne. Deze correlatie kan tooidentify gebeurtenissen die consistent met het tot stand gebrachte indicatoren van inbreuk zijn.

Voorbeelden zijn:
-   **Uitvoering van verdachte:** aanvallers gebruiken verschillende technieken tooexecute schadelijke software zonder detectie. Bijvoorbeeld een aanvaller mogelijk geven malware Hallo dezelfde naam als legitieme systeembestanden, maar deze bestanden in een andere locatie te plaatsen, gebruik een naam die is heel vergelijkbaar met een onschadelijk bestand of masker Hallo true bestandsextensie. Security Center modellen processen gedrag en monitors verwerken uitvoeringen toodetect uitschieters zoals deze.

-   **Verborgen kwaadaardige software en misbruik pogingen:** geavanceerde malware traditionele antimalwareproducten kunt omzeilen door nooit toodisk schrijven of software-onderdelen die zijn opgeslagen op schijf te versleutelen. Echter kan dergelijke schadelijke software worden gedetecteerd met behulp van de geheugenanalyse, zoals Hallo malware moet in het geheugen toofunction laten staan traceringen. Wanneer software vastloopt, bevat een crashdump een gedeelte van het geheugen tijdens het Hallo Hallo crash. Door te analyseren Hallo geheugen in Hallo crashdump, kunt Azure Security Center detecteren technieken tooexploit beveiligingslekken in software gebruikt, toegang krijgen tot vertrouwelijke gegevens en ongemerkt binnen een verdachte computer blijven behouden zonder enige impact op de prestaties van Hallo uw computer verwijderd.

-   **Lateral movement en interne reconnaissance:** toopersist in een waarmee is geknoeid netwerk- en zoeken/oogst waardevolle gegevens aanvallers proberen vaak toomove lateraal van Hallo geknoeid machine tooothers binnen Hallo hetzelfde netwerk. Security Center bewaakt proces en aanmelding activiteiten toodiscover tooexpand probeert een kwaadwillende persoon voet achter de deur binnen Hallo netwerk, zoals externe opdrachten uit te voeren, netwerk scannen en accountinventarisatie.

-   **Schadelijke PowerShell-Scripts:** PowerShell kan worden gebruikt door aanvallers tooexecute schadelijke code op de virtuele doelmachines voor een verschillende doeleinden. Security Center inspecteert PowerShell-activiteit op tekenen van verdachte activiteiten.

-   **Uitgaande aanvallen:** aanvallers vaak cloudresources met Hallo doel van het gebruik van deze resources toomount extra aanvallen zijn gericht. Geïnfecteerde virtuele machines bijvoorbeeld mogelijk gebruikte toolaunch beveiligingsaanvallen op andere virtuele machines, verzenden van SPAM, of open poorten en andere apparaten op Internet Hallo scannen. Door het toepassen van machine learning toonetwork verkeer Beveiligingscentrum kan detecteren wanneer uitgaande netwerkcommunicatie Hallo-norm overschrijden. Als SPAM, ongebruikelijke e verkeer Beveiligingscentrum ook gecorreleerd met intelligence van Office 365 toodetermine of Hallo mail is waarschijnlijk slechte of Hallo resultaat van een geldig e-campagne.

### <a name="anomaly-detection"></a>Afwijkingsdetectie

Azure Security Center gebruikt ook afwijkingsdetectie detectie tooidentify bedreigingen. In contrast toobehavioral analytics (die afhankelijk is van bekende patronen die zijn afgeleid van grote gegevenssets), anomaliedetectie is meer 'aangepast' en legt de nadruk op basislijnen die specifieke tooyour implementaties. Machine learning toegepaste toodetermine normale activiteiten voor uw implementaties en vervolgens regels gegenereerde toodefine uitschieter voorwaarden die een beveiligingsgebeurtenis kunnen vertegenwoordigen. Hier volgt een voorbeeld:

-   **Binnenkomend RDP/SSH beveiligingsaanvallen:** uw implementaties mogelijk bezet virtuele machines met veel aanmeldingen elke dag en andere virtuele machines hebt die weinig of aanmeldingen hebben. Azure Security Center kunt bepalen basislijn Aanmeldingsactiviteit voor deze virtuele machines en machine learning toodefine rond Hallo normale aanmelding activiteiten gebruiken. Als er een discrepantie met Hallo basislijn gedefinieerd voor gerelateerd aanmelding kenmerken, en vervolgens een waarschuwing worden gegenereerd. Ook hier weer wordt door machine learning bepaald wat een aanzienlijk verschil is.

### <a name="continuous-threat-intelligence-monitoring"></a>Continue dreigingen bewaking

Azure Security Center werkt met beveiliging onderzoeks- en wetenschappelijke teams binnen Hallo wereld die voortdurend op wijzigingen in Hallo threat liggend controleren. Dit omvat het Hallo-initiatieven te volgen:

-   **Threat intelligence bewaking:** Threat intelligence omvat mechanismen, indicators gevolgen en bruikbare advies over bestaande of nieuwe bedreigingen. Deze informatie wordt gedeeld in Hallo security-community en Microsoft bewaakt continu threat intelligence feeds van interne en externe bronnen.

-   **Delen van signaal:** inzichten voor teams van de beveiliging in brede portfolio van Microsoft cloud en on-premises services, servers en client eindpunt apparaten worden gedeeld en geanalyseerd.

-   **Microsoft security-specialisten:** actieve betrokkenheid bij via Microsoft-teams dat werkt in de velden van gespecialiseerde beveiliging, zoals forensische en web-aanvalsdetectie.

-   **Detectie afstemmen:** algoritmen voor bestaande klanten gegevenssets worden uitgevoerd en beveiligingsonderzoekers werken met klanten toovalidate Hallo resultaten. True en false positieven zijn gebruikte toorefine machine learning-algoritmen.

Deze gecombineerde inspanningen moet resulteren in nieuwe en verbeterde detecties die u van onmiddellijk profiteren kunt: Er is geen actie voor u tootake.

## <a name="advanced-threat-detection-features---other-azure-services"></a>Advanced Threat detectie onderdelen - andere Azure-Services

### <a name="virtual-machine-microsoft-antimalware"></a>Virtuele Machine: Microsoft Antimalware

[Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) voor Azure een oplossing voor één agent voor toepassingen en tenant-omgevingen is, ontworpen toorun op Hallo achtergrond, zonder menselijke tussenkomst. U kunt beveiliging op basis van Hallo behoeften van uw toepassing werkbelastingen, met een eenvoudige secure--standaard of aangepaste configuratie, met inbegrip van antimalware monitoring Geavanceerd implementeren. Azure antimalware is een beveiligingsoptie voor Azure Virtual Machines en wordt automatisch geïnstalleerd op alle Azure PaaS virtuele machines.

**Functies van Azure toodeploy en schakel Microsoft Antimalware voor uw toepassingen**

#### <a name="microsoft-antimalware-core-features"></a>Microsoft Antimalware-kernfuncties

-   **Real-timebeveiliging -** controleert de activiteit in de Cloud Services en op virtuele Machines toodetect en blok malware worden uitgevoerd.

-   **Geplande scan -** periodiek voert gerichte scannen toodetect schadelijke software, inclusief actieve programma's.

-   **Oplossen van malware -** neemt automatisch actie op de gedetecteerde malware, zoals het verwijderen of schadelijke bestanden in quarantaine plaatsen en schadelijke registervermeldingen opruimen.

-   **Updates van de handtekening -** automatisch wordt geïnstalleerd Hallo nieuwste beveiliging handtekeningen (virusdefinities) tooensure beveiliging is op de hoogte van een vooraf bepaald frequentie.

-   **Antimalware-Engine-updates -** automatisch updates Hallo Microsoft Antimalware-engine.

-   **Updates voor anti-malware-Platform-** automatisch updates Hallo Microsoft Antimalware-platform.

-   **Actieve beveiliging -** telemetrie metagegevens rapporten over gedetecteerde bedreigingen en verdachte resources tooMicrosoft Azure tooensure snelle respons toohello threat Liggend in ontwikkeling en het inschakelen van realtime synchrone handtekening levering via Hallo Microsoft Active Protection System (MAPS).

-   **Voorbeelden van de reporting -** biedt en rapporten voorbeelden toohello Microsoft Antimalware-service toohelp verfijnen Hallo-service en enable probleemoplossing.

-   **Uitsluitingen –** toepassing en service beheerders tooconfigure bepaalde bestanden, processen, en stations tooexclude ze uit de beveiliging en scannen voor prestaties en/of andere redenen.

-   **Gebeurtenissen verzamelen van Antimalware -** Hallo antimalware-servicestatus, verdachte activiteiten en herstelacties genomen in Hallo besturingssysteem gebeurtenislogboek vastgelegd en ze in Azure Storage-account van de klant Hallo verzamelt.

### <a name="azure-sql-database-threat-detection"></a>Detectie van dreigingen voor Azure SQL Database

[Azure SQL Database met detectie van dreigingen](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/) is een nieuwe beveiligingsfunctie intelligence ingebouwd in hello Azure SQL Database-service. Omzeilen Hallo kloksnelheid toolearn, profiel en afwijkende databaseactiviteiten gedetecteerd, Azure SQL Database met detectie van dreigingen identificeert potentiële bedreigingen toohello database.

-Afdelingen of andere aangewezen beheerders kunnen een onmiddellijke melding over verdachte databaseactiviteiten krijgen wanneer deze zich voordoen. Elke melding vindt u informatie over Hallo verdachte activiteit en wordt aanbevolen hoe toofurther onderzoeken en Hallo bedreiging beperken.

Op dit moment detecteert Azure SQL Database met detectie van dreigingen mogelijke beveiligingsproblemen en SQL-injectieaanvallen en database afwijkende toegangspatronen.

Nadat threat detectie e-mailmelding is ontvangen, zijn gebruikers kunnen toonavigate en bekijk Hallo relevante controlerecords via grondige Hallo-koppeling in e-Hiermee opent u een audit viewer en/of de vooraf geconfigureerde controle Excel sjabloon waarin de relevante audit Hallo Hallo records rond de tijd Hallo van Hallo verdachte gebeurtenis op basis van de volgende toohello:
-   Opslag voor Hallo databaseserver met Hallo afwijkende databaseactiviteiten controleren

-   Relevante audit opslag tabel die is gebruikt tijdens het Hallo van toowrite Hallo-audit gebeurtenislogboek

-   Records van het volgende uur sinds gebeurtenis Hallo Hallo-controlegebeurtenissen.

-   Controlerecords met vergelijkbare gebeurtenis-ID bij Hallo Hallo-gebeurtenis (optioneel voor sommige detectoren)

SQL Database Threat detectoren gebruiken een Hallo detectie methoden volgen:

-   **Deterministische detectie –** detecteert verdachte patronen (regels gebaseerd) in Hallo SQL-client-query's die overeenkomen met bekende aanvallen. Deze methode heeft de detectie van hoge en lage fout-positief dekking echter beperkt, omdat binnen de categorie met '-atomic detecties' hello vallen.

-   **Gedrag detectie –** gebreken van de afwijkende activiteit, die is abnormaal gedrag voor Hallo-database die niet tijdens het Hallo afgelopen 30 dagen gevonden is.  Een voorbeeld van de SQL client afwijkende activiteit mag een piek van mislukte aanmeldingen query's, hoog volume aan gegevens uitgepakt, ongebruikelijke canonieke query's en onbekende IP-adressen die worden gebruikt tooaccess Hallo-database

### <a name="application-gateway-web-application-firewall"></a>Application Gateway Web Application Firewall

[Web Application Firewall](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-web-application-firewall) is een functie van [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-webapplicationfirewall-overview) die beveiliging biedt tooweb toepassingen die gebruikmaken van toepassingsgateway voor standaard [levering Toepassingsbeheer](https://kemptechnologies.com/in/application-delivery-controllers) functies. Web application firewall doet dit door deze op basis van de meeste hello te beschermen [OWASP top 10 veelvoorkomende web beveiligingslekken](https://www.owasp.org/index.php/Top_10_2010-Main)

![Application Gateway-webtoepassing Firewally](./media/azure-threat-detection/azure-threat-detection-fig13.png)

-   Beveiliging tegen SQL-injecties

-   Beveiliging tegen scripting op meerdere sites

-   Beveiliging tegen veelvoorkomende aanvallen via internet, zoals opdrachtinjectie, het smokkelen van HTTP-aanvragen, het uitsplitsen van HTTP-antwoorden en aanvallen waarbij een extern bestand wordt ingesloten

-   Beveiliging tegen schendingen van het HTTP-protocol

-   Beveiliging tegen afwijkingen van het HTTP-protocol, zoals een gebruikersagent voor de host en Accept-headers die ontbreken

-   Beveiliging tegen bots, crawlers en scanners

-   Detectie van veelvoorkomende onvolkomenheden in toepassing (dat wil zeggen, Apache, IIS, enz.)

WAF configureren op Application Gateway biedt Hallo voordeel tooyou te volgen:

-   Uw webtoepassing beschermen tegen aanvallen zonder wijziging toobackend code en web beveiligingsproblemen.

-   Beveiligen van meerdere web applications op Hallo dezelfde tijd achter een toepassingsgateway. Toepassingsgateway biedt ondersteuning voor hosting van websites too20 achter een enkele gateway die kan worden alle beschermd tegen aanvallen via Internet.

-   U controleert de webtoepassing tegen aanvallen met behulp van een realtime rapport dat wordt gegenereerd door de WAF-logboeken in Application Gateway.

-   Bepaalde besturingselementen naleving vereisen alle internetgericht eindpunt toobe beveiligd door een WAF-oplossing. Wanneer u Application Gateway met de WAF-functionaliteit gebruikt, kunt u aan deze nalevingsvereisten voldoen.

### <a name="anomaly-detection--an-api-built-with-azure-machine-learning"></a>Afwijkingsdetectie – een gebouwd met Azure Machine Learning API

Afwijkingsdetectie is een API die is gebouwd met Azure Machine Learning die nuttig is voor het detecteren van verschillende soorten afwijkende patronen in de tijd reeksgegevens. Hallo API wijst een afwijkingsdetectie score tooeach in de tijdreeks hello, die kan worden gebruikt gegevenspunt voor het genereren van waarschuwingen, bewaking via dashboards of verbinding te maken met uw ticketsysteem systemen.

Hallo [Afwijkingsdetectie detectie API](https://docs.microsoft.com/azure/machine-learning/machine-learning-apps-anomaly-detection-api) Hallo typen afwijkingen volgen op tijd reeksgegevens kan detecteren:

-   **Bereikt en daalt:** bijvoorbeeld bij de bewaking van Hallo aantal aanmelding fouten tooa service of het nummer van de opdrachten om uitchecken in een e-commercesite ongebruikelijke pieken of dips kunnen wijzen op beveiligingsaanvallen of service-onderbrekingen.

-   **Positieve en negatieve trends:** wanneer het geheugengebruik in cloudcomputing bewaking, bijvoorbeeld verkleinen van de grootte van beschikbaar geheugen is indicatief voor een mogelijke Geheugenlek; bij de bewaking van de service-wachtrijlengte een voortdurende opwaartse trend kan duiden op een onderliggende softwareprobleem.

-   **Wijzigingen en wijzigingen in dynamische waardenbereik op niveau:** bijvoorbeeld niveau wijzigingen in de latenties van een service nadat een service bijwerken of lagere niveaus van uitzonderingen na de upgrade kan interessante toomonitor.

Hallo machine learning op basis van API waarmee:

-   **Flexibele en robuuste detectie:** hello afwijkingsdetectie detectie modellen gebruikers toestaan instellingen voor tooconfigure hoofdlettergevoeligheid en afwijkingen voor seizoensgebonden en niet-seizoensgebonden gegevenssets detecteren. Gebruikers kunnen minder Hallo detectie model toomake hello afwijkingsdetectie API aanpassen of gevoeliger volgens tootheir moet. Dit betekent dat er detecteren Hallo meer of minder zichtbaar afwijkingen in de gegevens met en zonder seizoensgebonden patronen.

-   **Schaalbare en tijdige detectie:** Hallo traditionele manier van bewaking met aanwezig drempels, opgegeven door deskundigen domein kennis kostbaar en niet-schaalbare toomillions dynamisch veranderende gegevenssets zijn. Hallo afwijkingsdetectie detectie modellen in deze API worden geleerd en modellen automatisch zijn afgestemd van historische en realtime-gegevens.

-   **Detectie van proactieve en actie worden uitgevoerd:** trage trend en detectie van de wijzigingen kunnen worden toegepast voor vroege afwijkingsdetectie. Hallo vroege abnormale signalen gedetecteerd worden gebruikte toodirect mensen tooinvestigate en reageren op Hallo probleemgebieden.  Bovendien hoofdoorzaak analysis modellen en waarschuwen hulpprogramma's boven op dit afwijkingsdetectie API-service kunnen worden ontwikkeld.

Hallo afwijkingsdetectie API is een oplossing effectiever en efficiënter voor een breed scala aan scenario's zoals de servicestatus & KPI bewaking, IoT, bewaking van toepassingsprestaties en controle van netwerkverkeer. Hier volgen enkele populaire scenario's waar deze API kan nuttig zijn:
- IT-afdelingen moeten extra tootrack gebeurtenissen, foutcode logboek voor informatie over het gebruik en prestaties (CPU, geheugen, enzovoort) tijdig.

-   Online commercewebsites wilt tootrack klantactiviteiten, paginaweergaven en klikt op.

-   Hulpprogramma voor bedrijven wilt tootrack verbruik van water, gas, elektriciteit en andere bronnen.

-   Faciliteit/gebouw management-services wilt toomonitor temperatuur, vocht en verkeer.

-   IoT/fabrikanten wilt toouse sensorgegevens in tijd reeks toomonitor werkstroom en kwaliteit.

-   Serviceproviders, wachten zoals aanroep centers toomonitor service vraag trend, volume aan incidenten, moeten wachtrijlengte enzovoort.

-   Analytics bedrijfsgroepen wilt toomonitor zakelijke KPI's (zoals sales volume klant patronen, prijzen) abnormale gegevensverplaatsing in realtime.

### <a name="cloud-app-security"></a>Cloud App Security

[Cloud App Security](https://docs.microsoft.com/cloud-app-security/what-is-cloud-app-security) is een essentieel onderdeel van Hallo Microsoft Cloud Security-stack. Er is een uitgebreide oplossing die uw organisatie helpen kan als u tootake volledig gebruikmaken van Hallo belofte van cloud-toepassingen te verplaatsen, maar zorgen ervoor dat u controle, dankzij verbeterde zichtbaarheid in de activiteit. Het helpt tevens Hallo beveiliging van essentiële gegevens in cloud-toepassingen te verhogen.

Met hulpprogramma's waarmee u shadow IT onthullen, risico's te beoordelen, beleid af te dwingen, activiteiten te onderzoeken en bedreigingen te stoppen, verplaatsen uw organisatie veilig toohello cloud tijdens de controle van kritieke gegevens te behouden.

<table style="width:100%">
 <tr>
   <td>Ontdekken</td>
   <td>Onthullen shadow IT-medewerkers met Cloud App Security. Inzicht krijgen door apps, activiteiten, gebruikers, gegevens en bestanden in uw cloudomgeving te detecteren. Detecteren van apps van derden die zijn verbonden tooyour cloud.</td>
 </tr>
 <tr>
   <td>Onderzoeken</td>
   <td>Onderzoek uw cloud-apps met behulp van cloud forensische hulpprogramma's voor toodeep Kennismaking in riskante apps, specifieke gebruikers en bestanden in uw netwerk. Zoek patronen in Hallo gegevens verzameld uit de cloud. Genereren van rapporten toomonitor uw cloud.</td>

 </tr>
 <tr>
   <td>Besturingselement</td>
   <td>Beperk risico's door beleidsregels en waarschuwingen instellen tooachieve maximale controle over het netwerkverkeer van de cloud. Uw gebruikers toosafe, erkende cloud app alternatieven voor Cloud App Security toomigrate gebruiken.</td>

 </tr>
 <tr>
   <td>Beschermen</td>
   <td>Cloud App Security toosanction gebruiken of verbieden toepassingen, afgedwongen preventie van gegevensverlies, machtigingen voor beheer en te delen en aangepaste rapporten en waarschuwingen te genereren.</td>

 </tr>
 <tr>
   <td>Besturingselement</td>
   <td>Beperk risico's door beleidsregels en waarschuwingen instellen tooachieve maximale controle over het netwerkverkeer van de cloud. Uw gebruikers toosafe, erkende cloud app alternatieven voor Cloud App Security toomigrate gebruiken.</td>

 </tr>
</table>


![Cloud App Security](./media/azure-threat-detection/azure-threat-detection-fig14.png)

Cloud App Security integreert zichtbaarheid met uw cloud door

-   Met behulp van Cloud Discovery toomap en identificeren van uw cloudomgeving en Hallo cloud-apps die uw organisatie worden gebruikt.


-   Verbieden van apps in uw cloud en de.



-   Met behulp van eenvoudig te implementeren app-connectors die gebruikmaken van de provider-API's, voor zichtbaarheid en beheer van apps waarmee u verbinding maakt.

-   Helpt u doorlopende controle door de instelling en voortdurend aan te passen, beleid.

Cloud App Security wordt op het verzamelen van gegevens van deze bronnen, geavanceerde analyses op Hallo gegevens uitgevoerd. Onmiddellijk waarschuwt u tooanomalous activiteiten en biedt u grondige zichtbaarheid in uw cloudomgeving. U kunt een beleid in de Cloud App Security configureren en gebruiken deze tooprotect alles in uw cloudomgeving.

## <a name="third-party-atd-capabilities-through-azure-marketplace"></a>Mogelijkheden van de derde partij ATD via Azure Marketplace

### <a name="web-application-firewall"></a>Web Application Firewall

Web Application Firewall inspecteert web binnenkomend verkeer en -blokken SQL-injectie, Cross-Site Scripting, malware uploads & DDoS-toepassing en andere aanvallen die gericht is op uw webtoepassingen. Deze ook inspecteert Hallo-antwoorden van back-end-webservers Hallo gegevens gegevensverlies te voorkomen (DLP). Hallo geïntegreerde access control-engine kan beheerders toocreate gedetailleerde toegangscontrolebeleid voor verificatie, autorisatie en Accounting (AAA), waarmee organisaties sterke verificatie en Gebruikersbeheer.

**Licht:**
-   Detecteert en blokkeert SQL injectie, Cross-Site Scripting, malware uploads, DDoS-toepassing of andere aanvallen op basis van uw toepassing.

-   Verificatie en toegangsbeheer.

-   Scant uitgaand verkeer toodetect gevoelige gegevens en kunt maskeren of blokkeren Hallo informatie uitlekken uit.

-   Hallo-levering van web application inhoud, met mogelijkheden, zoals caching, compressie en andere optimalisaties verkeer wordt versneld.

Voorbeeld van Web Application firewalls beschikbaar in de Azure-marktplaats volgen:

[Barracuda Web Application Firewall, Brocade virtuele Web Application Firewall (Brocade vWAF), Imperva SecureSphere & Hallo ThreatSTOP IP-Firewall.](https://azure.microsoft.com/marketplace/partners/brocade_communications/brocade-virtual-web-application-firewall-templatevtmcluster/)

## <a name="next-steps"></a>Volgende stappen

- [Detectiemogelijkheden van Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)

Geavanceerde detectiemogelijkheden van Azure Security Center helpt tooidentify actieve bedreigingen die gericht is op uw Microsoft Azure-resources en biedt u met Hallo insights toorespond snel nodig.

- [Detectie van dreigingen voor Azure SQL Database](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/)

Azure SQL Database met detectie van dreigingen geholpen adres hun opmerkingen over potentiële bedreigingen tootheir database.
