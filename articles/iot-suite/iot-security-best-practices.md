---
title: aanbevolen beveiligingsprocedures voor aaaIoT | Microsoft Docs
description: Aanbevolen beveiligingsprocedures voor het beveiligen van uw IoT-infrastructuur
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 24e7bda2-5f7b-44e3-b8af-761abd3276ff
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: yurid
ms.openlocfilehash: 3a546c67978a519446ab6c83917a0789675f1b52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a>Aanbevolen beveiligingsprocedures voor Internet der dingen
toosecure een Internet der dingen (IoT)-infrastructuur vereist een strengere beveiliging-in-depth-strategie. Deze strategie moet u de gegevens in de cloud Hallo toosecure, de integriteit van de gegevens onderweg te beschermen dan Hallo openbare internet en veilig apparaten inrichten. Elke laag builds groter beveiligingscontrole in Hallo algehele infrastructuur.

## <a name="secure-an-iot-infrastructure"></a>Een IoT-infrastructuur beveiligen
Deze strategie security-in-depth worden ontwikkeld en uitgevoerd met actieve deelname van verschillende spelers die betrokken zijn bij Hallo productie, ontwikkeling en implementatie van IoT-apparaten en infrastructuur. Hier volgt een beschrijving van deze spelers.  

* **IoT hardware fabrikant/integrator**: dit zijn meestal Hallo fabrikanten van IoT-hardware wordt geïmplementeerd, hardware en samen te stellen van verschillende fabrikanten of leveranciers bieden hardware voor de implementatie van een IoT geproduceerd SI's of geïntegreerde door andere leveranciers.
* **IoT-oplossing developer**: Hallo ontwikkeling van een IoT-oplossing gewoonlijk wordt uitgevoerd door de ontwikkelaar van een oplossing. Deze ontwikkelaar kan deel uitmaken van een intern team of een system integrator (SI) die zijn gespecialiseerd in deze activiteit. Hallo IoT-oplossing developer kunt diverse onderdelen van de IoT-oplossing Hallo vanaf het begin te ontwikkelen, integreren van verschillende gebruiksklare of open source-onderdelen of vooraf geconfigureerde oplossingen met kleine aanpassing vast.
* **IoT-oplossing deployer**: na een IoT-oplossing is ontwikkeld, moet het eerst toobe geïmplementeerd in het Hallo-veld. Hiervoor moet de implementatie van hardware, koppeling van apparaten en implementeren van oplossingen in hardwareapparaten of Hallo cloud.
* **IoT-oplossing operator**: nadat Hallo IoT-oplossing is geïmplementeerd, langlopende bewerkingen, bewaking, upgrades en onderhoud is vereist. Dit kan worden gedaan door een interne team dat bestaat uit gegevens technologiespecialisten, hardwarebewerkingen en onderhoud teams en domein specialisten die Hallo correctie van algemene IoT-infrastructuur bewaken.

Hallo gedeelten vindt u aanbevolen procedures voor elk van deze toohelp spelers ontwikkelen, implementeren en beheren van een beveiligde IoT-infrastructuur.

## <a name="iot-hardware-manufacturerintegrator"></a>IoT hardware fabrikant/integrator
Hallo volgen Hallo aanbevolen procedures voor IoT hardwarefabrikanten en hardware SI's.

* **Bereik toominimum hardwarevereisten**: Hallo hardwareontwerp Hallo minimale functies die vereist zijn voor de werking van Hallo hardware, en niets meer moet bevatten. Een voorbeeld is tooinclude USB-poorten alleen indien nodig voor de bewerking Hallo Hallo-apparaat. Deze extra functies open Hallo-apparaat voor ongewenste aanvalsvectoren die moeten worden vermeden.
* **Controleer hardware bewijs knoeien**: bouwen in mechanismen toodetect fysieke knoeien, zoals het openen van de Hallo apparaat dekking of een deel van het Hallo-apparaat verwijderen. Deze signalen knoeien maakt mogelijk deel uit van Hallo gegevens geüpload stroom toohello, waardoor operators van deze gebeurtenissen kan een waarschuwing.
* **Bouwen om beveiligde hardware**: als omzet is toegestaan, beveiligingsfuncties zoals beveiligd en versleuteld storage opbouwen of functionaliteit op basis van Trusted Platform Module (TPM) worden opgestart. Deze functies maken-apparaten meer beveiligen en te beveiligen Hallo algemene IoT-infrastructuur.
* **Beveiligen van upgrades**: Firmware bijwerken tijdens de levensduur Hallo Hallo apparaat zijn onvermijdelijk. Het bouwen van apparaten met beveiligde paden voor upgrades en cryptografische zekerheid van de firmware-versies kunt Hallo apparaat toobe beveiligde tijdens en na de upgrade.

## <a name="iot-solution-developer"></a>Ontwikkelaars van IoT-oplossing
Hallo volgen Hallo best practices voor ontwikkelaars van IoT-oplossingen:

* **Ga als volgt beveiligde software development methodologie**: ontwikkeling van beveiligde software vereist a t/m nadenkt over de beveiliging van Hallo begin van Hallo project alle Hallo manier tooits implementatie, testen en implementeren. Hallo keuzes platforms, talen en hulpprogramma's, worden met deze methode beïnvloed. Hallo Microsoft Security Development Lifecycle biedt een stapsgewijze benadering toobuilding beveiligde software.
* **Kies open source software zorgvuldig**: Open-source software biedt de mogelijkheid tooquickly oplossingen ontwikkelen. Bij het kiezen van open-source software, overweeg activiteitenniveau Hallo van Hallo community voor elk onderdeel van de open source. Een actieve community zorgt ervoor dat de software wordt ondersteund en dat problemen zijn gedetecteerd en opgelost. U kunt ook een verborgen en inactieve open source software wordt mogelijk niet ondersteund en problemen worden mogelijk niet gedetecteerd.
* **Integreren met zorg**: veel software beveiligingsfouten bestaat op Hallo grens van bibliotheken en -API. Functionaliteit die niet vereist voor de huidige implementatie Hallo zijn mogelijk nog steeds beschikbaar is via een API-laag. tooensure algehele beveiliging, zorg ervoor dat toocheck alle interfaces van onderdelen voor beveiligingsfouten wordt geïntegreerd.      

## <a name="iot-solution-deployer"></a>Implementatie van IoT-oplossing
Hallo hieronder vindt u aanbevolen procedures voor IoT-oplossing deployers:

* **Hardware veilig implementeren**: IoT-implementaties kunnen hardware toobe geïmplementeerd in niet-beveiligde locaties, zoals in openbare ruimten of zonder supervisie landinstellingen in beslag. In dergelijke situaties Zorg ervoor dat de implementatie van de hardware fraudebestendig toohello zover. Zorg ervoor dat ze veilig worden behandeld als het USB- of andere poorten beschikbaar op Hallo hardware zijn. Veel aanvalsvectoren kunnen deze als toegangspunten gebruiken.
* **Verificatiesleutels veilig te houden**: tijdens de implementatie van elk apparaat vereist dat apparaat-id's en bijbehorende verificatiesleutels gegenereerd door Hallo cloud-service. Beveilig deze sleutels fysiek zelfs na het Hallo-implementatie. Een willekeurige toets waarmee is geknoeid kan worden gebruikt door een kwaadwillende apparaat toomasquerade als een bestaand apparaat.

## <a name="iot-solution-operator"></a>IoT-oplossing operator
Hallo volgen Hallo best practices voor operators van IoT-oplossing:

* **Hallo systeem toodate houden**: Controleer of besturingssystemen van apparaten en alle apparaatstuurprogramma's de meest recente versies bijgewerkte toohello zijn. Als u automatische updates in Windows 10 (IoT of andere SKU's) inschakelen, houdt Microsoft deze up toodate, bieden een beveiligd besturingssysteem voor IoT-apparaten. Andere besturingssystemen (zoals Linux) up toodate ervoor zorgt dat ze ook zijn beschermd tegen schadelijke aanvallen.
* **Bescherming tegen schadelijke activiteiten**: als het Hallo-besturingssysteem toestaat, Hallo nieuwste antivirus- en antimalwaresoftware mogelijkheden op elk besturingssysteem installeren. Zo kunt u de meeste externe bedreigingen te verhelpen. U kunt de meeste moderne besturingssystemen tegen bedreigingen beveiligen door passende maatregelen te nemen.
* **Regelmatig controleren**: controle IoT-infrastructuur voor beveiligingsproblemen is sleutel wanneer toosecurity incidenten reageert. De meeste besturingssystemen bieden de registratie van de ingebouwde gebeurtenissen die moet worden gecontroleerd vaak toomake ervoor dat er geen inbreuk op de beveiliging is opgetreden. Controle-informatie kan worden verzonden als een cloudservice van afzonderlijke telemetrie stroom toohello waarin deze kan worden geanalyseerd.
* **Fysiek Hallo IoT-infrastructuur beveiligen**: Hallo slechtste beveiligingsaanvallen tegen IoT-infrastructuur met behulp van de fysieke toegang toodevices worden gestart. Een belangrijk veiligheid practice is tooprotect tegen kwaadaardig gebruik van USB-poorten en andere fysieke toegang. Een sleutel toouncovering schendingen die hebben plaatsgevonden is logboekregistratie van fysieke toegang tot, zoals USB-poort gebruiken. Windows 10 (IoT en andere SKU's) kunnen ook gedetailleerde logboekregistratie van deze gebeurtenissen.
* **Beveiligen van referenties van de cloud**: referenties voor Cloud-verificatie gebruikt voor het configureren en gebruiken van een IoT-implementatie zijn mogelijk Hallo gemakkelijkste manier toogain toegang en een IoT-systeem. Hallo referenties beveiligen door Hallo wachtwoord vaak veranderen, en geen deze referenties te gebruiken op openbare computers.

Mogelijkheden van andere IoT-apparaten variëren. Sommige apparaten mogelijk computers met algemene desktopbesturingssystemen en sommige apparaten mogelijk zeer lichte besturingssystemen worden uitgevoerd. Hallo best practices voor beveiliging beschreven eerder mogelijk van toepassing toothese apparaten in verschillende mate. Indien opgegeven, moeten aanvullende beveiligings- en best practices uit Hallo fabrikanten van deze apparaten worden gevolgd.

Sommige oudere en beperkte apparaten mogelijk niet hebben is speciaal ontworpen voor IoT-implementatie. Deze apparaten mogelijk Hallo mogelijkheid tooencrypt gegevens hebben geen verbinding maken met Internet Hallo of bieden geavanceerde controle. In dergelijke gevallen een moderne en veilige veldgateway statistische gegevens van oudere apparaten en Hallo beveiliging vereist voor deze apparaten via Internet Hallo verbinding te maken. Veld gateways kunnen bieden veilige verificatie, onderhandeling van versleutelde sessies, ontvangst van de opdrachten van Hallo cloud en veel andere beveiligingsfuncties.

## <a name="see-also"></a>Zie ook
toolearn meer informatie over het beveiligen van uw IoT-oplossing, Zie:

* [IoT-beveiligingsarchitectuur][lnk-security-architecture]
* [Beveiligen van uw IoT-omgeving][lnk-security-deployment]

U kunt ook verkennen van Hallo andere functies en mogelijkheden van Hallo vooraf geconfigureerde IoT Suite-oplossingen:

* [Overzicht van voorspeld onderhoud vooraf geconfigureerde oplossing][lnk-predictive-overview]
* [Veelgestelde vragen over Azure IoT Suite][lnk-faq]

U kunt meer informatie over beveiliging in IoT Hub [besturingselement toegang tooIoT Hub] [ lnk-devguide-security] in Hallo Ontwikkelaarshandleiding voor IoT Hub.

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md

[lnk-security-architecture]: iot-security-architecture.md
[lnk-security-deployment]: iot-suite-security-deployment.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md
