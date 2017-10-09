---
title: aaaLoad balancing op meerdere IP-configuraties in Azure | Microsoft Docs
description: Taakverdeling over de primaire en secundaire IP-configuraties.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 8619493b8102e9d158d428fe6c59ecf3f32edc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-hello-azure-portal"></a>Taakverdeling op meerdere IP-configuraties met hello Azure-portal

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)
> * [CLI](load-balancer-multiple-ip-cli.md)

Dit artikel wordt beschreven hoe toouse Azure Load Balancer met meerdere IP-adressen op een secundaire netwerkinterface (NIC). In dit scenario hebben we twee virtuele machines met Windows, elk met een primaire en een secundaire NIC. Elk van de secundaire Hallo NIC's, hebben twee IP-configuraties. Elke virtuele machine fungeert als host van websites contoso.com en fabrikam.com. Elke website is gebonden tooone Hallo IP-configuraties op Hallo secundaire NIC. We gebruiken Azure Load Balancer tooexpose twee frontend IP-adressen, één voor elke website, toodistribute verkeer toohello respectieve IP-configuratie voor Hallo-website. Dit scenario maakt gebruik van hetzelfde poortnummer Hallo over zowel frontends, evenals het IP-adressen van zowel back-end-groep.

![De installatiekopie van de Load Balancer-scenario](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

##<a name="prerequisites"></a>Vereisten
In dit voorbeeld wordt ervan uitgegaan dat er een resourcegroep met de naam *contosofabrikam* Hello volgende configuratie:
 -  een virtueel netwerk met de naam bevat *myVNet*, twee VMs aangeroepen *VM1* en *VM2* Hallo respectievelijk binnen dezelfde beschikbaarheidsset benoemde *myAvailset*. 
 - elke virtuele machine heeft een primaire NIC en een secundaire NIC. Hallo primaire NIC's zijn benoemde *VM1NIC1* en *VM2NIC1* en Hallo secundaire NIC's zijn benoemde *VM1NIC2* en *VM2NIC2*. Zie voor meer informatie over het maken van virtuele machines met meerdere NIC's [een virtuele machine maken met meerdere NIC's met behulp van PowerShell](../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Stappen tooload verdelen over meerdere IP-configuraties

Volg deze stappen hieronder tooachieve Hallo scenario in dit artikel wordt beschreven:

### <a name="step-1-configure-hello-secondary-nics-for-each-vm"></a>STAP 1: Configureer hello secundaire NIC's voor elke virtuele machine

Hallo secundaire NIC als volgt voor elke virtuele machine in het virtuele netwerk set IP-configuratie voor toevoegen:  

1. Ga vanuit een browser toohello Azure-portal: http://portal.azure.com en meld u aan met uw Azure-account.
2. Hallo bovenste links op Hallo scherm, klikt u op Hallo resourcegroep pictogram en klik vervolgens op Hallo resource groep Hallo VM's bevinden zich in (bijvoorbeeld *contosofabrikam*). Hallo **resourcegroepen** blade met een lijst met alle Hallo resources samen met de netwerkinterfaces Hallo voor Hallo VM's wordt nu weergegeven.
3. secundaire toohello NIC van elke VM toevoegen een IP-configuratie als volgt:
    1. Selecteer Hallo netwerkinterface tooadd Hallo IP-configuratie naar gewenste.
    2. Hallo blade die wordt weergegeven voor Hallo NIC die u hebt geselecteerd, klikt u op **IP-configuraties**. Klik vervolgens op **toevoegen** naar Hallo bovenaan Hallo-blade die wordt weergegeven.
    3. In Hallo **toevoegen IP-configuraties** blade een tweede IP-configuratie toohello NIC als volgt toevoegen: 
        1. Typ een naam voor de secundaire IP-configuratie (bijvoorbeeld voor de VM1 en VM2 naam Hallo IP-configuraties als *VM1NIC2 ipconfig2* en *VM2NIC2 ipconfig2* respectievelijk).
        2. Voor **particuliere IP-adres**, voor **toewijzing**, selecteer **statische**.
        3. Klik op **OK**.
        4. Als tweede IP-configuratie voor Hallo Hallo secundaire NIC voltooid is, wordt deze weergegeven in Hallo **IP-configuraties** instellingenblade voor Hallo gegeven NIC.

### <a name="step-2-create-a-load-balancer"></a>STAP 2: Een load balancer maken

Hiermee maakt u een load balancer als volgt:

1. Ga vanuit een browser toohello Azure-portal: http://portal.azure.com en meld u aan met uw Azure-account.
2. Hallo bovenste links op Hallo scherm, klikt u op **nieuw** > **Networking** > **Load Balancer**. Klik vervolgens op **maken**.
3. In Hallo **maken load balancer** blade, typ een naam voor de load balancer. Hier wordt genoemd *mylb*.
4. Maak onder de openbare IP-adres, een nieuwe openbare IP-adres aangeroepen **PublicIP1**.
5. Onder de resourcegroep, selecteer Hallo bestaande resourcegroep van uw virtuele machines (bijvoorbeeld *contosofabrikam*). Vervolgens selecteert u een geschikte locatie en klik vervolgens op **OK**. Hallo load balancer wordt toodeploy start en duurt een paar minuten toosuccessfully volledige implementatie.
6. Zodra geïmplementeerd, worden Hallo load balancer wordt weergegeven als een resource in de resourcegroep.

### <a name="step-3-configure-hello-frontend-ip-pool"></a>STAP 3: Configureer Hallo frontend-IP-adresgroep

De frontend-IP-adresgroep voor elke website (Contoso en Fabrikam) als volgt configureren:

1. Klik in de portal Hallo op **meer services** > type **openbaar IP-adres** in het filtervak Hallo en klik vervolgens op **openbare IP-adressen**. Klik op **toevoegen** naar Hallo bovenaan Hallo-blade die wordt weergegeven.
2. Configureer twee openbare IP-adressen (*PublicIP1* en *PublicIP2*) voor beide websites (contoso en fabrikam) als volgt:
    1. Typ een naam voor uw frontend-IP-adres.
    2. Voor **resourcegroep**, selecteer Hallo bestaande resourcegroep Hallo virtuele machines (bijvoorbeeld *contosofabrikam*).
    3. Voor **locatie**, selecteer Hallo dezelfde locatie als Hallo van virtuele machines.
    4. Klik op **OK**.
    5. Zodra Hallo twee openbare IP-adressen zijn gemaakt, worden deze beide weergegeven in Hallo **openbare IP-adres** adressen blade.
3. Klik in de portal Hallo op **meer services** > type **netwerktaakverdeler** in het filtervak Hallo en klik vervolgens op **Load Balancer**.  
4. Selecteer Hallo load balancer (*mylb*) dat u wilt dat tooadd Hallo frontend-IP-adresgroep op.
5. Onder **instellingen**, selecteer **Frontend Pools**. Klik vervolgens op **toevoegen** naar Hallo bovenaan Hallo-blade die wordt weergegeven.
6. Typ een naam voor uw frontend-IP-adres (*farbikamfe* of **contosofe*).
7. Klik op **IP-adres** en op Hallo **Kies openbaar IP-adres** blade, selecteer Hallo IP-adressen voor uw frontend (*PublicIP1* of *PublicIP2*).
8. Herhaal stap 3 too7 in deze sectie toocreate Hallo tweede frontend IP-adres.
9. Wanneer Hallo frontend-IP-adresgroepconfiguratie voltooid is, worden beide frontend-IP-adressen weergegeven in Hallo **Frontend-IP-adresgroep** blade van de load balancer. 
    
### <a name="step-4-configure-hello-backend-pool"></a>STAP 4: Hallo back-end-pool configureren   
Hallo back-end-adresgroepen op de load balancer voor elke website (Contoso en Fabrikam) als volgt configureren:
        
1. Klik in de portal Hallo op **meer services** > Hallo filtervak typt u load balancer en klik vervolgens op **Load Balancer**.  
2. Selecteer Hallo load balancer (*mylb*) dat u wilt dat tooadd Hallo back-endpools aan.
3. Onder **instellingen**, selecteer **back-Endpools**. Typ een naam voor uw back-endpool (bijvoorbeeld *contosopool* of *fabrikampool*). Klik vervolgens op Hallo **toevoegen** knop naar de bovenkant Hallo van Hallo-blade die wordt weergegeven. 
4. Voor **die is gekoppeld aan**, selecteer **beschikbaarheidsset**.
5. Voor **beschikbaarheidsset**, selecteer **myAvailset**.
6. Doel-IP-netwerkconfiguraties voor beide virtuele machines als volgt toevoegen (Zie afbeelding 2):  
    1. Voor **doel-virtuele machine**, selecteer Hallo VM die u wilt dat tooadd toohello back-endpool (bijvoorbeeld VM1 of VM2).
    2. Voor **netwerk-IP-configuratie**, selecteer Hallo secundaire NIC's IP-configuratie voor deze virtuele machine (bijvoorbeeld VM1NIC2 ipconfig2 of VM2NIC2 ipconfig2).
    ![De installatiekopie van de Load Balancer-scenario](./media/load-balancer-multiple-ip/lb-backendpool.PNG)
            
        **Afbeelding 2**: Hallo load balancer configureren met back-endpools  
7. Klik op **OK**.
8. Wanneer de configuratie van de groep back-end Hallo voltooid is, beide back-end-adresgroepen worden weergegeven in Hallo **back-end-pool-blade** van de load balancer.

### <a name="step-5-configure-a-health-probe-for-your-load-balancer"></a>STAP 5: Configureren voor de load balancer een health test
Voor de load balancer een health test als volgt configureren:
    1. Klik in het Hallo-portal op meer services > Hallo filtervak typt u load balancer en klik vervolgens op **Load Balancer**.  
    2. Hallo load balancer die u wilt dat tooadd Hallo back-endpools te selecteren.
    3. Onder **instellingen**, selecteer **Health test**. Klik vervolgens op **toevoegen** naar Hallo bovenaan Hallo-blade die wordt weergegeven.
    4. Typ een naam voor de Hallo health test (bijvoorbeeld HTTP) en klik op **OK**.

### <a name="step-6-configure-load-balancing-rules"></a>STAP 6: Configureer regels voor taakverdeling
Configureer regels voor taakverdeling (*HTTPc* en *HTTPf*) voor elke website als volgt:
    
1. Onder **instellingen**, selecteer **Health test**. Klik vervolgens op **toevoegen** naar Hallo bovenaan Hallo-blade die wordt weergegeven.
2. Voor **naam**, typ een naam voor de taakverdelingsregel hello (bijvoorbeeld *HTTPc* voor Contoso of *HTTPf* voor Fabrikam)
3. Selecteer voor Frontend IP-adres, Hallo Hallo frontend-IP-adres (bijvoorbeeld *Contosofe* of *Fabrikamfe*)
4. Voor **poort** en **backendpoort**, hou de standaardwaarde Hallo **80**.
5. Voor **zwevend IP (direct server return)**, klikt u op **ingeschakeld**.
6. Klik op **OK**.
7. Herhaal stap 1 too6 in deze sectie toocreate Hallo tweede Load Balancer-regel.
8. Wanneer regels Hallo load balancing-configuratie is voltooid, beide regels ((*HTTPc* en *HTTPf*) worden weergegeven in Hallo **Taakverdelingsregels** blade van de load balancer.

### <a name="step-7-configure-dns-records"></a>STAP 7: DNS-records configureren
Tot slot moet u DNS-resource records toopoint toohello respectieve frontend IP-adres van Hallo load balancer configureren. U kunt uw domeinen in Azure DNS hosten. Zie voor meer informatie over het gebruik van Azure DNS met Load Balancer [met behulp van Azure DNS met andere Azure-services](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over hoe toocombine load balancing-services in Azure in [met gelijke taakverdeling van services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Meer informatie over hoe u verschillende typen Logboeken gebruiken in Azure toomanage en oplossen van de load balancer in [analytics aanmelden voor Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).
