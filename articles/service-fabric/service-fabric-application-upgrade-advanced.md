---
title: Toepassing bijwerken onderwerpen aaaAdvanced | Microsoft Docs
description: In dit artikel bevat informatie over sommige geavanceerde onderwerpen die betrekking hebben tooupgrading Service Fabric-toepassing.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a>Upgrade van de service Fabric-toepassing: geavanceerde onderwerpen
## <a name="adding-or-removing-services-during-an-application-upgrade"></a>Het toevoegen of verwijderen van services tijdens een upgrade van de toepassing
Als een nieuwe service wordt tooan-toepassing die wordt al geïmplementeerd en gepubliceerd als een upgrade toegevoegd, is de nieuwe service Hallo toegevoegde toohello geïmplementeerd toepassing.  Een dergelijke upgrade heeft geen invloed op Hallo-services die al deel van de toepassing hello uitmaakten. Een exemplaar van Hallo-service die is toegevoegd moet echter worden gestart voor Hallo nieuwe service toobe active (met behulp van Hallo `New-ServiceFabricService` cmdlet).

Services kunnen ook worden verwijderd uit een toepassing als onderdeel van een upgrade. Echter alle huidige exemplaren van Hallo naar-worden verwijderd service moeten worden gestopt voordat u doorgaat met de Hallo-upgrade (met behulp van Hallo `Remove-ServiceFabricService` cmdlet).

## <a name="manual-upgrade-mode"></a>Handmatige upgrademodus
> [!NOTE]
> niet-bewaakte handmatige modus Hallo rekening met alleen voor de upgrade van een mislukte of onderbroken. Hallo bewaakte modus is Hallo aanbevolen upgrademodus voor Service Fabric-toepassingen.
>
>

Azure Service Fabric bevat meerdere upgrade modi toosupport ontwikkeling en productie-clusters. Implementatieopties gekozen kunnen afwijken voor verschillende omgevingen.

Er is een fout opgetreden in Hallo bewaakt rolling toepassing upgrade Hallo meest voorkomende upgrade toouse in de productieomgeving Hallo. Wanneer een upgrade Hallo beleid is opgegeven, Service Fabric zorgt ervoor dat de toepassing hello orde voordat Hallo upgrade wordt uitgevoerd.

 Hallo beheerder van de toepassing kunt Hallo handmatige rolling toepassing upgrademodus toohave volledige controle over upgradevoortgang via Hallo Hallo verschillende upgradedomeinen gebruiken. Deze modus is handig wanneer een aangepaste of complexe evaluatie statusbeleid vereist is, of een upgrade van een ongebruikelijke activiteiten (bijvoorbeeld Hallo toepassing is al in het verlies van gegevens).

Ten slotte is hello geautomatiseerde rolling upgrade van de toepassing handig voor ontwikkeling of tests omgevingen tooprovide een snelle iteratie cyclus tijdens het ontwikkelen van de service.

## <a name="change-toomanual-upgrade-mode"></a>Upgrade toomanual-modus wijzigen
**Handmatige**--stoppen Hallo upgrade van de toepassing op de huidige UD en wijzig Hallo Hallo modus tooUnmonitored handmatig bijwerken. Hallo beheerder moet toomanually aanroep **MoveNextApplicationUpgradeDomainAsync** tooproceed Hello upgraden of activeren van een terugdraaibewerking door een nieuwe upgrade initiëren. Zodra het Hallo-upgrade in de handmatige modus Hallo invoert, blijft in de handmatige modus Hallo totdat een nieuwe upgrade wordt gestart. Hallo **GetApplicationUpgradeProgressAsync** opdracht retourneert FABRIC\_toepassing\_UPGRADE\_status\_rollend\_doorsturen\_in behandeling.

## <a name="upgrade-with-a-diff-package"></a>Een upgrade uitvoert op een diff-pakket
Een Service Fabric-toepassing kan worden bijgewerkt door de inrichting met een volledige en zelfstandige toepassingspakket. Een toepassing kan ook worden bijgewerkt met behulp van een diff-pakket met alleen Hallo bijgewerkt toepassingsbestanden, Hallo toepassingsmanifest en Hallo service manifest-bestanden bijgewerkt.

Een volledige toepassingspakket bevat alle Hallo bestanden nodig toostart en een Service Fabric-toepassing uitvoeren. Een diff-pakket bevat alleen Hallo-bestanden die gewijzigd tussen Hallo laatste inrichten en de huidige upgrade hello, plus manifest van de volledige toepassing hello en Hallo service manifest bestanden. Elke vermelding in het toepassingsmanifest Hallo of servicemanifest dat niet is gevonden in Hallo build lay-out wordt gezocht naar in Hallo image store.

Volledige toepassingspakketten zijn vereist voor de eerste installatie Hallo van een toepassing toohello cluster. Daaropvolgende updates kunnen zijn voor een volledige toepassingspakket of een diff-pakket.

Gevallen terwijl een goede keuze met behulp van een pakket diff zou zijn:

* Een diff-pakket verdient de voorkeur wanneer u een groot pakket die verwijst naar verschillende service manifest-bestanden en/of verschillende pakketten code, config pakketten of gegevenspakketten hebt.
* Een diff-pakket verdient de voorkeur wanneer u een implementatiesysteem dat Hallo build indeling rechtstreeks vanuit uw buildproces toepassing genereert. Hoewel Hallo code nog niet is gewijzigd, ophalen nieuw gebouwde assembly's in dit geval een andere controlesom. Met behulp van een volledige toepassingspakket, moet u tooupdate Hallo versie op alle code pakketten. Met een diff-pakket bieden u alleen Hallo-bestanden die gewijzigd en Hallo manifestbestanden waarbij het Hallo-versie is gewijzigd.

Wanneer een toepassing wordt bijgewerkt met behulp van Visual Studio, wordt Hallo diff-pakket wordt automatisch gepubliceerd. toocreate een diff-pakket Hallo handmatig het manifest van de toepassing en Hallo service manifesten moeten worden bijgewerkt, maar alleen gewijzigd hello-pakketten moeten worden opgenomen in de laatste toepassingspakket Hallo.

Bijvoorbeeld, u begint met het Hallo volgende van toepassing (versienummers opgegeven voor het gemak van wat):

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

Nu gaan we ervan uit gewenste tooupdate alleen Hallo codepakket van service1 met een diff-pakket met behulp van PowerShell. Nu is uw bijgewerkte toepassing hello volgende mapstructuur:

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

In dit geval bijwerken u Hallo application manifest too2.0.0 en Hallo servicemanifest voor service1 tooreflect Hallo code pakketupdate. Hallo-map voor het toepassingspakket moet Hallo structuur te volgen:

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a>Volgende stappen
[Een upgrade van uw toepassing met behulp van Visual Studio](service-fabric-application-upgrade-tutorial.md) begeleidt u bij een upgrade van de toepassing met Visual Studio.

[Een upgrade van uw toepassing met behulp van Powershell](service-fabric-application-upgrade-tutorial-powershell.md) begeleidt u bij een upgrade van de toepassing met behulp van PowerShell.

Bepalen hoe uw toepassing wordt bijgewerkt met behulp van [Parameters Upgrade](service-fabric-application-upgrade-parameters.md).

Uw toepassingsupgrades compatibel maken door leren hoe toouse [serialisatie van gegevens](service-fabric-application-upgrade-data-serialization.md).

Veelvoorkomende problemen oplossen in toepassingsupgrades door te verwijzen toohello stappen in [toepassingsupgrades probleemoplossing](service-fabric-application-upgrade-troubleshooting.md).
