---
title: upgrade van de toepassing aaaService Fabric | Microsoft Docs
description: Dit artikel bevat een inleiding tooupgrading een Service Fabric-toepassing, waaronder kiezen upgrade modi en het uitvoeren van statuscontroles.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 803c9c63-373a-4d6a-8ef2-ea97e16e88dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 6f649ef4a5c0afab682522bcba7d2d66a4268ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade"></a>Upgrade van Service Fabric-toepassing uitvoeren
Een Azure Service Fabric-toepassing is een verzameling van services. Tijdens een upgrade, vergelijkt Service Fabric Hallo nieuwe [toepassingsmanifest](service-fabric-application-model.md#describe-an-application) met de vorige versie Hallo en bepaalt welke services in de toepassing hello updates vereisen. Service Fabric vergelijkt de getallen in de service Hallo met Hallo versienummers in de vorige versie Hallo manifesten Hallo-versie. Als een service niet is gewijzigd, wordt deze service is niet bijgewerkt.

## <a name="rolling-upgrades-overview"></a>Rolling upgrades-overzicht
In een uitrollende upgrade van de toepassing hello upgrade in fasen uitgevoerd. Hallo-upgrade is in elk stadium toegepaste tooa deelverzameling met knooppunten in het Hallo-cluster, een updatedomein genoemd. Als gevolg hiervan blijft Hallo toepassing beschikbaar in de hele Hallo upgrade. Tijdens de upgrade Hallo kan Hallo cluster een combinatie van oude en nieuwe versies van Hallo bevatten.

Daarom moet Hallo twee versies moet voorwaarts en achterwaarts compatibel. Als ze niet compatibel is, is beheerder van de toepassing hello verantwoordelijk voor gefaseerde installatie van de beschikbaarheid van een upgrade toomaintain meerdere-fase. Bij een upgrade van een meervoudige fasen, de eerste stap Hallo tooan tussenliggende versie van Hallo-toepassing die compatibel is met de vorige versie Hallo worden geüpgraded. de tweede stap Hallo is tooupgrade Hallo definitieve versie die compatibiliteit Hallo vooraf updateversie, maar is compatibel met Hallo tussenliggende versie.

Update domeinen zijn opgegeven in het clustermanifest Hallo bij het configureren van Hallo-cluster. Update domeinen ontvangt geen updates in een bepaalde volgorde. Een updatedomein is een logische eenheid van de implementatie voor een toepassing. Update domeinen toestaan Hallo services tooremain hoge beschikbaarheid tijdens een upgrade.

Upgrades niet rolling zijn mogelijk als Hallo upgrade toegepaste tooall-knooppunten in het Hallo-cluster Hallo geval is wanneer het Hallo-toepassing heeft slechts één updatedomein is. Deze methode wordt niet aanbevolen omdat het Hallo-service wordt uitgeschakeld en is niet beschikbaar op Hallo tijdstip van de upgrade. Azure biedt bovendien garanties wanneer een cluster met slechts één updatedomein is ingesteld.

## <a name="health-checks-during-upgrades"></a>Statuscontroles tijdens upgrades
Voor een upgrade statusbeleid hebt toobe ingesteld (of standaardwaarden kunnen worden gebruikt). Een upgrade wordt aangeduid als geslaagd wanneer alle domeinen van de update zijn bijgewerkt binnen Hallo opgegeven time-outs en wanneer alle bijwerkt domeinen als in orde worden beschouwd.  Een updatedomein in orde betekent dat domein van de update Hallo alle Hallo statuscontroles die zijn opgegeven in het statusbeleid Hallo doorgegeven. Bijvoorbeeld, een statusbeleid dat alle services in een toepassingsexemplaar moet mogelijk verplichten *orde*, zoals status wordt gedefinieerd door de Service Fabric.

Zijn de service en toepassing networkdirect statusbeleid en controles tijdens de upgrade door de Service Fabric. Dat wil zeggen, zijn geen servicespecifieke tests uitgevoerd.  Bijvoorbeeld, de service kan een vereiste doorvoer hebben, maar het Service Fabric heeft geen Hallo informatie toocheck doorvoer. Raadpleeg toohello [health artikelen](service-fabric-health-introduction.md) voor Hallo controles die worden uitgevoerd. Hallo-controles die zich voordoen tijdens een upgrade include-tests voor of Hallo toepassingspakket correct is gekopieerd of Hallo-exemplaar is gestart, enzovoort.

status van de toepassing Hello is een aggregatie van Hallo onderliggende entiteiten van de toepassing hello. Kortom, evalueert Service Fabric Hallo status van de toepassing hello via Hallo health die wordt gerapporteerd over de toepassing hello. Deze ook evalueert Hallo status van alle Hallo-services voor de toepassing hello op deze manier. Service Fabric verdere evalueert Hallo status van de toepassingsservices Hallo door aggregeren Hallo status van onderliggende items, zoals Hallo service replica. Zodra het statusbeleid voor de toepassing hello wordt voldaan, Hallo upgrade te kunnen voortzetten. Als Hallo statusbeleid wordt geschonden, mislukt de upgrade van de toepassing hello.

## <a name="upgrade-modes"></a>Upgrade-modi
Hallo-modus die wij voor de upgrade van de toepassing aanraden is hello bewaakte modus, waarbij Hallo gebruikte modus. Bewaakte modus Hallo-upgrade uitvoert op één updatedomein, en als alle health controleert op te geven (per Hallo beleid opgegeven), wordt verplaatst op de volgende updatedomein toohello automatisch.  Als statuscontroles mislukken en/of time-outs zijn bereikt, Hallo-upgrade is ofwel teruggedraaid voor Hallo updatedomein of Hallo-modus is handmatig gewijzigd toounmonitored. U kunt Hallo upgrade toochoose die twee modi voor upgrades van de mislukte configureren. 

Niet-bewaakte handmatige modus moet handmatige interventie na elke upgrade op een updatedomein, tookick uit Hallo upgrade op de volgende updatedomein Hallo. Er is geen health Service Fabric controles worden uitgevoerd. Hallo beheerder Hallo status of health controles voordat het Hallo-upgrade wordt gestart in de volgende updatedomein Hallo uitgevoerd.

## <a name="upgrade-default-services"></a>Standaard-services upgraden
Standaardservices in Service Fabric-toepassing kunnen worden bijgewerkt tijdens het Hallo bijwerken van een toepassing. Standaard-services worden gedefinieerd in Hallo [toepassingsmanifest](service-fabric-application-model.md#describe-an-application). Hallo standaardregels van de upgrade van de services die standaard zijn:

1. Standaard-services in de nieuwe Hallo [toepassingsmanifest](service-fabric-application-model.md#describe-an-application) die niet zijn opgenomen in het Hallo-cluster zijn gemaakt.
> [!TIP]
> [EnableDefaultServicesUpgrade](service-fabric-cluster-fabric-settings.md#fabric-settings-that-you-can-customize) moet toobe tootrue tooenable Hallo volgens de regels voor ingesteld. Deze functie wordt ondersteund door de v5.5.

2. In beide vorige bestaande services standaard [toepassingsmanifest](service-fabric-application-model.md#describe-an-application) en nieuwe versie worden bijgewerkt. Beschrijvingen van de service in de nieuwe versie Hallo overschrijft die al in het Hallo-cluster. Upgrade van de toepassing wilt terugdraaien automatisch tijdens het bijwerken van de standaard-fout-service.
3. Standaard-services in de vorige Hallo [toepassingsmanifest](service-fabric-application-model.md#describe-an-application) , maar niet in de nieuwe versie Hallo worden verwijderd. **Houd er rekening mee dat deze verwijderen standaardservices niet kunnen worden teruggezet.**

Voor het geval van een toepassing upgrade is teruggedraaid, zijn standaardservices teruggekeerde toohello status voordat de upgrade wordt gestart. Maar verwijderde services kunnen nooit worden gemaakt.

## <a name="application-upgrade-flowchart"></a>Toepassing bijwerken stroomdiagram
Hallo stroomdiagram hieronder vindt u informatie over de upgradeproces Hallo van een Service Fabric-toepassing. In het bijzonder Hallo stroom wordt beschreven hoe Hallo time-outs, met inbegrip van *HealthCheckStableDuration*, *HealthCheckRetryTimeout*, en *UpgradeHealthCheckInterval*, het beheren wanneer Hallo upgrade in één updatedomein wordt beschouwd als een geslaagd of mislukt.

![Hallo-upgradeproces voor een Service Fabric-toepassing][image]

## <a name="next-steps"></a>Volgende stappen
[Een upgrade van uw toepassing met behulp van Visual Studio](service-fabric-application-upgrade-tutorial.md) begeleidt u bij een upgrade van de toepassing met Visual Studio.

[Een upgrade van uw toepassing met behulp van Powershell](service-fabric-application-upgrade-tutorial-powershell.md) begeleidt u bij een upgrade van de toepassing met behulp van PowerShell.

Bepalen hoe uw toepassing wordt bijgewerkt met behulp van [Parameters Upgrade](service-fabric-application-upgrade-parameters.md).

Uw toepassingsupgrades compatibel maken door leren hoe toouse [serialisatie van gegevens](service-fabric-application-upgrade-data-serialization.md).

Meer informatie over hoe toouse geavanceerde functies tijdens het bijwerken van uw toepassing door ernaar te verwijzen[geavanceerde onderwerpen](service-fabric-application-upgrade-advanced.md).

Veelvoorkomende problemen oplossen in toepassingsupgrades door te verwijzen toohello stappen in [toepassingsupgrades probleemoplossing](service-fabric-application-upgrade-troubleshooting.md).

[image]: media/service-fabric-application-upgrade/service-fabric-application-upgrade-flowchart.png
