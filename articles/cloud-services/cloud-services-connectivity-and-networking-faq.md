---
title: Problemen met de netwerken en voor veelgestelde vragen over Microsoft Azure Cloud Services | Microsoft Docs
description: Dit artikel worden de veelgestelde vragen over de connectiviteit en netwerken voor Microsoft Azure Cloud Services.
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
ms.openlocfilehash: 55d5b692930e273af29c3de9d2b96b6d012b3415
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connectivity-and-networking-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemen met de netwerken en voor Azure Cloud Services: veelgestelde vragen (FAQ's)

Dit artikel bevat veelgestelde vragen over problemen met de netwerken en voor [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services). U kunt ook raadpleegt u de [VM-grootte voor Cloud Services-pagina](cloud-services-sizes-specs.md) voor informatie over de grootte.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Ik kan niet worden gereserveerd een IP-adres in een cloudservice meerdere VIP 's
Controleer eerst of de instantie van de virtuele machine die u probeert te reserveren van de IP voor is ingeschakeld. Controleer vervolgens of dat u gereserveerde IP's voor het Faseren en de productie-implementaties gebruikt. **Geen** de instellingen niet wijzigen terwijl het upgraden van de implementatie.

## <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Hoe kan ik extern bureaublad wanneer ik een NSG hebben?
Regels toevoegen aan het NSG waarmee verkeer op poorten **3389** en **20000**.  Extern bureaublad maakt gebruik van poort **3389**.  Cloud Service-exemplaren worden verdeeld, zodat u direct welk exemplaar verbinding maken met kan niet bepalen.  De *RemoteForwarder* en *RemoteAccess* agents RDP-verkeer te beheren en dat de client verzenden van een cookie RDP en geeft u een afzonderlijk exemplaar verbinding maken met.  De *RemoteForwarder* en *RemoteAccess* agents vereisen die poort **20000** worden geopend die worden geblokkeerd als er een NSG.

## <a name="can-i-ping-a-cloud-service"></a>Kan ik een cloudservice pingen?

Nee, niet met behulp van de normale 'pingen' / ICMP-protocol. Het ICMP-protocol is niet toegestaan via de Azure load balancer.

Connectiviteit testen raden we u een poortping. Terwijl Ping.exe ICMP gebruikt, wordt er andere hulpprogramma's, zoals psping om Nmap en telnet kunnen u voor het testen van verbinding met een specifieke TCP-poort.

Zie voor meer informatie [poort pings gebruiken in plaats van ICMP Azure VM-connectiviteit testen](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/).

## <a name="how-do-i-prevent-receiving-thousands-of-hits-from-unknown-ip-addresses-that-indicate-some-sort-of-malicious-attack-to-the-cloud-service"></a>Hoe voorkom ik dat ontvangst duizenden treffers van onbekende IP-adressen die wijzen op enige vorm van kwaadaardige aanvallen met de cloudservice?
Azure implementeert een gelaagde netwerkbeveiliging om te beschermen tegen aanvallen van gedistribueerde denial-of-service (DDoS) de platform-services. Het systeem Azure DDoS-beveiliging is onderdeel van Azure continue bewaking die voortdurend wordt verbeterd via het binnendringen testen. Dit systeem DDoS-bescherming is ontworpen om niet alleen aanvallen van buitenaf, maar ook van andere tenants Azure tolereren. Zie voor meer details [Microsoft Azure Network Security](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf).

U kunt ook een starten van de taak voor het selectief blokkeren enkele specifieke IP-adressen maken. Zie voor meer informatie [blokkeren van een specifiek IP-adres](cloud-services-startup-tasks-common.md#block-a-specific-ip-address).

## <a name="when-i-try-to-rdp-to-my-cloud-service-instance-i-get-the-message-the-user-account-has-expired"></a>Wanneer ik wil voor RDP mijn cloud service-exemplaar, het bericht wordt weergegeven, "de gebruikersaccount is verlopen."
Mogelijk dat u de foutmelding 'dit gebruikersaccount is verlopen' wanneer u de vervaldatum die is geconfigureerd in uw RDP-instellingen overslaan. U kunt de vervaldatum wijzigen via de portal met de volgende stappen:
1. Aanmelden bij de Azure Management Console (https://manage.windowsazure.com), gaat u naar de cloudservice en selecteer de **configureren** tabblad.
2. Selecteer **externe**.
3. De datum 'Verloopt op' wijzigen en vervolgens de configuratie op te slaan.

Nu moet u kunnen voor RDP naar uw computer.

## <a name="why-is-loadbalancer-not-balancing-traffic-equally"></a>Waarom is Load Balancer niet balancing verkeer gelijkmatig?
Zie voor meer informatie over hoe interne load balancer werkt [Azure Load Balancer nieuwe distributie modus](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/).

De verdeling algoritme is een 5-tuple (bron-IP, bronpoort, doel-IP, doelpoort protocoltype) hash verkeer toewijzen aan beschikbare servers. Het biedt gebruikerspad alleen een transportsessie. Pakketten in dezelfde TCP of UDP-sessie wordt omgeleid naar hetzelfde datacenter IP (DIP) exemplaar achter het eindpunt van de taakverdeling. Wanneer de client wordt gesloten en opnieuw de verbinding wordt geopend, of een nieuwe sessie vanaf dezelfde bron-IP begint, wordt de bronpoort wijzigt en zorgt ervoor dat het verkeer naar een ander DIP-eindpunt.
