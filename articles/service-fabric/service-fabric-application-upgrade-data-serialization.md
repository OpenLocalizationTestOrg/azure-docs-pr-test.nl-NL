---
title: 'Upgrade van de toepassing: serialisatie van gegevens | Microsoft Docs'
description: Aanbevolen procedures voor serialisatie van gegevens en de mogelijke gevolgen voor rollende toepassingsupgrades.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: a5f36366-a2ab-4ae3-bb08-bc2f9533bc5a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 1b65dfd3813423550631490640a81953864f58e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-data-serialization-affects-an-application-upgrade"></a>De invloed van serialisatie van gegevens op een upgrade van de toepassing
In een [rolling upgrade van de toepassing](service-fabric-application-upgrade.md), Hallo-upgrade is toegepaste tooa deelverzameling met knooppunten, één upgradedomein tegelijk. Tijdens dit proces een aantal upgradedomeinen zijn op Hallo nieuwere versie van uw toepassing en een aantal upgradedomeinen zijn op een oudere versie van uw toepassing hello. Tijdens het Hallo-implementatie, nieuwe versie van uw toepassing hello moet kunnen tooread Hallo oude versie van uw gegevens en Hallo oude versie van uw toepassing moet kunnen tooread Hallo nieuwe versie van uw gegevens. Als Hallo-gegevensindeling niet voorwaarts en achterwaarts compatibel zijn, Hallo upgrade mogelijk niet werkt of slechter, gegevens mogelijk verloren of beschadigd. Dit artikel wordt beschreven wat wordt verstaan onder de indeling van uw gegevens en biedt de aanbevolen procedures om ervoor te zorgen dat uw gegevens voorwaarts en achterwaarts zijn compatibel.

## <a name="what-makes-up-your-data-format"></a>Wat is de indeling van uw gegevens?
In de Azure Service Fabric afkomstig Hallo-gegevens die is opgeslagen en gerepliceerd van uw C#-klassen. Voor toepassingen die gebruikmaken van [betrouwbare verzamelingen](service-fabric-reliable-services-reliable-collections.md), dat er gegevens Hallo-objecten in Hallo betrouwbare woordenlijsten en wachtrijen. Voor toepassingen die gebruikmaken van [Reliable Actors](service-fabric-reliable-actors-introduction.md), namelijk Hallo status voor Hallo actor back-ups. Deze C#-klassen moet serializable toobe doorvoeren en repliceren. Daarom wordt Hallo gegevensindeling gedefinieerd door Hallo velden en eigenschappen die zijn geserialiseerd, evenals hoe ze worden geserialiseerd. Bijvoorbeeld in een `IReliableDictionary<int, MyClass>` Hallo gegevens is een geserialiseerde `int` en een geserialiseerde `MyClass`.

### <a name="code-changes-that-result-in-a-data-format-change"></a>Code wijzigt die resulteren in een wijziging van de indeling gegevens
Aangezien Hallo gegevensindeling wordt bepaald door de C#-klassen, mogelijk wijzigingen toohello klassen indeling gewijzigde gegevens. Wees voorzichtig tooensure dat kan worden verwerkt door een uitrollende upgrade Hallo gegevensindeling wijzigen. Voorbeelden kunnen leiden tot gegevenswijzigingen van de indeling:

* Het toevoegen of verwijderen van velden of eigenschappen
* Naamswijzigingen velden of eigenschappen
* Hallo-typen van velden of eigenschappen wijzigen
* Hallo de naam van klasse of naamruimte wijzigen

### <a name="data-contract-as-hello-default-serializer"></a>Gegevenscontract als standaard serialisatiefunctie Hallo
Hallo serialisatiefunctie is is verantwoordelijk voor het Hallo-gegevens lezen en bij het deserialiseren van het naar de huidige versie hello, zelfs als Hallo gegevens zich in een oudere of *nieuwere* versie. Hallo standaard serialisatiefunctie is Hallo [gegevenscontract serialisatiefunctie](https://msdn.microsoft.com/library/ms733127.aspx), die goed gedefinieerde versieregels heeft. Betrouwbare verzamelingen kunnen Hallo serialisatiefunctie toobe genegeerd, maar Reliable Actors momenteel niet. Hallo gegevens serialisatiefunctie speelt een belangrijke rol bij het inschakelen van rollende upgrades. Hallo gegevenscontract serialisatiefunctie is Hallo serialisatiefunctie die we voor Service Fabric-toepassingen aanbevelen.

## <a name="how-hello-data-format-affects-a-rolling-upgrade"></a>Hoe Hallo gegevensindeling is van invloed op een uitrollende upgrade
Tijdens een rolling upgrade er zijn twee hoofdscenario's waar Hallo serialisatiefunctie een oudere ondervinden of *nieuwere* versie van uw gegevens:

1. Nadat een knooppunt is bijgewerkt en wordt een back-up wordt gestart, wordt nieuwe serialisatiefunctie Hallo Hallo gegevens persistente toodisk door de oude versie Hallo geladen.
2. Tijdens het Hallo rolling upgrade, bevat Hallo cluster een combinatie van Hallo oude en nieuwe versies van uw code. Omdat replica's kunnen worden geplaatst in verschillende domeinen van de upgrade en replica's gegevens tooeach andere, hello nieuwe en/of oude verzenden kan versie van uw gegevens door Hallo nieuwe en/of de oude versie van de serializer worden aangetroffen.

> [!NOTE]
> Hallo ' nieuwe ' en 'oude versie' hier verwijzen toohello versie van uw code die wordt uitgevoerd. Hallo 'nieuwe serialisatiefunctie' verwijst toohello serialisatiefunctie code die wordt uitgevoerd in de nieuwe versie van uw toepassing hello. Hallo 'nieuwe gegevens' verwijst toohello geserialiseerd C#-klasse van de nieuwe versie van uw toepassing hello.
> 
> 

Hallo twee versies van code en indeling van gegevens moet voorwaarts en achterwaarts compatibel. Als ze niet compatibel zijn, Hallo rolling upgrade mislukken of mogelijk gegevens verloren. Hallo rolling upgrade mislukken omdat Hallo code of serialisatiefunctie veroorzaken kan uitzonderingen of een storing zodra het Hallo andere versie. Gegevens zijn mogelijk verloren als er bijvoorbeeld een nieuwe eigenschap is toegevoegd, maar Hallo oude serialisatiefunctie verwijdert alle tijdens de deserialisatie.

Gegevenscontract is Hallo aanbevolen oplossing om ervoor te zorgen dat uw gegevens compatibel is. Goed gedefinieerde versieregels voor toevoegen, verwijderen en wijzigen van velden heeft. Het biedt ook ondersteuning voor omgaan met onbekende velden en omgaan met klassenovername in Hallo serialisatie en deserialisatie proces vereist. Zie voor meer informatie [gegevenscontract met behulp van](https://msdn.microsoft.com/library/ms733127.aspx).

## <a name="next-steps"></a>Volgende stappen
[Een upgrade van uw toepassing met behulp van Visual Studio](service-fabric-application-upgrade-tutorial.md) begeleidt u bij een upgrade van de toepassing met Visual Studio.

[Een upgrade van uw toepassing met behulp van Powershell](service-fabric-application-upgrade-tutorial-powershell.md) begeleidt u bij een upgrade van de toepassing met behulp van PowerShell.

Bepalen hoe uw toepassing wordt bijgewerkt met behulp van [Parameters Upgrade](service-fabric-application-upgrade-parameters.md).

Meer informatie over hoe toouse geavanceerde functies tijdens het bijwerken van uw toepassing door ernaar te verwijzen[geavanceerde onderwerpen](service-fabric-application-upgrade-advanced.md).

Veelvoorkomende problemen oplossen in toepassingsupgrades door te verwijzen toohello stappen in [toepassingsupgrades probleemoplossing ](service-fabric-application-upgrade-troubleshooting.md).

