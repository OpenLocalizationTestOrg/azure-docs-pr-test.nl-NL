---
title: Azure Data Encryption in rust aaaMicrosoft | Microsoft Docs
description: In dit artikel biedt een overzicht van Microsoft Azure-gegevensversleuteling in rust, Hallo algemene mogelijkheden en algemene overwegingen.
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: TomSh
ms.assetid: 9dcb190e-e534-4787-bf82-8ce73bf47dba
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: yurid
ms.openlocfilehash: d74d103e4fd7585543b4f039877af7d742a6b2e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-encryption-at-rest"></a>Azure Data Encryption in rust
Er zijn meerdere hulpprogramma's in Microsoft Azure toosafeguard gegevens op basis van de behoeften van de beveiliging en naleving van de van het bedrijf tooyour. Dit artikel is gericht op hoe gegevens in rust in Microsoft Azure wordt beveiligd, besproken Hallo verschillende onderdelen die deel uitmaken van Hallo data protection-implementatie en beoordeelt de voor- en nadelen van Hallo verschillende Sleutelbeheer beveiliging methoden. 

Codering in rust is een algemene beveiligingsvereiste. Een voordeel van Microsoft Azure is dat organisaties versleuteling in rust zonder Hallo kosten van de implementatie en beheer- en Hallo risico's van een aangepaste sleutel beheersysteem kunnen bereiken. Organisaties hebben Hallo optie laten Azure versleuteling in rust volledig te beheren. Bovendien hebben organisaties verschillende opties tooclosely versleuteling of versleutelingssleutels beheren.

## <a name="what-is-encryption-at-rest"></a>Wat is versleuteling in rust?
Codering in rust verwijst toohello cryptografische-codering (versleuteling) gegevens wanneer deze wordt bewaard. Hallo versleuteling bij rust ontwerpen in Azure met symmetrische codering tooencrypt en ontsleutelen van grote hoeveelheden gegevens snel volgens tooa eenvoudige conceptuele model:

- Een coderingssleutel voor symmetrische zijn gebruikte tooencrypt gegevens zoals persistent wordt gemaakt 
- Hallo dezelfde versleutelingssleutel is gebruikte toodecrypt als deze is readied voor gebruik in het geheugen die gegevens
- Kan de gegevens worden gepartitioneerd en verschillende sleutels kunnen worden gebruikt voor elke partitie
- Sleutels moeten worden opgeslagen op een veilige locatie met toegang toocertain identiteiten en logboekregistratie sleutelgebruik beperkende beleid voor toegangsbeheer. Gegevensversleutelingssleutels vaak worden versleuteld met asymmetrische codering toofurther limiet toegang (besproken in Hallo *sleutel hiërarchie*verderop in dit artikel)

Hallo hierboven wordt beschreven Hallo op hoog niveau standaardelementen van versleuteling in rust. In de praktijk vereisen belangrijke scenario's voor beheer en controle, evenals de schaal en beschikbaarheid garanties, extra constructies. Microsoft Azure-versleuteling in de Rest-concepten en -onderdelen worden hieronder beschreven.

## <a name="hello-purpose-of-encryption-at-rest"></a>Hallo-doel van versleuteling in rust
Versleuteling in rust is beoogde tooprovide gegevensbeveiliging voor gegevens in rust (zoals hierboven beschreven.) Aanvallen tegen gegevens in rust pogingen tooobtain fysieke toegang toohello hardware op welke Hallo gegevens worden opgeslagen, en vervolgens Hallo inbreuk op gegevens uit. Bij een aanval harde schijf van de server kan hebben is kunnen stoten tijdens het onderhoud zodat een aanvaller tooremove Hallo harde schijf. Hoger Hallo aanvaller plaatst Hallo harde schijf in een computer onder hun besturingselement tooattempt tooaccess Hallo gegevens. 

Codering in rust is ontworpen tooprevent Hallo kwaadwillende persoon toegang krijgen tot gegevens van niet-versleuteld Hallo door ervoor te zorgen Hallo gegevens worden versleuteld op de schijf. Als een aanvaller erin tooobtain een harde schijf met een dergelijke gegevens en geen toegang tot toohello-versleutelingssleutels versleuteld, Hallo aanvaller zou niet in gevaar brengt Hallo gegevens zonder grote problemen. Een aanvaller zou hebben tooattempt aanvallen tegen de versleutelde gegevens die zijn te veel complexere en resource verbruikt dan de toegang tot gegevens op een harde schijf niet-versleuteld in een dergelijk scenario. Om deze reden versleuteling in rust wordt nadrukkelijk aanbevolen en een hoge prioriteit vereiste voor veel organisaties. 

In sommige gevallen is versleuteling in rust ook vereist voor een organisatie behoefte aan gegevens bestuur en naleving inspanningen. Industrie- en government voorschriften, zoals HIPAA, PCI en FedRAMP en internationale voorschriften indelen van specifieke veiligheidsmaatregelen via processen en het beleid met betrekking tot vereisten voor beveiliging en versleuteling van gegevens. Voor veel van deze voorschriften is versleuteling in rust een verplichte meting compatibele gegevensbeheer en-beveiliging vereist. 

Bovendien toocompliance en voorschriften, kan versleuteling in rust moet worden beschouwd als een defense-in-depth-platforms. Microsoft biedt een compatibel platform voor services, toepassingen en gegevens, uitgebreide faciliteit en fysieke beveiliging, data access-beheer en controle, zijn maar er belangrijk tooprovide extra 'overlappende' veiligheidsmaatregelen in geval een Hallo andere veiligheidsmaatregelen is mislukt. Codering in rust is dergelijke een extra defense-mechanisme.

Microsoft is doorgevoerd tooproviding versleuteling in rest-opties voor cloudservices en tooprovide klanten geschikte beheerbaarheid van versleutelingssleutels en toegang toologs weergegeven wanneer de versleutelingssleutels worden gebruikt. Bovendien werkt Microsoft bij het bereiken Hallo doel van het maken van alle klantgegevens die standaard in rust versleuteld.

## <a name="azure-encryption-at-rest-components"></a>Versleuteling van Azure in Rest-onderdelen

Zoals eerder beschreven, Hallo doel is van versleuteling in rust dat de gegevens die worden bewaard op de schijf worden versleuteld met een codering met geheime sleutel. tooachieve dat doel beveiligde sleutel maken, opslag, toegangsbeheer en beheer van Hallo versleuteling sleutels moeten worden opgegeven. Hoewel details variëren kunnen, kunnen Azure-services versleuteling bij rust implementaties worden beschreven in termen van Hallo hieronder concepten die vervolgens in het volgende diagram Hallo worden geïllustreerd.

![Onderdelen](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig1.png)

### <a name="azure-key-vault"></a>Azure Key Vault

locatie voor de opslag van versleutelingssleutels Hallo en toegangstoetsen besturingselement toothose Hallo is de versleuteling van de centrale tooan in rest-model. Hallo sleutels moeten toobe maximaal maar beheerbare zijn beveiligd door de opgegeven gebruikers en services beschikbaar toospecific. Voor Azure-services is Azure Sleutelkluis Hallo aanbevolen oplossing voor opslag van sleutels en biedt een algemene beheerervaring op services. Sleutels worden opgeslagen en beheerd in sleutelkluizen, en toegang tooa sleutelkluis toousers of services kan worden opgegeven. Azure Sleutelkluis ondersteunt klant het maken van sleutels of importeren van de klant sleutels voor versleuteling door de klant beheerd belangrijke scenario's.

### <a name="azure-active-directory"></a>Azure Active Directory

Machtigingen toouse Hallo sleutels opgeslagen in Azure Key Vault toomanage of tooaccess ze voor versleuteling op Rest versleuteling en ontsleuteling, Active Directory-accounts tooAzure kan worden opgegeven. 

### <a name="key-hierarchy"></a>Sleutel hiërarchie

Gewoonlijk meer dan één versleutelingssleutel wordt gebruikt in een versleuteling op rest-implementatie. Asymmetrische codering is nuttig voor het tot stand brengen van Hallo vertrouwen en verificatie nodig voor toegang tot de sleutel en beheer. Symmetrische codering is efficiënter voor bulksgewijze versleuteling en ontsleuteling, waardoor het sterkere versleuteling wilt gebruiken en betere prestaties. Bovendien beperking Hallo gebruik van een sleutel afname één versleuteling Hallo risico dat Hallo sleutel mogelijk meer en kosten van het opnieuw versleutelen Hallo wanneer een sleutel moet worden vervangen. tooleverage hello voordelen van asymmetrische en symmetrische codering en limiet Hallo gebruikt en blootstelling van één sleutel, gebruikt Azure versleuteling bij rust modellen een sleutel hiërarchie bestaat uit Hallo typen sleutels te volgen:

- **Gegevensversleutelingsleutel (DEK)** – een symmetrische sleutel met AES256 tooencrypt gebruikt een partitie of een blok gegevens.  Een enkele bron kan zijn veel partities en veel gegevensversleutelingssleutels. Elk blok van gegevens te versleutelen met een andere sleutel maakt crypto geanalyseerd moeilijker. TooDEKs toegang nodig is voor Hallo resource provider of de toepassing-exemplaar dat is versleutelen en ontsleutelen van een specifiek blok. Wanneer een DEK is vervangen door een nieuwe sleutel alleen moet hello gegevens in de bijbehorende blok opnieuw versleuteld met de nieuwe sleutel Hallo.
- **Versleuteling KEK Key Key ()** – een asymmetrische versleutelingssleutel tooencrypt Hallo versleutelingssleutels gegevens gebruikt. Gebruik van een coderingssleutel Key kunt Hallo gegevensversleutelingssleutels zelf toobe versleuteld en beheerd. Hallo-entiteit die toegang toohello heeft de KEK mogelijk anders dan Hallo-entiteit die Hallo DEK vereist. Hierdoor kan een entiteit toobroker toegang toohello DEK voor Hallo doel om ervoor te zorgen beperkte toegang van elk DEK toospecific partitie. Aangezien Hallo KEK-sleutel vereist toodecrypt hello DEKs is, is Hallo KEK in feite een potentieel waarmee DEKs kunnen worden effectief verwijderd door het verwijderen van Hallo KEK.

Hallo gegevensversleutelingssleutels versleuteld met Hallo sleutel versleutelingssleutels apart zijn opgeslagen en alleen een entity met toegang toohello die coderingssleutel Key tot de versleutelingssleutels voor alle gegevens krijgen kunt versleuteld met die sleutel. Verschillende modellen van opslag van sleutels worden ondersteund. Elk model later in de volgende sectie Hallo uitvoeriger behandeld.

## <a name="data-encryption-models"></a>Versleuteling gegevensmodellen

Understanding Hallo verschillende versleuteling modellen en hun voordelen en nadelen is essentieel voor informatie over hoe verschillende resourceproviders in Azure implementeren versleuteling in rust Hallo. Deze definities worden gedeeld door alle resourceproviders in Azure tooensure gemeenschappelijke taal en taxonomie. 

Er zijn drie scenario's voor serverzijde versleuteling:

- Serverzijde codering met sleutels Service beheerd
    - Azure Resourceproviders uitvoeren Hallo-versleuteling en ontsleuteling bewerkingen
    - Microsoft beheert Hallo sleutels
    - Volledige cloud-functionaliteit

- Server-side '-codering met behulp van de klant beheerd sleutels in Azure Sleutelkluis
    - Azure Resourceproviders uitvoeren Hallo-versleuteling en ontsleuteling bewerkingen
    - Controleert de klant sleutels via Azure Sleutelkluis
    - Volledige cloud-functionaliteit

- Server-side '-versleuteling met behulp van de klant beheerd sleutels van de klant beheerd hardware
    - Azure Resourceproviders uitvoeren Hallo-versleuteling en ontsleuteling bewerkingen
    - Sleutels van de klant besturingselementen van de klant beheerd hardware
    - Volledige cloud-functionaliteit

Overweeg Hallo volgende voor client-side '-versleuteling:

- Azure-services zien te ontsleutelen gegevens niet
- Klanten beheren en opslaan van sleutels lokale (of in andere secure winkels). Sleutels zijn niet beschikbaar tooAzure services
- Cloud verminderde functionaliteit

Hallo ondersteund versleuteling modellen in Azure splitsen in twee groepen: 'Client codering' en 'Server-side codering' als eerder is vermeld. Opmerking, onafhankelijk van Hallo versleuteling bij rust model gebruikt, Azure-services altijd aan te Hallo gebruik van een beveiligde transport, zoals het TLS- of HTTPS raden. Daarom transport-versleuteling moet worden opgelost door Hallo-transportprotocol en mag niet een belangrijke factor om te bepalen welke versleuteling bij rust model toouse zijn.

### <a name="client-encryption-model"></a>Model voor client-versleuteling

Client versleuteling model verwijst tooencryption die buiten Hallo Resource Provider of Azure door Hallo service of de aanroepende toepassing wordt uitgevoerd. Hallo-versleuteling kan worden uitgevoerd door het Hallo-servicetoepassing in Azure of door een toepassing die wordt uitgevoerd in Hallo klant Datacenter. In beide gevallen wanneer de mogelijkheden van dit model versleuteling, hello Azure Resource Provider een versleutelde blob van gegevens zonder Hallo mogelijkheid toodecrypt Hallo gegevens ontvangt op een manier of toegangstoetsen toohello versleuteling. In dit model Hallo sleutelbeheer wordt gerealiseerd door het aanroepen van de service-toepassing hello en is volledig ondoorzichtig toohello Azure-service.

![Client](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig2.png)

### <a name="server-side-encryption-model"></a>De model-serverzijde versleuteling

Serverzijde versleuteling modellen Raadpleeg tooencryption die door hello Azure-service wordt uitgevoerd. In dit model Hallo Resource Provider Hallo voert versleutelen en ontsleutelen van bewerkingen. Bijvoorbeeld, Azure Storage gegevens kan ontvangen in tekst zonder opmaak bewerkingen en voert Hallo versleuteling en ontsleuteling intern. Hallo Resource Provider mogelijk gebruik van de versleutelingssleutels die worden beheerd door Microsoft of door de klant, afhankelijk van de opgegeven configuratie Hallo Hallo. 

![Server](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig3.png)

### <a name="server-side-encryption-key-management-models"></a>Versleuteling serverzijde Sleutelbeheer modellen

Elk Hallo serverzijde versleuteling bij rust modellen impliceert opvallende kenmerken van Sleutelbeheer. Dit omvat waar en hoe de versleutelingssleutels zijn gemaakt en opgeslagen als evenals Hallo toegangsmodellen en Hallo sleutel rotatie procedures. 

#### <a name="server-side-encryption-using-service-managed-keys"></a>Serverzijde codering met sleutels van de service die wordt beheerd

Voor veel klanten is essentiële eis Hallo tooensure die Hallo gegevens worden versleuteld wanneer deze zich in rust. Server-side-versleuteling met behulp van Service beheerd sleutels kunnen dit model waardoor klanten toomark Hallo specifieke bron (Storage-Account, SQL-database, etc.) voor versleuteling en wordt alle Sleutelbeheer aspecten zoals sleuteluitgave, draaiing en back-up tooMicrosoft. De meeste Azure-Services die ondersteuning bieden voor versleuteling in rust doorgaans ondersteuning voor dit model offloading Hallo beheer van Hallo versleuteling sleutels tooAzure. Hello Azure-resourceprovider Hallo sleutels maakt, worden deze in de veilige opslag en haalt wanneer dit nodig is. Dit betekent dat Hallo-service volledige toegang toohello sleutels heeft en Hallo-service volledig beheer over Hallo lifecycle Referentiebeheer heeft.

![Beheerd](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig4.png)

Serverzijde versleuteling met behulp van service beheerd sleutels dus snel adressen Hallo nodig toohave versleuteling in rust met weinig overhead toohello klant. Zodra deze beschikbaar wordt een klant doorgaans hello Azure-portal voor het doelabonnement Hallo en resourceprovider wordt geopend en controleert een vak die aangeeft dat ze graag Hallo gegevens toobe versleuteld. In sommige bronbeheer serverzijde versleuteling met service beheerde sleutels is standaard ingeschakeld. 

Serverzijde versleuteling met Microsoft beheerd sleutels impliceert Hallo-service heeft volledige toegang toostore en beheert Hallo sleutels. Terwijl sommige klanten toomanage Hallo sleutels wilt omdat ze van mening bent dat ze kunnen controleren of de betere beveiliging, moeten hello kosten en risico's die zijn gekoppeld aan een aangepaste sleutel opslagoplossing worden beschouwd bij het evalueren van dit model. In veel gevallen kan een organisatie bepalen dat resourcebeperkingen of risico's van een on-premises-oplossing, kan dit groter is dan de cloudbeheer van versleuteling op rest sleutels Hallo Hallo risico.  Echter dit model kan niet voldoende zijn voor organisaties die vereisten toocontrol Hallo maken hebben of de levenscyclus van versleutelingssleutels Hallo of andere personeel toohave beheren van een service versleutelingssleutels dan die service hello (dat wil zeggen, beheren scheiding van Sleutelbeheer van Hallo algemene model voor het beheer voor Hallo-service).

##### <a name="key-access"></a>Toegang tot de sleutel

Bij gebruik van Server-side-codering met sleutels Service beheerd Hallo sleutel maken, toegang tot opslag en de service worden beheerd door Hallo-service. Normaal gesproken, hello Azure resourceproviders fundamentele versleutelingssleutels Hallo-gegevens in een archief dat toohello gegevens sluit en snel beschikbaar en toegankelijk tijdens het Hallo sleutel versleutelingssleutels worden opgeslagen in een beveiligd archief van de interne wordt opgeslagen.

**Voordelen**

- Eenvoudige instellingen
- Microsoft beheert de belangrijkste rotatie, back-up en redundantie
- De klant heeft geen kosten in verband met de implementatie of Hallo risico van een aangepaste Sleutelbeheer schema Hallo.

**Nadelen**

- Geen controle van de klant over versleutelingssleutels hello (sleutelspecificatie, levenscyclus, intrekken, enz.)
- Er is geen mogelijkheid toosegregate-sleutelbeheer van algemene model voor het beheer voor Hallo-service

#### <a name="server-side-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Server-side '-codering met behulp van de klant beheerde sleutels in Azure Sleutelkluis 

Voor scenario's waarbij Hallo vereiste tooencrypt Hallo gegevens in rust en besturingselement Hallo versleuteling sleutels klanten kunnen met behulp van de klant beheerd sleutels in de Sleutelkluis-serverzijde-versleuteling gebruiken. Sommige services kunnen alleen Hallo hoofdmap coderingssleutel Key opslaan in Azure Sleutelkluis en store Hallo Data Encryption Key in een interne locatie dichter toohello gegevens versleuteld. In dat scenario klanten kunnen brengen hun eigen sleutels tooKey kluis (BYOK: Breng uw eigen sleutel), of nieuwe te genereren en ze tooencrypt Hallo gewenst resources gebruiken. Tijdens het Hallo Resource Provider Hallo-versleuteling en ontsleuteling bewerkingen uitvoert wordt gebruikt Hallo geconfigureerd sleutel Hallo basissleutel voor alle versleutelingsbewerkingen. 

##### <a name="key-access"></a>Toegang tot de sleutel

Hallo omvat-serverzijde versleuteling model met de klant beheerd sleutels in Azure Key Vault het Hallo-service toegang tot Hallo sleutels tooencrypt en ontsleutelen indien nodig. Versleuteling bij rust sleutels bestaan toegankelijk tooa service via een beleid voor toegangsbeheer die identiteit tooreceive Hallo toegangssleutel verlenen. Een Azure-service uitgevoerd namens een bijbehorende-abonnement kan worden geconfigureerd met een identiteit voor de service binnen dat abonnement. Hallo-service kunt Azure Active Directory-verificatie uitvoeren en een verificatietoken voor zichzelf te identificeren als die service namens Hallo abonnement ontvangen. Dat token kan vervolgens worden gepresenteerd tooKey kluis tooobtain een sleutel deze toegang heeft gekregen aan.

Voor bewerkingen met behulp van coderingssleutels, een service-identiteit kan worden toegekend toegang tooany Hallo volgende bewerkingen: ontsleutelen, versleutelen, unwrapKey, wrapKey, controleren, meld u aan, ophalen, weergeven, bijwerken, maken, importeren, verwijderen, back-up en herstellen.

tooobtain een sleutel voor gebruik in versleutelen of ontsleutelen van gegevens in rust Hallo service-identiteit die Hallo Resource Manager-service-exemplaar wordt uitgevoerd als mag UnwrapKey (tooget Hallo-sleutel voor ontsleuteling) en WrapKey (tooinsert een sleutel in de sleutelkluis bij het maken van een nieuwe sleutel).


>[!NOTE] 
>Voor meer informatie over Sleutelkluis autorisatie Hallo beveiligen van uw pagina sleutelkluis in Hallo Zie [Azure Key Vault documentatie](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault). 

**Voordelen**

- Volledige controle over Hallo sleutels gebruikt – sleutels worden beheerd in de Sleutelkluis van Hallo klant onder het beheer van de klant Hallo versleuteling.
- Mogelijkheid tooencrypt meerdere services tooone master
- Kan scheiden sleutelbeheer van algemene model voor het beheer voor Hallo-service
- Service en de locatie van de sleutel kunt over regio's definiëren

**Nadelen**

- De klant heeft volledige verantwoordelijkheid voor het beheer van toegang tot de sleutel
- De klant heeft volledige verantwoordelijkheid voor het beheer van levenscyclus
- Extra overhead voor installatie en configuratie

#### <a name="server-side-encryption-using-service-managed-keys-in-customer-controlled-hardware"></a>Server-side '-codering met behulp van service beheerde sleutels in de hardware van de klant beheerd

Sommige Azure-services inschakelen voor scenario's waarbij Hallo vereiste tooencrypt Hallo gegevens in rust en sleutels in een eigen opslagplaats buiten het beheer van Microsoft hello beheren, Hallo Host uw eigen sleutel (HYOK) Sleutelbeheer model. In dit model Hallo service Hallo sleutel moet worden opgehaald van een externe site en zijn daarom van invloed op prestaties en beschikbaarheid garanties configuratie complexere is. Bovendien zijn vergelijkbaar toowhen Hallo sleutels zijn aan de klant beheerd in Azure Key Vault omdat Hallo-service toegang toohello DEK tijdens het Hallo-versleuteling heeft en ontsleuteling operations Hallo algehele beveiligingsgaranties van dit model.  Dit model is daardoor niet geschikt is voor de meeste organisaties tenzij ze specifieke Sleutelbeheer vereisten waardoor deze hebben. De meeste Azure-Services ondersteunen vanwege beperkingen toothese, niet-serverzijde versleuteling met behulp van de server beheerd sleutels in de hardware van de klant beheerd.

##### <a name="key-access"></a>Toegang tot de sleutel

Bij het gebruik van sleutels van de service die wordt beheerd in de hardware van de klant beheerd serverzijde-versleuteling wordt gebruikt worden op een systeem dat is geconfigureerd door de klant Hallo Hallo sleutels gehandhaafd. Azure-services die ondersteuning bieden voor dit model bieden een manier tot stand brengen van een beveiligde verbinding tooa klant sleutelarchief opgegeven.

**Voordelen**

- Volledige controle over de basissleutel Hallo gebruikte: versleuteling sleutels worden beheerd door een klant opgegeven store
- Mogelijkheid tooencrypt meerdere services tooone master
- Kan scheiden sleutelbeheer van algemene model voor het beheer voor Hallo-service
- Service en de locatie van de sleutel kunt over regio's definiëren

**Nadelen**

- Volledige verantwoordelijkheid voor opslag van sleutels, beveiliging, prestaties en beschikbaarheid
- Volledige verantwoordelijkheid voor het beheer van toegang tot de sleutel
- Volledige verantwoordelijkheid voor het beheer van levenscyclus
- Aanzienlijke-installatie, configuratie en lopende onderhoudskosten
- Verbeterde afhankelijkheid van de beschikbaarheid van het netwerk tussen Hallo klant datacenter en Azure-datacenters.

## <a name="encryption-at-rest-in-microsoft-cloud-services"></a>Versleuteling in rust in de Microsoft cloud-services

Microsoft Cloud-services worden gebruikt in alle drie modellen: IaaS, PaaS, SaaS. Hieronder hebt u voorbeelden van hoe ze op elk model passen:

- Softwareservices, waarnaar wordt verwezen tooas Software als een Server of SaaS waarvoor de toepassing geleverd door de cloud Hallo zoals Office 365.
- Welke klanten gebruikmaken van Hallo cloud in hun toepassingen met behulp van Hallo cloud voor zaken platform-services zoals opslag, analytics en service bus-functionaliteit.
- Infrastructuur als een Service (IaaS) in welke klant implementeren van besturingssystemen en toepassingen die worden gehost in Hallo of infrastructuurservices cloud en andere mogelijk gebruik van cloudservices.

### <a name="encryption-at-rest-for-saas-customers"></a>Codering in rust voor SaaS-klanten

Software als een Service (SaaS)-klanten hebben doorgaans versleuteling in rust ingeschakeld of beschikbaar is in elke service. Office 365-services bevat verschillende opties voor klanten tooverify of schakel versleuteling in rust. Zie voor informatie over Office 365-services gegevens Versleutelingstechnologieën voor Office 365.

### <a name="encryption-at-rest-for-paas-customers"></a>Codering in rust voor PaaS-klanten

Platform als een Service (PaaS) klantgegevens bevindt zich doorgaans in de omgeving van een toepassing kan worden uitgevoerd en een Azure Resource Providers toostore klantgegevens gebruikt. toosee hello versleuteling bij rust opties beschikbaar tooyou onderzoeken Hallo tabel hieronder voor Hallo opslag- en platforms die u gebruikt. Waar wordt ondersteund, worden koppelingen tooinstructions over het inschakelen van versleuteling in rust zijn beschikbaar voor elke resourceprovider. 

### <a name="encryption-at-rest-for-iaas-customers"></a>Codering in rust voor IaaS-klanten

Infrastructuur als een Service (IaaS)-klanten zijn tal van services en toepassingen in gebruik. IaaS-services kunnen inschakelen versleuteling in rust in hun Azure gehoste virtuele machines en VHD's met behulp van Azure Disk Encryption. 

#### <a name="encrypted-storage"></a>Versleutelde opslag

Zoals PaaS, kunnen IaaS-oplossingen gebruikmaken van andere Azure-services waarmee gegevens in rust versleuteld opgeslagen. In dergelijke gevallen kunt u Hallo versleuteling op Rest-ondersteuning inschakelen worden geleverd door elke verbruikte Azure-service. Hallo onderstaande tabel inventariseren Hallo primaire opslag, services en platforms van toepassing en het Hallo-model van versleuteling in rust ondersteund. Waar wordt ondersteund, worden koppelingen tooinstructions gegeven over het inschakelen van versleuteling in rust. 

#### <a name="encrypted-compute"></a>Versleutelde compute

Een volledige codering op Rest-oplossing is vereist dat Hallo gegevens nooit in versleuteld wordt bewaard. Terwijl het in gebruik is, op een server laden Hallo-gegevens in het geheugen, gegevens lokaal op verschillende manieren, met inbegrip van wisselbestand van Windows hello, een crashdump en eventuele Hallo logboekregistratie kan worden gehandhaafd mag toepassing uitvoeren. tooensure deze gegevens worden versleuteld in rust IaaS toepassingen kunnen gebruikmaken van Azure Disk Encryption op een Azure IaaS virtuele machine (Windows of Linux) en de virtuele schijf. 

#### <a name="custom-encryption-at-rest"></a>Aangepaste versleuteling in rust

Het wordt aanbevolen dat waar mogelijk, IaaS toepassingen gebruikmaken van Azure Disk Encryption en versleuteling op Rest-opties die zijn opgegeven door verbruikte Azure-services. In sommige gevallen, zoals onregelmatige versleutelingsvereisten of niet-Azure op basis van opslag, een ontwikkelaar van een IaaS-toepassing moet mogelijk tooimplement versleuteling in rest-zelf. Ontwikkelaars van IaaS-oplossingen beter integreren met Azure verwachtingen voor beheer en de klant dankzij het gebruik van bepaalde onderdelen van Azure. Ontwikkelaars moeten in het bijzonder hello Azure Key Vault service tooprovide beveiligde opslag van sleutels, alsmede hun klanten te bieden met consistente sleutelbeheeropties met die van de meeste Azure-platformservices gebruiken. Aangepaste oplossingen moeten daarnaast tooaccess versleutelingssleutels voor Azure Managed Service-identiteiten tooenable service-accounts gebruiken. Zie voor informatie voor ontwikkelaars over Azure Sleutelkluis en de Service-identiteiten beheerd hun respectieve SDK's.

## <a name="azure-resource-providers-encryption-model-support"></a>Ondersteuning voor Azure-resource providers codering model

Microsoft Azure-Services elke ondersteuning voor een of meer van de versleuteling van Hallo in rest-modellen. Voor sommige services echter een of meer Hallo versleuteling modellen mogelijk niet van toepassing. Services kunnen bovendien ondersteuning voor deze scenario's op verschillende schema's vrijgeven. Deze sectie beschrijft Hallo versleuteling op rest-ondersteuning op Hallo moment van schrijven van dit voor elk Hallo belangrijke gegevens voor Azure storage-services.

### <a name="azure-disk-encryption"></a>Azure schijfversleuteling

De klant met behulp van Azure-infrastructuur als een Service (IaaS)-onderdelen versleuteling in rust voor hun IaaS VM's en schijven via Azure Disk Encryption kunnen bereiken. Versleuteling Zie voor meer informatie over Azure-schijf Hallo [documentatie voor Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

#### <a name="azure-storage"></a>Azure-opslag

Azure Blob- en -bestanden ondersteunt versleuteling in rust voor serverzijde versleutelde scenario's, evenals versleuteld klantgegevens (client-side '-versleuteling).

- Serverzijde: klanten die gebruikmaken van Azure blob-opslag kunnen versleuteling in rust op elke Azure-opslagaccount resource inschakelen. Eenmaal ingeschakeld serverzijde-versleuteling is transparant toohello toepassing uitgevoerd. Zie [Azure Storage Service: versleuteling van gegevens in rust](https://docs.microsoft.com/azure/storage/storage-service-encryption) voor meer informatie.
- Client-side: versleuteling aan clientzijde van Azure Blobs wordt ondersteund. Wanneer met behulp van versleuteling aan clientzijde klanten Hallo-gegevens versleutelen en Hallo gegevens als een gecodeerde blob uploaden. Sleutelbeheer wordt gedaan door de klant Hallo. Zie [Client-Side-versleuteling en Azure Key Vault voor Microsoft Azure Storage](https://docs.microsoft.com/azure/storage/storage-client-side-encryption) voor meer informatie.


#### <a name="sql-azure"></a>SQL Azure

SQL Azure ondersteunt momenteel versleuteling in rust voor servicezijde Microsoft beheerd en versleuteling van de client-side '-scenario's.

Ondersteuning voor server op dat moment wordt de versleuteling geleverd via Hallo SQL-functie is aangeroepen met transparante gegevensversleuteling. Wanneer een klant SQL Azure kunt TDE sleutel automatisch worden gemaakt en ze worden beheerd. Codering in rust kan worden ingeschakeld op Hallo-database en server niveaus. Vanaf juni 2017 [Transparent Data Encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx) standaard op nieuwe databases wordt ingeschakeld.

Client-side '-versleuteling van gegevens van de SQL Azure wordt ondersteund door Hallo [altijd versleuteld](https://msdn.microsoft.com/library/mt163865.aspx) functie. Versleutelde gebruikt altijd een sleutel die zijn gemaakt en opgeslagen door Hallo-client. Klanten kunnen Hallo hoofdsleutel opslaan in een certificaatarchief van de Windows Azure Key Vault of een lokale Hardware Security Module. SQL-gebruikers met behulp van SQL Server Management Studio, kies wat sleutel ze zouden graag toouse tooencrypt welke kolom.

|                                  |                |                     | **Versleuteling Model**             |                              |        |
|----------------------------------|----------------|---------------------|------------------------------|------------------------------|--------|
|                                  |                |                     |                              |                              | **Client** |
|                                  | **Sleutelbeheer** | **Service beheerd sleutel** | **De klant beheerd in de Sleutelkluis** | **Beheer van de klant On-premises** |        |
| **Opslag- en -Databases**            |                |                     |                              |                              |        |
| Schijf (IaaS)                      |                | -                   | Ja                          | Ja*                         | -      |
| SQL Server (IaaS)                |                | Ja                 | Ja                          | Ja                          | Ja    |
| Azure SQL (PaaS)                 |                | Ja                 | Preview                      | -                            | Ja    |
| Azure-opslag (blokkeren/pagina-BLOB's) |                | Ja                 | Preview                      | -                            | Ja    |
| Azure-opslag (bestanden)            |                | Ja                 | -                            | -                            | -      |
| Azure-opslag (tabellen, wachtrijen)   |                | -                   | -                            | -                            | Ja    |
| Cosmos-DB (Document DB)          |                | Ja                 | -                            | -                            | -      |
| StorSimple                       |                | Ja                 | -                            | -                            | Ja    |
| Back-up                           |                | -                   | -                            | -                            | Ja    |
| **Intelligence en analyses**       |                |                     |                              |                              |        |
| Azure Data Factory               |                | Ja                 | -                            | -                            | -      |
| Azure Machine Learning           |                | -                   | Preview                      | -                            | -      |
| Azure Stream Analytics           |                | Ja                 | -                            | -                            | -      |
| HDInsights (Azure Blob-opslag)  |                | Ja                 | -                            | -                            | -      |
| HDInsights (Data Lake Storage)   |                | Ja                 | -                            | -                            | -      |
| Azure Data Lake Store            |                | Ja                 | Ja                          | -                            | -      |
| Azure Data Catalog               |                | Ja                 | -                            | -                            | -      |
| Power BI                         |                | Ja                 | -                            | -                            | -      |
| **IoT-Services**                     |                |                     |                              |                              |        |
| IoT Hub                          |                | -                   | -                            | -                            | Ja    |
| Service Bus                      |                | -              | -                            | -                            | Ja    |
| Event Hubs                       |                | -             | -                            | -                            | -      |


## <a name="conclusion"></a>Conclusie

Bescherming van klantgegevens opgeslagen in Azure-Services is van essentieel belang tooMicrosoft. Alle Azure gehoste services zijn doorgevoerd tooproviding versleuteling bij rust opties. Fundamentele services zoals Azure Storage, Azure SQL en sleutel analytics en services voor bedrijfsinformatie een al versleuteling wilt gebruiken op de Rest-opties. Sommige van deze services sleutels van de klant beheerd en clientzijde versleuteling ondersteunen, evenals service beheerde sleutels en versleuteling. Microsoft Azure-services zijn grotendeels verbeteren van versleuteling Rest beschikbaarheid en nieuwe opties voor de preview en algemene beschikbaarheid in de komende maanden Hallo zijn gepland.

