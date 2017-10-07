---
title: aaaLoad Balancer aangepaste tests en bewaking gezondheidsstatus | Microsoft Docs
description: Meer informatie over hoe toouse aangepaste tests voor exemplaren van Azure Load Balancer toomonitor achter de Load Balancer
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 46b152c5-6a27-4bfc-bea3-05de9ce06a57
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3dfcfcd2d5cffa58b160cb38d63acffbd997d452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-load-balancer-probes"></a>Load Balancer-testen

Azure Load Balancer biedt Hallo mogelijkheid toomonitor Hallo status van exemplaren van de server met behulp van de tests. Wanneer een test toorespond mislukt stopt Load Balancer nieuwe verbindingen toohello slecht exemplaar verzenden. Hallo bestaande verbindingen worden niet beïnvloed en nieuwe verbindingen toohealthy exemplaren worden verzonden.

Guest agent cloud service-rollen (werkrollen en webrollen) gebruiken voor het bewaken van de test. Aangepaste TCP- of HTTP-tests moeten worden geconfigureerd wanneer u virtuele machines achter de Load Balancer gebruiken.

## <a name="understand-probe-count-and-timeout"></a>Aantal van de test- en time begrijpen

Afhankelijk van het gedrag van de test:

* Hallo aantal geslaagde tests die een exemplaar toobe gelabeld als bedrijfs toestaan.
* Hallo aantal mislukte tests die ertoe leiden een exemplaar toobe gelabeld als omlaag dat.

Hallo-waarde voor time-outs en frequentie instellen in SuccessFailCount bepalen of een exemplaar bevestigde toobe uitgevoerd of niet actief is. In hello Azure-portal, Hallo time-out tootwo keren Hallo waarde van Hallo frequentie ingesteld.

Hallo test de configuratie van alle exemplaren van de taakverdeling voor een eindpunt (dat wil zeggen, een set taakverdeling) moet Hallo dezelfde. Dit betekent dat er geen een andere test-configuratie voor elke rolinstantie of de virtuele machine in Hallo dezelfde gehoste service voor de combinatie van een bepaald eindpunt. Elk exemplaar moet bijvoorbeeld identieke lokale poorten en time-outs.

> [!IMPORTANT]
> Hallo IP-adres 168.63.129.16 maakt gebruik van een Load Balancer-test. Dit openbare IP-adres vergemakkelijkt de communicatie toointernal platform resources voor Hallo bring-your-eigenaar-IP-scenario Azure Virtual Network. Hallo virtuele openbare IP-adres 168.63.129.16 wordt gebruikt in alle regio's en wordt niet gewijzigd. We raden u aan dit IP-adres in een lokale firewall-beleid. Deze mogen niet worden beschouwd als een beveiligingsrisico omdat er een bericht van dat adres kan als bron worden alleen Hallo interne Azure-platform. Als u dit doet, zullen er onverwacht gedrag in verschillende scenario's zoals het configureren van Hallo hetzelfde IP-adresbereik van 168.63.129.16 en IP-adressen die worden gedupliceerd.

## <a name="learn-about-hello-types-of-probes"></a>Meer informatie over Hallo typen tests

### <a name="guest-agent-probe"></a>Test voor gast-agent

Deze test is alleen beschikbaar voor Azure Cloud Services. Load Balancer gebruikmaakt van de gastagent Hallo in Hallo virtuele machine, en vervolgens luistert en reageert met een HTTP 200 OK antwoord alleen wanneer hello exemplaar is Hallo status Ready heeft (dat wil zeggen, niet in een andere status zoals bezet, Recycling of stoppen).

Zie voor meer informatie [configureren Hallo servicedefinitiebestand (csdef) voor statuscontroles](https://msdn.microsoft.com/library/azure/ee758710.aspx) of [maken van een Internet gerichte load balancer voor cloudservices aan de slag](load-balancer-get-started-internet-classic-cloud.md#check-load-balancer-health-status-for-cloud-services).

### <a name="what-makes-a-guest-agent-probe-mark-an-instance-as-unhealthy"></a>Een test voor gast-agent is een exemplaar als beschadigd gemarkeerd is?

Als Hallo guest-agent toorespond met HTTP 200 OK mislukt, Hallo Hallo load balancer aanhalingstekens exemplaar als niet-reagerende en stopt met het verzenden van verkeer toothat exemplaar. Hallo load balancer blijft tooping Hallo-exemplaar. Als Hallo guest-agent met een HTTP 200 reageert, verzendt Hallo load balancer verkeer toothat exemplaar opnieuw.

Wanneer u een Webrol gebruikt, wordt Hallo websitecode gewoonlijk wordt uitgevoerd in w3wp.exe die niet wordt bewaakt door hello Azure-infrastructuur of guest-agent. Dit betekent dat fouten in w3wp.exe (bijvoorbeeld HTTP 500-antwoorden) niet gemeld toohello guest-agent worden en Hallo load balancer niet in werking te dat exemplaar buiten de draaihoek laten.

### <a name="http-custom-probe"></a>Aangepaste HTTP-test

aangepaste HTTP-Load Balancer-test Hallo overschrijft Hallo standaard guest agent test, wat betekent dat u uw eigen aangepaste regels toodetermine Hallo gezondheid van de rolinstantie Hallo kunt maken. Hallo load balancer-tests uw eindpunt elke 15 seconden standaard. Hallo-exemplaar als toobe in Hallo load balancer rotatie beschouwd als deze met een HTTP 200 binnen Hallo time-outperiode (31 seconden standaard reageert).

Dit is handig als u uw eigen logica tooremove exemplaren van de load balancer rotatie tooimplement wilt. U kan bijvoorbeeld tooremove een exemplaar besluit als deze hoger dan 90% CPU is en een niet-200 opgevraagd. Als u web-functies die er gebruik van w3wp.exe hebt, betekent dit ook dat krijgt u automatische bewaking van uw website, omdat er fouten in uw websitecode retourneert een niet-200 status toohello load balancer-test.

> [!NOTE]
> aangepaste HTTP-test Hallo ondersteunt relatieve paden en HTTP-protocol. HTTPS wordt niet ondersteund.

### <a name="what-makes-an-http-custom-probe-mark-an-instance-as-unhealthy"></a>Een aangepaste HTTP-test een exemplaar als beschadigd gemarkeerd is?

* HTTP-toepassing Hello retourneert een HTTP-antwoordcode dan 200 (bijvoorbeeld 403, 404 of 500). Dit is een positieve bevestiging die toepassing hello exemplaar moet worden uitgevoerd buiten de service meteen.
* Hallo HTTP-server reageert niet op alle na het Hallo-time-outperiode. Afhankelijk van Hallo time-outwaarde die is ingesteld, kan dit betekenen dat meerdere test Ga voordat Hallo test opgehaald gemarkeerd als niet wordt uitgevoerd met openstaande aanvragen (dat wil zeggen, voordat SuccessFailCount tests worden verzonden).
* Hallo server sluit Hallo verbinding via een TCP-reset.

### <a name="tcp-custom-probe"></a>Aangepaste TCP-test

Een verbinding starten TCP tests door het uitvoeren van een handshake drie richtingen met poort Hallo gedefinieerd.

### <a name="what-makes-a-tcp-custom-probe-mark-an-instance-as-unhealthy"></a>Een aangepaste TCP-test een exemplaar als beschadigd gemarkeerd is?

* Hallo TCP-server reageert niet op alle na het Hallo-time-outperiode. Wanneer de test Hallo is gemarkeerd als niet actief is afhankelijk van het aantal mislukte test Hallo aanvragen die zijn geconfigureerd toogo openstaande voordat u markeert Hallo test niet uitgevoerd.
* Hallo test ontvangt een opnieuw instellen van de rolinstantie Hallo TCP.

Zie voor meer informatie over het configureren van de statuscontrole van een HTTP- of een TCP-controle [een internetgerichte load balancer maken in Resource Manager, met behulp van PowerShell](load-balancer-get-started-internet-arm-ps.md).

## <a name="add-healthy-instances-back-into-load-balancer-rotation"></a>In orde exemplaren weer in de load balancer rotatie toevoegen

TCP- en HTTP-tests worden beschouwd als in orde en markeren Hallo rolinstantie als in orde wanneer:

* Hallo load balancer opgehaald uit een positief test Hallo eerste tijd Hallo die VM wordt opgestart.
* Hallo getal SuccessFailCount (zoals eerder beschreven) definieert Hallo-waarde van geslaagde tests die vereist toomark hello rolinstantie als in orde zijn. Als een rolinstantie werd verwijderd, moet Hallo aantal geslaagd, opeenvolgende tests gelijk zijn aan of groter zijn dan de waarde Hallo van SuccessFailCount toomark hello rolinstantie als die wordt uitgevoerd.

> [!NOTE]
> Als Hallo status van een rolinstantie is veranderen, wordt Hallo load balancer meer wacht voordat u Hallo rolinstantie terug in Hallo foutloze toestand bevindt. Dit wordt gedaan via beleid tooprotect Hallo gebruiker en het Hallo-infrastructuur.

## <a name="use-log-analytics-for-load-balancer"></a>Log analytics gebruiken voor de Load Balancer

U kunt [analytics aanmelden voor de Load Balancer](load-balancer-monitor-log.md) toocheck op Hallo test health-status en test count. Logboekregistratie kan worden gebruikt met Power BI of Azure Operational Insights tooprovide statistieken over de status van de Load Balancer.
