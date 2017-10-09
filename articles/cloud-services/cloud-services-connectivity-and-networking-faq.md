---
title: problemen met aaaConnectivity en netwerken voor veelgestelde vragen over Microsoft Azure Cloud Services | Microsoft Docs
description: Dit artikel worden Hallo Veelgestelde vragen over de connectiviteit en netwerken voor Microsoft Azure Cloud Services.
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: e725dbbf585a76807362c59299d0a31f511afd3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connectivity-and-networking-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemen met de netwerken en voor Azure Cloud Services: veelgestelde vragen (FAQ's)

Dit artikel bevat veelgestelde vragen over problemen met de netwerken en voor [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services). U kunt ook contact opnemen met Hallo [VM-grootte voor Cloud Services-pagina](cloud-services-sizes-specs.md) voor informatie over de grootte.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Ik kan niet worden gereserveerd een IP-adres in een cloudservice meerdere VIP 's
Controleer eerst of de instantie van die Hallo-virtuele machine die u probeert tooreserve Hallo IP voor is ingeschakeld. Controleer vervolgens of dat u gereserveerde IP-adressen voor beide Hallo fasering en productie-implementaties. **Geen** Hallo-instellingen niet wijzigen terwijl het Hallo-implementatie worden geüpgraded.

## <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Hoe kan ik extern bureaublad wanneer ik een NSG hebben?
Voeg regels toohello NSG waarmee verkeer op poorten **3389** en **20000**.  Extern bureaublad maakt gebruik van poort **3389**.  Cloud Service-exemplaren worden verdeeld, zodat u niet rechtstreeks welke tooconnect exemplaar om te controleren.  Hallo *RemoteForwarder* en *RemoteAccess* agents beheren van RDP-verkeer en Hallo client toosend een RDP-cookie toestaan en opgeven van een afzonderlijke instantie tooconnect aan.  Hallo *RemoteForwarder* en *RemoteAccess* agents vereisen die poort **20000** worden geopend die worden geblokkeerd als er een NSG.

## <a name="can-i-ping-a-cloud-service"></a>Kan ik een cloudservice pingen?

Nee, niet via Hallo normaal 'pingen' / ICMP-protocol. Hallo ICMP-protocol is niet toegestaan via hello Azure load balancer.

tootest connectiviteit, wordt aangeraden pingen poort te doen. Terwijl Ping.exe ICMP gebruikt, kunnen u andere hulpprogramma's, zoals psping om Nmap en telnet tootest connectiviteit tooa bepaalde TCP-poort.

Zie voor meer informatie [poort pings gebruiken in plaats van ICMP-tootest Azure VM-connectiviteit](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/).

## <a name="how-do-i-prevent-receiving-thousands-of-hits-from-unknown-ip-addresses-that-indicate-some-sort-of-malicious-attack-toohello-cloud-service"></a>Hoe voorkom ik dat ontvangst duizenden treffers van onbekende IP-adressen die wijzen op enige vorm van kwaadaardige aanvallen toohello cloudservice?
Azure implementeert een gelaagde network security tooprotect platformservices tegen aanvallen van gedistribueerde denial-of-service (DDoS). Hello Azure DDoS verdediging system is onderdeel van Azure continue bewaking die voortdurend wordt verbeterd via het binnendringen testen. Dit systeem DDoS-bescherming is ontworpen toowithstand aanvallen niet alleen uit Hallo buiten, maar ook op andere Azure-tenants. Zie voor meer details [Microsoft Azure Network Security](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf).

U kunt een blok met starten van de taak tooselectively ook enkele specifieke IP-adressen maken. Zie voor meer informatie [blokkeren van een specifiek IP-adres](cloud-services-startup-tasks-common.md#block-a-specific-ip-address).

## <a name="when-i-try-toordp-toomy-cloud-service-instance-i-get-hello-message-hello-user-account-has-expired"></a>Wanneer ik probeer tooRDP toomy cloud service-exemplaar, ophalen van het Hallo-bericht, "Hallo-gebruikersaccount is verlopen."
Krijgt u mogelijk Hallo foutbericht 'dit gebruikersaccount is verlopen' wanneer u een bypass hebt Hallo vervaldatum die is geconfigureerd in uw RDP-instellingen. Kunt u de vervaldatum Hallo van Hallo portal met de volgende stappen:
1. Aanmelden toohello Azure Management Console (https://manage.windowsazure.com), gaat u tooyour cloudservice en selecteer Hallo **configureren** tabblad.
2. Selecteer **externe**.
3. Wijzigen van de datum 'Verloopt op' hello en vervolgens opslaan Hallo-configuratie.

Nu moet u kunnen tooRDP tooyour machine.

## <a name="why-is-loadbalancer-not-balancing-traffic-equally"></a>Waarom is Load Balancer niet balancing verkeer gelijkmatig?
Zie voor meer informatie over hoe interne load balancer werkt [Azure Load Balancer nieuwe distributie modus](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/).

Hallo distributie algoritme is een 5-tuple (bron-IP, bronpoort, doel-IP, doelpoort protocoltype) hash-toomap verkeer tooavailable servers. Het biedt gebruikerspad alleen een transportsessie. Pakketten in Hallo dezelfde TCP of UDP-sessie worden omgeleid toohello dezelfde datacenter IP (DIP) achter Hallo taakverdeling endpoint-instantie. Wanneer Hallo van client wordt gesloten en opnieuw opent Hallo verbinding of een nieuwe sessie begint vanaf Hallo dezelfde bron-IP, bronpoort Hallo wijzigingen en zorgt ervoor dat Hallo verkeer toogo tooa ander DIP eindpunt.
