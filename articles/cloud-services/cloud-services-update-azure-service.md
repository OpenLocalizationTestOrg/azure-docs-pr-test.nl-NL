---
title: aaaHow tooupdate een cloudservice | Microsoft Docs
description: Meer informatie over hoe tooupdate cloud-services in Azure. Meer informatie over hoe een update op een cloudservice tooensure beschikbaarheid wordt voortgezet.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c6a8b5e6-5c99-454c-9911-5c7ae8d1af63
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 7e4c8bd46e51a555b4309ea8927d120e8efcf0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-a-cloud-service"></a>Hoe tooupdate een cloudservice

Bijwerken van een cloudservice, inclusief de functies en de gastbesturingssysteem, is een proces drie stappen. Eerst Hallo binaire bestanden en de configuratiebestanden voor de nieuwe Hallo cloudservice of versie van het besturingssysteem moet worden geüpload. Vervolgens reserveert Azure compute- en netwerkbronnen voor op basis van de vereisten van de nieuwe versie van cloud service Hallo HALLO hallo-cloudservice. Ten slotte voert Azure een rolling upgrade tooincrementally hello tenant toohello nieuwe versie van de update of het gastbesturingssysteem, behoud uw beschikbaarheid. Dit artikel worden de details op Hallo van deze laatste stap – Hallo rolling upgrade.

## <a name="update-an-azure-service"></a>Een Azure-Service bijwerken
Azure worden uw rolinstanties georganiseerd in logische groepen indelen upgradedomeinen (UD) genoemd. Upgradedomeinen (UD) zijn logische verzamelingen rolexemplaren die als een groep worden bijgewerkt.  Azure-updates een cloud service één UD tegelijk, waardoor exemplaren worden weergegeven in andere UDs toocontinue behoeve van verkeer.

Hallo standaardaantal upgradedomeinen is 5. U kunt een verschillend aantal upgradedomeinen opgeven door Hallo upgradeDomainCount kenmerk in Hallo van servicedefinitiebestand (.csdef). Zie voor meer informatie over Hallo upgradeDomainCount kenmerk [WebRole Schema](https://msdn.microsoft.com/library/azure/gg557553.aspx) of [WorkerRole Schema](https://msdn.microsoft.com/library/azure/gg557552.aspx).

Wanneer u een update in plaats van een of meer rollen in uw service uitvoert, Azure-updates sets rolinstanties volgens toohello upgradedomein toowhich die ze behoren. Azure alle Hallo-exemplaren in een opgegeven upgradedomein – stoppen, bijwerken, worden gezet online – back-updates gaat vervolgens naar de volgende Hallo-domein. Door te stoppen alleen Hallo instanties die worden uitgevoerd in de huidige Hallo upgradedomein, Azure zorgt ervoor dat een update gebeurt met Hallo zo weinig mogelijk impact toohello waarop service wordt uitgevoerd. Zie voor meer informatie [hoe Hallo update voortgezet](#howanupgradeproceeds) verderop in dit artikel.

> [!NOTE]
> Tijdens het Hallo-voorwaarden **bijwerken** en **upgrade** iets andere betekenis hebben in de context van hello Azure, kan door elkaar Hallo processen en beschrijvingen van functies in dit document hello worden gebruikt.
>
>

Uw service moet ten minste twee exemplaren van een rol voor deze rol toobe bijgewerkt ter plekke zonder uitvaltijd definiëren. Als het Hallo-service bestaat uit slechts één exemplaar van een rol, zijn uw service niet beschikbaar totdat hello InPlace-update is voltooid.

Dit onderwerp bevat informatie over Azure-updates na Hallo:

* [Servicewijzigingen toegestaan tijdens het bijwerken](#AllowedChanges)
* [Hoe een upgrade wordt uitgevoerd](#howanupgradeproceeds)
* [Terugdraaien van een update](#RollbackofanUpdate)
* [Meerdere mutating bewerkingen op een actieve implementatie initiëren](#multiplemutatingoperations)
* [Distributie van functies tussen domeinen upgraden](#distributiondfroles)

<a name="AllowedChanges"></a>

## <a name="allowed-service-changes-during-an-update"></a>Servicewijzigingen toegestaan tijdens het bijwerken
Hallo ziet volgende tabel u Hallo toegestaan wijzigingen tooa service tijdens het bijwerken:

| Wijzigingen worden toegestaan toohosting, services en functies | InPlace-update | Gefaseerde (VIP's wisselen) | Verwijderen en opnieuw implementeren |
| --- | --- | --- | --- |
| Besturingssysteem |Ja |Ja |Ja |
| .NET-vertrouwensniveau |Ja |Ja |Ja |
| Grootte van virtuele machine<sup>1</sup> |Ja<sup>2</sup> |Ja |Ja |
| Instellingen voor de lokale opslag |Alleen verhogen<sup>2</sup> |Ja |Ja |
| Toevoegen of verwijderen van rollen in een service |Ja |Ja |Ja |
| Aantal exemplaren van een bepaalde rol |Ja |Ja |Ja |
| Aantal of type eindpunten voor een service |Ja<sup>2</sup> |Nee |Ja |
| Namen en waarden van configuratie-instellingen |Ja |Ja |Ja |
| Waarden (maar niet de namen van) van configuratie-instellingen |Ja |Ja |Ja |
| Nieuwe certificaten toevoegen |Ja |Ja |Ja |
| Wijzigen van bestaande certificaten |Ja |Ja |Ja |
| Implementeer nieuwe code |Ja |Ja |Ja |

<sup>1</sup> wijziging van grootte beperkt toohello subset van grootten beschikbaar voor Hallo cloudservice.

<sup>2</sup> vereist Azure SDK 1.5 of hoger.

> [!WARNING]
> Het wijzigen van de grootte van de virtuele machine Hallo vernietigt lokale gegevens.
>
>

Hallo volgende items worden niet ondersteund tijdens het bijwerken:

* Hallo-naam van een rol wijzigen. Verwijderen en voeg vervolgens Hallo-rol met de nieuwe naam Hallo.
* Hallo aantal Upgrade wijzigen.
* Verkleinen Hallo Hallo lokale bronnen.

Als u andere updates tooyour van servicedefinitie doorvoert, zoals Hallo verkleinen van een lokale bron, moet u een VIP wisselen update uitvoeren. Zie voor meer informatie [wisselen implementatie](https://msdn.microsoft.com/library/azure/ee460814.aspx).

<a name="howanupgradeproceeds"></a>

## <a name="how-an-upgrade-proceeds"></a>Hoe een upgrade wordt uitgevoerd
U kunt beslissen of u tooupdate alle Hallo rollen in uw service of een enkele rol bij het Hallo-service. In beide gevallen worden alle exemplaren van elke rol die wordt bijgewerkt en deel uitmaken van de eerste upgradedomein toohello gestopt, bijgewerkt en weer online. Zodra deze weer online, zijn Hallo-exemplaren in de tweede upgradedomein Hallo gestopt, bijgewerkt en weer online. Een cloudservice kan maximaal één upgrade tegelijk actief hebben. Hallo-upgrade wordt altijd uitgevoerd tegen Hallo meest recente versie van Hallo-cloudservice.

Hallo volgende diagram illustreert hoe Hallo upgrade wordt uitgevoerd als u een van alle Hallo rollen in Hallo-service upgrade:

![Upgrade van service](media/cloud-services-update-azure-service/IC345879.png "Upgrade van service")

Deze volgende diagram illustreert hoe Hallo update wordt uitgevoerd als u slechts één functie bijwerkt:

![Upgrade rol](media/cloud-services-update-azure-service/IC345880.png "Upgrade rol")  

Tijdens een automatische update hello Azure-Infrastructuurcontroller periodiek geëvalueerd Hallo status van Hallo cloud service toodetermine wanneer de veilige toowalk Hallo volgende UD. Deze health-evaluatie wordt uitgevoerd op basis van per rol en overweegt alleen exemplaren in Hallo meest recente versie (dat wil zeggen de exemplaren van UDs die al zijn gelopen). Controleert of dat een minimum aantal rolexemplaren, voor elke rol, hebben een goede definitieve status bereikt.

### <a name="role-instance-start-timeout"></a>Time-out voor de Start van de rol exemplaar
Hallo Infrastructuurcontroller wacht 30 minuten voor elke rol exemplaar tooreach een status gestart. Als de time-outduur Hallo verstrijkt, blijft Hallo Infrastructuurcontroller toohello volgende rolinstantie lopen.

### <a name="impact-toodrive-data-during-cloud-service-upgrades"></a>Gegevens van de impact toodrive tijdens Cloudservice upgrades

Bij het bijwerken van een service van een enkele instantie toomultiple exemplaren wordt uw service worden verbroken tijdens het Hallo-upgrade wordt uitgevoerd vanwege toohello manier die Azure services worden bijgewerkt. Hallo service level agreement aansprakelijke servicebeschikbaarheid tooservices die zijn geïmplementeerd met meer dan één exemplaar is alleen van toepassing. Hallo hieronder wordt beschreven hoe gegevens op elk station hello wordt beïnvloed door elke Azure-service-upgrade scenario:

|Scenario|C-schijf|D-station|E-station|
|--------|-------|-------|-------|
|VM opnieuw wordt opgestart|Behouden|Behouden|Behouden|
|Portal opnieuw opstarten|Behouden|Behouden|Vernietigd|
|Portal terugzetten van de installatiekopie|Behouden|Vernietigd|Vernietigd|
|In-Place Upgrade|Behouden|Behouden|Vernietigd|
|Migratie van knooppunt|Vernietigd|Vernietigd|Vernietigd|

Houd er rekening mee dat in Hallo boven lijst Hallo station E: basisstation Hallo-rol en mag geen vastgelegde. Gebruik in plaats daarvan Hallo **% RoleRoot %** omgeving variabele toorepresent Hallo station.

toominimize hello uitvaltijd bij een upgrade van een service single instance een nieuwe meerdere exemplaren service toohello staging-server implementeren en geen VIP's wisselen.

<a name="RollbackofanUpdate"></a>

## <a name="rollback-of-an-update"></a>Terugdraaien van een update
Azure biedt flexibiliteit voor het beheren van services tijdens het bijwerken doordat u kunt aanvullende bewerkingen op een service starten na Hallo initiële update-aanvraag wordt geaccepteerd door hello Azure-Infrastructuurcontroller. Terugdraaien kan alleen worden uitgevoerd wanneer een update (configuratie wijzigen) of upgrade wordt Hallo **Bezig** status op Hallo-implementatie. Een update of upgrade wordt beschouwd als toobe wordt uitgevoerd, zolang er is ten minste één exemplaar van het Hallo-service die nog niet bijgewerkt toohello nieuwe versie is. tootest of een terugdraaibewerking is toegestaan, Controleer Hallo-waarde van Hallo RollbackAllowed vlag die wordt geretourneerd door [ophalen implementatie](https://msdn.microsoft.com/library/azure/ee460804.aspx) en [Cloud Service-eigenschappen ophalen](https://msdn.microsoft.com/library/azure/ee460806.aspx) bewerkingen, tootrue is ingesteld.

> [!NOTE]
> U stelt alleen zin toocall terugdraaien op een **in-place** bijwerken of bijwerken omdat het VIP wisselen upgrades hebben betrekking op één volledige actief exemplaar van uw service met een andere vervangen.
>
>

Terugdraaien van een update wordt uitgevoerd heeft de volgende gevolgen voor de implementatie van Hallo Hallo:

* Alle rolinstanties die nieuwe versie bijgewerkt of bijgewerkte toohello nog niet was is niet bijgewerkt of bijgewerkt, omdat deze instanties al Hallo doelversie van Hallo-service wordt uitgevoerd.
* Een rol van exemplaren die al is bijgewerkt of de nieuwe versie van de bijgewerkte toohello van Hallo servicepakket (\*.cspkg) bestand of Hallo serviceconfiguratie (\*.cscfg)-bestand (of beide bestanden) zijn teruggekeerde toohello vóór de upgrade-versie van Deze bestanden.

Dit gebeurt functioneel door Hallo volgende kenmerken:

* Hallo [terugdraaien bijwerken of bijwerken](https://msdn.microsoft.com/library/azure/hh403977.aspx) bewerking die kan worden aangeroepen voor een configuratie-update (geactiveerd door het aanroepen van [implementatie-configuratie wijzigen](https://msdn.microsoft.com/library/azure/ee460809.aspx)) of een upgrade (geactiveerd door het aanroepen van [ Upgrade-implementatie](https://msdn.microsoft.com/library/azure/ee460793.aspx)), zolang er ten minste één exemplaar in Hallo service is toohello nieuwe versie die nog niet is bijgewerkt.
* Hallo vergrendeld element en Hallo RollbackAllowed element die worden geretourneerd als onderdeel van de antwoordtekst Hallo Hallo [ophalen implementatie](https://msdn.microsoft.com/library/azure/ee460804.aspx) en [Cloud Service-eigenschappen ophalen](https://msdn.microsoft.com/library/azure/ee460806.aspx) bewerkingen:

  1. Hallo vergrendeld element kunt u toodetect wanneer een mutating bewerking kan worden aangeroepen voor een bepaalde implementatie.
  2. Hallo RollbackAllowed element kunt u toodetect wanneer hello [terugdraaien van de Update of Upgrade](https://msdn.microsoft.com/library/azure/hh403977.aspx) bewerking kan worden aangeroepen voor een bepaalde implementatie.

  In de volgorde tooperform terugdraaien, hoeft u geen toocheck zowel vergrendeld Hallo Hallo RollbackAllowed elementen. Deze achtervoegsels tooconfirm dat RollbackAllowed tootrue is ingesteld. Deze elementen zijn alleen geretourneerd als deze methoden worden aangeroepen met behulp van Hallo aanvraagheader stellen te ' x-ms-version: 2011-10-01 ' of een latere versie. Zie voor meer informatie over kopteksten versioning [Management Serviceversiebeheer](https://msdn.microsoft.com/library/azure/gg592580.aspx).

Zijn er situaties waarin een terugdraaien van een update of upgrade wordt niet ondersteund, dit als volgt zijn:

* Verlaging van de lokale bronnen - kunnen als Hallo update toeneemt Hallo lokale bronnen voor een functie hello Azure-platform niet worden teruggedraaid.
* Quotumbeperkingen - als Hallo-update is een schaal omlaag bewerking die u mogelijk niet meer voldoende compute quotum toocomplete Hallo terugdraaibewerking hebben. Elk Azure-abonnement heeft een quotum gekoppeld waarmee Hallo kunt u het maximum aantal kernen dat kan worden gebruikt door alle gehoste services die deel uitmaken van toothat abonnement. Als u dat terugdraaien van een bepaalde update uw abonnement via quotum vervolgens die plaatst wordt een rollback niet ingeschakeld.
* Race condition - als de initiële update Hallo heeft voltooid, terugdraaien is niet mogelijk.

Een voorbeeld van wanneer Hallo terugdraaien van een update mogelijk nuttig is als u Hallo [Upgrade-implementatie](https://msdn.microsoft.com/library/azure/ee460793.aspx) bewerking in de handmatige modus toocontrol Hallo frequentie waarmee een primaire in-place upgrade tooyour Azure service gehoste is geïmplementeerd.

Tijdens implementatie van de upgrade Hallo Hallo u aanroepen [Upgrade-implementatie](https://msdn.microsoft.com/library/azure/ee460793.aspx) in de handmatige modus en upgradedomeinen toowalk beginnen. Als op een bepaald moment tijdens het controleren van Hallo upgrade u notitie sommige rolinstanties in Hallo eerste upgradedomeinen die u hebt niet meer reageren, kunt u Hallo aanroepen [terugdraaien van de Update of Upgrade](https://msdn.microsoft.com/library/azure/hh403977.aspx) bewerking op de implementatie van Hallo die blijft ongewijzigd Hallo-serverexemplaren die was nog niet zijn bijgewerkt en terugdraaien-serverexemplaren die was bijgewerkt toohello vorige servicepakket en configuratie.

<a name="multiplemutatingoperations"></a>

## <a name="initiating-multiple-mutating-operations-on-an-ongoing-deployment"></a>Meerdere mutating bewerkingen op een actieve implementatie initiëren
In sommige gevallen kunt u tooinitiate meerdere gelijktijdige mutating bewerkingen op een actieve implementatie. Bijvoorbeeld, u kunt een service-update uitvoeren en, terwijl deze update is teruggedraaid uit over uw service, gewenste toomake een andere, bijvoorbeeld tooroll Hallo update terug, een andere update toepassen of zelfs verwijderen Hallo-implementatie. Een aanvraag waarin dit wordt mogelijk nodig is als een service-upgrade bevat buggy code die ervoor zorgt een bijgewerkte rol exemplaar toorepeatedly vastlopen dat. Hello Azure-Infrastructuurcontroller worden in dit geval niet kunnen toomake uitgevoerd bij het toepassen van die worden bijgewerkt omdat een onvoldoende aantal exemplaren in de bijgewerkte domein Hallo zijn in orde. Deze status is waarnaar wordt verwezen tooas een *vastgelopen implementatie*. U kunt Hallo implementatie Registreer door terugdraaien Hallo update of een nieuwe update toepassen via bovenaan Hallo een mislukt.

Nadat Hallo eerste aanvraag tooupdate of upgrade Hallo-service door hello Azure-Infrastructuurcontroller is ontvangen, kunt u de volgende mutating bewerkingen starten. Dat wil zeggen, hoeft u geen toowait voor Hallo initiële bewerking toocomplete voordat u kunt een andere mutating bewerking.

Een tweede update-bewerking starten terwijl de eerste update hello uitgevoerd wordt, wordt vergelijkbaar toohello terugdraaibewerking is uitgevoerd. Als tweede Hallo-update in de automatische modus is, de eerste upgradedomein Hallo onmiddellijk worden geüpgraded, mogelijk tooinstances voorloopspaties uit meerdere upgradedomeinen offline op Hallo dezelfde tijdstip voor herstel.

Hallo mutating bewerkingen zijn als volgt: [implementatie-configuratie wijzigen](https://msdn.microsoft.com/library/azure/ee460809.aspx), [Upgrade-implementatie](https://msdn.microsoft.com/library/azure/ee460793.aspx), [Update Implementatiestatus](https://msdn.microsoft.com/library/azure/ee460808.aspx), [verwijderen Implementatie](https://msdn.microsoft.com/library/azure/ee460815.aspx), en [terugdraaien van de Update of Upgrade](https://msdn.microsoft.com/library/azure/hh403977.aspx).

Twee bewerkingen [ophalen implementatie](https://msdn.microsoft.com/library/azure/ee460804.aspx) en [Cloud Service-eigenschappen ophalen](https://msdn.microsoft.com/library/azure/ee460806.aspx), Hallo vergrendeld vlag die onderzocht toodetermine worden kunnen of een mutating bewerking kan worden aangeroepen voor een bepaalde implementatie te retourneren.

In de volgorde toocall Hallo versie van deze methoden die als Hallo vergrendeld vlag resultaat, moet u aanvraagheader te instellen ' x-ms-version: 2011-10-01 ' of een later. Zie voor meer informatie over kopteksten versioning [Management Serviceversiebeheer](https://msdn.microsoft.com/library/azure/gg592580.aspx).

<a name="distributiondfroles"></a>

## <a name="distribution-of-roles-across-upgrade-domains"></a>Distributie van functies tussen domeinen upgraden
Azure worden exemplaren van een rol gelijkmatig over een bepaald aantal upgradedomeinen die kan worden geconfigureerd als onderdeel van hello (.csdef) servicedefinitiebestand verdeeld. maximum aantal upgradedomeinen Hallo is 20 en Hallo standaardwaarde is 5. Zie voor meer informatie over hoe toomodify servicedefinitiebestand Hallo [Azure Service definitie Schema (.csdef-bestand)](cloud-services-model-and-package.md#csdef).

Bijvoorbeeld, als uw rol tien exemplaren heeft, bevat elk upgradedomein standaard twee exemplaren. Als uw rol 14 exemplaren heeft, bevat vier hello upgradedomeinen drie exemplaren en een vijfde domein bevat twee.

Upgradedomeinen worden aangeduid met een op nul gebaseerde index: eerste upgradedomein Hallo heeft een ID van 0 en Hallo tweede upgradedomein heeft een ID van 1, enzovoort.

Hallo volgende diagram illustreert hoe een service dan bevat twee rollen worden gedistribueerd wanneer Hallo service definieert twee upgradedomeinen. Hallo-service wordt uitgevoerd acht exemplaren van Hallo-Webrol en negen exemplaren van Hallo-werkrol.

![Distributie van Upgradedomeinen](media/cloud-services-update-azure-service/IC345533.png "distributie van Upgradedomeinen")

> [!NOTE]
> Houd er rekening mee dat Azure bepaalt hoe exemplaren worden toegewezen via upgradedomeinen. Het is niet mogelijk toospecify welke exemplaren toowhich domein zijn toegewezen.
>
>

## <a name="next-steps"></a>Volgende stappen
[Hoe tooManage Cloud-Services](cloud-services-how-to-manage.md)  
[Hoe tooMonitor Cloud-Services](cloud-services-how-to-monitor.md)  
[Hoe tooConfigure Cloud-Services](cloud-services-how-to-configure.md)  
