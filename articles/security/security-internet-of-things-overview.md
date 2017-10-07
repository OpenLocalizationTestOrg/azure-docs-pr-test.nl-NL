---
title: aaaSecure uw Internet der dingen (IoT) in Azure | Microsoft Docs
description: " Azure internet der dingen (IoT)-services bieden een breed scala aan mogelijkheden. In dit artikel helpt u begrijpen hoe toosecure uw IoT-oplossingen in Azure. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a>Overzicht van Internet of Things-beveiliging
Azure internet der dingen (IoT)-services bieden een breed scala aan mogelijkheden. Met deze hoogwaardige services kunt u het volgende doen:

* Gegevens van apparaten verzamelen
* Gegevensstromen in beweging analyseren
* Grote gegevenssets opslaan en er query’s op uitvoeren
* Gegevens in realtime en historische gegevens visualiseren
* Integraties met back-officesystemen uitvoeren

toodeliver deze mogelijkheden kunnen Azure IoT Suite-pakketten meerdere Azure services met aangepaste extensies als vooraf geconfigureerde oplossingen. Deze vooraf geconfigureerde oplossingen zijn basisimplementaties van algemene patronen van IoT-oplossing waarmee tooreduce Hallo u tijd toodeliver uw IoT-oplossingen. Hallo IoT-SDK's gebruikt, kunt u aanpassen en uitbreiden van deze oplossingen toomeet uw eigen vereisten. U kunt deze oplossingen gebruiken als voorbeelden of sjablonen als u nieuwe IoT-oplossingen ontwikkelt.

Hello Azure IoT suite is een krachtige oplossing voor uw IoT-behoeften. Het is echter van upmost belang dat uw IoT-oplossingen zijn ontworpen met beveiligd zijn van Hallo starten. Alle beveiligingsincidenten vanwege het grote aantal Hallo van IoT-apparaten, kan snel een wijdverbreid gebeurtenis met grote gevolgen worden.

toohelp u begrijpt hoe toosecure uw IoT-oplossingen hebben we Hallo informatie te volgen.

## <a name="security-architecture"></a>Beveiligingsarchitectuur
Bij het ontwerpen van een systeem is belangrijk toounderstand Hallo mogelijke bedreigingen toothat systeem en dienovereenkomstig juiste beveiliging niet toevoegen als Hallo system is ontworpen en ontworpen. Het is belangrijk toodesign Hallo product van Hallo begin rekening met beveiliging omdat informatie over hoe een hacker mogelijk kunnen toocompromise een systeem zorgt ervoor geschikt oplossingen zijn in plaats van Hallo begin.

U kunt meer informatie over IoT-beveiligingsarchitectuur door te lezen [Internet van dingen beveiligingsarchitectuur](../iot-suite/iot-security-architecture.md).

Dit artikel worden de volgende onderwerpen Hallo:

* [Beveiliging begint met een risicomodel](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [Beveiliging in IoT](../iot-suite/iot-security-architecture.md#security-in-iot)
* [Threat modellering hello Azure IoT Reference Architecture](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a>Beveiliging van Hallo gemalen
Hallo IoT vormt unieke beveiliging, privacy en naleving uitdagingen toobusinesses overal ter wereld. In tegenstelling tot traditionele cyberbeveiliging technologie waar deze problemen gebaseerd op software- en hoe deze wordt geïmplementeerd, IoT heeft betrekking op wat er gebeurt wanneer Hallo cyberbeveiliging en Hallo fysieke werelden convergeren. Beveiligen van IoT-oplossingen vereist gezorgd beveiligde inrichting van de apparaten, beveiligde verbindingen tussen deze apparaten en het Hallo cloud en de beveiliging van de beveiligde gegevens in de cloud Hallo tijdens de verwerking en opslag. Werken met dergelijke functionaliteit, zijn echter resource beperkte apparaten, geografische verdeling van implementaties en veel apparaten binnen een oplossing.

U leert hoe beveiliging toohandle in de volgende gebieden door te lezen [beveiliging van Internet der dingen van Hallo gemalen](../iot-suite/securing-iot-ground-up.md).

Hallo aan de orde Hallo volgende onderwerpen:

* [Infrastructuur niet vanuit Hallo gemalen beveiligen](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [Microsoft Azure: beveiligde IoT-infrastructuur voor uw bedrijf](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a>Beste praktijken
Een IoT-infrastructuur beveiligen vereist een strengere beveiliging-in-depth-strategie. Van de beveiliging van gegevens in de cloud hello, integriteit van gegevens beveiligt terwijl overdracht in Hallo builds openbare internet, toosecurely inrichting apparaten, elke laag groter beveiligingscontrole Hallo algehele infrastructuur.

U kunt meer informatie over beveiliging van Internet der dingen aanbevolen procedures door te lezen [aanbevolen beveiligingsprocedures voor Internet der dingen](../iot-suite/iot-security-best-practices.md).

Hallo aan de orde Hallo volgende onderwerpen:

* [IoT hardware fabrikant/integrator](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [Ontwikkelaars van IoT-oplossing](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [Implementatie van IoT-oplossing](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [IoT-oplossing operator](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
