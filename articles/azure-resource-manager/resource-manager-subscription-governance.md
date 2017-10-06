---
title: aaaBest procedures voor ondernemingen tooAzure verplaatsen | Microsoft Docs
description: Beschrijft een scaffold dat ondernemingen tooensure een veilige en beheerbare omgeving kunnen gebruiken.
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: 8692f37e-4d33-4100-b472-a8da37ce628f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: d1402cf21d0cf740e44c03fc345ecd39a6e1680c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-enterprise-scaffold---prescriptive-subscription-governance"></a>Azure enterprise scaffold - prescriptieve abonnement governance
Ondernemingen zijn steeds meer gebruik nemen van de openbare cloud Hallo voor de wendbaarheid en flexibiliteit. Ze zijn met behulp van de cloud Hallo sterkte toogenerate omzet of resources voor bedrijven Hallo optimaliseren. Microsoft Azure biedt een groot aantal services dat ondernemingen een breed scala aan werkbelastingen en toepassingen zoals bouwstenen tooaddress samenstellen kunnen. 

Maar weten waar toobegin is het vaak moeilijk. Na toouse Azure bepaalt, worden enkele vragen vaak veroorzaakt:

* 'Hoe ik voldoen aan onze wettelijke vereisten voor onafhankelijkheid van de gegevens in bepaalde landen?'
* 'Hoe kan ik ervoor zorgen dat iemand niet per ongeluk een kritieke systeem wijzigt?'
* 'Hoe weet ik elke bron die wordt ondersteund op zodat ik kan account voor het bestand en factuur nauwkeurig weer?'

Hallo kandidaat van een leeg abonnement met geen rails guard is uitdaging. Deze spatie kan uw tooAzure verplaatsen belemmeren.

In dit artikel biedt een startpunt voor technische professionals tooaddress Hallo behoeften voor beheer en saldo met Hallo nodig voor flexibiliteit. Het geeft Hallo concept van een enterprise-scaffold die organisaties helpt in de implementatie en beheer van Azure-abonnementen. 

## <a name="need-for-governance"></a>De noodzaak voor toezicht
Wanneer u tooAzure verplaatst, moet u Hallo onderwerp van governance vroege tooensure Hallo succesvol gebruik van cloud binnen de onderneming Hallo Hallo houden. Helaas Hallo tijd en bureaucracy van het maken van een systeem uitgebreide governance betekent dat sommige bedrijfsgroepen gaat u rechtstreeks toovendors zonder tussenkomst van bedrijven. Deze aanpak kunt Hallo enterprise open toovulnerabilities laten als Hallo resources niet correct worden beheerd. Hallo-kenmerken van de openbare cloud Hallo - flexibiliteit, flexibiliteit en prijzen op basis van verbruik - zijn belangrijk toobusiness groepen die tooquickly moeten voldoen aan Hallo verzoeken van klanten (intern en extern). Maar enterprise IT moet tooensure gegevens en systemen effectief worden beveiligd.

In werkelijkheid is steigers gebruikte toocreate Hallo basis van Hallo-structuur. Hallo scaffold Hallo algemeen overzicht begeleidt en vindt u ankerpunten voor een meer permanente systemen toobe gekoppeld. Een enterprise-scaffold is dezelfde Hallo: een reeks flexibele besturingselementen en mogelijkheden van Azure die structuur toohello omgeving en ankers voor services die zijn gebouwd op Hallo openbare cloud bieden. Het Hallo-opbouwfuncties biedt (IT en bedrijfsgroepen) een toocreate foundation en het koppelen van nieuwe services.

Hallo scaffold is gebaseerd op procedures die we hebben die afkomstig zijn uit veel betrokkenheid met clients van verschillende grootte. Deze clients kunnen variëren van kleine organisaties ontwikkelen van oplossingen in Hallo cloud tooFortune 500 ondernemingen en onafhankelijke softwareleveranciers die zijn gemigreerd en oplossingen in de cloud Hallo te ontwikkelen. Hallo enterprise scaffold is 'speciaal hiervoor gemaakte' toobe flexibele toosupport zowel traditionele IT-werkbelastingen en flexibele werkbelastingen; zoals ontwikkelaars maken van software-as-a-service (SaaS)-toepassingen gebaseerd op de mogelijkheden van Azure.

Hallo enterprise scaffold is bedoeld toobe Hallo foundation van elk nieuw abonnement in Azure. Kunnen beheerders tooensure werkbelastingen voldoen aan Hallo minimale vereisten van een organisatie zonder zo wordt voorkomen dat bedrijfsgroepen en ontwikkelaars snel voldoen aan hun eigen doelstellingen.

> [!IMPORTANT]
> Toezicht is cruciaal toohello succes van Azure. Dit artikel doelen Hallo technische implementatie van een enterprise-scaffold maar alleen raakt op Hallo breder proces en relaties tussen onderdelen Hallo. Beleid governance loopt van Hallo boven naar beneden en door welke Hallo business tooachieve wil wordt bepaald. Natuurlijk Hallo maken van een model governance voor Azure bevat vertegenwoordigers van IT, maar belangrijker sterk weergave van de groep leidinggevenden en gegevensbeveiliging en risicobeheer beheer heeft. In Hallo-end is een enterprise-scaffold over zakelijke risico toofacilitate beperkende missie en doelstellingen van een organisatie.
> 
> 

Hallo volgende afbeelding wordt Hallo onderdelen van Hallo scaffold beschreven. Hallo foundation afhankelijk van een solide plan voor afdelingen, accounts en -abonnementen. Hallo stijlen bestaan uit het Resource Manager-beleid en sterke naamgevingsstandaarden. Hallo rest van Hallo scaffold afkomstig is van de belangrijkste mogelijkheden van Azure en functies die een veilige en beheerbare omgeving.

![scaffold onderdelen](./media/resource-manager-subscription-governance/components.png)

> [!NOTE]
> Azure is snel toegenomen sinds de introductie in 2008. Deze groei vereist Microsoft engineering teams toorethink hun benadering voor het beheren en implementeren van services. Hello Azure Resource Manager-model is in 2014 geïntroduceerd en het klassieke implementatiemodel Hallo vervangt. Resource Manager kunt organisaties toomore eenvoudig implementeren, organiseert en Azure-resources te beheren. Resource Manager bevat garandeert bij het maken van resources voor een snellere implementatie van complexe, onderling afhankelijk oplossingen. Dit omvat ook gedetailleerde toegangsbeheer en Hallo mogelijkheid tootag resources met metagegevens. Microsoft raadt u alle resources via Hallo Resource Manager-model te maken. Hallo enterprise scaffold is expliciet ontworpen voor Hallo Resource Manager-model.
> 
> 

## <a name="define-your-hierarchy"></a>Uw hiërarchie definiëren
Hallo basis van Hallo scaffold is hello Azure Enterprise-inschrijving (en Hallo Enterprise Portal). Hallo enterprise-inschrijving Hallo vorm gedefinieerd en gebruiken van Azure-services binnen een bedrijf Hallo core bestuursstructuur is. Binnen Hallo enterprise agreement klanten kunnen toofurther onderverdelen Hallo-omgeving naar afdelingen, accounts en ten slotte abonnementen. Een Azure-abonnement is de basiseenheid Hallo waarbij alle resources zijn opgenomen. Het definieert ook diverse limieten in Azure, zoals het aantal kernen, bronnen, enzovoort.

![hiërarchie](./media/resource-manager-subscription-governance/agreement.png)

Elke enterprise verschilt en Hallo hiërarchie in de vorige afbeelding Hallo kunt u aanzienlijke flexibiliteit voor hoe Azure is ingedeeld binnen Hallo bedrijf. Voordat u implementeert Hallo richtlijnen die zijn opgenomen in dit document, moet u uw hiërarchie model en Hallo het effect van facturering, toegang tot bedrijfsbronnen en complexiteit.

Hallo drie algemene patronen voor Azure inschrijvingen zijn:

* Hallo **functionele** patroon
  
    ![functionele](./media/resource-manager-subscription-governance/functional.png)
* Hallo **bedrijfseenheid** patroon 
  
    ![bedrijf](./media/resource-manager-subscription-governance/business.png)
* Hallo **geografische** patroon
  
    ![geografische](./media/resource-manager-subscription-governance/geographic.png)

U toepassen Hallo scaffold op Hallo abonnement niveau tooextend Hallo beheervereisten van Hallo onderneming in Hallo abonnement.

## <a name="naming-standards"></a>Naamgevingsstandaarden
de eerste pillar Hallo van Hallo scaffold is naamgevingsvereisten. Goed ontworpen naamgevingsstandaarden inschakelen tooidentify resources in Hallo-portal op een factuur en binnen scripts. Zeer waarschijnlijk al naamgevingsvereisten voor on-premises infrastructuur. Wanneer u Azure tooyour omgeving toevoegt, moet u de naamgeving van standaarden tooyour Azure-resources uitbreiden. Standaard Naming waardoor efficiënter beheer van Hallo-omgeving op alle niveaus.

> [!TIP]
> Voor naamgevingsregels:
> * Bekijk en vaststellen waar mogelijk Hallo [Patterns and practice richtlijnen](../guidance/guidance-naming-conventions.md). In deze richtlijnen kunt u op een zinvolle naamgevingsnorm bepalen.
> * Gebruik camelCasing voor namen van bronnen (zoals myResourceGroup en vnetNetworkName). Opmerking: Er zijn bepaalde bronnen, zoals de storage-accounts, waarbij de enige optie Hallo toouse kleine letters (en geen speciale tekens).
> * Overweeg het gebruik van Azure Resource Manager-beleid (beschreven in de volgende sectie Hallo) tooenforce naamgevingsvereisten.
> 
> Hallo voorgaande tips helpen u bij het invoeren van een consistente naamgeving.

## <a name="policies-and-auditing"></a>Beleid en controle
de tweede pillar Hallo van Hallo scaffold omvat het maken van [Azure Resource Manager-beleid](resource-manager-policy.md) en [controle Hallo activiteitenlogboek](resource-group-audit.md). Resource Manager-beleid biedt u met Hallo mogelijkheid toomanage risico in Azure. U kunt beleidsregels die onafhankelijkheid van de gegevens te garanderen door te beperken, afdwingen of controle van bepaalde acties definiëren. 

* Beleid is een standaard **toestaan** system. U beheren acties door te definiëren en toewijzen van beleid tooresources die weigeren of acties op de bronnen wilt controleren.
* Beleidsregels worden beschreven door de beleidsdefinities in een beleid definition language (als dan voorwaarden).
* U maakt beleidsregels met JSON (Javascript Object Notation) ingedeelde bestanden. Na het definiëren van een beleid voor u deze toewijzen tooa bepaald bereik: abonnement, resourcegroep of resource.

Beleidsregels hebben meerdere acties waarmee een fijnmazig benadering tooyour scenario's. Hallo acties zijn:

* **Weigeren**: blokken Hallo resource aanvraag
* **Audit**: kunt Hallo aanvraag maar voegt een regel toohello activiteitenlogboek (die kan worden gebruikt tooprovide waarschuwingen of tootrigger runbooks)
* **Toevoeg-**: voegt de opgegeven informatie toohello bron. Bijvoorbeeld, als er geen een label 'CostCenter' van een resource, dat label met een standaardwaarde toevoegen.

### <a name="common-uses-of-resource-manager-policies"></a>Veelvoorkomende toepassingen van Resource Manager-beleid
Azure Resource Manager-beleidsregels zijn een krachtig hulpprogramma in hello Azure toolkit. Hiermee kunt u tooavoid onverwachte kosten, tooidentify een kostenplaats voor resources via tagging en tooensure die compliancy vereisten wordt voldaan. Wanneer beleidsregels worden gecombineerd met ingebouwde controlefuncties hello, kunt u complexe en flexibele oplossingen fashion. Beleidsregels kunnen bedrijven tooprovide besturingselementen voor werkbelastingen 'Traditionele IT' en 'Agile' werkbelastingen; zoals ontwikkelen van toepassingen van de klant. Hallo zijn meest voorkomende die we voor de beleidsregels zien:

* **Geo-compatibiliteitsgegevens onafhankelijkheid** -Azure regio's biedt verschillende Hallo wereld. Ondernemingen willen vaak toocontrol waar resources worden gemaakt (of tooensure gegevens onafhankelijkheid of net tooensure resources sluiten toohello end consumenten van Hallo bronnen gemaakt worden).
* **Kostenbeheer** -een Azure-abonnement kan de resources van veel typen en schaal bevatten. Ondernemingen vaak wilt tooensure die standaard abonnementen Vermijd het gebruik van onnodig groot resources die het kost honderden bedragen een maand of langer.
* **Standaard governance via vereiste tags** -vereisen van labels is een van de meest voorkomende en maximaal gewenste functies Hallo. Met behulp van Azure Resource Manager-beleid zijn ondernemingen kunnen tooensure dat een resource op de juiste wijze is gecodeerd. Hallo meest voorkomende labels, zijn: afdeling, Resource-eigenaar en omgeving type (bijvoorbeeld - productie, testen en ontwikkeling)

**Voorbeelden**

"Traditionele IT ' abonnement voor line-of-business-toepassingen

* Afdeling en de eigenaar van tags op alle bronnen afdwingen
* Beperken van de resource maken toohello regio Noord-Amerika
* Hallo mogelijkheid toocreate G-serie VM's en HDInsight-Clusters beperken

'Flexibele' omgeving voor een zakelijke eenheid cloudtoepassingen maken

* Hallo maken van resources met behulp van toomeet gegevens onafhankelijkheid vereisten, alleen in een specifieke regio.
* Omgevingstag voor alle resources worden afgedwongen. Als een bron wordt gemaakt zonder een label, toevoeg-Hallo **omgeving: onbekende** tag toohello resource.
* Audit wanneer bronnen buiten Noord-Amerika worden gemaakt, maar niet.
* Audit wanneer hoge kosten voor resources worden gemaakt.

> [!TIP]
> Hallo meest voorkomende gebruik van Resource Manager-beleid tussen verschillende organisaties is toocontrol *waar* resources kunnen worden gemaakt en *wat* typen resources kunnen worden gemaakt. Bovendien tooproviding besturingselementen op *waar* en *wat*, vele ondernemingen gebruik beleid tooensure bronnen Hallo toepasselijke metadata toobill terug voor consumptie hebben. U wordt aangeraden toepassen van beleid op abonnementsniveau Hallo voor:
> 
> * Geo-compatibiliteitsgegevens onafhankelijkheid
> * Kostenbeheer
> * Vereiste tags (bepaald door zakelijke behoeften, zoals BillTo, de eigenaar van de toepassing)
> 
> U kunt extra beleidsregels op lagere niveaus van bereik toepassen.
> 
> 

### <a name="audit---what-happened"></a>Audit - wat is er gebeurd?
tooview hoe uw omgeving werkt, moet u tooaudit gebruikersactiviteit. De meeste brontypen in Azure maken diagnostische logboeken die u via een hulpprogramma log of in Azure Operations Management Suite kunt analyseren. U kunt verzamelen activiteitenlogboeken tussen meerdere abonnementen tooprovide een afdelingen of enterprise-weergave. Controlerecords zijn zowel een belangrijk hulpprogramma voor Netwerkcontrole en een cruciaal mechanisme tootrigger-gebeurtenissen in hello Azure-omgeving.

Activiteitenlogboeken van de van implementaties van Resource Manager kunt u toodetermine hello **operations** die vond plaats en door wie deze uitgevoerd. Activiteitenlogboeken kunnen worden verzameld en worden geaggregeerd met de hulpprogramma's zoals logboekanalyse.

## <a name="resource-tags"></a>Resourcetags
Als gebruikers in uw organisatie resources toohello abonnement toevoegt, wordt het steeds belangrijker tooassociate resources met de juiste afdeling hello, klanten en omgeving. U kunt metagegevens tooresources via bijvoegen [labels](resource-group-using-tags.md). U labels tooprovide informatie over het Hallo-resource of Hallo eigenaar. Labels kunnen u alleen cumulatieve toonot en resources op verschillende manieren groeperen, maar die gegevens gebruiken voor de toepassing hello van doorberekening. U kunt labelen resources met up too15: sleutelwaarde-paren. 

Resourcetags moeten flexibel zijn en gekoppelde toomost resources. Voorbeelden van algemene resourcelabels zijn:

* BillTo
* Afdeling (of bedrijfseenheid)
* Omgeving (ontwikkeling productie, fase)
* Laag (weblaag, toepassingslaag)
* De eigenaar van de toepassing
* ProjectName

![tags](./media/resource-manager-subscription-governance/resource-group-tagging.png)

Zie voor meer voorbeelden van labels [aanbevolen naamgevingsregels voor Azure-resources](../guidance/guidance-naming-conventions.md).

> [!TIP]
> Overweeg een beleid dat labelen bepaalt voor:
> 
> * Resourcegroepen
> * Storage
> * Virtuele machines
> * Service-omgevingen of web-toepassingsservers
> 
> Deze labels strategie identificeert voor uw abonnementen welke metagegevens nodig is voor Hallo business, financiën, beveiliging, risicobeheer en algemene beheer van Hallo-omgeving. 

## <a name="resource-group"></a>Resourcegroep
Resource Manager kunt u tooput resources in zinvolle groepen voor beheer, facturerings- of natuurlijke affiniteit. Zoals eerder vermeld, wordt Azure heeft twee implementatiemodellen. Eerdere model Klassiek Hallo basiseenheid voor beheer is Hallo Hallo-abonnement. Was het moeilijk toobreak resources binnen een abonnement, wat geleid toohello maken van een groot aantal abonnementen heeft. We zagen Hallo introductie van resourcegroepen met Hallo-Resource Manager-model. Resourcegroepen zijn containers voor resources die een gemeenschappelijk levenscyclus hebben of delen van een kenmerk zoals 'alle SQL servers' of 'Application A'.

Resourcegroepen kunnen niet worden opgenomen in elkaar en resources kunnen alleen deel uitmaken van de resourcegroep tooone. U kunt bepaalde acties toepassen op alle bronnen in een resourcegroep. Bijvoorbeeld, verwijdert een resourcegroep alle resources binnen het Hallo-resourcegroep. Normaal gesproken u een volledige toepassings- of verwante plaatsen in Hallo dezelfde resourcegroep. Bijvoorbeeld, een toepassing met drie lagen Contoso-webtoepassing aangeroepen zou bevatten Hallo-webserver, toepassingsserver en SQL server in Hallo dezelfde resourcegroep.

> [!TIP]
> Hoe het ordenen van uw resourcegroepen kan afwijken van 'Traditionele IT' werkbelastingen te 'Flexibele IT' werkbelastingen:
> 
> * "Traditionele IT ' werkbelastingen zijn meestal gegroepeerd op items in Hallo dezelfde levenscyclus, zoals een toepassing. Groepering door toepassing kunt u afzonderlijke Toepassingsbeheer.
> * ' Flexibele IT ' werkbelastingen vaak toofocus op externe klantgerichte cloud-toepassingen. Hallo resourcegroepen moeten overeenkomen met Hallo lagen van implementatie (zoals weblaag, App-laag) en beheer.
> 
> Inzicht in uw werkbelasting, kunt u een resource group-strategie ontwikkelen.

## <a name="role-based-access-control"></a>Op rollen gebaseerd toegangsbeheer
Waarschijnlijk vraagt u uzelf "wie moeten toegang tooresources hebben?" en 'hoe ik deze toegang beheren?' Toestaan of verbieden toohello toegang tot Azure-portal en beheren van toegang tooresources in Hallo-portal is van cruciaal belang. 

Wanneer Azure in eerste instantie is uitgebracht, toegang besturingselementen tooa abonnement basic zijn: Administrator of CO-beheerder. Toegang tot tooa abonnement in Hallo klassieke model geïmpliceerde tooall Hallo resources te openen in Hallo-portal. Dit gebrek aan nauwkeuriger beheer geleid toohello verspreiding van abonnementen tooprovide een niveau van redelijke toegangsbeheer voor een Azure-inschrijving.

De verspreiding van abonnementen is niet meer nodig. Met op rollen gebaseerde toegangsbeheer, kunt u gebruikers toewijzen toostandard functies (zoals algemene 'Lezer' en 'schrijver' typen rollen). U kunt ook aangepaste rollen definiëren.

> [!TIP]
> tooimplement op rollen gebaseerde toegangsbeheer:
> * Verbinding maken met uw zakelijke identiteit archief (meestal Active Directory) tooAzure Active Directory met Hallo AD Connect-hulpprogramma.
> * Hallo beheerder/Co-beheerder van een abonnement met behulp van een beheerde identiteit van het besturingselement. **Geen** beheerder/Co-beheerder tooa nieuwe abonnement eigenaar toewijzen. Gebruik in plaats daarvan RBAC rollen tooprovide **eigenaar** rechten tooa groep of persoon.
> * Azure tooa gebruikersgroep (bijvoorbeeld X Toepassingseigenaars) toevoegen aan Active Directory. Hallo gesynchroniseerde groep tooprovide groep leden Hallo juiste rechten toomanage Hallo resourcegroep gebruiken met Hallo-toepassingen.
> * Ga als volgt Hallo principe voor het verlenen van Hallo **minimale bevoegdheden** vereist toodo Hallo werk verwacht. Bijvoorbeeld:
>   * Implementatie-groep: Een groep die alleen kunnen toodeploy resources.
>   * : Virtuele Machine een beheergroep die virtuele machines kunnen toorestart (voor bewerkingen)
> 
> Deze tips helpen u bij het beheren van toegang voor gebruikers in uw abonnement.

## <a name="azure-resource-locks"></a>Azure-resource-vergrendelingen
Als uw organisatie core services toohello abonnement toevoegt, wordt het steeds belangrijker tooensure dat deze services beschikbaar tooavoid business wordt onderbroken zijn. [Resource vergrendelingen](resource-group-lock-resources.md) kunt u toorestrict bewerkingen op waardevolle bronnen waar wijzigt of verwijdert deze zou aanzienlijke gevolgen voor uw toepassingen of cloudinfrastructuur hebben. U kunt vergrendelingen tooa abonnement, resourcegroep of resource toepassen. Normaal gesproken toepassen u vergrendelingen toofoundational resources, zoals virtuele netwerken, gateways en storage-accounts. 

Resource vergrendelingen momenteel ondersteuning voor twee waarden: CanNotDelete en alleen-lezen. CanNotDelete betekent dat gebruikers (met de juiste rechten Hallo) kunnen wel lezen of wijzigen van een bron, maar kan niet worden verwijderd. Alleen-lezen betekent dat gemachtigde gebruikers niet verwijderen of wijzigen van een resource.

management-vergrendelingen toocreate of verwijderen, moet u beschikken te`Microsoft.Authorization/*` of `Microsoft.Authorization/locks/*` acties.
Van de ingebouwde rollen hello, worden alleen de eigenaar en de beheerder voor gebruikerstoegang die acties verleend.

> [!TIP]
> Belangrijkste netwerkopties moeten worden beveiligd met vergrendelingen. Per ongeluk verwijderen van een site-naar-site VPN-gateway zijn rampzalig zijn tooan Azure-abonnement. Azure is niet toegestaan toodelete een virtueel netwerk dat wordt gebruikt, maar meer beperkingen toepassen voorzorgsmaatregel handig is. 
> 
> * Virtueel netwerk: CanNotDelete
> * Netwerkbeveiligingsgroep: CanNotDelete
> * Beleid: CanNotDelete
> 
> Beleidsregels zijn ook cruciaal toohello onderhoud van de juiste besturingselementen. Het is raadzaam dat u van toepassing een **CanNotDelete** vergrendelen toopolices die gebruikt worden.

## <a name="core-networking-resources"></a>Netwerkresources Core
Toegang tooresources kan zijn (binnen Hallo bedrijfsnetwerk) interne of externe (via internet Hallo). Het is gemakkelijker voor gebruikers in uw organisatie tooinadvertently put-resources in de verkeerde positie Hallo en blootstellen ze toomalicious toegang. Net als bij de on-premises apparaten, moeten de ondernemingen juiste besturingselementen tooensure dat Azure gebruikers Hallo rechts beslissingen toevoegen. We identificeren belangrijkste resources die elementaire controle van toegang bieden voor abonnement-toezicht. Hallo belangrijkste resources bestaan uit:

* **Virtuele netwerken** containerobjecten voor subnetten zijn. Hoewel niet strikt noodzakelijk is het vaak gebruikt bij het verbinden van toepassingen toointernal bedrijfsbronnen.
* **Netwerkbeveiligingsgroepen** zijn vergelijkbaar tooa firewall en regels voor hoe een resource "praten kan" via Hallo netwerk opgeeft. Ze bieden gedetailleerde controle over hoe / als een subnet (of de virtuele machine) verbinding kunt maken toohello Internet of andere subnetten in hetzelfde Hallo virtueel netwerk.

![Core-netwerken](./media/resource-manager-subscription-governance/core-network.png)

> [!TIP]
> Voor netwerken:
> * Virtuele netwerken toegewezen tooexternal gerichte werklast en werkbelastingen van interne maken. Deze benadering minder kans op Hallo van virtuele machines die zijn bedoeld voor interne werkbelastingen in een extern gerichte ruimte per ongeluk te brengen.
> * Configureer de beveiligde groepen toolimit netwerktoegang. Ten minste blokkeren toohello toegang tot internet vanaf interne virtuele netwerken en blok toegang toohello bedrijfsnetwerk van de externe virtuele netwerken.
> 
> De volgende tips helpen u beveiligde netwerkresources implementeren.

### <a name="automation"></a>Automatisering
Resources afzonderlijk te beheren is tijdrovend en mogelijk foutgevoelig voor bepaalde bewerkingen. Azure biedt verschillende mogelijkheden tot automatisering met Azure Automation, Logic Apps en Azure Functions. [Azure Automation](../automation/automation-intro.md) kunnen beheerders toocreate en algemene taken voor runbooks toohandle definiëren bij het beheren van resources. U kunt runbooks maken met behulp van een PowerShell-code-editor of een grafische editor. U kunt meerdere fasen werkstromen maken. Azure Automation is vaak gebruikte toohandle algemene taken zoals niet-gebruikte resources afgesloten of maken van resources in het antwoord tooa specifieke trigger zonder menselijke tussenkomst.

> [!TIP]
> Voor automatisering:
> * Een Azure Automation-account maken en bekijk Hallo beschikbare runbooks (grafische en command line) beschikbaar in Hallo [Runbookgalerie](../automation/automation-runbook-gallery.md).
> * Importeren en aanpassen van de belangrijkste runbooks voor uw eigen gebruik.
> 
> Een gebruikelijk scenario is Hallo mogelijkheid tooStart/afsluiten virtuele machines op een planning. Er zijn voorbeeld runbooks die beschikbaar zijn in de galerie hello, die zowel voor het verwerken van dit scenario en leert u hoe tooexpand deze.
> 
> 

## <a name="azure-security-center"></a>Azure Security Center
Mogelijk is een van de overstap op Hallo grootste blockers toocloud Hallo zorgen over beveiliging. IT-risicomanagers en beveiliging afdelingen moeten tooensure bronnen in Azure zijn beveiligd. 

Hallo [Azure Security Center](../security-center/security-center-intro.md) biedt een centrale weergave van de beveiligingsstatus Hallo van resources in het Hallo-abonnementen en aanbevelingen die helpen te voorkomen dat resources waarmee is geknoeid. Deze kunt beleidsregels voor meer gedetailleerd (bijvoorbeeld toepassen beleid toospecific resourcegroepen waarmee Hallo enterprise tootailor hun houding toohello risico die ze adresseert) inschakelen. Ten slotte is Azure Security Center een open platform waarmee Microsoft-partners en onafhankelijke software leveranciers toocreate software die de mogelijkheden in Azure Security Center tooenhance wordt geplaatst. 

> [!TIP]
> Azure Security Center is standaard ingeschakeld in elk abonnement. U moet echter de agent voor het verzamelen van virtuele machines tooallow Azure Security Center tooinstall inschakelen en beginnen met het verzamelen van gegevens.
> 
> ![Verzamelen van gegevens](./media/resource-manager-subscription-governance/data-collection.png)
> 
> 

## <a name="next-steps"></a>Volgende stappen
* Nu u over een abonnement governance hebt geleerd, is het tijd toosee deze aanbevelingen in de praktijk. Zie [voorbeelden van de implementatie van Azure-abonnement governance](resource-manager-subscription-examples.md).

