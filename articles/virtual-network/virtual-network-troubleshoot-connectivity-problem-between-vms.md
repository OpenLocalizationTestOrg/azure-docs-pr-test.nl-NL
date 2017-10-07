---
title: problemen met de netwerkconnectiviteit tussen Azure Virtual machines aaaTroubleshooting | Microsoft Docs
description: Meer informatie over hoe tooTroubleshoot Hallo problemen met de netwerkconnectiviteit tussen Azure VM's.
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a>Het oplossen van problemen met de netwerkconnectiviteit tussen Azure VM 's

Er kunnen problemen met de netwerkconnectiviteit tussen Azure VM's. In dit artikel voor probleemoplossing stappen toohelp vindt u dit probleem oplossen. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a>Symptoom

Een virtuele machine van Azure kan geen verbinding tooanother Azure VM.

## <a name="troubleshooting-guidance"></a>Hulp bij het oplossen van problemen 

1. [Controleer als NIC is onjuist geconfigureerd](#step-1-check-if-nic-is-misconfigured)
2. [Als het netwerkverkeer wordt geblokkeerd door NSG of UDR controleren](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [Controleer als netwerkverkeer wordt geblokkeerd door VM-firewall](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [Controleer of VM-app of service op poort Hallo luistert](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [Controleer of de Hallo probleem wordt veroorzaakt door snat omzetten](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [Controleer of het verkeer wordt geblokkeerd door de ACL's voor Hallo klassieke VM](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [Controleer of het Hallo-eindpunt is gemaakt voor Hallo klassieke VM](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [Kan geen tooconnect tooa VM-netwerkshare](#step-8-unable-to-connect-to-a-vm-network-share)
9. [Inter Vnet-connectiviteit](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a>Stappen voor probleemoplossing

Volg deze stappen tootroubleshoot Hallo probleem. Controleer of het Hallo-probleem opgelost na elke stap is. 

### <a name="step-1-check-if-nic-is-misconfigured"></a>Stap 1: Controleer of NIC is onjuist geconfigureerd

Ga als volgt [hoe tooreset netwerkinterface voor virtuele machine van Windows Azure](../virtual-machines/windows/reset-network-interface.md). 

Als Hallo probleem optreedt nadat u de netwerkinterface hello (NIC) wijzigen, voert u de volgende stappen uit:

**Virtuele machines mulit-NIC**

1. Toevoegen van een NIC.
2. Hallo-problemen oplossen in Hallo onjuiste NIC of Verwijder ongeldige NIC.  Vervolgens readd Hallo NIC.

Zie voor meer informatie [toevoegen network interfaces tooor verwijderen van virtuele machines](virtual-network-network-interface-vm.md).

**Één NIC VM** 

- [Implementeer Windows VM opnieuw](../virtual-machines/windows/redeploy-to-new-node.md)
- [Virtuele Linux-machine implementeren](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a>Stap 2: Controleer of het netwerkverkeer wordt geblokkeerd door NSG of UDR

Gebruikmaken van [netwerk-Watcher IP-stroom controleren](../network-watcher/network-watcher-ip-flow-verify-overview.md) en [NSG stroom logboekregistratie](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify als er een Netwerkbeveiligingsgroep of door de gebruiker gedefinieerde Route die netwerkverkeer verstoort.

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a>Stap 3: Controleren als netwerkverkeer wordt geblokkeerd door VM-firewall

Hallo firewall uitschakelen en test Hallo resultaat. Als het Hallo-probleem is opgelost, Hallo-instellingen in de firewall Hallo valideren en opnieuw inschakelen.

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a>Stap 4: Controleren of VM-app of service op poort Hallo luistert

U kunt een van de volgende methoden toocheck of VM-toepassing of Service op poort Hallo luistert Hallo

- Hallo opdrachten toocheck te volgen of Hallo server op deze poort luistert worden uitgevoerd.

**Windows-VM**

    netstat –ano

**Linux-VM**

    netstat -l

- Voer Hallo **Telnet** opdracht op Hallo VM tooitself tootest Hallo poort. Hallo-test niet slaagt, is toepassing of service niet als geconfigureerde toolisten op Hallo-poort.

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a>Stap 5: Controleren of Hallo probleem wordt veroorzaakt door snat omzetten

In sommige scenario's, hello VM geplaatst achter een Load balance oplossing met een afhankelijkheid op resources buiten Azure. In deze scenario's, als u met de verbinding problemen, Hallo probleem kan worden veroorzaakt door [snat omzetten poort bronuitputting](../load-balancer/load-balancer-outbound-connections.md). tooresolve hello probleem, een VIP (of ILPIP voor klassieke) voor elke VM die achter Hallo Load balancer maken en beveiligen met NSG of ACL. 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a>Stap 6: Controleer of het verkeer wordt geblokkeerd door de ACL's voor Hallo klassieke VM

Een ACL biedt Hallo mogelijkheid tooselectively toestaan of weigeren van verkeer voor het eindpunt van een virtuele machine. Zie voor meer informatie [beheren Hallo ACL op een eindpunt](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a>Stap 7: Controleer of het Hallo-eindpunt is gemaakt voor Hallo klassieke VM

Alle virtuele machines die u maakt in Azure met behulp van het klassieke implementatiemodel Hallo kunnen automatisch communiceren via een particulier netwerkkanaal met andere virtuele machines in Hallo dat dezelfde cloud service- of virtuele netwerk. Computers met andere virtuele netwerken vereisen echter eindpunten toodirect Hallo netwerk binnenkomend verkeer tooa virtuele machine. Zie voor meer informatie [hoe tooset eindpunten](../virtual-machines/windows/classic/setup-endpoints.md).

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a>Stap 8: Kan geen tooconnect tooa VM-netwerkshare

Als u tooconnect tooa VM netwerkshare bevindt, kan Hallo probleem worden veroorzaakt door niet beschikbaar NIC's in Hallo VM. toodelete Hallo niet beschikbaar NIC's, Zie [hoe toodelete Hallo niet beschikbaar NIC's](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)

### <a name="step-9-inter-vnet-connectivity"></a>Stap 9: Inter Vnet-connectiviteit

Gebruikmaken van [netwerk-Watcher IP-stroom controleren](../network-watcher/network-watcher-ip-flow-verify-overview.md) en [NSG stroom logboekregistratie](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify als er een Netwerkbeveiligingsgroep of door de gebruiker gedefinieerde Route die netwerkverkeer verstoort. U kunt ook uw Inter Vnet-configuratie valideren [hier](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).

### <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.
Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget uw probleem snel worden opgelost.
