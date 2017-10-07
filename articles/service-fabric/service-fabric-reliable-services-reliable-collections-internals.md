---
title: interne werking van Service Fabric betrouwbare status Manager en betrouwbare verzameling aaaAzure | Microsoft Docs
description: Deep dive op betrouwbare verzameling concepten en ontwerp in Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a>Interne werking van Azure Service Fabric betrouwbaar status Manager en betrouwbare verzameling
Dit document delves binnen betrouwbare statusbeheer en betrouwbare verzamelingen toosee hoe kernonderdelen achter de schermen Hallo werken.

> [!NOTE]
> Dit document is werk wordt uitgevoerd. Voeg opmerkingen toothis artikel tootell ons welke onderwerp u graag meer informatie over toolearn.
>

##  <a name="local-persistence-model-log-and-checkpoint"></a>Lokale persistentie model: logboek- en controlepunt
Ga als volgt een persistentie model dat wordt aangeroepen logboek- en controlepunt Hallo betrouwbare statusbeheer en betrouwbare verzamelingen.
In dit model wordt elke wijziging in de status op de schijf voor het eerst geregistreerd en vervolgens toegepast in het geheugen.
Hallo voltooid staat zelf is alleen sporadisch persistent (ook Controlepunt).
Hallo voordeel is dat de delta's zijn ingeschakeld in opeenvolgende alleen toevoegen schrijfbewerkingen op de schijf voor betere prestaties.

toobetter hello logboek- en controlepunt model begrijpen, laten we eerst bekijkt hello oneindige schijf scenario.
Hallo betrouwbare status Manager registreert elke bewerking voordat deze worden gerepliceerd.
Hallo betrouwbare verzamelingen tooapply Hallo bewerking kan logboekregistratie alleen in het geheugen.
Omdat logboeken zijn persistent hebt gemaakt, zelfs wanneer Hallo replica mislukt en toobe opnieuw is opgestart, moet heeft Hallo betrouwbare statusbeheer voldoende informatie in het logboek tooreplay alle Hallo bewerkingen Hallo replica heeft verloren.
Als het Hallo-schijf is oneindig, logboekrecords nooit moeten toobe verwijderd en hello betrouwbare verzameling moet toomanage alleen Hallo geheugenstatus.

Nu gaan we kijken Hallo eindig schijf scenario.
Zoals logboekrecords verzamelen, voert Hallo betrouwbare statusbeheer onvoldoende schijfruimte.
Voordat dit gebeurt, moet Hallo betrouwbare statusbeheer tootruncate de logboek toomake ruimte voor nieuwere Hallo-records.
Betrouwbaar status Manager aanvragen Hallo betrouwbare verzamelingen toocheckpoint hun toodisk geheugenstatus.
Op dit moment zou Hallo betrouwbare verzamelingen blijven behouden de status in het geheugen.
Zodra het Hallo betrouwbare verzamelingen hun controlepunten hebt voltooid, kunt Hallo betrouwbare statusbeheer Hallo logboek toofree schijfruimte vrij afkappen.
Wanneer Hallo replica toobe opnieuw opgestart moet, betrouwbare verzamelingen hun controlepunt herstellen en hello betrouwbare statusbeheer herstelt en alle Hallo statuswijzigingen die sinds de laatste controlepunt Hallo afspeelt.

Een andere waarde toevoegen van controlepunten is dat het verbetert de hersteltijden in algemene scenario's. Het logboek bevat alle bewerkingen die sinds de laatste controlepunt Hallo zich hebben voorgedaan.
Deze kan dus meerdere versies van een item, zoals meerdere waarden voor een bepaalde rij in betrouwbare woordenlijst bevatten.
De controlepunten van een betrouwbare verzameling Hallo daarentegen alleen meest recente versie van elke waarde voor een sleutel.

## <a name="next-steps"></a>Volgende stappen
* [Transacties en vergrendelingen](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

