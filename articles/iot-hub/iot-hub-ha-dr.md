---
title: IoT Hub hoge beschikbaarheid en herstel na noodgevallen aaaAzure | Microsoft Docs
description: Beschrijft hello Azure en IoT Hub functies waarmee u maximaal beschikbare Azure IoT-oplossingen toobuild met mogelijkheden voor herstel na noodgevallen.
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: ae320e58-aa20-45b9-abdc-fa4faae8e6dd
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: elioda
ms.openlocfilehash: 74e1fa1682258819ffb3fd84eb79e42fc6e4120f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-high-availability-and-disaster-recovery"></a>IoT Hub hoge beschikbaarheid en herstel na noodgevallen
Een Azure-service biedt IoT Hub redundantie op het niveau van de Azure-regio hello, zonder extra werk vereist door Hallo oplossing met hoge beschikbaarheid (HA). Hallo Microsoft Azure-platform omvat ook functies toohelp bouwen van oplossingen met herstelfuncties van noodherstel (DR) of de regio-overschrijdende beschikbaarheid. Als u wilt tooprovide globale, hoge beschikbaarheid van de regio-overschrijdende voor apparaten of gebruikers, ontwerpen en voorbereiden van uw oplossingen tootake profiteren van deze Azure DR-functies. Hallo artikel [Azure zakelijke continuïteit technische richtlijnen](../resiliency/resiliency-technical-guidance.md) beschrijving Hallo ingebouwde functies in Azure voor bedrijfscontinuïteit en Noodherstel. Hallo [herstel na noodgevallen en hoge beschikbaarheid voor Azure-toepassingen] [ Disaster recovery and high availability for Azure applications] papier biedt architectuurrichtlijnen voor strategieën voor Azure-toepassingen tooachieve HA en Noodherstel.

## <a name="azure-iot-hub-dr"></a>Azure IoT-Hub DR
Bovendien toointra regio HA, IoT Hub implementeert failover-mechanismen voor herstel na noodgevallen die geen tussenkomst van Hallo-gebruiker vereisen. IoT Hub DR automatisch wordt gestart en heeft een beoogde hersteltijd (RTO) van 2-26 uur en Hallo herstelpuntdoelen (RPO's) te volgen.

| Functionaliteit | RPO |
| --- | --- |
| Beschikbaarheid van de service voor register- en bewerkingen |Mogelijk CName verlies |
| Identiteitsgegevens in register-id 's |0-5 minuten gegevensverlies |
| Apparaat-naar-cloud-berichten |Alle ongelezen berichten gaan verloren |
| Bewerkingen berichten controleren |Alle ongelezen berichten gaan verloren |
| Cloud-naar-apparaat-berichten |0-5 minuten gegevensverlies |
| Cloud-naar-apparaat feedbackwachtrij |Alle ongelezen berichten gaan verloren |

## <a name="regional-failover-with-iot-hub"></a>Regionale failover met IoT Hub
Een volledige behandeling van implementatietopologieën in IoT-oplossingen is buiten het bereik van dit artikel Hallo. Hallo aan de orde Hallo *regionale failover* implementatiemodel voor Hallo doel van hoge beschikbaarheid en herstel na noodgevallen.

Hallo oplossing voor back-end wordt uitgevoerd voornamelijk in een datacenter-locatie in een model regionale failover en een secundaire IoT-hub en de back-end zijn geïmplementeerd in een andere locatie van het datacenter. Als Hallo IoT-hub in Hallo primaire datacenter te lijden heeft onder een storing of de netwerkverbinding Hallo van Hallo apparaat toohello primaire datacenter wordt onderbroken. Apparaten gebruiken een secundaire service-eindpunt wanneer Hallo primaire gateway niet bereikbaar. Met een regio-overschrijdende failoverfunctionaliteit kan Hallo oplossing beschikbaarheid buiten Hallo hoge beschikbaarheid van één regio worden verbeterd.

Op hoog niveau, tooimplement een regionale failover-model met IoT Hub, hebt u Hallo volgende nodig:

* **Een secundaire iothub en routering logica apparaat**: In geval van een onderbreking van de service in uw primaire regio Hallo apparaten verbinden tooyour secundaire regio moeten worden gestart. Hallo statusbewust aard van de meeste services die betrokken zijn opgegeven, is het gebruikelijk oplossing beheerders tootrigger Hallo regio inter failover-proces. Hallo aanbevolen manier toocommunicate Hallo nieuwe eindpunt toodevices, terwijl het besturingselement van het Hallo-proces is toohave ze regelmatig te controleren een *concierge* service voor de huidige actieve eindpunt Hallo. Hallo concierge-service is een webtoepassing die is gerepliceerd en bewaard bereikbaar met behulp van DNS-omleiding technieken (bijvoorbeeld [Azure Traffic Manager][Azure Traffic Manager]).
* **Identiteit register repliceren** -toobe bruikbaar, Hallo secundaire IoT-hub moet bevatten alle apparaat-id's die verbinding van toohello oplossing maken kunnen. Hallo-oplossing moet behoudt back-ups geogerepliceerde van apparaat-id's en toohello secundaire IoT-hub uploaden voordat u de Hallo actief eindpunt voor Hallo-apparaten. Hallo apparaat identiteit export-functionaliteit van IoT Hub is handig in deze context. Zie voor meer informatie [IoT Hub developer guide - id-register][IoT Hub developer guide - identity registry].
* **Samenvoegen van logica** : wanneer de primaire regio Hallo weer beschikbaar is, alle Hallo status en gegevens die zijn gemaakt in de secundaire site Hallo moet gemigreerde back toohello primaire regio. Deze status en gegevens verbindt voornamelijk toodevice identiteiten en metagegevens van toepassing moet worden samengevoegd met de Hallo primaire iothub en andere toepassingsspecifieke winkels in de primaire regio Hallo. toosimplify deze stap moet u de idempotent-bewerkingen. De Idempotent operations minimaliseren Hallo neveneffecten van Hallo eventuele consistente distributie van gebeurtenissen en van duplicaten of out-van-levering van gebeurtenissen. Bovendien moet Hallo toepassingslogica ontworpen tootolerate mogelijke inconsistenties of 'enigszins' uit datum-status. Deze situatie kan optreden vanwege toohello extra tijd die nodig is voor Hallo systeem te 'retoucheren' op basis van herstelpuntdoelen (RPO).

## <a name="next-steps"></a>Volgende stappen
Volg deze koppelingen toolearn meer informatie over Azure IoT Hub:

* [Aan de slag met IoT Hubs (zelfstudie)][lnk-get-started]
* [Wat is Azure IoT Hub?][What is Azure IoT Hub?]

[Disaster recovery and high availability for Azure applications]: ../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md
[Azure Business Continuity Technical Guidance]: https://azure.microsoft.com/documentation/articles/resiliency-technical-guidance/
[Azure Traffic Manager]: https://azure.microsoft.com/documentation/services/traffic-manager/
[IoT Hub developer guide - identity registry]: iot-hub-devguide-identity-registry.md

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[What is Azure IoT Hub?]: iot-hub-what-is-iot-hub.md
