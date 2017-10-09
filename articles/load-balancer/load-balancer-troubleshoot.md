---
title: Azure Load Balancer aaaTroubleshoot | Microsoft Docs
description: Bekende problemen oplossen met Azure Load Balancer
services: load-balancer
documentationcenter: na
author: RamanDhillon
manager: timlt
editor: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/10/2017
ms.author: kumud
ms.openlocfilehash: 56b73fcbf0bbf18cedfd113a280cfafa2a3dc9f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-load-balancer"></a>Azure Load Balancer oplossen

Deze pagina bevat informatie over probleemoplossing voor veelgestelde vragen voor Azure Load Balancer. Wanneer het Hallo-connectiviteit taakverdeler niet beschikbaar is, zijn de meest voorkomende problemen Hallo als volgt: 
- Virtuele machines achter de Load Balancer niet reageren toohealth tests Hallo 
- Virtuele machines achter Hallo Load Balancer reageert niet toohello verkeer op poort Hallo geconfigureerd

## <a name="symptom-vms-behind-hello-load-balancer-are-not-responding-toohealth-probes"></a>Symptoom: VM's achter de Load Balancer niet reageren toohealth tests Hallo
Hallo back-end servers tooparticipate in Hallo load balancer-set, moeten ze Hallo test selectievakje doorgeeft. Zie voor meer informatie over statuscontroles [Understanding Load Balancer-tests](load-balancer-custom-probe-overview.md). 

Hallo Load Balancer back-endpool virtuele machines reageert mogelijk niet toohello tests vanwege tooany Hallo volgende redenen: 
- Back-endpool VM voor Load Balancer is slecht 
- Load Balancer back-endpool die VM wordt niet geluisterd op Hallo testpoort 
- Firewall of een netwerkbeveiligingsgroep blokkeert Hallo-poort op Hallo back-endpool van de Load Balancer virtuele machines 
- Overige configuratiefouten in de Load Balancer

### <a name="cause-1-load-balancer-backend-pool-vm-is-unhealthy"></a>1 oorzaak: De back-endpool van de Load Balancer VM is slecht 

**Validatie en oplossing**

tooresolve dit probleem aanmelden toohello deel van de virtuele machines en controleer of de Hallo VM-status in orde, en te kunnen reageren**psping om** of **TCPing** uit een andere virtuele machine in Hallo van toepassingen. Als Hallo VM beschadigd is of kan geen toorespond toohello test, moet u Hallo probleem corrigeren en Hallo VM back-status in orde tooa voordat deze kan deelnemen aan de load balancer ophalen.

### <a name="cause-2-load-balancer-backend-pool-vm-is-not-listening-on-hello-probe-port"></a>Oorzaak 2: Back-endpool van de Load Balancer VM wordt niet geluisterd op Hallo testpoort
Als Hallo VM in orde is, maar toohello test niet reageert, kan vervolgens een mogelijke reden zijn dat Hallo testpoort is niet geopend op Hallo deelnemende VM of Hallo VM niet geluisterd op poort.

**Validatie en oplossing**

1. Meld u bij de back-end voor toohello VM. 
2. Open een opdrachtprompt en Voer Hallo opdracht toovalidate er is een toepassing die luistert op Hallo testpoort te volgen:   
            netstat - an
3. Als de poortstatus Hallo wordt niet vermeld als **LISTENING**, de juiste poort Hallo configureren. 
4. Selecteer een andere poort, die wordt vermeld als **LISTENING**, en bij te werken load balancer-configuratie dienovereenkomstig.              

###<a name="cause-3-firewall-or-a-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vms"></a>3 oorzaak: Firewall of een netwerkbeveiligingsgroep blokkeert Hallo-poort op de back-endpool voor load balancer Hallo virtuele machines  
Als Hallo-firewall op Hallo die VM blokkeert Hallo testpoort of een of meer netwerkbeveiligingsgroepen geconfigureerd op Hallo subnet of op Hallo VM, niet Hallo test tooreach Hallo poort toestaat is, is het Hallo VM niet kan toorespond toohello health test.          

**Validatie en oplossing**

* Als Hallo-firewall is ingeschakeld, controleert u of dit is geconfigureerd tooallow Hallo testpoort. Als dit niet het geval is, Hallo firewall tooallow verkeer op Hallo testpoort configureren en test opnieuw. 
* In de lijst Hallo van netwerkbeveiligingsgroepen, Controleer of de Hallo binnenkomende of uitgaande verkeer op Hallo testpoort storing. 
* Controleer ook als een **weigeren alle** netwerkbeveiligingsgroepen-regel op Hallo NIC Hallo VM of subnet op dat een hogere prioriteit dan Hallo standaardregel waarmee LB tests & verkeer Hallo (netwerkbeveiligingsgroepen moeten toestaan Load Balancer IP-adres van 168.63.129.16). 
* Als een van deze regels Hallo test-verkeer blokkeert zijn, verwijderen en opnieuw configureren Hallo regels tooallow Hallo test verkeer.  
* Test Hallo VM is nu gestart toohello statuscontroles reageert. 

### <a name="cause-4-other-misconfigurations-in-load-balancer"></a>4 oorzaak: Andere configuratiefouten in de Load Balancer
Als alle Hallo lijken voorgaande oorzaken toobe gevalideerd en de juiste manier omgezet en Hallo backend VM nog steeds niet reageren toohello health test, en vervolgens handmatig test de verbinding, en sommige traceringen toounderstand Hallo connectiviteit verzamelen.

**Validatie en oplossing**

* Gebruik **psping om** uit een Hallo Hallo andere virtuele machines binnen VNet tootest Hallo test poort antwoord (voorbeeld:.\psping.exe -t 10.0.0.4:3389) en noteer de resultaten. 
* Gebruik **TCPing** uit een Hallo Hallo andere virtuele machines binnen VNet tootest Hallo test poort antwoord (voorbeeld:.\tcping.exe 10.0.0.4 3389) en noteer de resultaten. 
* Als er geen reactie wordt ontvangen in de deze ping-tests vervolgens
    - Voer een gelijktijdige Netsh trace op Hallo doel back-endpool VM en een andere virtuele testmachine van Hallo dezelfde VNet. Nu, voert u een test psping om enige tijd, sommige netwerktracering verzamelen en vervolgens stoppen van de Hallo test. 
    - Hallo netwerkopname analyseren en zien of er zowel binnenkomende en uitgaande pakketten gerelateerde toohello ping-query zijn. 
        - Als geen inkomende pakketten worden waargenomen op Hallo back-endpool VM, is er mogelijk een netwerkbeveiligingsgroepen of UDR onjuiste configuratie blokkerende Hallo-verkeer. 
        - Als er geen uitgaande pakketten worden waargenomen op Hallo back-endpool VM, moet Hallo VM toobe gecontroleerd op niet-verwante problemen (voor eample, toepassing blokkerende Hallo testpoort). 
    - Controleer of als Hallo testpakketten geforceerde tooanother bestemming (mogelijk via instellingen UDR) worden alvorens Hallo load balancer. Dit kan Hallo verkeer toonever reach Hallo backend VM veroorzaken. 
* Hallo test type (bijvoorbeeld HTTP tooTCP) wijzigen en het configureren van de bijbehorende poort Hallo in netwerkbeveiligingsgroepen ACL's en firewall toovalidate als Hallo probleem met de Hallo configuratie van de test-antwoord is. Zie voor meer informatie over de configuratie van health test [configuratie van health test eindpunt Load Balancing](https://blogs.msdn.microsoft.com/mast/2016/01/26/endpoint-load-balancing-heath-probe-configuration-details/).

## <a name="symptom-vms-behind-load-balancer-are-not-responding-tootraffic-on-hello-configured-data-port"></a>Symptoom: VM's achter de Load Balancer niet reageren tootraffic op Hallo geconfigureerd gegevenspoort

Als een back-endpool VM wordt vermeld als goed en toohello statuscontroles reageert, maar is nog steeds geen deelnemer in Hallo Load Balancing of toohello gegevensverkeer niet reageert, kan dit worden veroorzaakt door tooany Hallo volgende redenen: 
* Load Balancer-back-endpool die VM niet geluisterd op poort Hallo 
* Netwerkbeveiligingsgroep blokkeert Hallo-poort op Hallo back-endpool van de Load Balancer VM  
* Toegang tot Hallo Hallo Load Balancer van hetzelfde VM- en NIC 
* Toegang tot Internet Load Balancer-VIP Hallo vanaf Hallo deel van de back-endpool van de Load Balancer VM 

### <a name="cause-1-load-balancer-backend-pool-vm-is-not-listening-on-hello-data-port"></a>1 oorzaak: Back-endpool van de Load Balancer VM niet geluisterd op poort Hallo 
Als een virtuele machine toohello gegevensverkeer niet reageert, mogelijk het omdat Hallo doelpoort is niet geopend op Hallo deel van de virtuele machine, of, Hallo VM niet geluisterd op poort. 

**Validatie en oplossing**

1. Meld u bij de back-end voor toohello VM. 
2. Open een opdrachtprompt en voer de volgende opdracht toovalidate er is een toepassing die luistert op poort Hallo Hallo uit:  
            netstat - an 
3. Als Hallo poort niet wordt vermeld met status 'Luistert', de juiste luisterpoort Hallo configureren 
4. Als Hallo-poort is gemarkeerd als Listening, controleert u de doeltoepassing Hallo bij die poort voor mogelijke problemen. 

### <a name="cause-2-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vm"></a>2 oorzaak: De netwerkbeveiligingsgroep blokkeert Hallo-poort op Hallo back-endpool van de Load Balancer VM  

Als een of meer beveiligingsgroepen die zijn geconfigureerd op Hallo subnet of op Hallo VM-netwerk wordt blokkeert Hallo bron-IP- of -poort, dan is hello VM niet kan toorespond.

* Lijst Hallo netwerkbeveiligingsgroepen op Hallo back-end VM geconfigureerd. Zie voor meer informatie:
    -  [Netwerkbeveiligingsgroepen met Hallo Portal beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md)
    -  [Netwerkbeveiligingsgroepen beheren met behulp van PowerShell](../virtual-network/virtual-network-manage-nsg-arm-ps.md)
* Controleer of in lijst Hallo van netwerkbeveiligingsgroepen:
    - Hallo binnenkomende of uitgaande verkeer op poort Hallo heeft een storing. 
    - een **weigeren alle** groep netwerkbeveiligingsregel op Hallo NIC uit Hallo VM of Hallo subnet dat een hogere prioriteit heeft die Hallo standaardregel waarmee Load Balancer-tests en verkeer (netwerkbeveiligingsgroepen moeten toestaan Load Balancer IP-adres van 168.63.129.16 die testpoort) 
* Als regels Hallo Hallo verkeer blokkeren, verwijderen en opnieuw configureren van deze regels tooallow Hallo-gegevensverkeer.  
* Test Hallo VM is nu toorespond toohello statuscontroles gestart.

### <a name="cause-3-accessing-hello-load-balancer-from-hello-same-vm-and-network-interface"></a>3 oorzaak: Toegang tot Load Balancer Hallo van Hallo dezelfde virtuele machine en een netwerkinterface 

Als uw toepassing die wordt gehost in Hallo back-end VM van een Load Balancer probeert tooaccess een andere toepassing die wordt gehost hello dezelfde back-end VM via Hallo hetzelfde netwerk Interface, maar is een niet-ondersteunde scenario mislukken. 

**Resolutie** kunt u dit probleem op via een van de volgende methoden Hallo oplossen:
* Configureer afzonderlijke back-endpool VM's per toepassing. 
* Hallo-toepassing in dual NIC VM's configureren zodat elke toepassing een eigen netwerkinterface en de IP-adres is gebruikt. 

### <a name="cause-4-accessing-hello-internal-load-balancer-vip-from-hello-participating-load-balancer-backend-pool-vm"></a>4 oorzaak: Toegang tot Hallo interne Load Balancer-VIP van Hallo deel van de back-endpool van de Load Balancer VM

Als een ILB VIP is geconfigureerd in een VNet en een Hallo deelnemer backend VMs probeert Hallo tooaccess interne Load Balancer-VIP, waardoor de fout. Dit scenario wordt niet ondersteund.
**Resolutie** toepassingsgateway evalueren of andere toosupport proxy's (bijvoorbeeld nginx of haproxy) dat kind van het scenario. Zie voor meer informatie over Application Gateway [overzicht van Application Gateway](../application-gateway/application-gateway-introduction.md)

## <a name="additional-network-captures"></a>Aanvullende netwerkopnamen
Als u een ondersteuningsaanvraag tooopen, verzamelen Hallo-informatie voor een snellere oplossing te volgen. Kies een back-end van één VM tooperform Hallo tests te volgen:
- Gebruik psping om een van de Hallo back-end virtuele machines binnen Hallo VNet tootest Hallo test poort antwoord (voorbeeld: psping om 10.0.0.4:3389) en noteer de resultaten. 
- Gebruik TCPing uit een Hallo back-end virtuele machines binnen Hallo VNet tootest Hallo test poort antwoord (voorbeeld: psping om 10.0.0.4:3389) en noteer de resultaten.
- Als er geen reactie wordt ontvangen in de deze pingtests, een gelijktijdige Netsh-trace uitvoeren op Hallo back-end VM en VNet virtuele testmachine Hallo terwijl u psping om Voer vervolgens de Netsh-trace Hallo stoppen. 
  
## <a name="next-steps"></a>Volgende stappen

Als hello voorgaande stappen probleem niet hello verhelpen, opent u een [ondersteunen ticket](https://azure.microsoft.com/support/options/).

