---
title: De Load Balancer op meerdere IP-configuraties in Azure | Microsoft Docs
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
ms.openlocfilehash: cf1e68c7b37b2506de007bdf24eea63a27187a33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-the-azure-portal"></a>De Load Balancer op meerdere IP-configuraties met de Azure portal

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)
> * [CLI](load-balancer-multiple-ip-cli.md)

Dit artikel wordt beschreven hoe u Azure Load Balancer met meerdere IP-adressen op een secundaire netwerkinterface (NIC). In dit scenario hebben we twee virtuele machines met Windows, elk met een primaire en een secundaire NIC. Elk van de secundaire NIC's twee IP-configuraties hebben. Elke virtuele machine fungeert als host van websites contoso.com en fabrikam.com. Elke website is gebonden aan een van de IP-configuraties voor de secundaire NIC. We Azure Load Balancer gebruiken om twee IP-adressen voor frontend, één voor elke website, voor het distribueren van het verkeer naar de respectieve IP-configuratie voor de website weer te geven. Dit scenario gebruikt hetzelfde poortnummer op zowel frontends, evenals het IP-adressen van zowel back-end-groep.

![De installatiekopie van de Load Balancer-scenario](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

##<a name="prerequisites"></a>Vereisten
In dit voorbeeld wordt ervan uitgegaan dat er een resourcegroep met de naam *contosofabrikam* met de volgende configuratie:
 -  een virtueel netwerk met de naam bevat *myVNet*, twee VMs aangeroepen *VM1* en *VM2* binnen dezelfde beschikbaarheidsset benoemde *myAvailset*. 
 - elke virtuele machine heeft een primaire NIC en een secundaire NIC. De primaire NIC's zijn benoemde *VM1NIC1* en *VM2NIC1* en de secundaire NIC's zijn benoemde *VM1NIC2* en *VM2NIC2*. Zie voor meer informatie over het maken van virtuele machines met meerdere NIC's [een virtuele machine maken met meerdere NIC's met behulp van PowerShell](../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a>Stappen om taken te verdelen over meerdere IP-configuraties

Volg onderstaande stappen om het bereiken van het scenario in dit artikel wordt beschreven:

### <a name="step-1-configure-the-secondary-nics-for-each-vm"></a>STAP 1: De secundaire NIC's voor elke virtuele machine configureren

Voor elke virtuele machine in uw virtuele netwerk, voegt u als volgt set IP-configuratie voor de secundaire NIC:  

1. Navigeer vanuit een browser naar de Azure-portal: http://portal.azure.com en meld u aan met uw Azure-account.
2. Op de bovenste linkerkant van het scherm en klik op het pictogram van de resourcegroep en klik vervolgens op de resourcegroep die de virtuele machines bevinden zich in (bijvoorbeeld *contosofabrikam*). De **resourcegroepen** blade met een lijst met alle resources samen met de netwerkinterfaces voor de virtuele machines wordt nu weergegeven.
3. Naar de secundaire NIC. van elke virtuele machine, moet u een IP-configuratie als volgt toevoegen:
    1. Selecteer de netwerkinterface die u wilt toevoegen, de IP-configuratie.
    2. In de blade die wordt weergegeven voor de Netwerkkaart op die u hebt geselecteerd, klikt u op **IP-configuraties**. Klik vervolgens op **toevoegen** naar de bovenkant van de blade die wordt weergegeven.
    3. In de **toevoegen IP-configuraties** blade toevoegen van een tweede IP-configuratie op de NIC als volgt: 
        1. Typ een naam voor de secundaire IP-configuratie (bijvoorbeeld voor de VM1 en VM2 van de IP-configuraties als naam *VM1NIC2 ipconfig2* en *VM2NIC2 ipconfig2* respectievelijk).
        2. Voor **particuliere IP-adres**, voor **toewijzing**, selecteer **statische**.
        3. Klik op **OK**.
        4. Het tweede IP-configuratie voor de secundaire NIC is voltooid, wordt weergegeven in de **IP-configuraties** instellingenblade voor de opgegeven netwerkadapter.

### <a name="step-2-create-a-load-balancer"></a>STAP 2: Een load balancer maken

Hiermee maakt u een load balancer als volgt:

1. Navigeer vanuit een browser naar de Azure-portal: http://portal.azure.com en meld u aan met uw Azure-account.
2. Klik op de bovenste linkerkant van het scherm en **nieuw** > **Networking** > **Load Balancer**. Klik vervolgens op **maken**.
3. Voer op de blade **Load balancer maken** een naam in voor de load balancer. Hier wordt genoemd *mylb*.
4. Maak onder de openbare IP-adres, een nieuwe openbare IP-adres aangeroepen **PublicIP1**.
5. Selecteer onder de resourcegroep, de bestaande resourcegroep van uw virtuele machines (bijvoorbeeld *contosofabrikam*). Vervolgens selecteert u een geschikte locatie en klik vervolgens op **OK**. De load balancer wordt nu geïmplementeerd. Dit proces duurt enkele minuten.
6. Zodra geïmplementeerd, wordt de load balancer wordt weergegeven als een resource in de resourcegroep.

### <a name="step-3-configure-the-frontend-ip-pool"></a>STAP 3: Configureer de frontend-IP-adresgroep

De frontend-IP-adresgroep voor elke website (Contoso en Fabrikam) als volgt configureren:

1. Klik in de portal op **meer services** > type **openbaar IP-adres** in het filtervak en klik vervolgens op **openbare IP-adressen**. Klik op **toevoegen** naar de bovenkant van de blade die wordt weergegeven.
2. Configureer twee openbare IP-adressen (*PublicIP1* en *PublicIP2*) voor beide websites (contoso en fabrikam) als volgt:
    1. Typ een naam voor uw frontend-IP-adres.
    2. Voor **resourcegroep**, selecteert u de bestaande resourcegroep van de virtuele machines (bijvoorbeeld *contosofabrikam*).
    3. Voor **locatie**, selecteert u dezelfde locatie als de virtuele machines.
    4. Klik op **OK**.
    5. Als de twee openbare IP-adressen zijn gemaakt, worden deze beide weergegeven in de **openbare IP-adres** adressen blade.
3. Klik in de portal op **meer services** > type **netwerktaakverdeler** in het filtervak en klik vervolgens op **Load Balancer**.  
4. Selecteer de load balancer (*mylb*) dat u wilt toevoegen de frontend-IP-adresgroep op.
5. Onder **instellingen**, selecteer **Frontend Pools**. Klik vervolgens op **toevoegen** naar de bovenkant van de blade die wordt weergegeven.
6. Typ een naam voor uw frontend-IP-adres (*farbikamfe* of **contosofe*).
7. Klik op **IP-adres** en klik op de **Kies openbaar IP-adres** blade, selecteer de IP-adressen voor uw frontend (*PublicIP1* of *PublicIP2*).
8. Herhaal stap 3 tot 7 in deze sectie voor het maken van de tweede frontend-IP-adres.
9. Wanneer de frontend-IP-adresgroepconfiguratie voltooid is, worden beide frontend-IP-adressen weergegeven in de **Frontend-IP-adresgroep** blade van de load balancer. 
    
### <a name="step-4-configure-the-backend-pool"></a>STAP 4: Configureer de back-endpool   
De back-end-adresgroepen op de load balancer voor elke website (Contoso en Fabrikam) als volgt configureren:
        
1. Klik in de portal op **meer services** > load balancer in het filtervak typt en klik vervolgens op **Load Balancer**.  
2. Selecteer de load balancer (*mylb*) dat u wilt toevoegen aan de back-endpools.
3. Onder **instellingen**, selecteer **back-Endpools**. Typ een naam voor uw back-endpool (bijvoorbeeld *contosopool* of *fabrikampool*). Klik vervolgens op de **toevoegen** knop naar de bovenkant van de blade die wordt weergegeven. 
4. Voor **die is gekoppeld aan**, selecteer **beschikbaarheidsset**.
5. Voor **beschikbaarheidsset**, selecteer **myAvailset**.
6. Doel-IP-netwerkconfiguraties voor beide virtuele machines als volgt toevoegen (Zie afbeelding 2):  
    1. Voor **doel-virtuele machine**, selecteert u de virtuele machine die u wilt toevoegen aan de back-endpool (bijvoorbeeld VM1 of VM2).
    2. Voor **netwerk-IP-configuratie**, selecteert u de secundaire NIC's IP-configuratie voor deze virtuele machine (bijvoorbeeld VM1NIC2 ipconfig2 of VM2NIC2 ipconfig2).
    ![De installatiekopie van de Load Balancer-scenario](./media/load-balancer-multiple-ip/lb-backendpool.PNG)
            
        **Afbeelding 2**: configuratie van de load balancer met back-endpools  
7. Klik op **OK**.
8. Wanneer de configuratie van de back-end-adresgroep voltooid is, beide back-end-adresgroepen worden weergegeven in de **back-end-pool-blade** van de load balancer.

### <a name="step-5-configure-a-health-probe-for-your-load-balancer"></a>STAP 5: Configureren voor de load balancer een health test
Voor de load balancer een health test als volgt configureren:
    1. Klik in de portal op meer services > load balancer in het filtervak typt en klik vervolgens op **Load Balancer**.  
    2. Selecteer de load balancer die u wilt toevoegen aan de back-endpools.
    3. Onder **instellingen**, selecteer **Health test**. Klik vervolgens op **toevoegen** naar de bovenkant van de blade die wordt weergegeven.
    4. Typ een naam voor de health-test (bijvoorbeeld HTTP) en klik op **OK**.

### <a name="step-6-configure-load-balancing-rules"></a>STAP 6: Configureer regels voor taakverdeling
Configureer regels voor taakverdeling (*HTTPc* en *HTTPf*) voor elke website als volgt:
    
1. Onder **instellingen**, selecteer **Health test**. Klik vervolgens op **toevoegen** naar de bovenkant van de blade die wordt weergegeven.
2. Voor **naam**, typ een naam voor de taakverdelingsregel (bijvoorbeeld *HTTPc* voor Contoso of *HTTPf* voor Fabrikam)
3. Frontend IP-adres, selecteert u de de frontend-IP-adres (bijvoorbeeld *Contosofe* of *Fabrikamfe*)
4. Voor **poort** en **backendpoort**, hou de standaardwaarde **80**.
5. Voor **zwevend IP (direct server return)**, klikt u op **ingeschakeld**.
6. Klik op **OK**.
7. Herhaal stap 1 tot en met 6 in deze sectie voor het maken van de tweede regel voor Load Balancer.
8. Wanneer de taakverdeling regels in configuratie is voltooid, beide regels ((*HTTPc* en *HTTPf*) worden weergegeven in de **Taakverdelingsregels** blade van de load balancer.

### <a name="step-7-configure-dns-records"></a>STAP 7: DNS-records configureren
Tot slot moet u DNS-bronrecords om te verwijzen naar de respectieve frontend-IP-adres van de load balancer configureren. U kunt uw domeinen in Azure DNS hosten. Zie voor meer informatie over het gebruik van Azure DNS met Load Balancer [met behulp van Azure DNS met andere Azure-services](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over het combineren van de load balancer-services in Azure in [met gelijke taakverdeling van services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Meer informatie over hoe u verschillende typen logboeken kunt gebruiken in Azure te beheren en oplossen van de load balancer in [analytics aanmelden voor Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).
