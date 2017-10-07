---
title: aaaGovernance in Azure | Microsoft Docs
description: Meer informatie over cloud-gebaseerde computers onder meer services als een groot aantal compute-exemplaren en services die kunnen worden geschaald omhoog en omlaag automatisch toomeet Hallo behoeften van uw toepassing of enterprise.
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
ms.date: 06/01/2017
ms.author: TomSh
ms.openlocfilehash: 956e82e92f4232c24069bdb79fed5315f1d6486f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="governance-in-azure"></a>Beheeracties in Azure

We weten dat beveiliging taak in de cloud Hallo en het is belangrijk dat u tijdig en informatie over Azure-beveiliging. Een van de Hallo beste redenen-toouse Azure voor uw toepassingen en services is tootake profiteren van de breed scala aan mogelijkheden en hulpprogramma's voor beveiliging. Deze hulpprogramma's en mogelijkheden helpen mogelijke toocreate veilige oplossingen maken op Hallo beveiligde Azure-platform.

u beter te begrijpen Hallo-matrix van Governance besturingselementen geïmplementeerd in Microsoft Azure van beide Hallo-klant en de Microsoft operations perspectieven, in dit artikel, 'Governance in Azure', wordt geschreven biedt uitgebreide bekijkt hello toohelp Beheer functies die beschikbaar zijn met Microsoft Azure.

## <a name="azure-platform"></a>Azure-platform

Azure is een openbare cloud service-platform die ondersteuning biedt voor een brede selectie van besturingssystemen, programmeertalen, frameworks, hulpprogramma's, databases en apparaten. Linux-containers kan worden uitgevoerd door de integratie van Dockers; bouwen van apps met JavaScript, Python, .NET, PHP, Java en Node.js; Build back-ends voor iOS, Android en Windows-apparaten. Hallo van dezelfde technologieën miljoenen van ontwikkelaars en IT-professionals al zijn afhankelijk van en vertrouwen wordt ondersteund door Azure openbare cloud-services.

Wanneer u bouwen op of IT-activa te migreren, een openbare cloud serviceprovider u zijn afhankelijk te zijn van die organisatie mogelijkheden tooprotect uw toepassingen en gegevens met Hallo services en Hallo besturingselementen ze bieden toomanage Hallo beveiliging van uw cloud-gebaseerde activa.

Azure infrastructuur is speciaal ontworpen van Hallo faciliteit tooapplications voor het hosten van miljoenen klanten tegelijkertijd en biedt een betrouwbare basis waarop bedrijven kunnen voldoen aan de beveiligingsvereisten. Bovendien Azure biedt u veel beveiligingsopties en Hallo mogelijkheid toocontrol ze zodat u beveiliging toomeet Hallo unieke vereisten van uw organisatie implementaties kunt aanpassen.

Dit document helpt u begrijpen hoe Azure Governance mogelijkheden kunnen u helpen te voldoen aan deze vereisten.

## <a name="abstract"></a>Abstracte

Microsoft Azure cloud governance biedt een geïntegreerde controle en advies benadering voor het controleren en adviseren organisaties op het gebruik van hello Azure-platform. Microsoft Azure cloud governance verwijst beleidsregels die zijn betrokken, criteria en toohello besluitvormingsprocessen automatiseert in Hallo planning, architectuur, overname, implementatie, bewerking en beheer van een Cloud computing.

toocreate een plan voor Microsoft Azure cloud toezicht, moet u een diepgaande blik op Hallo mensen, processen en -technologieën die met tootake en vervolgens build frameworks die eenvoudig IT tooconsistently bedrijfsbehoeften en end tegelijkertijd ondersteunen gebruikers met Hallo flexibiliteit toouse Hallo andere van krachtige functies van Microsoft Azure.

Dit artikel wordt beschreven hoe u een verhoogd niveau van beheer van uw IT-bronnen in Microsoft Azure kunt bereiken. Dit artikel vindt u informatie over Hallo beveiliging en beheeracties functies ingebouwd tooMicrosoft Azure.

Hallo Hieronder volgen de belangrijkste Hallo governance besproken in dit artikel:

- Implementatie van beleid, processen en procedures conform de instelling voor organisatiedoelstellingen.

- Beveiliging en continue naleving met de standaarden van organisatie

- Bewaking en waarschuwingen

## <a name="implementation-of-policies-processes-and-procedures"></a>Implementatie van beleid, processen en procedures 

Beheer tot stand heeft gebracht, rollen en verantwoordelijkheden toooversee-implementatie van Hallo informatie beveiligingsbeleid en operationele continuïteit in Azure. Beheer van Microsoft Azure is verantwoordelijk voor het beheren van beveiliging en procedures voor bedrijfscontinuïteit binnen hun respectieve teams (inclusief derden) en om naleving van beveiligingsbeleid, processen en standaarden.

Hier volgen Hallo factoren ontwikkeld:

- Account inrichten

- Abonnement-besturingselementen

- Rollen gebaseerd toegangsbeheer

- Resourcebeheer

- Bronnen bijhouden

- Kritieke bronnen

- API-toegang tooBilling informatie

- Besturingselementen voor netwerken

## <a name="account-provisioning"></a>Account inrichten

Account hiërarchie is een belangrijke stap toouse en de structuur Azure-services binnen een bedrijf en Hallo core bestuursstructuur definiëren. Klanten kunnen verder Hallo-omgeving naar afdelingen, accounts en ten slotte abonnementen onderverdelen in geval van klanten met enterprise agreement voor Hallo.

![Account inrichten](./media/governance-in-azure/security-governance-in-azure-fig1.png)

Als u een enterprise agreement niet hebt, kunt u overwegen [Azure labels](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) op abonnement niveau toodefine hiërarchie. Een Azure-abonnement is de basiseenheid Hallo waarbij alle resources zijn opgenomen. Het definieert ook diverse limieten in Azure, zoals het aantal kernen, bronnen, enzovoort. Abonnementen kunnen bevatten [resourcegroepen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview), die bronnen kunnen bevatten. [RBAC](https://docs.microsoft.com/azure/api-management/api-management-role-based-access-control) beginselen van toepassing op deze drie niveaus.

Elke enterprise verschilt en Hallo-hiërarchie met Azure-Tags in geval van een niet-zakelijke klanten kunt u aanzienlijke flexibiliteit voor hoe Azure is ingedeeld binnen Hallo bedrijf. Voordat u resources in Microsoft Azure implementeert, moet u model van de hiërarchie en Hallo het effect van facturering, toegang tot bedrijfsbronnen en complexiteit.

## <a name="subscription-controls"></a>Abonnement-besturingselementen

Abonnement bepaalt hoe verbruik van resources is gerapporteerd en kosten in rekening gebracht. Abonnementen kunnen worden ingesteld voor afzonderlijke facturering en betaling. We kunnen meerdere abonnementen hebben als genoemde eerdere in een Azure-account. Abonnementen kunnen worden gebruikt toodetermine hello Azure brongebruik van meerdere afdelingen in een bedrijf.

Bijvoorbeeld, als een bedrijf heeft IT, HR en Marketing afdelingen en deze afdelingen hebben verschillende projecten uitgevoerd. Op basis van Hallo informatie over het gebruik van Azure-resources zoals virtuele machines door elke afdeling, kunnen ze worden gefactureerd dienovereenkomstig. Dit kunt we Hallo financiële gegevens van elke afdeling bepalen.

Azure-abonnementen tot stand brengen van de drie parameters:

- een unieke abonnements-ID

- een locatie facturering

- Aantal beschikbare resources

Voor een afzonderlijke die voor een Microsoft-account-ID geldt, een creditcard aantal en de Hallo volledige suite van Azure services--Hoewel Microsoft verbruik limieten, afhankelijk van het type Hallo-abonnement worden afgedwongen.

Azure inschrijving hiërarchieën definiëren hoe de structuur van services binnen een Enterprise Agreement. Hallo Enterprise Portal kan klanten toodivide toegang tooAzure resources zijn gekoppeld aan een Enterprise Agreement op basis van flexibele hiërarchieën aanpasbare tooan organisatie unieke behoeften. Hallo hiërarchie patroon moet overeenkomen met het beheer en de geografische structuur van een organisatie zodat Hallo facturering gekoppelde en toegang tot bedrijfsbronnen nauwkeurig kan worden gehouden voor.

Hallo drie op hoog niveau zijn functionele, zakelijke eenheid en afdelingen geografische, met als een administratieve constructie voor account groeperingen. Binnen elke afdeling kunnen de accounts worden toegewezen aan abonnementen, die silo voor facturerings- en diverse belangrijke limieten maken in Azure (bijv, aantal virtuele machines, opslagaccounts, enz.).

![Abonnement-besturingselementen](./media/governance-in-azure/security-governance-in-azure-fig2.png)


Azure-abonnementen voor organisaties met een Enterprise Agreement, Ga als volgt een hiërarchie vier niveaus:

- de beheerder van de Enterprise-inschrijving

- afdeling beheerder

- de eigenaar van account

- Servicebeheerder

Deze hiërarchie beheerst Hallo volgende:

- Facturering relatie

- Beheer

- Rollen gebaseerd toegangsbeheer (RBAC) tooartifacts

- Grenzen/limieten

- Grenzen

  - Informatie over het gebruik en facturering (tariefkaart op basis van de aanbieding cijfers)

  - Limieten

  - Virtual Network

- Too1 AAD gekoppeld (1 AAD worden gekoppeld aan veel abonnementen)

- Gekoppelde tooan enterprise-inschrijving account

## <a name="role-based-access-controls"></a>Toegangsbeheer op basis van rollen

Wanneer Azure in eerste instantie is uitgebracht, toegang besturingselementen tooa abonnement basic zijn: Administrator of CO-beheerder. Toegang tot tooa abonnement in Hallo klassieke model geïmpliceerde tooall Hallo resources te openen in Hallo-portal. Dit gebrek aan nauwkeuriger beheer geleid toohello verspreiding van abonnementen tooprovide een niveau van redelijke toegangsbeheer voor een Azure-inschrijving.

![Toegangsbeheer op basis van rollen](./media/governance-in-azure/security-governance-in-azure-fig3.png)

De verspreiding van abonnementen is niet meer nodig. Met op rollen gebaseerde toegangsbeheer, kunt u gebruikers toewijzen toostandard functies (zoals algemene 'Lezer' en 'schrijver' typen rollen). U kunt ook aangepaste rollen definiëren.

[Azure op rollen gebaseerde toegangsbeheer (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) kunt Geavanceerd toegangsbeheer voor Azure. Met RBAC kunt verleent u alleen Hallo hoeveelheid toegang die gebruikers nodig tooperform hun werk hebben. Beveiliging gerichte bedrijven moeten zich richten op uw werknemers Hallo exacte machtigingen die ze nodig hebben. Te veel machtigingen tonen een tooattackers account. Te weinig machtigingen betekenen dat werknemers hun werk efficiënt kunnen niet ophalen. Azure op rollen gebaseerde toegangsbeheer (RBAC) kunt u dit probleem oplossen door het aanbieden van Geavanceerd toegangsbeheer voor Azure. Met RBAC toosegregate rechten binnen uw team en verleen alleen Hallo hoeveelheid toegang toousers die zij nodig hebben tooperform hun werk. In plaats van iedereen geven onbeperkte machtigingen in uw Azure-abonnement of de bronnen, kunt u alleen bepaalde acties.

Bijvoorbeeld gebruik RBAC toolet één werknemer virtuele machines in een abonnement beheren, terwijl andere kunt beheren van SQL-databases binnen Hallo hetzelfde abonnement.

Azure RBAC heeft drie basic rollen die tooall brontypen die van toepassing:

- **Eigenaar** heeft volledige toegang tooall bronnen, met inbegrip van Hallo rechts toodelegate toegang tooothers.

- **Inzender** kunt maken en beheren van alle soorten Azure-resources, maar kan geen tooothers toegang verlenen.

- **Lezer** bestaande Azure-resources kunt weergeven.

Hallo rest van Hallo RBAC-rollen in Azure toestaan van beheer van specifieke Azure-resources. Bijvoorbeeld, Hallo rol van inzender van de virtuele Machine kunt Hallo gebruiker toocreate en beheren van virtuele machines. Deze geeft geen ze toegang tot het virtuele netwerk toohello of Hallo-subnet dat Hallo van virtuele machine verbinding maakt.

[Ingebouwde RBAC-rollen](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) lijsten Hallo functies die beschikbaar zijn in Azure. Deze geeft Hallo bewerkingen en het bereik dat elke ingebouwde rol toousers verleent.

Toegang verlenen door toe te wijzen Hallo juiste RBAC-rol toousers, groepen en toepassingen op een bepaalde scope. Hallo-bereik van een roltoewijzing kan dit een abonnement, een resourcegroep of één resource. Een rol die is toegewezen aan een bovenliggend bereik verleent toegang ook toohello onderliggende items erin opgenomen.

Een gebruiker met toegang tooa resourcegroep kunt bijvoorbeeld alle Hallo resources, zoals websites, virtuele machines en subnetten bevat te beheren.

Azure RBAC alleen ondersteunt beheerbewerkingen van Azure-resources in Hallo hello Azure portal en Azure Resource Manager-API's. Deze kan niet toestaan dat alle gegevens niveau bewerkingen voor Azure-resources. U kunt bijvoorbeeld iemand toomanage Storage-Accounts, maar niet toohello blobs of tabellen binnen een Opslagaccount kunnen niet autoriseren. Op deze manier een SQL-database kan worden beheerd, maar niet Hallo tabellen in deze.

Zie [Wat is op rollen gebaseerd toegangsbeheer](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) als u meer informatie wilt over het beheren van toegang met RBAC.

U kunt ook [maakt u een aangepaste rol](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) in gebaseerd toegangsbeheer (RBAC) als geen van de ingebouwde rollen Hallo aan uw specifieke toegang nodig heeft. Aangepaste rollen kunnen worden gemaakt met [Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell), [Azure-opdrachtregelinterface (CLI)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-azure-cli), en Hallo [REST-API](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-rest). Net als de ingebouwde rollen kunnen aangepaste rollen toousers, groepen en toepassingen bij het abonnement, resourcegroep en resource bereiken worden toegewezen.

U kunt binnen elk abonnement verlenen up too2000 roltoewijzingen.

## <a name="resource-management"></a>Resourcebeheer

Door Azure geleverde oorspronkelijk alleen Hallo-klassieke implementatiemodel. In dit model bestonden elke resource afzonderlijk; Er kon geen enkele manier toogroup verwante resources samen. In plaats daarvan moest u toomanually bijhouden welke resources bestaat uit uw oplossing of de toepassing en onthouden toomanage ze in een gecoördineerde benadering.

een oplossing toodeploy, moest u tooeither elke resource afzonderlijk via de klassieke portal Hallo maken of een script maken dat alle Hallo resources in de juiste volgorde Hallo geïmplementeerd. een oplossing toodelete, moest u toodelete elke resource afzonderlijk. U kan niet eenvoudig toepassen en bijwerken van beleid voor toegangsbeheer voor verwante resources. Ten slotte kunt u codes tooresources toolabel ze met voorwaarden die u helpen uw resources bewaken en beheren van facturering niet toepassen.

In 2014 geïntroduceerd Azure Resource Manager, dat Hallo concept van een resourcegroep wordt toegevoegd. Een resourcegroep is een container voor resources die een gemeenschappelijk levenscyclus delen. Hallo Resource Manager-implementatiemodel biedt verschillende voordelen:

- U kunt implementeren, beheren en bewaken van alle Hallo-services voor uw oplossing als een groep in plaats van deze services afzonderlijk te verwerken.

- U kunt herhaaldelijk implementeren van uw oplossing gedurende de levenscyclus en erop vertrouwen dat uw resources worden geïmplementeerd in een consistente status.

- U kunt toegang tot besturingselement tooall bronnen toepassen in de resourcegroep en deze beleidsregels worden automatisch toegepast wanneer nieuwe resources toohello resourcegroep worden toegevoegd.

- U kunt tags toepassen tooresources toologically organiseren alle Hallo resources in uw abonnement.

- U kunt de notatie JSON (JavaScript Object) toodefine Hallo infrastructuur voor uw oplossing. Hallo JSON-bestand staat bekend als Resource Manager-sjabloon.

- U kunt Hallo afhankelijkheden tussen resources zo ze zijn geïmplementeerd in de juiste volgorde Hallo definiëren.

![Resourcebeheer](./media/governance-in-azure/security-governance-in-azure-fig4.png)

Resource Manager kunt u tooput resources in zinvolle groepen voor beheer, facturerings- of natuurlijke affiniteit. Zoals eerder vermeld, wordt Azure heeft twee implementatiemodellen. In eerdere Hallo [model Klassiek](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model), Hallo basiseenheid voor beheer is Hallo-abonnement. Was het moeilijk toobreak resources binnen een abonnement, wat geleid toohello maken van een groot aantal abonnementen heeft. We zagen Hallo introductie van resourcegroepen met Hallo-Resource Manager-model.

Een resourcegroep is een container met verwante resources voor een Azure-oplossing. [Hallo resourcegroep](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) kunnen zijn voor alle Hallo resources voor Hallo oplossing of alleen de resources die u wilt toomanage als een groep. U bepalen hoe u resources tooallocate tooresource groepen op basis van het wat zinvol Hallo meeste voor uw organisatie.

Ga voor aanbevelingen over sjablonen naar [Aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices).

Azure Resource Manager analyseert afhankelijkheden tooensure resources in de juiste volgorde Hallo worden gemaakt. Als een resource afhankelijk is van een waarde uit een andere resource (zoals een virtuele machine die een opslagaccount nodig heeft voor schijven), stelt u een afhankelijkheid in.

>[!Note]
>Zie voor meer informatie [Afhankelijkheden definiëren in Azure Resource Manager-sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-define-dependencies).

U kunt ook Hallo-sjabloon gebruiken voor updates toohello infrastructuur. U kunt bijvoorbeeld een resource tooyour oplossing toevoegen en configuratieregels toevoegen voor Hallo-resources die al zijn geïmplementeerd. Als Hallo-sjabloon maken van een bron, maar dat er bestaat al een resource, voert Azure Resource Manager een update in plaats van een nieuwe asset maken. Azure Resource Manager updates Hallo bestaande asset toohello dezelfde status zoals deze zou zijn als een nieuwe.

Resource Manager biedt uitbreidingen voor scenario's als u extra bewerkingen zoals het installeren van software die niet is opgenomen in het Hallo-installatieprogramma nodig.

## <a name="resource-tracking"></a>Bronnen bijhouden

Als gebruikers in uw organisatie resources toohello abonnement toevoegt, wordt het steeds belangrijker tooassociate resources met de juiste afdeling hello, klanten en omgeving. U kunt metagegevens tooresources via tags toevoegen. U gebruikt [labels](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) tooprovide informatie over het Hallo-resource of Hallo eigenaar. Labels kunnen u alleen cumulatieve toonot en resources op verschillende manieren groeperen, maar die gegevens gebruiken voor de toepassing hello van doorberekening.

Labels gebruiken wanneer u een verzameling complexe resourcegroepen en resources hebben en moet toovisualize deze assets op Hallo handige manier Hallo meeste zin tooyou. U kunt bijvoorbeeld resources die een vergelijkbare rol vervullen in uw organisatie of toohello behoren labelen dezelfde afdeling.

Zonder tags kunnen gebruikers in uw organisatie maken van kunnen meerdere resources die mogelijk moeilijk toolater identificeren en te beheren. Bijvoorbeeld, kunt u desgewenst toodelete alle Hallo resources voor een project. Als deze resources zijn niet gecodeerd voor Hallo-project, moet u deze handmatig zoeken. Taggen kan een belangrijke manier tooreduce onnodige kosten in uw abonnement zijn.

Resources hoeven niet tooreside in Hallo dezelfde resource groep tooshare een label. U kunt uw eigen code taxonomie tooensure dat alle gebruikers in uw organisatie gebruiken algemene labels in plaats van gebruikers die per ongeluk afwijkende tags (zoals 'Afd' in plaats van 'afdeling') toepassen maken.

Bronbeleid kunnen u de standaardregels toocreate voor uw organisatie. U kunt beleidsregels die zorg ervoor dat resources worden gemarkeerd met de juiste waarden Hallo maken.

> [!Note]
> Zie voor meer informatie [bronbeleid voor tags toepassen](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags).

U kunt ook met tags resources via hello Azure-portal bekijken.

Hallo [gebruiksrapport](https://docs.microsoft.com/azure/billing/billing-understand-your-bill) voor uw abonnement bevat labelnamen en waarden, waarmee u toobreak uit de kosten door tags.

> [!Note]
> Zie voor meer informatie over tags [Using tags tooorganize uw Azure-resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

Hallo volgen beperkingen toepassen tootags:

- Elke resource of resourcegroep kan maximaal 15 tag sleutel/waarde-paren hebben. Deze beperking is alleen van toepassing tootags rechtstreeks toegepast toohello resourcegroep of resource. Een resourcegroep mag veel bronnen die elk 15 tag sleutel/waarde-paren hebben.

- Hallo tagnaam is beperkt too512 tekens.

- Hallo tagwaarde is beperkt too256 tekens.

- Labels toegepast toohello resourcegroep wordt niet overgenomen door Hallo resources in die resourcegroep.

Als u meer dan 15 waarden moet u tooassociate aan een resource hebt, gebruikt u een JSON-tekenreeks voor de labelwaarde Hallo. Hallo JSON-tekenreeks kan veel waarden die toegepast tooa enkel labelsleutel zijn bevatten.

### <a name="tags-and-billing"></a>Labels en facturering

Labels kunnen u toogroup uw factureringsgegevens. Bijvoorbeeld, als u meerdere virtuele machines voor verschillende organisaties uitvoert, gebruik Hallo labels toogroup gebruik door kostenplaats. U kunt ook labels toocategorize kosten gebruiken door de runtimeomgeving. Hallo, zoals facturering gebruiksgegevens voor virtuele machines die worden uitgevoerd in de productieomgeving.

U kunt informatie over tags via Hallo ophalen [Azure brongebruik en RateCard APIs](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) of Hallo-gebruik door komma's gescheiden waarden (CSV)-bestand. U Hallo gebruik bestand downloaden van Hallo [Azure-accounts portal](https://account.windowsazure.com/) of [EA portal](https://ea.azure.com/).

>[!Note]
> Zie voor meer informatie over toegang op programmeerniveau toobilling [inzicht in uw Microsoft Azure-brongebruik](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview). Zie voor REST-API-bewerkingen, [Azure Billing REST API-verwijzing](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).

Bij het downloaden van Hallo gebruik CSV voor services die ondersteuning bieden voor facturerings-tags is Hallo labels worden weergegeven in Hallo labels kolom.

## <a name="critical-resource-controls"></a>Besturingselementen voor kritieke bronnen

Als uw organisatie core services toohello abonnement toevoegt, wordt het steeds belangrijker tooensure dat deze services beschikbaar tooavoid business wordt onderbroken zijn. [Resource vergrendelingen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) kunt u toorestrict bewerkingen op waardevolle bronnen waar wijzigt of verwijdert deze zou aanzienlijke gevolgen voor uw toepassingen of cloudinfrastructuur hebben. U kunt vergrendelingen tooa abonnement, resourcegroep of resource toepassen. Normaal gesproken toepassen u vergrendelingen toofoundational resources, zoals virtuele netwerken, gateways en storage-accounts.

Resource vergrendelingen momenteel ondersteuning voor twee waarden: CanNotDelete en alleen-lezen. CanNotDelete betekent dat gebruikers (met de juiste rechten Hallo) kunnen wel lezen of wijzigen van een bron, maar kan niet worden verwijderd. Alleen-lezen betekent dat gemachtigde gebruikers niet verwijderen of wijzigen van een resource.

Vergrendelingen van Resource Manager alleen toooperations die ontstaan in vlak voor Hallo die uit operations verzonden bestaat toepassen<https://management.azure.com>. Hallo vergrendelingen niet beperken hoe resources hun eigen functies uitvoeren. Wijzigingen in de resourcedefinitie zijn beperkt, maar de bewerkingen van resources zijn niet beperkt. Bijvoorbeeld, een vergrendeling van het kenmerk alleen-lezen voor een SQL-Database, voorkomt u dat verwijderen of wijzigen Hallo-database, maar het verhindert niet dat u maken, bijwerken of verwijderen van gegevens in het Hallo-database.

Toepassen van **ReadOnly** toounexpected resultaten kan leiden, omdat bepaalde bewerkingen die lijkt lezen bewerkingen extra acties vereist. Bijvoorbeeld, brengen een **ReadOnly** vergrendeling van een opslagaccount wordt voorkomen dat alle gebruikers aanbieding Hallo sleutels. Hallo lijst sleutels opnieuw wordt verwerkt door een POST-aanvraag omdat Hallo geretourneerd sleutels zijn beschikbaar voor schrijfbewerkingen.

![Besturingselementen voor kritieke bronnen](./media/governance-in-azure/security-governance-in-azure-fig5.png)

Voor een ander voorbeeld: een alleen-lezen-vergrendeling plaatsen op een App Service-resource voorkomt u dat Visual Studio Server Explorer weergeven van bestanden voor de resource Hallo omdat die interactie voor toegang voor schrijven vereist.

In tegenstelling tot rollen gebaseerd toegangsbeheer kunt u management vergrendelingen tooapply een beperking voor alle gebruikers en -functies gebruiken. toolearn over het instellen van machtigingen voor gebruikers en rollen, Zie [toegangsbeheer op basis van rollen in Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure).

Wanneer u een vergrendeling op een bovenliggend bereik toepast, alle resources binnen dat bereik Hallo overnemen dezelfde vergrendelen. Hallo vergrendeling overnemen zelfs resources die u later toevoegen van bovenliggende Hallo. de meest beperkende vergrendeling Hallo in Hallo overname voorrang.

management-vergrendelingen toocreate of verwijderen, moet u toegang tooMicrosoft.Authorization/ hebben _of Microsoft.Authorization/locks/_ acties. Hallo ingebouwde rollen, alleen **eigenaar** en **beheerder voor gebruikerstoegang** deze acties worden verleend.

## <a name="api-access-toobilling-information"></a>API-toegangsgegevens toobilling

Toopull gebruiks- en -gegevens in Azure Billing-API's gebruiken in uw voorkeur hulpprogramma's voor gegevensanalyse. Hello Azure brongebruik en RateCard APIs kunt u nauwkeurige voorspellen en beheren van uw kosten. Hallo API's worden geïmplementeerd als een Resource Provider en een deel van het Hallo-serie API's die worden weergegeven door hello Azure Resource Manager.

### <a name="azure-resource-usage-api-preview"></a>Azure-resource gebruiks-API (Preview)

Gebruik hello Azure [Resource gebruik API](https://msdn.microsoft.com/library/azure/mt219003) tooget uw geschatte Azure verbruiksgegevens. Hallo API bevat:

- **Azure op rollen gebaseerd toegangsbeheer** -toegang configureren beleidsregels op Hallo [Azure-portal](https://portal.azure.com/) of via [Azure PowerShell-cmdlets](https://docs.microsoft.com/powershell/azure/overview) toospecify welke gebruikers of toepassingen toegang kan krijgen gebruiksgegevens van toohello abonnement. Aanroepfuncties moeten standaard tokens van Azure Active Directory voor verificatie gebruiken. Hallo aanroeper tooeither Hallo facturering lezer, de lezer, de eigenaar of bijdrager rol tooget toegang toohello gebruiksgegevens voor een specifieke Azure-abonnement toevoegen.

- **Elk uur of dagelijkse samenvoegingen** - aanroepfuncties kunnen opgeven of ze hun Azure gebruiksgegevens wilt elk uur tijdsintervallen of dagelijks tijdsintervallen. Hallo standaardwaarde is dagelijks.

- **Metagegevens van het exemplaar (inclusief resourcetags)** – ophalen op exemplaarniveau details zoals Hallo volledig gekwalificeerde resource-uri (/subscriptions/ {abonnement-id} /..), groep resourcegegevens en resourcetags Hallo. Deze metagegevens kunt u deterministische en gebruik programmatisch toewijzen door Hallo-tags voor gebruiksvoorbeelden zoals cross in rekening gebracht.

- **Bron-metagegevens** -Resourcedetails zoals de naam van de meter hello, meter categorie meter subcategorie, eenheid en regio geven Hallo aanroeper een beter inzicht in wat is verbruikt. We proberen tooalign resource metagegevens terminologie ook via hello Azure-portal, Azure verbruik CSV, EA CSV, facturering en andere openbare ervaringen, toolet correleren van gegevens over ervaringen.

- **Gebruik voor alle typen bieden** – gebruiksgegevens beschikbaar is voor alle typen zoals betalen naar gebruik, MSDN, bedrag, financieel tegoed en EA bieden.

**Azure-resource RateCard API (Preview)**

Gebruik hello Azure Resource RateCard API tooget Hallo lijst met beschikbare Azure-resources en de geschatte prijsgegevens voor elk. Hallo API bevat:

- **Azure op rollen gebaseerd toegangsbeheer** : uw beleidsregels configureren op Hallo Azure-portal of via Azure PowerShell-cmdlets toospecify waarmee gebruikers of toepassingen kunnen u toegang tot toohello RateCard gegevens. Aanroepfuncties moeten standaard tokens van Azure Active Directory voor verificatie gebruiken. Hallo aanroeper tooeither Hallo lezer, de eigenaar of bijdrager rol tooget toegang toohello gebruiksgegevens voor een bepaald Azure-abonnement toevoegen.

- **Ondersteuning voor betalen per gebruik, MSDN, bedrag en financieel tegoed (EA niet ondersteund) biedt** -voor deze API biedt Azure-aanbieding niveau snelheid informatie. Hallo aanroeper van deze API moet doorgeven in Hallo aanbieding tooget resource Gegevensdetails en tarieven. We kunnen momenteel niet tooprovide EA tarieven omdat EA aanbiedingen tarieven per inschrijving hebt aangepast. Hier volgen enkele Hallo-scenario's die zijn aangebracht met Hallo combinatie van Hallo gebruik en Hallo RateCard APIs mogelijk:

- **Azure besteden tijdens Hallo maand** -gebruik Hallo combinatie van Hallo gebruik en RateCard APIs tooget beter inzicht in uw cloud te besteden aan de tijdens Hallo maand. U kunt elk uur Hallo analyseren en maakt een schatting van dagelijkse buckets van gebruiks- en kosten.

- **Stel waarschuwingen** : Hallo gebruik gebruiken en hello RateCard APIs tooget geschatte cloud verbruik en de kosten en resource of monetaire gebaseerde waarschuwingen instellen.

- **Factuur voorspellen** – Get uw geschatte gebruiks- en cloud besteden en machine learning-algoritmen toopredict welke factuur Hallo achter Hallo Hallo facturering cyclus zou zijn van toepassing.

- **Vooraf verbruik kosten analysis-** – hello RateCard API toopredict hoeveel uw factuur voor het gebruik van uw verwachte niet wanneer u uw werkbelastingen tooAzure verplaatst gebruiken. Als u bestaande workloads in andere clouds of privéclouds hebt, kunt u ook gebruik van uw met hello Azure tarieven tooget een betere schatting van Azure te besteden aan toewijzen. Deze schatting geeft u Hallo toopivot mogelijkheid bieden, en vergelijken tussen Hallo andere aanbiedingstypen dan betalen naar gebruik, zoals bedrag en financieel tegoed. Hallo API biedt u eveneens Hallo mogelijkheid toosee kosten verschillen per regio en kunt u toodo een wat-als kosten analysis toohelp u implementatie beslissingen nemen.

- **Wat-als-analyse** -u kunt bepalen of het meer rendabele toorun werkbelastingen in een andere regio of op een andere configuratie van hello Azure-resource. Azure-resource kosten kunnen verschillen op basis van Hallo u Azure-regio.

- U kunt ook bepalen als een ander Azure-aanbiedingtype resulteert in een betere rentabiliteit op een Azure-resource.

## <a name="networking-controls"></a>Besturingselementen voor netwerken

Toegang tooresources kan zijn (binnen Hallo bedrijfsnetwerk) interne of externe (via internet Hallo). Het is gemakkelijker voor gebruikers in uw organisatie tooinadvertently put-resources in de verkeerde positie Hallo en blootstellen ze toomalicious toegang. Als met on-premises / apparaten, juiste besturingselementen tooensure dat Azure gebruikers Hallo rechts beslissingen voor ondernemingen moeten toevoegen.

![Besturingselementen voor netwerken](./media/governance-in-azure/security-governance-in-azure-fig6.png)

We identificeren belangrijkste resources die elementaire controle van toegang bieden voor abonnement-toezicht. Hallo belangrijkste resources bestaan uit:

### <a name="network-connectivity"></a>Netwerkverbinding

[Virtuele netwerken](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) containerobjecten voor subnetten zijn. Hoewel niet strikt noodzakelijk is het vaak gebruikt bij het verbinden van toepassingen toointernal bedrijfsbronnen. Hallo Azure Virtual Network service kunt u toosecurely andere Azure-resources tooeach verbinding met virtuele netwerken (vnet's).

Een VNet is een weergave van uw eigen netwerk in Hallo cloud. Een VNet is een logische isolatie van hello Azure cloud toegewezen tooyour-abonnement. U kunt ook VNets tooyour on-premises netwerk verbinden.

Hieronder vindt u mogelijkheden voor virtuele netwerken van Azure:

- **Isolatie**: VNets die zijn geïsoleerd van elkaar. U kunt afzonderlijke VNets voor ontwikkeling, testen en productie te maken die Hallo gebruik dezelfde CIDR-adresblokken. Als u daarentegen, kunt u meerdere VNets die gebruikmaken van verschillende CIDR-adresblokken en netwerken met elkaar verbinden. U kunt een VNet segmenteren in meerdere subnetten. Azure biedt interne naamomzetting voor virtuele machines en Cloud Services-rolexemplaren verbonden tooa VNet. U kunt een VNet-toouse desgewenst uw eigen DNS-servers, in plaats van Azure interne naamomzetting configureren.

- **Verbinding met Internet**: alle Azure virtuele Machines (VM) en Cloud Services-rolexemplaren verbonden tooa VNet hebben toegang tot Internet, toohello standaard. U kunt ook een inkomend toospecific resources, inschakelen indien nodig.

- **Azure-resource connectiviteit**: Azure-resources zoals Cloudservices en virtuele machines kunnen worden verbonden toohello hetzelfde VNet. Hallo resources verbinding kunnen maken van andere tooeach met particuliere IP-adressen, zelfs als ze zich in verschillende subnetten. Azure biedt standaardroutering tussen subnetten, VNets en on-premises netwerken, zodat u niet tooconfigure hebt en beheren van routes.

- **VNet-connectiviteit**: VNets, kunt u andere verbonden tooeach tooany VNet toocommunicate inschakelen resources worden verbonden met een resource op een andere VNet.

- **Lokale connectiviteit**: VNets verbonden tooon-premises netwerken via persoonlijke netwerkverbindingen tussen uw netwerk en Azure of een site-naar-site VPN-verbinding via Internet Hallo kan zijn.

- **Filteren van verkeer**: virtuele machine en Cloud Services-rol exemplaren netwerkverkeer kan worden gefilterd binnenkomend en uitgaand op bron-IP-adres en poort, doel-IP-adres en poort en protocol.

- **Routering**: U kunt eventueel Azure standaard routering met BGP-routes via een netwerkgateway of configureren van uw eigen routes overschrijven.

## <a name="network-access-controls"></a>Netwerk-toegangsbeheer

[Netwerkbeveiligingsgroepen](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) zijn vergelijkbaar met een firewall en regels voor hoe een resource "praten kan" via Hallo netwerk opgeeft. Ze bieden gedetailleerde controle over hoe / als een subnet (of de virtuele machine) verbinding kunt maken toohello Internet of andere subnetten in hetzelfde Hallo virtueel netwerk.

Een netwerkbeveiligingsgroep (NSG) bevat een lijst met regels voor toestaan of weigeren netwerkverkeer tooresources verbonden tooAzure virtuele netwerken (VNet). Nsg's kunnen worden gekoppeld toosubnets, afzonderlijke virtuele machines (klassiek) of afzonderlijke netwerkinterfaces (NIC) tooVMs (Resource Manager) zijn gekoppeld.

Wanneer een NSG gekoppeld tooa subnet is, Hallo regels van toepassing tooall bronnen verbonden toohello subnet. Verkeer kan verder worden beperkt door het ook een NSG tooa VM of NIC koppelen

## <a name="security-and-continuous-compliance-with-organizational-standards"></a>Beveiliging en continue naleving met organisatie-standaarden

Elk bedrijf heeft verschillende behoeften en elk bedrijf wordt benutten van verschillende voordelen van cloudoplossingen. Toch klanten van alle soorten Hallo hebben dezelfde basic zorgen over het verplaatsen van toohello cloud. Ze willen tooretain controle over hun gegevens en ze willen dat gegevens toobe veilig bewaard en privé, alle behoud transparantie en naleving.

Klanten willen van cloudproviders is:

- **Beveiligen van onze gegevens** terwijl zijn bevestigd of Hallo cloud kan bieden betere beveiliging van gegevens en beheer, IT-managers nog steeds betreft dat migreren toohello cloud ze kwetsbaarder toohackers dan de huidige laat interne oplossingen.

- **Onze gegevens behouden** persoonlijke Cloud-services verhogen unieke privacy uitdagingen voor bedrijven. Wanneer bedrijven toohello cloud toosave op de kosten van infrastructuur zoeken en hun flexibiliteit verbeteren, bang ze ook te verliezen van de controle van waar hun gegevens worden opgeslagen, wie het en hoe deze wordt gebruikt.

- **Geef ons besturingselement** zelfs als ze van Hallo cloud toodeploy meer innovatieve oplossingen profiteren, bedrijven zijn zeer betrokken zijn bij de controle over hun gegevens verliezen. Hallo recente vermeldingen van overheidsinstanties toegang tot gegevens van de klant, juridische en extra juridische wijze, zorg sommige CIO hoede hun gegevens opslaan in de cloud Hallo.

- **Bevorderen de transparantie** beveiliging, privacy en controle zijn belangrijk toobusiness besluitvormers, ze ook de mogelijkheid hello wilt tooindependently controleren hoe de gegevens worden opgeslagen, geopend en beveiligd.

- **Behouden van compatibiliteit** bij bedrijven uitbreiden voor het gebruik van cloudtechnologieën, Hallo complexiteit en het bereik van standaarden en -voorschriften tooevolve gaan. Bedrijven moeten tooknow die hun compatibiliteit normen wordt voldaan en dat naleving wordt aangepast als de wijziging van de voorschriften gedurende een bepaalde periode.

## <a name="security-configuration-monitoring-and-alerting"></a>Configuratie van beveiliging, controle en waarschuwingen

Azure-abonnees kunnen hun cloudomgevingen beheren vanaf meerdere apparaten, waaronder beheerwerkstations, de pc's van ontwikkelaars en zelfs apparaten van bevoegde eindgebruikers met taakspecifieke rechten. In sommige gevallen worden beheerfuncties uitgevoerd via het web gebaseerde consoles zoals hello Azure-portal. In andere gevallen is er mogelijk rechtstreekse verbindingen tooAzure van on-premises systemen via virtuele particuliere netwerken (VPN's), Terminal Services, protocollen van clienttoepassingen of (programmatisch) hello Azure Service Management API (SMAPI). Clienteindpunten kunnen bovendien zowel in een domein zijn samengevoegd als op zichzelf staand en niet-beheerd zijn, zoals tablets en smartphones.

Hoewel meerdere mogelijkheden voor toegang en beheer een groot aantal opties bieden, kan deze verscheidenheid tooa-cloudimplementatie aanzienlijke risico's kunt toevoegen. Het kan zijn moeilijk toomanage volgen en te controleren. Deze verscheidenheid kan ook leiden tot beveiligingsrisico's via ongereglementeerde toegang tooclient eindpunten die worden gebruikt voor het beheer van cloudservices. Het gebruik van algemene of persoonlijke werkstations voor het ontwikkelen en beheren van infrastructuur brengt onvoorspelbare bedreigingen met zich mee voor bijvoorbeeld surfen op internet (denk aan waterhole-aanvallen) of e-mail (zoals social engineering en phishing).

Bewaking, logboekregistratie en controle bieden een basis voor het bijhouden en begrijpen van beheeractiviteiten, maar deze mogelijk niet altijd haalbaar tooaudit alle acties in detail vanwege de hoeveelheid gegevens die zijn gegenereerd toohello voltooien. Is een aanbevolen procedure echter controle Hallo effectiviteit van Hallo management-beleid.

Azure-beveiliging Governance van AD DS-groepsbeleidsobjecten toocontrol alle Hallo beheerders hun Windows-interfaces, zoals het delen van bestanden. Voer voor beheerwerkstations controle-, bewakings- en logboekregistratieprocessen uit. Houd toegang en gebruik van alle beheerders en ontwikkelaars bij.

### <a name="azure-security-center"></a>Azure security center

Hallo [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) biedt een centrale weergave van de beveiligingsstatus Hallo van resources in het Hallo-abonnementen en aanbevelingen die helpen te voorkomen dat resources waarmee is geknoeid. Deze kunt beleidsregels voor meer gedetailleerd (bijvoorbeeld toepassen beleid toospecific resourcegroepen waarmee Hallo enterprise tootailor hun houding toohello risico die ze adresseert) inschakelen.

![Azure Security Center](./media/governance-in-azure/security-governance-in-azure-fig7.png)

Security Center biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt bedreigingen die anders onopgemerkt, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen te detecteren. Nadat u hebt ingeschakeld [beveiligingsbeleid](https://docs.microsoft.com/azure/security-center/security-center-policies) voor resources van een abonnement, analyseert Security Center Hallo beveiliging van uw resources tooidentify potentiële beveiligingslekken naar voren. Informatie over uw netwerkconfiguratie is onmiddellijk beschikbaar.

Azure Security Center vertegenwoordigt een combinatie van best practice analyse- en beleidsbeheer voor alle resources binnen een Azure-abonnement. Met dit hulpprogramma toouse krachtige en eenvoudig kunt beveiliging teams en risico managers tooprevent, detecteren en reageren toosecurity bedreigingen zoals deze worden automatisch verzameld en beveiligingsgegevens van uw Azure-resources, het Hallo-netwerk en partneroplossingen zoals analyseert antimalwareprogramma's en firewalls.

Bovendien Azure Security Center geavanceerde analyses toegepast, met inbegrip van machine learning en gedragsanalyse tijdens het gebruik van Microsoft-producten en services, Microsoft Digital Crimes Unit (DCU), Hallo Hallo Microsoft over wereldwijde dreigingen Security Response Center (MSRC) en externe feeds. [Beveiliging governance](https://www.credera.com/blog/credera-site/azure-governance-part-4-other-tools-in-the-toolbox/) grote schaal kan worden toegepast op het abonnementsniveau Hallo of domeinpartitie toospecific, gedetailleerde vereisten toegepast tooindividual resources via beleidsdefinitie.

Ten slotte Azure Security Center analyseert de beveiligingsstatus van de resource op basis van deze beleidsregels en gebruikt deze tooprovide begrijpelijke manier mee dashboards en waarschuwingen voor gebeurtenissen zoals detectie van malware of schadelijke IP-verbinding pogingen.

>[!Note]
> Voor meer informatie over het tooapply aanbevelingen lezen [beveiligingsaanbevelingen implementeren in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-recommendations).

Security Center verzamelt gegevens van uw virtuele machines tooassess hun beveiligingsstatus, aanbevelingen voor beveiliging bieden en waarschuwt u toothreats. Wanneer u Security Center voor het eerst opent, worden gegevensverzameling is ingeschakeld op alle virtuele machines in uw abonnement. Verzamelen van gegevens wordt aanbevolen, maar u kunt opt-out door [uitschakelen van gegevensverzameling](https://docs.microsoft.com/azure/security-center/security-center-faq) in Hallo Security Center-beleid.

Ten slotte is Azure Security Center een open platform waarmee Microsoft-partners en onafhankelijke software leveranciers toocreate software die de mogelijkheden in Azure Security Center tooenhance wordt geplaatst.

Azure Security Center monitors hello Azure-resources te volgen:

- Virtuele machines (VM's) (inclusief Cloudservices)

- Virtuele netwerken van Azure

- Azure SQL-service

- Partneroplossingen die zijn geïntegreerd met uw Azure-abonnement zoals web application firewall op virtuele machines en klik op [App Service-omgeving](https://docs.microsoft.com/azure/app-service/app-service-app-service-environments-readme).

### <a name="operations-management-suite"></a>Operations Management Suite

Hallo OMS software development en service van het team informatiebeveiliging en [governance programma](https://github.com/Microsoft/azure-docs/blob/master/articles/log-analytics/log-analytics-security.md) ondersteunt de zakelijke vereisten en toolaws en -voorschriften voldoet zoals beschreven op [Microsoft Azure Trust Center ](https://azure.microsoft.com/support/trust-center/) en [Microsoft Trust Center naleving](https://www.microsoft.com/TrustCenter/Compliance/default.aspx). Hoe OMS beveiligingsvereisten tot stand brengen, identificeert beveiligingsmechanismen beheert en bewaakt de risico's worden er ook beschreven. Jaarlijks, wij controleren beleidsregels, standaarden, procedures en richtlijnen.

Elk teamlid OMS-ontwikkeling ontvangt beveiligingstraining formele toepassing. We gebruiken een versiebeheersysteem intern voor softwareontwikkeling. Elk software-project wordt beveiligd door Hallo versiebeheersysteem.

Microsoft heeft een beveiliging en naleving team dat verantwoordelijk en alle services in Microsoft evalueert. Informatie-afdelingen gezamenlijk Hallo team en niet zijn gekoppeld met Hallo engineering afdelingen die OMS ontwikkelen. Hallo-afdelingen hebben hun eigen Managementketen en uitvoering van een onafhankelijke beoordelingen van producten en services tooensure-beveiliging en naleving.

Operations Management Suite (ook wel bekend als OMS) is een verzameling van management-services die zijn ontworpen in de cloud Hallo van Hallo starten. In plaats van te implementeren en beheren van lokale bronnen, worden OMS onderdelen volledig gehost in Azure. De benodigde configuratie is minimaal en u kunt alles letterlijk binnen een paar minuten in werking zetten.

![Operations Manager-Suite](./media/governance-in-azure/security-governance-in-azure-fig8.png)

Omdat OMS-services worden uitgevoerd Hallo cloud betekent niet dat dat ze uw on-premises omgeving effectief niet beheren.

Het plaatsen van een agent op elke Windows of Linux-computer in uw datacenter en deze stuurt gegevens tooLog Analytics waarin deze kan worden geanalyseerd samen met alle andere gegevens verzameld uit de cloud of op de lokale services. Azure Backup en Azure Site Recovery tooleverage Hallo cloud voor back-up en hoge beschikbaarheid voor op de lokale bronnen gebruiken.

Runbooks in de cloud Hallo geen gewoonlijk toegang tot uw lokale bronnen, maar u kunt een agent installeren op een of meer computers te die fungeert als host voor runbooks in uw datacenter. Wanneer u een runbook start, geeft u gewoon of u wilt dat deze toorun in Hallo cloud of op een lokale worker.

Hallo kernfunctionaliteit van OMS wordt verstrekt door een set services die worden uitgevoerd in Azure. Elke service biedt een specifieke beheerfunctie en u kunt verschillende scenario's voor services tooachieve combineren.

![Operations Manager-Suite](./media/governance-in-azure/security-governance-in-azure-fig9.JPG)

Azure-bewerking manager biedt de functionaliteiten door oplossingen voor het beheer. [Oplossingen voor](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions) voorverpakte sets van logica die een beheerscenario gebruik te maken van een of meer OMS-services te implementeren.

![Azure-bewerking beheren](./media/governance-in-azure/security-governance-in-azure-fig10.png)

Er zijn verschillende oplossingen beschikbaar van Microsoft en partners kunt u eenvoudig toevoegen tooyour Azure-abonnement tooincrease Hallo waarde van uw investering in OMS.

Als partner kunt u uw eigen oplossingen toosupport uw toepassingen en services maken en bieden ze toousers via hello Azure Marketplace of Quick Start-sjablonen.

## <a name="performance-alerting-and-monitoring"></a>Prestatiewaarschuwingen en controle

### <a name="alerting"></a>Waarschuwingen

Waarschuwingen zijn een methode voor het bewaken van metrische gegevens voor Azure-resources, gebeurtenissen of Logboeken en wordt gewaarschuwd wanneer een voorwaarde die u opgeeft wordt voldaan.

**Waarschuwingen in verschillende Azure-services**

Waarschuwingen zijn beschikbaar via andere services, waaronder:

- Application Insights: Kunt WebTest en metrische waarschuwingen.

>[!Note]
> Zie [meldingen instellen in Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-alerts) en [beschikbaarheid en reactiesnelheid van een website bewaken](https://docs.microsoft.com/azure/application-insights/app-insights-monitor-web-app-availability).

- Log Analytics (Operations Management Suite): Hallo van diagnostische logboeken en activiteit tooLog Analytics routering is ingeschakeld. Operations Management Suite kunt metrische gegevens, het logboek en overige Waarschuwingstypen.

>[!Note]
> Zie voor meer informatie, waarschuwingen in [logboekanalyse](https://docs.microsoft.com/azure/log-analytics/log-analytics-alerts).

- Azure bewaken: Hiermee schakelt u waarschuwingen op basis van zowel de metrische waarden als de activiteit logboekgebeurtenissen. U kunt Hallo [REST-API van Azure-Monitor](https://msdn.microsoft.com/library/dn931943.aspx) toomanage waarschuwingen.

>[!Note]
> Zie voor meer informatie [met hello Azure-portal of PowerShell Hallo opdrachtregelinterface toocreate waarschuwingen](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-alerts-portal).

### <a name="monitoring"></a>Bewaking

Prestatieproblemen in uw cloud-app kunnen invloed hebben op uw bedrijf. Degradations kan met meerdere onderdelen onderling verbonden en releases vaak gebeuren op elk gewenst moment. En als u een app ontwikkelt, uw gebruikers problemen die u hebt niet vinden in het testen van meestal te detecteren. U moet weten over deze problemen direct en hulpprogramma's voor het opsporen en oplossen van problemen Hallo hebben. Microsoft Azure is een reeks hulpmiddelen om deze problemen te identificeren.

**Hoe bewaak ik mijn Azure-cloud-apps?**

Er is een reeks hulpmiddelen voor het bewaken van Azure-toepassingen en services. Enkele van hun functies overlappen. Dit is gedeeltelijk omwille van de historische en deels vanwege toohello zorgt voor een vervaging tussen ontwikkeling en de werking van een toepassing.

Hier volgen Hallo principal hulpprogramma's:

- **Monitor voor Azure** is basic hulpprogramma voor het bewaken van services die worden uitgevoerd op Azure. Dit biedt u niveau van de infrastructuur gegevens over de doorvoer van een service en de omgeving rondom Hallo Hallo. Als u uw apps in Azure beheert, moet u bepalen of tooscale omhoog of omlaag bronnen, Azure Monitor u krijgt dan wat u toostart.

- **Application Insights** kunnen worden gebruikt voor ontwikkeling en als een productie-bewakingsoplossing. Deze werkt met een pakket in uw app installeert en biedt dus een meer interne weergave van wat er gebeurt. De gegevens omvatten reactietijden van afhankelijkheden, uitzondering traceringen, foutopsporing van momentopnamen, profielen kan worden uitgevoerd. Het biedt krachtige smart tools voor het analyseren van alle telemetrie deze beide toohelp u fouten opsporen in een app en u begrijpt wat gebruikers doen met het toohelp. U kunt zien of een piek in de reactietijden vervalt toosomething in een app, of een bepaalde externe resourcing probleem. Als u Visual Studio gebruiken en het Hallo-app beschadigd is, kunt u geleid rechts toohello probleem regel (s) van code zodat u deze kunt oplossen.

- **Meld u Analytics** voor degenen die tootune prestaties en plan onderhoud van toepassingen die worden uitgevoerd in de productieomgeving nodig is. In Azure is gebaseerd. Deze verzamelt en gegevens uit diverse bronnen al met een vertraging van 10 too15 minuten worden verzameld. Dit biedt een holistische oplossing voor IT-beheer voor Azure, on-premises en cloud-gebaseerde infrastructuur hebben van derden (zoals Amazon Web Services). Het biedt uitgebreidere extra tooanalyze gegevens over meer bronnen, kunt u complexe query's via alle logboeken en proactief kan waarschuwing bij de opgegeven voorwaarden. U kunt ook aangepaste gegevens verzamelen in de centrale opslagplaats zodat kunnen opvragen en visualiseren van deze.

- **System Center Operations Manager (SCOM)** is voor het beheren en controleren van grote cloud-installaties. U mogelijk al bekend bent met het beheerprogramma voor on-premises Windows Server en op basis van Hyper-V-clouds, maar het kan ook integreren met en beheren van apps van Azure. Onder andere kan Application Insights worden geïnstalleerd op bestaande live apps. Als een app uitgeschakeld wordt, krijgt u in seconden.


## <a name="next-steps"></a>Volgende stappen

- [Aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices).

- [Voorbeelden van de implementatie van Azure-abonnement governance](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-subscription-examples).

- [Microsoft Azure Government](https://docs.microsoft.com/azure/azure-government/).
