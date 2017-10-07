---
title: aaaVerify Azure Traffic Manager-instellingen | Microsoft Docs
description: Dit artikel helpt u de instellingen van uw Traffic Manager controleren
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 2180b640-596e-4fb2-be59-23a38d606d12
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: c670be6cf55e140c7ab63d5d526de08e14774d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="verify-traffic-manager-settings"></a>Controleer de instellingen voor het Traffic Manager

tootest uw Traffic Manager-instellingen, moet u toohave na meerdere clients, op verschillende locaties, van waaruit u kunt uw tests uitvoeren. Vervolgens, Hallo eindpunten te brengen in uw Traffic Manager-profiel beneden één tegelijk.

* Hallo DNS TTL-waarde laag ingesteld zodat wijzigingen die zijn doorgegeven snel (bijvoorbeeld 30 seconden).
* Weten Hallo IP-adressen van uw Azure-cloudservices en websites in Hallo profiel die u wilt testen.
* Gebruik hulpprogramma's waarmee u een IP-adres van DNS-naam tooan omzetten en dat adres weer te geven.

Toosee dat Hallo DNS-namen tooIP adressen Hallo-eindpunten in uw profiel omzetten dat u controleert. Hallo namen moeten worden omgezet in samenhang met de Hallo verkeersrouteringsmethode gedefinieerd in Hallo Traffic Manager-profiel. U kunt Hallo hulpmiddelen zoals **nslookup** of **verdiepen** tooresolve DNS-namen.

Hallo volgende voorbeelden laten zien hoe u uw Traffic Manager-profiel te testen.

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a>Traffic Manager-profiel met nslookup en ipconfig in Windows controleren

1. Open een opdracht of een Windows PowerShell-prompt als beheerder.
2. Type `ipconfig /flushdns` tooflush Hallo cache DNS-resolver.
3. Typ `nslookup <your Traffic Manager domain name>`. Bijvoorbeeld, Hallo opdracht controles Hallo domeinnaam met Hallo voorvoegsel na *myapp.contoso*

        nslookup myapp.contoso.trafficmanager.net

    Een typische resultaat ziet Hallo volgende informatie:

    + Hallo DNS-naam en IP-adres van het Hallo DNS-server wordt geopend tooresolve deze Traffic Manager-domeinnaam.
    + Hallo Traffic Manager-domeinnaam u hebt getypt op Hallo vanaf de opdrachtregel na 'nslookup' en Hallo IP-adres toowhich Hallo Traffic Manager-domein wordt omgezet. Hallo tweede IP-adres is belangrijk een toocheck Hallo. Deze moet overeenkomen met een openbare virtueel IP-adres (VIP)-adres voor een van de Hallo cloudservices of websites in Hallo Traffic Manager-profiel die u wilt testen.

## <a name="how-tootest-hello-failover-traffic-routing-method"></a>Hoe tootest Hallo failover methode voor het doorsturen van verkeer

1. Laat alle eindpunten.
2. Met behulp van één client, DNS-omzetting voor de domeinnaam van uw bedrijf met nslookup of een vergelijkbaar hulpprogramma aanvragen.
3. Zorg ervoor dat Hallo opgelost IP-adres overeenkomt met de primaire eindpunt Hallo.
4. Buiten uw primaire eindpunt of verwijder Hallo bestand bewaking zodat hij beschouwt Traffic Manager die toepassing hello niet actief is.
5. Wachten op Hallo DNS Time-to-Live (TTL) van Hallo Traffic Manager-profiel plus nog twee minuten zijn verstreken. Bijvoorbeeld, als uw DNS-TTL is 300 seconden (5 minuten), moet u wachten zeven minuten.
6. Uw DNS-client cache en aanvraag DNS-omzetting met nslookup leegmaken. In Windows kunt u uw DNS-cache met Hallo ipconfig/flushdns opdracht leegmaken.
7. Zorg ervoor dat Hallo opgelost IP-adres overeenkomt met uw secundaire eindpunt.
8. Herhaal hello, op zijn beurt omlaag elk eindpunt te brengen. Controleer of dat deze Hallo DNS Hallo IP-adres van de volgende eindpunt Hallo in Hallo lijst retourneert. Wanneer alle eindpunten niet beschikbaar zijn, moet u opnieuw Hallo IP-adres van de primaire eindpunt Hallo verkrijgen.

## <a name="how-tootest-hello-weighted-traffic-routing-method"></a>Hoe tootest hello verkeersrouteringsmethode gewogen

1. Laat alle eindpunten.
2. Met behulp van één client, DNS-omzetting voor de domeinnaam van uw bedrijf met nslookup of een vergelijkbaar hulpprogramma aanvragen.
3. Zorg ervoor dat Hallo opgelost IP-adres overeenkomt met een van de eindpunten.
4. Uw DNS-client-cache leegmaken en Herhaal stappen 2 en 3 voor elk eindpunt. Hier ziet u verschillende IP-adressen voor elk van uw eindpunten worden geretourneerd.

## <a name="how-tootest-hello-performance-traffic-routing-method"></a>Hoe tootest Hallo prestaties methode voor het doorsturen van verkeer

tooeffectively prestaties verkeersrouteringsmethode testen, moet u clients zich in verschillende onderdelen van Hallo wereld hebben. U kunt clients maken in verschillende Azure-regio's die gebruikt tootest worden kunnen uw services. Als u een wereldwijd netwerk hebt, kunt u op afstand tooclients in andere onderdelen van Hallo wereld aanmelden en uw tests van daaruit uitvoeren.

U kunt ook er zijn gratis, webgebaseerde DNS-zoekopdracht en kennis van de services die beschikbaar zijn. Sommige van deze hulpprogramma's kunt u de mogelijkheid toocheck DNS-naamomzetting vanaf verschillende locaties Hallo wereld Hallo. Voer een zoekopdracht op 'DNS-zoekopdracht' voor voorbeelden. De services van derden zoals Gomez of Keynote mag gebruikte tooconfirm dat de profielen van uw verkeer distribueert zoals verwacht.

## <a name="next-steps"></a>Volgende stappen

* [Over verkeersrouteringsmethoden voor Traffic Manager](traffic-manager-routing-methods.md)
* [Prestatieoverwegingen voor Traffic Manager](traffic-manager-performance-considerations.md)
* [Problemen met Traffic Manager in gedegradeerde status oplossen](traffic-manager-troubleshooting-degraded.md)
