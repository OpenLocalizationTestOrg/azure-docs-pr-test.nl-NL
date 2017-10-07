---
title: overzicht van de Load Balancer aaaAzure | Microsoft Docs
description: Overzicht van Azure Load Balancer-functies, architectuur en implementatie. Informatie over de werking van Hallo load balancer en in de cloud Hallo van maken.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 0f313dc0-f007-4cee-b2b9-f542357925a3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2376a02f7cbbbed6a90f216419c0c3d30f594272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-load-balancer-overview"></a>Overzicht van Azure Load Balancer

Azure Load Balancer biedt hoge beschikbaarheid en netwerkprestaties tooyour toepassingen. Het is een laag 4 (TCP, UDP) load balancer die binnenkomend verkeer over orde exemplaren van services gedefinieerd in een set met gelijke taakverdeling distribueert.

Azure Load Balancer kan worden geconfigureerd voor:

* Taakverdeling saldo binnenkomende Internet verkeer toovirtual machines. Deze configuratie wordt ook wel [internetgerichte taakverdeling](load-balancer-internet-overview.md).
* Load balance verkeer tussen virtuele machines in een virtueel netwerk, tussen virtuele machines in de cloud-services of tussen virtuele machines in een virtueel netwerk met cross-premises en lokale computers. Deze configuratie wordt ook wel [interne load balancing](load-balancer-internal-overview.md).
* Doorsturen externe verkeer tooa specifieke virtuele machine.

Alle resources in de cloud Hallo moeten een openbare IP-adres toobe bereikbaar is vanaf Internet Hallo. Hallo-cloudinfrastructuur in Azure maakt gebruik van niet-routeerbare IP-adressen voor de bronnen. Azure maakt gebruik van NAT (Netwerkadresomzetting) met openbare IP-adressen toocommunicate toohello Internet.

## <a name="azure-deployment-models"></a>Azure-implementatiemodellen

Het is belangrijk toounderstand Hallo verschillen tussen hello Azure classic en Resource Manager [implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md). Azure Load Balancer is anders geconfigureerd in elk model.

### <a name="azure-classic-deployment-model"></a>Azure klassieke implementatiemodel

Virtuele machines geïmplementeerd binnen de grens van een cloud-service kan worden gegroepeerd toouse een load balancer. In dit model is een openbaar IP-adres en een volledig gekwalificeerde domeinnaam, (FQDN) tooa-cloudservice zijn toegewezen. Hallo load balancer de vertaling van poort- en load Hallo-netwerkverkeer met behulp van Hallo openbaar IP-adres voor de cloudservice Hallo's.

Taakverdeling verkeer wordt gedefinieerd door de eindpunten. Poort vertaling eindpunten hebben een-op-een relatie tussen Hallo openbare poort Hallo openbaar IP-adres en de lokale poort Hallo toohello-service op een specifieke virtuele machine wordt toegewezen. Load balancing eindpunten hebben een een-op-veel-relatie tussen Hallo openbaar IP-adres en Hallo lokale poorten die zijn toegewezen toohello services op Hallo virtuele machines in het Hallo-cloudservice.

![Azure Load Balancer in het klassieke implementatiemodel Hallo](./media/load-balancer-overview/asm-lb.png)

Afbeelding 1: Azure Load Balancer in het klassieke implementatiemodel Hallo

Hallo domein het label voor het openbare IP-adres hello, dat Hallo load balancer wordt gebruikt voor dit implementatiemodel is \<cloudservicenaam\>. cloudapp.net. Hallo volgende afbeelding ziet u hello Azure Load Balancer in dit model.

### <a name="azure-resource-manager-deployment-model"></a>Azure Resource Manager-implementatiemodel

Hallo Resource Manager-implementatiemodel is er geen toocreate moet een cloudservice. Hallo load balancer wordt tooexplicitly routeverkeer over meerdere virtuele machines worden gemaakt.

Een openbaar IP-adres is een afzonderlijke resource met de domeinlabel van een (DNS-naam). Hallo openbaar IP-adres is gekoppeld aan Hallo load balancer-resource. Load balancer-regels en binnenkomende NAT-regels gebruiken Hallo openbaar IP-adres als de Internet-eindpunt voor Hallo-resources die zijn ontvangen netwerkverkeer taakverdeling Hallo.

Een persoonlijke of openbare IP-adres is toegewezen toohello network interface resource gekoppeld tooa virtuele machine. Nadat een netwerkinterface kan tooa load balancer backend-IP-adresgroep hebt toegevoegd, is Hallo load balancer kunnen toosend taakverdeling netwerkverkeer op basis van Hallo taakverdeling regels die zijn gemaakt.

Hallo ziet volgende afbeelding u hello Azure Load Balancer in dit model:

![Azure Load Balancer in Resource Manager](./media/load-balancer-overview/arm-lb.png)

Afbeelding 2: Azure Load Balancer in Resource Manager

Hallo load balancer kan worden beheerd via Resource Manager gebaseerde sjablonen, API's en hulpprogramma's. toolearn meer over Resource Manager, Zie Hallo [overzicht van Resource Manager](../azure-resource-manager/resource-group-overview.md).

## <a name="load-balancer-features"></a>Load Balancer-kenmerken

* Hash-distributiepunt

    Azure Load Balancer gebruikmaakt van een distributiepunt op basis van het hash-algoritme. Standaard wordt een 5-tuple hash bestaat uit de bron-IP, bronpoort, doel-IP, doelpoort en protocol type toomap verkeer tooavailable servers gebruikt. Het gebruikerspad alleen biedt *binnen* een transportsessie. Pakketten in Hallo dezelfde TCP of UDP-sessie worden omgeleid toohello dezelfde achter Hallo taakverdeling endpoint-instantie. Wanneer hello client wordt gesloten en opnieuw heeft geopend Hallo verbinding of een nieuwe sessie begint vanaf Hallo dezelfde bron-IP, Hallo wijzigingen in gegevensbron poort. Hierdoor kunnen Hallo verkeer toogo tooa ander eindpunt in een ander datacenter.

    Zie voor meer informatie [Load balancer-distributie modus](load-balancer-distribution-mode.md). Hallo toont volgende afbeelding Hallo op basis van het hash-distributie:

    ![Hash-distributiepunt](./media/load-balancer-overview/load-balancer-distribution.png)

    Afbeelding 3 - hash-gebaseerd distributiepunt

* Poort doorsturen

    Azure Load Balancer hebt die u meer controle over hoe binnenkomende communicatie wordt beheerd. Deze communicatie omvat het verkeer van Internet-hosts, virtuele machines in andere cloudservices of virtuele netwerken wordt geïnitialiseerd. Dit besturingselement wordt vertegenwoordigd door een eindpunt (ook wel een invoereindpunt).

    Een invoereindpunt luistert op een openbare poort en stuurt verkeer tooan interne poort. U kunt dezelfde voor een interne of externe eindpunt poorten Hallo toewijzen of een andere poort gebruiken voor deze. U kunt bijvoorbeeld een web server is geconfigureerd toolisten tooport 81 hebben terwijl Hallo openbaar eindpunt toewijzing poort 80 wordt. Hallo maken van een openbaar eindpunt activeert Hallo maken van een load balancer-exemplaar.

    Wanneer gemaakt met hello Azure-portal, maakt Hallo portal automatisch eindpunten toohello virtuele machine voor Hallo Remote Desktop Protocol (RDP) en externe verkeer voor Windows PowerShell-sessie. U kunt deze eindpunten tooremotely Hallo virtuele machine beheren via Hallo Internet.

* Automatische herconfiguratie

    Azure Load Balancer opnieuw onmiddellijk als u exemplaren omhoog of omlaag schalen. Bijvoorbeeld, deze herconfiguratie gebeurt er wanneer u verhogen Hallo aantal exemplaren voor web/worker rollen in een cloudservice of wanneer u aanvullende virtuele machines aan Hallo toevoegen dezelfde Netwerktaakverdeling instellen.

* Servicecontrole

    Azure Load Balancer kunt Hallo health Hallo WebTest verschillende exemplaren van de server. Wanneer een test toorespond mislukt stopt Hallo load balancer verzenden nieuwe verbindingen toohello slecht exemplaren. Bestaande verbindingen worden niet beïnvloed.

    Drie soorten tests worden ondersteund:

    + **Test van de Guest-agent (op Platform als een Service alleen virtuele Machines):** Hallo load balancer gebruikmaakt van de gastagent Hallo in Hallo virtuele machine. Hallo guest-agent luistert en reageert met een HTTP 200 OK antwoord alleen wanneer hello exemplaar is Hallo status ready heeft (dat wil zeggen Hallo-exemplaar is niet in een status zoals gebruik recycling of stoppen). Als Hallo agent toorespond met een HTTP 200 OK mislukt, Hallo Hallo load balancer aanhalingstekens exemplaar als niet-reagerende en stopt met het verzenden van verkeer toothat exemplaar. Hallo load balancer blijft tooping Hallo-exemplaar. Hallo guest-agent reageert met een HTTP 200, stuurt Hallo load balancer als verkeer toothat exemplaar opnieuw. Wanneer u een Webrol, wordt de websitecode van uw doorgaans in w3wp.exe die niet wordt bewaakt door hello Azure-infrastructuur of guest-agent uitgevoerd. Dit betekent dat fouten in w3wp.exe (bijv. HTTP 500-antwoorden) niet gemeld toohello guest-agent worden en Hallo load balancer niet tootake dat exemplaar buiten de draaihoek weet.
    + **Aangepaste HTTP-test:** deze test overschrijft Hallo standaard (gastagent)-test. U kunt deze toocreate uw eigen aangepaste regels toodetermine Hallo gezondheid van de rolinstantie Hallo. Hallo load balancer wordt regelmatig probe voor het eindpunt (elke 15 seconden, standaard). Hallo-exemplaar als toobe in rotatie beschouwd als deze met een TCP ACK of een HTTP 200 binnen Hallo time-outperiode (standaard 31 seconden reageert). Dit is handig voor het implementeren van uw eigen logica tooremove exemplaren van Hallo load balancer worden gedraaid. U kunt bijvoorbeeld Hallo exemplaar tooreturn de status van een niet-200 configureren als Hallo exemplaar hoger dan 90% CPU is. Voor web-functies die gebruikmaken van w3wp.exe, ook dat u automatische bewaking van uw website, omdat er fouten in de websitecode van uw een niet-200 statustest toohello retourneren.
    + **Aangepaste TCP-test:** deze test is afhankelijk van geslaagde TCP-sessie tot stand brengen van tooa gedefinieerd testpoort.

    Zie voor meer informatie, Hallo [LoadBalancerProbe schema](https://msdn.microsoft.com/library/azure/jj151530.aspx).

* Bron NAT

    Alle uitgaande verkeer toohello Internet dat afkomstig van uw service is ondergaat NAT (snat omzetten) de gegevensbron met behulp van dezelfde VIP-adres Hallo zoals Hallo binnenkomend verkeer. Snat omzetten biedt belangrijke voordelen:

    + Hiermee kunt eenvoudige upgrade en herstel na noodgevallen van services, aangezien Hallo die VIP kan dynamisch worden toegewezen tooanother exemplaar van Hallo-service.
    + Dit maakt het eenvoudiger toegangsbeheer toegangsbeheerlijst (ACL). ACL's die zijn uitgedrukt in termen van VIP's niet wijzigen als services schaal omhoog, omlaag of ophalen opnieuw geïmplementeerd.

    Hallo load balancer-configuratie ondersteunt volledige kegel NAT voor UDP. Volledige kegel NAT is een type NAT waar Hallo poort binnenkomende verbindingen vanaf elke externe host (in het antwoord tooan uitgaande aanvraag kunnen).

    Voor elke nieuwe uitgaande verbinding die een virtuele machine start, wordt ook een uitgaande poort toegewezen door Hallo load balancer. de externe host Hallo ziet verkeer met een virtueel IP-adres VIP toegewezen poort. Scenario's waarvoor een groot aantal uitgaande verbindingen, wordt aangeraden toouse [instantieniveau openbare IP-adres](../virtual-network/virtual-networks-instance-level-public-ip.md) adressen, zodat Hallo VM's een speciale uitgaande IP-adres voor snat omzetten hebben. Dit vermindert het risico van uitputting van de poort Hallo.

    Zie [uitgaande verbindingen](load-balancer-outbound-connections.md) artikel voor meer informatie over dit onderwerp.

### <a name="support-for-multiple-load-balanced-ip-addresses-for-virtual-machines"></a>Ondersteuning voor meerdere netwerktaakverdeling IP-adressen voor virtuele machines
U kunt meer dan één taakverdeling openbare IP-adres tooa set van virtuele machines toewijzen. Met deze mogelijkheid kunt u meerdere SSL-websites en/of meerdere SQL Server AlwaysOn-beschikbaarheidsgroep-listeners op Hallo dezelfde van virtuele machines set hosten. Zie voor meer informatie [meerdere VIP's per cloudservice](load-balancer-multivip.md).

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="limitations"></a>Beperkingen

Load Balancer back-endpools kunnen VM-SKU behalve basisstaffel bevatten.

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [internetgerichte load balancer](load-balancer-internet-overview.md)

- Meer informatie over [interne load balancer-overzicht](load-balancer-internal-overview.md)

- Maak een [internetgerichte load balancer](load-balancer-get-started-internet-portal.md)

- Meer informatie over een aantal Hallo andere sleutel [netwerkmogelijkheden](../networking/networking-overview.md) van Azure

