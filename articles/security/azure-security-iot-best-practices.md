---
title: aaaInternet van aanbevolen beveiligingsprocedures voor dingen | Microsoft Docs
description: Hallo artikel bevat een samengestelde lijst met Microsoft Internet van dingen Best Practices voor beveiliging en algemene aanbevelingen.
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 7ee31c912e8ac230ffa5efcd5b4c2b0b0713584f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a>Internet der dingen Best Practices voor beveiliging
Beveiligen Hallo Internet der dingen (IoT)-infrastructuur is een kritieke onderneming voor iedereen die betrokken zijn bij IoT-oplossingen. Vanwege het aantal apparaten bij betrokken zijn hello en Hallo verwante gedistribueerde aard van deze apparaten, Hallo impact een beveiligingsgebeurtenis toocompromise miljoenen IoT-apparaten is niet-triviale en wijdverbreid invloed kan hebben.

IoT-beveiliging moet daarom een security-in-depth-benadering. Gegevens behoeften toobe beveiligd in cloud Hallo en die worden verplaatst via persoonlijke en openbare netwerken. Methoden moeten toobe in place toosecurely inrichten Hallo IoT-apparaten zelf. Elke laag van het apparaat, toonetwork, toocloud back-end moet sterke beveiliging garantie.

Aanbevolen procedures van IoT kunnen worden ingedeeld in de volgende manieren Hallo:

* IoT-hardwarefabrikant of integrator
* Ontwikkelaars van IoT-oplossing
* Implementatie van IoT-oplossing
* IoT-oplossing operator

In dit artikel bevat een overzicht van [Internet van dingen aanbevolen beveiligingsprocedures](../iot-suite/iot-security-best-practices.md). Raadpleeg toothat artikel voor meer gedetailleerde informatie.

## <a name="iot-hardware-manufacturer-or-integrator"></a>IoT-hardwarefabrikant of integrator
Volg de aanbevolen procedures Hallo hieronder als u een hardwarefabrikant IoT of een integrator hardware:

* **Bereik toominimum hardwarevereisten**: Hallo hardwareontwerp minimale functies die vereist zijn voor de werking van Hallo hardware, en niets meer moet bevatten. 
* **Controleer hardware bewijs knoeien**: bouwen in mechanismen toodetect fysieke knoeien met hardware, zoals het openen van Hallo apparaat behandeld, verwijderen van een deel van het Hallo-apparaat, enzovoort. 
* **Bouwen om beveiligde hardware**: als [omzet](https://en.wikipedia.org/wiki/Cost_of_goods_sold) toestaan, beveiligingsfuncties zoals beveiligd en versleuteld opslag en functionaliteit van de Trusted Platform Module TPM-opstart opbouwen.
* **Beveiligen van upgrades**: firmware bijwerken tijdens de levensduur van Hallo-apparaat is onvermijdelijk.

## <a name="iot-solution-developer"></a>Ontwikkelaars van IoT-oplossing
Volg de aanbevolen procedures Hallo hieronder als u een ontwikkelaar IoT-oplossing:

* **Ga als volgt beveiligde software development methodologie**: a t/m nadenkt over de beveiliging van Hallo begin van Hallo project alle Hallo manier tooits implementatie, testen en de implementatie ontwikkelen van beveiligde software vereist.
* **Kies open-sourcesoftware zorgvuldig**: open-sourcesoftware biedt de mogelijkheid tooquickly oplossingen ontwikkelen.
* **Integreren met zorg**: veel Hallo software beveiligingsfouten bestaat op Hallo grens van bibliotheken en -API. 

## <a name="iot-solution-deployer"></a>Implementatie van IoT-oplossing
Volg de aanbevolen procedures Hallo hieronder als u een deployer IoT-oplossing:

* **Hardware veilig implementeren**: IoT-implementaties kunnen hardware toobe geïmplementeerd in niet-beveiligde locaties, zoals in openbare ruimten of zonder supervisie landinstellingen in beslag.
* **Verificatiesleutels veilig te houden**: tijdens de implementatie van elk apparaat vereist dat apparaat-id's en bijbehorende verificatiesleutels gegenereerd door Hallo cloud-service. Beveilig deze sleutels fysiek zelfs na het Hallo-implementatie. Een willekeurige toets waarmee is geknoeid kan worden gebruikt door een kwaadwillende apparaat toomasquerade als een bestaand apparaat.

## <a name="iot-solution-operator"></a>IoT-oplossing operator
Volg de aanbevolen procedures Hallo hieronder als u een IoT-oplossing operator:

* **Houd systemen toodate**: Zorg ervoor dat de besturingssystemen van apparaten en alle apparaatstuurprogramma's zijn de meest recente versies bijgewerkte toohello. 
* **Bescherming tegen schadelijke activiteiten**: als het Hallo-besturingssysteem toestaat, Hallo nieuwste antivirus- en anti-malware-mogelijkheden op elk besturingssysteem plaatsen. 
* **Regelmatig controleren**: controle IoT-infrastructuur voor beveiliging problemen is sleutel verwante wanneer toosecurity incidenten reageert.
* **Fysiek Hallo IoT-infrastructuur beveiligen**: Hallo slechtste beveiligingsaanvallen tegen IoT-infrastructuur met behulp van de fysieke toegang toodevices worden gestart.
* **Beveiligen van referenties van de cloud**: referenties voor cloud-verificatie gebruikt voor het configureren en gebruiken van een IoT-implementatie zijn mogelijk Hallo gemakkelijkste manier toogain toegang en een IoT-systeem. 

