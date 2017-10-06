---
title: aaaDesign Azure-sjablonen voor complexe oplossingen | Microsoft Docs
description: Bevat aanbevolen procedures voor het ontwerpen van Azure Resource Manager-sjablonen voor complexe scenario 's
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ce1141d6-ece7-4976-acea-1db1f775409e
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: aa45e9a46d79a6336b696cff8fd37f65fa449f11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-azure-resource-manager-templates-when-deploying-complex-solutions"></a>Ontwerppatronen voor Azure Resource Manager-sjablonen bij het implementeren van complexe oplossingen
Flexibele wijze op basis van Azure Resource Manager-sjablonen gebruikt, kunt u complexe topologieën implementeren snel en consistent. U kunt deze implementaties eenvoudig als de offerings evolueren core of tooaccommodate varianten voor uitschieter scenario's of klanten aanpassen.

In dit onderwerp maakt deel uit van een grotere technisch document. tooread hello volledige papier downloaden [World klasse Azure Resource Manager-sjablonen overwegingen en procedures bewezen](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).

Sjablonen combineren Hallo voordelen van hello Azure Resource Manager onderliggende met Hallo aanpassingsvermogen en de leesbaarheid van Notation JSON (JavaScript Object). Met sjablonen, kunt u het volgende doen:

* Topologieën en hun werkbelasting consistent te implementeren.
* Alle resources in een toepassing die samen met resourcegroepen beheren.
* Toepassen op rollen gebaseerde toegang toegangsbeheer (RBAC) toogrant juiste-toousers, groepen en services.
* Labels koppelingen toostreamline taken zoals facturering samentellingen gebruiken.

In dit artikel biedt details over het verbruik scenario's, architectuur en implementatie-patronen die zijn geïdentificeerd tijdens onze ontwerp sessies en de werkelijke sjabloon implementaties van klanten Azure Customer Advisory Team (AzureCAT). Verre academic, deze benaderingen procedures op de hoogte door Hallo ontwikkeling van sjablonen voor 12 van Hallo boven op basis van Linux OSS-technologieën, waaronder zijn beproefde: Apache Kafka, Apache Spark, Cloudera, Couchbase, Hortonworks HDP, DataStax Enterprise aangedreven door Apache Cassandra, Elasticsearch Jenkins, MongoDB, PostgreSQL, Redis en Nagios. 

In dit artikel deelt deze bewezen toohelp u world klasse Azure Resource Manager-sjablonen ontwerpen.  

In onze werk met klanten hebben we verschillende Resource Manager-sjabloon verbruik ervaringen geïdentificeerd voor ondernemingen, systeem SI's (SI) s en CSV's. Hallo volgende secties bevatten een overzicht van veelvoorkomende scenario's en patronen voor verschillende soorten klanten.

## <a name="enterprises-and-system-integrators"></a>Ondernemingen en systeemintegrators
In grote organisaties vaak ziet u twee consumenten van Resource Manager-sjablonen: ontwikkelteams interne software en zakelijke IT. We hebben gevonden dat Hallo scenario's voor Hallo SIs toohello scenario's voor ondernemingen, toegewezen geval Hallo dezelfde overwegingen van toepassing.

### <a name="internal-software-development-teams"></a>Interne software ontwikkelteams
Als uw team software toosupport uw bedrijf ontwikkelt, kunnen sjablonen gemakkelijk tooquickly technologieën voor gebruik in bedrijfsspecifieke oplossingen implementeren. U kunt ook sjablonen toorapidly training omgevingen waarmee team leden toogain nodig vaardigheden maken.

U kunt sjablonen als-is of uitbreiden of ze tooaccommodate opstellen uw behoeften. Met labels binnen sjablonen, kunt u een facturering samenvatting met verschillende weergaven zoals team, project, afzonderlijke en education bieden.

Bedrijven willen vaak software development teams toocreate een sjabloon voor consistente implementatie van een oplossing. Hallo sjabloon vergemakkelijkt beperkingen zodat bepaalde items in deze omgeving vast blijven en kunnen niet worden overschreven. Bijvoorbeeld, een bank mogelijk een sjabloon tooinclude RBAC zodat programmeurs niet een oplossing voor bankieren herzien toosend gegevens tooa persoonlijke storage-account.

### <a name="corporate-it"></a>Zakelijke IT
Zakelijke IT-organisaties doorgaans sjablonen gebruiken voor het leveren van cloud-capaciteit en cloud-gebaseerde mogelijkheden.

#### <a name="cloud-capacity"></a>Cloudcapaciteit
Er is een veelgebruikte manier voor zakelijke IT groepen tooprovide cloudcapaciteit voor teams met 't-shirt grootten', die standaard aanbieding grootten zoals kleine, middelgrote en grote zijn. Hallo t-shirt grootte aanbiedingen kunnen combineren verschillende brontypen en aantallen en tegelijkertijd een niveau van standaardisering die het mogelijk toouse sjablonen maakt. Hallo sjablonen bieden capaciteit in een consistente manier die wordt afgedwongen bedrijfsbeleid en labels tooprovide terugstorting tooconsuming organisaties gebruikt.

Bijvoorbeeld, moet u mogelijk tooprovide ontwikkeling, testen of productieomgevingen binnen welke Hallo software ontwikkelteams hun oplossingen kunnen implementeren. Hallo-omgeving heeft een vooraf gedefinieerde netwerktopologie en elementen die software ontwikkelteams Hallo niet wijzigen, zoals regels voor toegang toohello openbare internet en packet inspection. Mogelijk hebt u ook de organisatie-specifieke rollen voor deze omgevingen met verschillende toegangsrechten voor Hallo-omgeving.

#### <a name="cloud-hosted-capabilities"></a>Cloud-gebaseerde mogelijkheden
U kunt sjablonen toosupport cloud-gebaseerde mogelijkheden, zoals afzonderlijke softwarepakketten of samengestelde aanbiedingen die worden aangeboden toointernal regels van bedrijven gebruiken. Een voorbeeld van een samengestelde aanbieding is analytics as a service-analyse, visualisatie en andere technologieën, geleverd in de configuratie van een geoptimaliseerde, met elkaar verbonden op een vooraf gedefinieerde netwerktopologie.

Cloud-gebaseerde mogelijkheden worden beïnvloed door Hallo beveiligings- en rol overwegingen bij het tot stand gebracht door Hallo cloudcapaciteit aanbiedt op waarop ze worden gebouwd. Deze mogelijkheden worden aangeboden ongewijzigd of als een beheerde service. Voor deze laatste hello, toegang tot beperkte rollen zijn vereist tooenable toegang naar Hallo-omgeving voor beheerdoeleinden.

## <a name="cloud-service-vendors"></a>Leveranciers van cloud-service
Na het praten toomany CSV's, geïdentificeerd we meerdere manieren toodeploy services voor uw klanten en de bijbehorende vereisten.

### <a name="csv-hosted-offering"></a>Aanbieding CSV gehost
Als u uw aanbod in uw eigen Azure-abonnement host, twee hosting benaderingen gelden: een unieke implementatie implementeren voor elke klant of implementeren van schaaleenheden die onderbouwing van een gedeelde infrastructuur, die wordt gebruikt voor alle klanten.

* **Verschillende implementaties voor elke klant.** Verschillende implementaties per klant vereisen vaste topologieën van verschillende bekende configuraties. Deze implementaties mogelijk andere virtuele machine (VM) grootten, verschillend aantal knooppunten en andere hoeveelheden bijbehorende opslag. Labels van implementaties wordt gebruikt voor totaliseren facturering van elke klant. RBAC mogelijk ingeschakelde tooallow klanten toegang tooaspects van hun cloudomgeving.
* **Schaaleenheden in een gedeelde omgeving met meerdere tenants.** Een schaaleenheid voor omgevingen met meerdere tenants kan bestaan uit een sjabloon. In dit geval Hallo dezelfde infrastructuur gebruikte toosupport alle klanten is. Hallo implementaties vertegenwoordigen een groep resources die een niveau van de capaciteit voor Hallo gehost aanbieden, zoals het aantal gebruikers en het aantal transacties leveren. Deze schaaleenheden worden verhoogd of verlaagd omdat vraag vereist.

### <a name="csv-offering-injected-into-customer-subscription"></a>CSV-aanbieding is opgenomen in het klantabonnement
U kunt toodeploy uw software in abonnementen die eigendom zijn van end-klanten. U kunt sjablonen toodeploy verschillende implementaties in een klant Azure-account gebruiken.

Deze implementaties gebruikmaken van RBAC zodat u kunt bijwerken en Hallo implementatie binnen Hallo klantaccount beheren.

### <a name="azure-marketplace"></a>Azure Marketplace
tooadvertise en de offerings via een marketplace, zoals Azure Marketplace verkopen, kunt u sjablonen toodeliver verschillende soorten implementaties die worden uitgevoerd in Azure-account van een klant ontwikkelen. Deze unieke implementaties kunnen doorgaans worden beschreven als een t-shirt grootte (klein, normaal, groot), product/doelgroep type (community, developer, enterprise) of onderdeeltype (basic, hoge beschikbaarheid).  In sommige gevallen kan deze typen kunnen u toospecify bepaalde kenmerken van het Hallo-implementatie, zoals VM-type of aantal schijven.

## <a name="oss-projects"></a>OSS-projecten
Resource Manager-sjablonen inschakelen een community-toodeploy een oplossing snel met bewezen in open-source-projecten. U kunt sjablonen opslaan in een GitHub-opslagplaats zodat Hallo community gedurende een bepaalde periode herzien kunt. Gebruikers kunnen deze sjablonen in hun eigen Azure-abonnementen implementeren.

Hallo volgende secties beschrijven de Hallo dingen die u nodig hebt tooconsider voordat het ontwerpen van uw oplossing.

## <a name="identifying-what-is-outside-and-inside-a-vm"></a>Wat is buiten en in een virtuele machine identificeren
Bij het ontwerpen van uw sjabloon is het handig toolook op Hallo-vereisten in termen van wat buiten en in Hallo virtuele machines (VM's is):

* Buiten betekent Hallo VM's en andere resources van uw implementatie, zoals de netwerktopologie hello, tagging, verwijzingen toohello certificaten/geheimen en toegangsbeheer op basis van rollen. Al deze resources maken deel uit van uw sjabloon.
* Inside betekent dat Hallo software is geïnstalleerd en de algemene desired state configuration. Andere methoden, zoals VM-extensies of scripts worden gebruikt in een geheel of gedeeltelijk. Deze mechanismen kunnen worden geïdentificeerd en uitgevoerd door het Hallo-sjabloon, maar niet in deze.

Algemene voorbeelden van activiteiten die u 'in box Hallo doen zou' zijn-  

* Installeren of verwijderen van serverfuncties en onderdelen
* Software installeren en configureren op Hallo knooppunt- of -cluster
* Websites op een webserver implementeren
* Database-schema's implementeren
* Register of andere typen van configuratie-instellingen beheren
* Bestanden en mappen beheren
* Starten, stoppen en beheren van processen en services
* Lokale groepen en gebruikersaccounts beheren
* Installeren en beheren van pakketten (.msi, .exe, yum, enz.)
* Omgevingsvariabelen beheren
* Uitvoeren van systeemeigen scripts (Windows PowerShell, bash, enz.)

### <a name="desired-state-configuration-dsc"></a>Configuratie van de gewenste status (DSC)
Nadenkt over Hallo interne status van uw VM's na de implementatie, wilt u ervoor dat deze implementatie niet 'nemen' uit Hallo-configuratie die u hebt gedefinieerd en ingeschakeld in broncodebeheer toomake. Deze aanpak zorgt ervoor dat uw ontwikkelaars of beheerders ad-hoc wijzigingen tooan omgeving die niet goedgekeurd, getest, of vastgelegd in de verbinding met broncodebeheer niet maken. Dit besturingselement is belangrijk, omdat Hallo handmatige wijzigingen niet in verbinding met broncodebeheer zijn. Ze zijn ook niet deel uit van de standaardimplementatie Hallo en toekomstige geautomatiseerde implementaties van software Hallo is van invloed op.

Configuratie van de gewenste status is ook belangrijk vanuit het beveiligingsoogpunt van buiten uw interne werknemers. Hackers probeert regelmatig toocompromise en misbruik van softwaresystemen. Als het lukt algemene tooinstall bestanden is en anders Hallo-status van een geïnfecteerd systeem te wijzigen. Met behulp van de van de gewenste statusconfiguratie kunt u identificeren delta's tussen Hallo gewenst en de huidige status en herstellen van een bekende configuratie.

Er zijn resource-uitbreidingen voor Hallo populairste mechanismen voor DSC - PowerShell DSC, Chef en Puppet. Elk van deze uitbreidingen kunt Hallo initiële status van uw virtuele machine implementeren en ook gebruikte toomake ervoor Hallo gewenst status wordt bijgehouden.

## <a name="common-template-scopes"></a>Algemene sjabloon scopes
In onze ervaring hebt we drie key-oplossing sjablonen scopes ontstaan gezien. Deze drie scopes, capaciteit, functionaliteit en end-to-end-oplossing, worden beschreven in Hallo uit te voeren.

### <a name="capacity-scope"></a>Capaciteit bereik
Een scope capaciteit biedt een aantal resources in een standard-topologie die vooraf geconfigureerde toobe in overeenstemming met de voorschriften en het beleid. Hallo meest voorkomende voorbeeld is een standaard ontwikkelingsomgeving in een Enterprise-IT of SI-scenario implementeren.

### <a name="capability-scope"></a>Mogelijkheid bereik
Een scope mogelijkheid is gericht op het implementeren en configureren van een topologie voor een bepaalde technologie. Algemene scenario's met inbegrip van technologieën zoals SQL Server, Cassandra, Hadoop.

### <a name="end-to-end-solution-scope"></a>End-to-end oplossing bereik
Een End-to-End oplossing bereik is gericht dan een enkele functie en in plaats daarvan zijn gericht op een end tooend oplossing bestaat uit meerdere mogelijkheden.  

Een sjabloon gericht op de oplossing scope doet zich voor als een set van een of meer sjablonen voor gericht op de mogelijkheid met oplossings-specifieke bronnen, de logica en de gewenste status. Een voorbeeld van een sjabloon gericht op de oplossing is een oplossingssjabloon end tooend data pipeline. Hallo sjabloon mogelijk oplossings-specifieke topologie en status meng met meerdere gericht op de mogelijkheid oplossingssjablonen zoals Kafka, Storm en Hadoop.

## <a name="choosing-free-form-vs-known-configurations"></a>Gratis formulier versus bekende configuraties te kiezen
U kunt een sjabloon moet bieden consumenten Hallo zoveel mogelijk flexibiliteit, maar een aantal zaken invloed op Hallo keuze van of u in eerste instantie overwegen toouse vrije vorm configuraties versus bekende configuraties. Deze sectie geeft Hallo belangrijke klantvereisten en technische overwegingen die in de vorm van Hallo benadering gedeeld in dit document.

### <a name="free-form-configurations"></a>Vrije-configuraties
Vrije vorm configuraties geluid op Hallo oppervlak, ideaal. Ze kunt u een VM-type tooselect leveren en een willekeurig aantal knooppunten en de gekoppelde schijven voor knooppunten, en als parameters tooa sjabloon doen. Deze aanpak is echter niet ideaal voor een aantal scenario's.

In [grootten voor virtuele machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), Hallo verschillende VM typen en beschikbare grootten worden geïdentificeerd en elk Hallo duurzame aantal schijven (2, 4, 8, 16 of 32) die kan worden gekoppeld. Elke gekoppelde schijf biedt 500 IOPS en veelvouden van deze schijven kunnen worden gegroepeerd voor vermenigvuldigingsfactor dat aantal IOPS. Bijvoorbeeld 16 schijven gegroepeerde tooprovide 8000 IOP's kan worden. Groeperen wordt met configuratie in het Hallo-besturingssysteem, met behulp van Microsoft Windows Storage Spaces of redundante matrix van goedkope schijven (RAID) in Linux uitgevoerd.

Een vrije vorm configuratie maakt het mogelijk Hallo selectie meerdere exemplaren van de virtuele machine, VM verschillende typen en groottes voor deze verschillende schijven voor Hallo VM-type-exemplaren en een of meer scripts tooconfigure Hallo VM inhoud.

Het is gebruikelijk dat een implementatie mogelijk meerdere typen knooppunten, zoals de master- en gegevensknooppunten, zodat deze flexibiliteit vaak voor elk knooppunttype is opgegeven.

Als u clusters toodeploy een significante begint, kunt u beginnen toowork met deze complexe scenario's. Als u een Hadoop-cluster zijn implementeert, bijvoorbeeld zou met 8 hoofdknooppunten 200 gegevensknooppunten en gegroepeerde 4 gekoppelde schijven op elk knooppunt master en gegroepeerde 16 gekoppelde schijven per gegevensknooppunt, er 208 VM's en toomanage 3,232 schijven.

Een opslagaccount wordt vertraging aanvragen bovenstaande die de geïdentificeerde 20.000 transacties per seconde beperken, zodat u moet partitioneren van de storage-account kijken en berekeningen toodetermine Hallo geschikt aantal storage accounts tooaccommodate deze topologie gebruiken. Hallo enorm combinaties die worden ondersteund door Hallo vrije vorm benadering, dynamische berekeningen gegeven zijn vereiste toodetermine Hallo juiste partitioneren. Hallo sjabloontaal van Azure Resource Manager biedt momenteel geen wiskundige functies zodat u moet deze berekeningen uitvoeren in code genereren van een unieke, vastgelegde sjabloon met de juiste informatie Hallo.

In de enterprise IT en SI-scenario's, moet iemand Hallo sjablonen onderhouden en ondersteuning voor topologieën Hallo geïmplementeerd voor een of meer organisaties. Deze extra overhead: verschillende configuraties en sjablonen voor elke klant: sterk wenselijk.

U kunt deze sjablonen toodeploy omgevingen in Azure-abonnement van uw klant, maar zakelijke IT-teams en CSV's doorgaans deze implementeren in hun eigen abonnementen, met behulp van een functie terugstorting toobill hun klanten. In deze scenario's, Hallo doel toodeploy capaciteit voor meerdere klanten is in een pool van abonnementen en veel ingevuld in Hallo abonnementen toominimize abonnement kabels keep-implementaties, dat wil zeggen, meer abonnementen toomanage. Met echt dynamische implementatiegrootte vereist bereiken van dit type dichtheid zorgvuldige planning en extra ontwikkeling voor steigers werk namens Hallo-organisatie.

Bovendien geen abonnementen via een API-aanroep kunt maken maar handmatig moet doen via Hallo-portal. Als het aantal abonnementen Hallo toeneemt, alle resulterende abonnement kabels menselijke tussenkomst vereist, kan niet worden geautomatiseerd. Met zoveel variabiliteit in Hallo grootten van implementaties, hebt u toopre inrichten een aantal abonnementen handmatig tooensure abonnementen beschikbaar zijn.

Deze factoren in overweging moet aan een werkelijk vrije vorm-configuratie is minder dan ten eerste blush interessante.

### <a name="known-configurations--hello-t-shirt-sizing-approach"></a>Bekende configuraties: Hallo t-shirt sizing benadering
In plaats daarvan dan een sjabloon die voorziet in totaal flexibiliteit en talloze variaties bieden, in onze ervaring een algemene patroon is tooprovide Hallo mogelijkheid tooselect bekende configuraties — in feite standaard t-shirt groottes zoals sandbox, kleine, middelgrote en grote. Andere voorbeelden van t-shirt grootten zijn de producten, zoals community edition of enterprise edition.  In andere gevallen mogelijk werklastspecifiek configuraties van een technologie – zoals kaart verminderen of er zijn geen sql.

Veel bedrijven organisaties, OSS-leveranciers en SIs Maak de offerings beschikbaar zijn op deze manier in on-premises gevirtualiseerde omgevingen (ondernemingen) of als software as a service (SaaS)-aanbiedingen (CSV's en OSVs).

Deze aanpak geeft goede, bekende configuraties van verschillende grootten die vooraf zijn geconfigureerd voor klanten. Zonder bekende configuraties moeten end klanten vast formaat van het cluster zelf, rekening te houden in resourcebeperkingen platform en ga math tooidentify Hallo resulterende partitionering van storage-accounts en andere bronnen (vervaldatum toocluster grootte en de resource beperkingen). Bekende configuraties inschakelen klanten tooeasily Selecteer Hallo juiste t-shirt grootte — dat wil zeggen, een bepaalde implementatie. Bovendien toomaking een betere ervaring voor de klant hello, een klein aantal bekende configuraties is eenvoudiger toosupport en kunt u een hoger niveau van de dichtheid leveren.

Een benadering bekende configuratie is gericht op t-shirt grootten kan ook verschillend aantal knooppunten binnen een grootte hebben. Bijvoorbeeld, een klein t-shirt mogelijk tussen 3 en 10 knooppunten.  Hallo t-shirt grootte zou worden ontworpen tooaccommodate up too10 knooppunten en geef Hallo consumer Hallo mogelijkheid toomake vrije vorm selecties toohello maximale grootte geïdentificeerd.  

De grootte van een t-shirt op basis van het type werkbelasting, mogelijk meer vrije vorm van aard in termen van het aantal knooppunten dat kan worden geïmplementeerd, maar heeft verschillende knooppunt werkbelastingsgrootte en configuratie van Hallo software op Hallo knooppunt Hallo.

T-shirt grootten op basis van producten, zoals community of Enterprise, kan unieke resourcetypen en maximum aantal knooppunten dat kan worden geïmplementeerd, hebben doorgaans toolicensing prestaties of beschikbaarheid van functies gekoppeld via andere aanbiedingen Hallo.

U kunt ook geschikt voor klanten met unieke varianten Hallo op basis van een JSON-sjablonen. Uitschieters betreft, kunt u de juiste planning Hallo en overwegingen voor ontwikkeling, ondersteuning en de kosten kunt opnemen.

Op basis van Hallo klant sjabloon verbruik scenario's en vereisten geïdentificeerd aan Hallo begin van dit document, wordt een patroon voor de sjabloon ontleding geïdentificeerd.

## <a name="capacity-and-capability-scoped-solution-templates"></a>Capaciteit en de mogelijkheid bereik oplossingssjablonen
Afbreken biedt een modulaire benadering tootemplate ontwikkeling die ondersteuning biedt voor hergebruik, uitbreidbaarheid, testen en tooling. Deze sectie bevat details over hoe een benadering afbreken toegepaste tootemplates met een bereik van de capaciteit of mogelijkheden kan worden.

Deze aanpak een belangrijkste sjabloon parameterwaarden ontvangt van een sjabloon consumer vervolgens tooseveral typen sjablonen en scripts downstream koppelingen zoals hieronder wordt weergegeven. Parameters en variabelen met statische gegenereerde variabelen zijn waarden gebruikte tooprovide in en uit Hallo gekoppelde sjablonen.

![Sjabloonparameters](./media/best-practices-resource-manager-design-templates/template-parameters.png)

**Parameters worden doorgegeven tooa belangrijkste sjabloon vervolgens toolinked sjablonen**

Hallo secties focus Hallo typen sjablonen en scripts die één sjabloon is onderverdeeld te volgen. Hallo secties vindt u strategieën voor het doorgeven van gegevens tussen Hallo sjablonen staat. Elke sjabloon en Hallo scripttypen in de installatiekopie van het Hallo worden samen met voorbeelden beschreven. Zie voor een voorbeeld contextuele ' samen te stellen: een voorbeeldimplementatie ' verderop in dit document.

### <a name="template-metadata"></a>Metagegevens van de sjabloon
Metagegevens van de sjabloon (Hallo metadata.json-bestand) bevat een sleutel-waardeparen die een sjabloon in de JSON die kan worden gelezen door mensen en softwaresystemen te beschrijven.

![Metagegevens van de sjabloon](./media/best-practices-resource-manager-design-templates/template-metadata.png)

**Metagegevens van de sjabloon wordt beschreven in Hallo metadata.json bestand**

Softwareagents Hallo metadata.json bestand ophalen en Hallo informatie en een koppeling toohello sjabloon publiceren in een webpagina of directory. Elementen zijn *itemDisplayName*, *beschrijving*, *samenvatting*, *githubUsername*, en *dateUpdated*.

Een voorbeeld van een bestand wordt hieronder weergegeven in zijn geheel.

    {
        "itemDisplayName": "PostgreSQL 9.3 on Ubuntu VMs",
        "description": "This template creates a PostgreSQL streaming-replication between a master and one or more slave servers each with 2 striped data disks. hello database servers are deployed into a private-only subnet with one publicly accessible jumpbox VM in a DMZ subnet with public IP.",
        "summary": "PostgreSQL stream-replication with multiple slave servers and a publicly accessible jumpbox VM",
        "githubUsername": "arsenvlad",
        "dateUpdated": "2015-04-24"
    }

### <a name="main-template"></a>Belangrijkste sjabloon
Hallo belangrijkste sjabloon parameters van een gebruiker ontvangt, die informatie toopopulate complexe objectvariabelen worden gebruikt en Hallo gekoppelde sjablonen wordt uitgevoerd.

![Belangrijkste sjabloon](./media/best-practices-resource-manager-design-templates/main-template.png)

**Hallo belangrijkste sjabloon ontvangt parameters van een gebruiker**

Een parameter die is opgegeven is een bekende configuratietype ook wel bekend als Hallo t-shirt grootteparameter vanwege de gestandaardiseerde waarden zoals klein, normaal of groot. In de praktijk, kunt u deze parameter op verschillende manieren. Zie 'Bekende configuratie resources sjabloon' verderop in dit document voor meer informatie.

Sommige resources worden ongeacht Hallo bekende configuratie wordt opgegeven door de parameter van een gebruiker geïmplementeerd. Deze resources zijn ingericht met een sjabloon met één gedeelde resource en worden gedeeld door andere sjablonen zodat Hallo gedeelde bron sjabloon eerste wordt uitgevoerd.

Sommige resources zijn optioneel geïmplementeerd ongeacht Hallo opgegeven bekende configuratie.

### <a name="shared-resources-template"></a>Gedeelde bronnen sjabloon
Deze sjabloon biedt resources die door alle bekende configuraties gedeeld worden. Het bevat Hallo virtueel netwerk, beschikbaarheidssets en andere bronnen die zijn vereist, ongeacht Hallo bekende configuratiesjabloon die is geïmplementeerd.

![Sjabloonresources](./media/best-practices-resource-manager-design-templates/template-resources.png)

**Gedeelde bronnen sjabloon**

Resourcenamen, zoals Hallo virtuele-netwerknaam zijn gebaseerd op de belangrijkste Hallo-sjabloon. U kunt ze als een variabele in die sjabloon opgeven of ze ontvangen als een parameter van de gebruiker hello, zoals vereist door uw organisatie.

### <a name="optional-resources-template"></a>Optionele resources sjabloon
Hallo optionele resources sjabloon bevat resources die programmatisch zijn geïmplementeerd op basis van het Hallo-waarde van een parameter of variabele.

![Optionele resources](./media/best-practices-resource-manager-design-templates/optional-resources.png)

**Optionele resources sjabloon**

Bijvoorbeeld, u kunt een optionele resources sjabloon tooconfigure een jumpbox waarmee indirecte toegang tooa geïmplementeerd omgeving van Hallo openbare Internet. U zou gebruiken als een parameter of variabele tooidentify hello jumpbox moet worden ingeschakeld en Hallo *concat* toobuild Hallo doelnaam voor Hallo-sjabloon, zoals werken *jumpbox_enabled.json*. Sjabloon koppelen Hallo resulterende variabele tooinstall hello jumpbox gebruikt.

U kunt een koppeling Hallo optionele resources sjabloon vanaf meerdere locaties:

* Wanneer de implementatie van toepassing tooevery, maak een koppeling basis van parameters van Hallo gedeelde bronnen sjabloon.
* Wanneer van toepassing tooselect bekende configuraties — bijvoorbeeld alleen installeren op grote implementaties: Maak een koppeling aangestuurde parameter of variabele aangestuurde van Hallo bekende configuratiesjabloon.

Hiermee wordt aangegeven of een bepaalde bron is optioneel mag niet worden aangedreven door Hallo sjabloon consumer maar door Hallo sjabloonprovider. Bijvoorbeeld, moet u mogelijk toosatisfy een bepaald Productvereiste of product-invoegtoepassing (algemeen voor CSV's) of beleidsregels tooenforce (common voor SIs- en enterprise IT groepen). In dergelijke gevallen kunt u een variabele tooidentify of Hallo resource moet worden geïmplementeerd.

### <a name="known-configuration-resources-template"></a>Configuratie voor bekende bronnen sjabloon
In de belangrijkste Hallo-sjabloon is een parameter blootgestelde tooallow Hallo sjabloon consumer toospecify een gewenste configuratie voor bekende toodeploy. Deze bekende configuratie wordt vaak een benadering van de grootte t-shirt gebruikt met een set van configuratie van vaste grootte zoals sandbox, klein, normaal en groot.

![Configuratie voor bekende bronnen](./media/best-practices-resource-manager-design-templates/known-config.png)

**Configuratie voor bekende bronnen sjabloon**

Hallo t-shirt grootte benadering wordt meestal gebruikt, maar Hallo parameters kunnen bestaan uit een reeks bekende configuraties. U kunt bijvoorbeeld een reeks omgevingen voor een zakelijke toepassing zoals ontwikkelen, testen en Product opgeven. Of u kunt deze gebruiken voor een andere cloud service toorepresent eenheden, productversies of configuraties van het product zoals Community-, Developer- of Enterprise schalen.

Net als bij Hallo gedeelde bron sjabloon, worden variabelen toohello bekende configuratiesjabloon doorgegeven vanuit:

* Een eindgebruiker — dat wil zeggen, Hallo parameters toohello belangrijkste sjabloon verzonden.
* Een organisatie, dat wil zeggen, Hallo variables in de belangrijkste Hallo-sjabloon die staan voor interne vereisten of beleidsregels.

### <a name="member-resources-template"></a>Lid resources sjabloon
Een of meer knooppunt lidtypen zijn vaak opgenomen binnen een bekende configuratie. Bijvoorbeeld, met Hadoop hebt u hoofdknooppunten- en gegevensknooppunten. Als u MongoDB installeert, hebt u gegevensknooppunten en een instellingen. Als u DataStax implementeert, hebt u gegevensknooppunten en een virtuele machine met OpsCenter geïnstalleerd.

![Leden resources](./media/best-practices-resource-manager-design-templates/member-resources.png)

**Lid resources sjabloon**

Elk type knooppunten kunt hebben verschillende grootten van virtuele machines, het aantal gekoppelde schijven, scripts tooinstall en instellen Hallo knooppunten, poortconfiguraties voor virtuele machines hello, aantal exemplaren en andere details. Zodat elk knooppunttype opgehaald eigen wordt lid resource sjabloon, die Hallo bevat gedetailleerde informatie over het implementeren en configureren van een infrastructuur, evenals het uitvoeren van scripts toodeploy en configureren van software binnen Hallo VM.

Voor virtuele machines zijn twee soorten scripts meestal gebruikt, algemeen herbruikbare en aangepaste scripts.

### <a name="widely-reusable-scripts"></a>Algemeen herbruikbare scripts
Algemeen herbruikbare scripts kunnen worden gebruikt over meerdere typen sjablonen. Een van Hallo betere voorbeelden van deze algemeen herbruikbare scripts stelt RAID op Linux toopool schijven en een groter aantal IOPS krijgen. Ongeacht Hallo software wordt geïnstalleerd in Hallo VM, biedt dit script hergebruik van bewezen voor algemene scenario's.

![Herbruikbare scripts](./media/best-practices-resource-manager-design-templates/reusable-scripts.png)

**Lid resources sjablonen kunnen algemeen herbruikbare scripts aanroepen**

### <a name="custom-scripts"></a>Aangepaste scripts
Sjablonen roept vaak een of meer scripts die installeren en configureren van software binnen de virtuele machines. Een algemene patroon wordt weergegeven met grote topologieën waarin meerdere exemplaren van een of meer lidtypen zijn geïmplementeerd. Een script voor installatie wordt gestart voor elke virtuele machine die kan worden uitgevoerd parallel, gevolgd door een setup-script dat wordt aangeroepen nadat alle virtuele machines (of alle virtuele machines van het type van een opgegeven lid) zijn geïmplementeerd.

![Aangepaste scripts](./media/best-practices-resource-manager-design-templates/custom-scripts.png)

**Lid resources sjablonen kunnen scripts aanroepen voor een specifiek doel zoals VM-configuratie**

## <a name="capability-scoped-solution-template-example---redis"></a>Gericht op de mogelijkheid oplossing sjabloon voorbeeld - Redis
tooshow hoe een implementatie kan werken, bekijk een voorbeeld van het bouwen van een sjabloon voor Hallo-implementatie en configuratie van Redis in standaard t-shirt formaten.  

Er zijn een set gedeelde bronnen (virtueel netwerk, storage-account, beschikbaarheidssets) en een optionele bron (jumpbox) voor Hallo-implementatie. Er zijn meerdere bekende configuraties die worden weergegeven als t-shirt grootten (klein, normaal, groot), maar met één knooppunt elk type. Er zijn ook twee specifiek doel-scripts (installatie, configuratie).

### <a name="creating-hello-template-files"></a>Hallo maken sjabloonbestanden
Maakt u een Main-sjabloon met de naam azuredeploy.json.

Maken van gedeelde Resources sjabloon met de naam gedeeld resources.json

U maakt een optionele Resource Template tooenable Hallo implementatie van een jumpbox, met de naam jumpbox_enabled.json

Redis maakt gebruik van slechts één knooppunt-type, zodat u één lid Resource sjabloon met de naam knooppunt resources.json maken.

Redis, u wilt tooinstall elke afzonderlijke knooppunten en stel Hallo-cluster.  U hebt scripts tooaccommodate Hallo installatie en ingesteld, redis-cluster-install.sh en redis-cluster-setup.sh.

### <a name="linking-hello-templates"></a>Hallo sjablonen koppelen
Met behulp van sjabloon koppelen, Hallo belangrijkste sjabloon uit de sjabloon gedeelde bronnen toohello, waaruit blijkt dat het virtuele netwerk Hallo gekoppeld.

Logica toegevoegd binnen Hallo belangrijkste sjabloon tooenable consumenten van Hallo sjabloon toospecify of een jumpbox moet worden geïmplementeerd. Een *ingeschakeld* waarde voor Hallo *EnableJumpbox* parameter geeft die klant Hallo wil toodeploy een jumpbox. Wanneer deze waarde is opgegeven, Hallo sjabloon worden aaneengeschakeld *_enabled* als achtervoegsel tooa basissjabloon naam voor de Hallo jumpbox mogelijkheid.

Hallo belangrijkste sjabloon wordt toegepast Hallo *grote* parameter waarde als de naam van een achtervoegsel tooa basissjabloon voor t-shirt grootten en gebruikt vervolgens die waarde in de koppeling van een sjabloon uit te*technology_on_os_large.json*.

Hallo-topologie zou lijken op deze afbeelding.

![Sjabloon redis](./media/best-practices-resource-manager-design-templates/redis-template.png)

**Structuur van de sjabloon voor een Redis-sjabloon**

### <a name="configuring-state"></a>Status configureren
Hallo-knooppunten in cluster hello, er zijn twee stappen tooconfiguring Hallo status, allebei vertegenwoordigd door specifieke doel-Scripts.  Redis installeert 'redis-cluster-install.sh' en 'redis-cluster-setup.sh' hello cluster heeft ingesteld.

### <a name="supporting-different-size-deployments"></a>Ondersteuning van verschillende grootte implementaties
Binnen variabelen, Hallo t-shirt grootte sjabloon Hallo aantal knooppunten van elk type worden toodeploy voor Hallo opgegeven grootte (*grote*). Het aantal VM-exemplaren die gebruikmaken van de resource lussen, unieke namen tooresources bieden door de naam van een knooppunt met een numerieke reeksnummer van toe te voegen implementeert *copyIndex()*. Wordt deze stappen voor beide hot en warme zone VM's, zoals gedefinieerd in Hallo t-shirt naam sjabloon

## <a name="decomposition-and-end-to-end-solution-scoped-templates"></a>End-to-end-oplossing en afbreken binnen het bereik van sjablonen
Een oplossingssjabloon met een bereik van de end-to-end-oplossing is gericht op een end-to-end-oplossing levert.  Deze aanpak is meestal een samenstelling van meerdere gericht op de mogelijkheid sjablonen met aanvullende bronnen, logische en status.

Als gemarkeerd in de onderstaande afbeelding voor hello, wordt hello hetzelfde model gebruikt voor functionaliteit binnen het bereik van sjablonen uitgebreid voor sjablonen met een bereik van de oplossing voor End-to-End.

Een gedeelde Resources sjabloon en een optionele Resources sjablonen fungeren Hallo dezelfde functie als in het Hallo-capaciteit en de mogelijkheid om binnen het bereik van sjabloon benaderingen, maar zijn binnen het bereik van Hallo end tooend oplossing.

Zoals end tooend oplossing binnen het bereik van sjablonen kunnen doorgaans hebben t-shirt grootten, Hallo bekend configuratie Resources sjabloon komt overeen met wat vereist voor een bepaalde bekende configuratie van Hallo-oplossing.

Hallo bekend configuratie Resources sjabloon koppelingen tooone of meer mogelijkheden binnen het bereik oplossingssjablonen die zijn relevante toohello end tooend oplossing zoals Hallo lid Resource sjablonen die vereist voor Hallo end tooend oplossing zijn.

Hallo t-shirt grootte van Hallo oplossing misschien niet anders dan Hallo afzonderlijke gericht op de mogelijkheid sjabloon, zijn variabelen binnen Hallo bekend configuratie Resources sjabloon gebruikte tooprovide Hallo juiste waarden voor downstream mogelijkheid binnen het bereik van oplossing sjablonen toodeploy Hallo juiste t-shirt grootte.

![End-to-end](./media/best-practices-resource-manager-design-templates/end-to-end.png)

**Hallo model wordt gebruikt voor capaciteit of oplossingssjablonen mogelijkheid binnen het bereik kunnen gemakkelijk worden uitgebreid voor end tooend oplossing sjabloon scopes**

## <a name="preparing-templates-for-hello-marketplace"></a>Sjablonen voorbereiden voor Hallo Marketplace
Hallo aanpak gemakkelijk voorgaande is geschikt voor scenario's waarbij ondernemingen SIs en CSV's wilt tooeither Hallo-sjablonen zelf implementeren of hun klanten toodeploy op hun eigen inschakelen.

Een andere gewenste scenario met het implementeren van een sjabloon via Hallo marketplace.  Deze aanpak afbreken werkt voor Hallo marketplace, evenals met enkele kleine wijzigingen.

Zoals eerder vermeld, kunnen de sjablonen gebruikte toooffer distinct implementatietypen in Hallo marketplace koop zijn. Afzonderlijke implementatietypen mogelijk t-shirt grootten (klein, normaal, groot), het product/doelgroep type (community, developer, enterprise) of onderdeeltype (basic, hoge beschikbaarheid).

Gebruikt toolist Hallo verschillende bekende configuraties in Hallo marketplace als onderstaande, Hallo end tooend bestaande oplossing of bereik sjablonen kunnen gemakkelijk worden-mogelijkheden.

Hallo parameters toohello belangrijkste sjabloon worden eerst gewijzigd tooremove Hallo inkomende parameter met de naam tshirtSize.

Tijdens het Hallo verschillende implementatietypen toohello bekend configuratie Resources sjabloon worden toegewezen, moet ook Hallo gemeenschappelijke bronnen en configuratie gevonden in Hallo gedeelde Resources sjabloon en mogelijk die in optionele Resource sjablonen.

Als u uw sjabloon toohello marketplace toopublish wilt, kunt u een afzonderlijk exemplaar van uw sjabloon Main ter vervanging van Hallo eerder beschikbaar inkomende parameter van tshirtSize tooa variabele zijn ingesloten in Hallo-sjabloon maken.

![Marketplace](./media/best-practices-resource-manager-design-templates/marketplace.png)

**Aanpassing van een oplossing binnen het bereik van de sjabloon voor Hallo marketplace**

## <a name="next-steps"></a>Volgende stappen
* toolearn over het delen van de status van en naar sjablonen, Zie [delen status in Azure Resource Manager-sjablonen](best-practices-resource-manager-state.md).
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).

