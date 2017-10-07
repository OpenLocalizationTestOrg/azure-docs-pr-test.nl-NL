---
title: aaaService Fabric app upgrade-zelfstudie | Microsoft Docs
description: In dit artikel wordt uitgelegd Hallo-ervaring van een Service Fabric-toepassing implementeren, Hallo programmacode wijzigen en implementeren van een upgrade met behulp van Visual Studio.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a3181a7a-9ab1-4216-b07a-05b79bd826a4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: d069ff0b291018dbac846e65cddff1e9d73d156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-tutorial-using-visual-studio"></a>Service Fabric-toepassing upgraden zelfstudie met Visual Studio
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Azure Service Fabric vereenvoudigt Hallo proces van updaten van cloud-toepassingen door ervoor te zorgen dat alleen gewijzigde services worden bijgewerkt en dat de status van gedurende het upgradeproces Hallo wordt bewaakt. Deze teruggedraaid ook automatisch Hallo toepassing toohello eerdere versie wordt uitgevoerd voor problemen. Service Fabric-toepassingsupgrades worden *Zero Downtime*, aangezien het Hallo-toepassing kan worden bijgewerkt zonder uitvaltijd. Deze zelfstudie bevat informatie over hoe toocomplete een uitrollende upgrade vanuit Visual Studio.

## <a name="step-1-build-and-publish-hello-visual-objects-sample"></a>Stap 1: Bouwen en Hallo visuele objecten voorbeeld publiceren
Eerst downloaden Hallo [visuele objecten](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Actors/VisualObjects) toepassing vanuit GitHub. Vervolgens bouwen en Hallo toepassing publiceren door met de rechtermuisknop op het Hallo-toepassingsproject **VisualObjects**, en het selecteren van Hallo **publiceren** opdracht in Hallo Service Fabric-menu-item.

![Contextmenu voor een Service Fabric-toepassing][image1]

Selecteren **publiceren** opstart, wordt een pop-up en u kunt Hallo **profiel als doel** te**PublishProfiles\Local.xml**. Hallo venster ziet er als Hallo voordat u op volgende **publiceren**.

![Een Service Fabric-toepassing publiceren][image2]

Nu kunt u **publiceren** in het dialoogvenster Hallo. U kunt [Service Fabric Explorer tooview Hallo cluster en Hallo toepassing](service-fabric-visualizing-your-cluster.md). Hallo visuele objecten toepassing heeft een webservice die u kunt gaan tooby typen [http://localhost:8081/visualobjects/](http://localhost:8081/visualobjects/) in de adresbalk Hallo van uw browser.  Hier ziet u 10 zwevende visual objecten verplaatsen in het welkomstscherm.

**Opmerking:** als implementeert te`Cloud.xml` profiel (Azure Service Fabric) moet beschikbaar zijn op de toepassing hello vervolgens **http://{ServiceFabricName}. { Region}.cloudapp.Azure.com:8081/visualobjects/**. Zorg ervoor dat u hebt `8081/TCP` geconfigureerd in Hallo Load Balancer (Hallo Load Balancer niet vinden in Hallo dezelfde resourcegroep als Hallo Service Fabric-instantie).

## <a name="step-2-update-hello-visual-objects-sample"></a>Stap 2: Hallo visuele objecten voorbeeld bijwerken
U wellicht opgevallen dat met Hallo-versie die is geïmplementeerd in stap 1, Hallo visuele objecten niet draaien. Deze toepassing tooone waar Hallo visuele objecten ook draaien gaat upgraden.

Selecteer Hallo VisualObjects.ActorService-project binnen Hallo VisualObjects oplossing en open het Hallo **VisualObjectActor.cs** bestand. Ga in dat bestand toohello methode `MoveObject`, uitcommentariëren `visualObject.Move(false)`, en verwijder het commentaarteken `visualObject.Move(true)`. Deze codewijziging draait Hallo objecten na de upgrade van Hallo-service.  **Nu kunt u (niet opnieuw opbouwen) oplossing Hallo**, projecten die Hallo builds worden gewijzigd. Als u selecteert *alles opnieuw opbouwen*, er tooupdate Hallo versies voor alle projecten Hallo.

Er moet ook tooversion onze toepassing. toomake hello versie wordt gewijzigd nadat u met de rechtermuisknop op Hallo **VisualObjects** project, kunt u Visual Studio Hallo **Manifest versies bewerken** optie. Deze optie wordt in het dialoogvenster voor editie-versies Hallo als volgt:

![Dialoogvenster versiebeheer][image3]

Hallo Updateversies voor Hallo gewijzigd projecten en hun code pakketten, samen met de Hallo toepassing tooversion 2.0.0. Nadat Hallo wijzigingen zijn aangebracht, Hallo manifest moet eruitzien als in de volgende Hallo (vet gedeelten weergeven Hallo wijzigingen):

![Versies bijwerken][image4]

Hallo Visual Studio-hulpprogramma's kunnen doen automatische samentellingen van versies bij het selecteren van **automatisch bijwerken van toepassing en Serviceversies**. Als u [SemVer](http://www.semver.org), moet u tooupdate Hallo code en/of configuratie pakket versie alleen als deze optie is geselecteerd.

Hallo wijzigingen opslaan en nu controleren Hallo **Upgrade Hallo toepassing** vak.

## <a name="step-3--upgrade-your-application"></a>Stap 3: Uw toepassing bijwerken
Maak uzelf bekend met Hallo [parameters voor het bijwerken van toepassing](service-fabric-application-upgrade-parameters.md) en Hallo [upgradeproces](service-fabric-application-upgrade.md) tooget een goed begrip van Hallo verschillende parameters, time-outs en health criterium kunt upgraden worden toegepast. Voor dit scenario is Hallo service health evaluatiecriterium toohello standaard (niet-bewaakte modus) ingesteld. U kunt deze instellingen configureren door te selecteren **instellingen configureren voor Upgrade** en vervolgens Hallo parameters naar wens te bewerken.

Nu we alle set toostart Hallo toepassing zijn door het selecteren van de upgrade **publiceren**. Deze optie voert een upgrade van uw toepassing tooversion 2.0.0, waarin Hallo objecten draaien. Service Fabric upgrades één updatedomein tegelijk (sommige objecten zijn bijgewerkt eerst, gevolgd door anderen) en Hallo-service tijdens de upgrade Hallo toegankelijk blijft. Toohello-Access-service kan worden gecontroleerd via de client (browser).  

Nu, zoals upgrade opbrengst toepassing hello, u kunt deze bewaken met Service Fabric Explorer met Hallo **Upgrades uitgevoerd** tabblad onder Hallo-toepassingen.

Alle domeinen van de update moeten worden bijgewerkt (voltooid) over een paar minuten en Visual Studio-uitvoervenster Hallo moet ook-status dat die Hallo-upgrade is voltooid. En u ziet dat *alle* Hallo visuele objecten in uw browservenster zijn nu draaien!

U kunt wilt tootry Hallo versies wijzigen en het verplaatsen van versie 2.0.0 tooversion 3.0.0 wijze van oefening maakt, of zelfs van versie 2.0.0 back-tooversion 1.0.0. Spelen met time-outs en health beleid toomake uzelf bekend mee. Wanneer het lokale cluster tooa implementeren tooan Azure als het cluster worden geboden, misschien Hallo parameters gebruikt toodiffer. U wordt aangeraden dat u de Hallo time-outs conservatieve ingesteld.

## <a name="next-steps"></a>Volgende stappen
[Bijwerken van uw toepassing met behulp van PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) begeleidt u bij een upgrade van de toepassing met behulp van PowerShell.

Bepalen hoe uw toepassing wordt bijgewerkt met behulp van [parameters upgrade](service-fabric-application-upgrade-parameters.md).

Uw toepassingsupgrades compatibel maken door leren hoe toouse [serialisatie van gegevens](service-fabric-application-upgrade-data-serialization.md).

Meer informatie over hoe toouse geavanceerde functies tijdens het bijwerken van uw toepassing door ernaar te verwijzen[geavanceerde onderwerpen](service-fabric-application-upgrade-advanced.md).

Veelvoorkomende problemen oplossen in toepassingsupgrades door te verwijzen toohello stappen in [probleemoplossing toepassingsupgrades](service-fabric-application-upgrade-troubleshooting.md).

[image1]: media/service-fabric-application-upgrade-tutorial/upgrade7.png
[image2]: media/service-fabric-application-upgrade-tutorial/upgrade1.png
[image3]: media/service-fabric-application-upgrade-tutorial/upgrade5.png
[image4]: media/service-fabric-application-upgrade-tutorial/upgrade6.png
