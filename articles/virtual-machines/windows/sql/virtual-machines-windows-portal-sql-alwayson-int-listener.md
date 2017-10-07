---
title: een SQL Server voor de beschikbaarheidsgroeplistener in virtuele machines in Azure aaaCreate | Microsoft Docs
description: Stapsgewijze instructies voor het maken van een listener voor een AlwaysOn-beschikbaarheidsgroep voor SQL Server in Azure virtuele machines
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: d1f291e9-9af2-41ba-9d29-9541e3adcfcf
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/01/2017
ms.author: mikeray
ms.openlocfilehash: c6a44dc5c7c18b572c2bf5772b4651b7210aacbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-load-balancer-for-an-always-on-availability-group-in-azure"></a>Een load balancer voor een AlwaysOn-beschikbaarheidsgroep configureren in Azure
Dit artikel wordt uitgelegd hoe toocreate een load balancer voor een beschikbaarheidsgroep SQL Server Always On in Azure virtuele machines die worden uitgevoerd met Azure Resource Manager. Een beschikbaarheidsgroep is een load balancer vereist wanneer Hallo SQL Server-exemplaren op virtuele machines in Azure. Hallo load balancer slaat Hallo IP-adres voor Hallo beschikbaarheidsgroep-listener. Als een beschikbaarheidsgroep meerdere regio's omvat, moet elke regio een load balancer.

toocomplete deze taak moet u een SQL Server-beschikbaarheidsgroep is geïmplementeerd op Azure virtuele machines die worden uitgevoerd met Resource Manager toohave. Beide virtuele machines van SQL Server moet behoren toohello dezelfde beschikbaarheidsset. U kunt Hallo [Microsoft sjabloon](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically Hallo-beschikbaarheidsgroep maken in de Resource Manager. Deze sjabloon maakt automatisch een interne load balancer voor u. 

Als u liever, kunt u [handmatig configureren van een beschikbaarheidsgroep](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

In dit artikel is vereist dat uw beschikbaarheidsgroepen al zijn geconfigureerd.  

Verwante onderwerpen zijn:

* [Altijd op beschikbaarheidsgroepen configureren in Azure VM (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Een VNet-naar-VNet-verbinding configureren met behulp van Azure Resource Manager en PowerShell](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

Door de stappen in dit artikel, moet u maken en configureren van een load balancer in hello Azure-portal. Nadat het Hallo-proces is voltooid, configureert u Hallo cluster toouse Hallo IP-adres uit Hallo load balancer voor Hallo beschikbaarheidsgroep-listener.

## <a name="create-and-configure-hello-load-balancer-in-hello-azure-portal"></a>Maken en configureren van Hallo load balancer in hello Azure-portal
In dit gedeelte van de taak Hallo Hallo te volgen:

1. Hallo load balancer maken in hello Azure-portal, en Hallo IP-adres configureren.
2. Hallo back-end-pool configureren.
3. Hallo-test maken. 
4. Hallo taakverdelingsregels ingesteld.

> [!NOTE]
> Als Hallo SQL Server-exemplaren in meerdere resourcegroepen en regio's zijn, voert elke stap tweemaal eenmaal binnen elke resourcegroep.
> 
> 

### <a name="step-1-create-hello-load-balancer-and-configure-hello-ip-address"></a>Stap 1: Hallo load balancer maken en Hallo IP-adres configureren
Maak eerst Hallo load balancer. 

1. Open in hello Azure-portal, Hallo resourcegroep die Hallo SQL Server-virtuele machines bevatten. 

2. Klik in de resourcegroep hello, **toevoegen**.

3. Zoeken naar **netwerktaakverdeler** en selecteer vervolgens in de zoekresultaten Hallo **Load Balancer**, die is gepubliceerd via **Microsoft**.

4. Op Hallo **Load Balancer** blade, klikt u op **maken**.

5. In Hallo **maken load balancer** dialoogvenster Hallo load balancer als volgt configureren:

   | Instelling | Waarde |
   | --- | --- |
   | **Naam** |De tekstnaam van een hello load balancer die vertegenwoordigt. Bijvoorbeeld: **sqlLB**. |
   | **Type** |**Interne**: de meeste implementaties gebruikt een interne load balancer, waardoor toepassingen binnen Hallo hetzelfde virtuele netwerk tooconnect toohello-beschikbaarheidsgroep.  </br> **Externe**: kan groep van toepassingen tooconnect toohello beschikbaarheid via een openbare internetverbinding. |
   | **Virtueel netwerk** |Selecteer Hallo virtuele netwerk die SQL Server-intances Hallo in. |
   | **Subnet** |Selecteer Hallo subnet die Hallo SQL Server-exemplaren in. |
   | **IP-adrestoewijzing** |**Statische** |
   | **Privé IP-adres** |Geef een beschikbaar IP-adres van Hallo subnet. Dit IP-adres gebruiken bij het maken van een listener op Hallo-cluster. In een PowerShell-script wordt verderop in dit artikel kunt u dit adres gebruiken voor Hallo `$ILBIP` variabele. |
   | **Abonnement** |Als u meerdere abonnementen hebt, wordt dit veld mogelijk weergegeven. Selecteer Hallo-abonnement dat u wilt dat tooassociate aan deze resource. Dit is hetzelfde abonnement normaal gesproken als alle Hallo resources voor de beschikbaarheidsgroep Hallo Hallo. |
   | **Resourcegroep** |Selecteer de resourcegroep Hallo die Hallo SQL Server-exemplaren in. |
   | **Locatie** |Selecteer Hallo Hallo SQL Server-exemplaren zijn in Azure-locatie. |

6. Klik op **Create**. 

Azure maakt Hallo load balancer. Hallo load balancer hoort tooa specifieke netwerk, subnet, resourcegroep en locatie. Nadat Azure Hallo taken is voltooid, controleert u of Hallo load balancer-instellingen in Azure. 

### <a name="step-2-configure-hello-back-end-pool"></a>Stap 2: Hallo back-end-pool configureren
Azure aanroepen Hallo back-end-adresgroep *back-endpool*. In dit geval is Hallo back-end-pool hello-mailadressen van Hallo twee exemplaren van SQL Server in de beschikbaarheidsgroep. 

1. Klik in de resourcegroep op Hallo load balancer die u hebt gemaakt. 

2. Op **instellingen**, klikt u op **back-endpools**.

3. Op **back-endpools**, klikt u op **toevoegen** toocreate een back-end-adresgroep. 

4. Op **toevoegen van de back-endpool**onder **naam**, typ een naam voor Hallo back-end-pool.

5. Onder **virtuele machines**, klikt u op **toevoegen van een virtuele machine**. 

6. Onder **virtuele machines kiezen**, klikt u op **een beschikbaarheidsset kiezen**, en geef vervolgens Hallo beschikbaarheidsset dat Hallo SQL Server-virtuele machines deel uitmaken.

7. Nadat u de beschikbaarheidsset Hallo hebt gekozen, klikt u op **Hallo virtuele machines kiezen**, Selecteer twee virtuele machines die als host van SQL Server-exemplaren in de beschikbaarheidsgroep Hallo Hallo en klik vervolgens op Hallo **Selecteer**. 

8. Klik op **OK** tooclose Hallo blades voor **virtuele machines kiezen**, en **toevoegen van de back-endpool**. 

Hallo-instellingen voor Hallo back-end-adresgroep voor Azure-updates. De beschikbaarheidsset heeft nu een pool van twee exemplaren van SQL Server.

### <a name="step-3-create-a-probe"></a>Stap 3: Een test maken
Hallo test definieert hoe Azure verifieert dat SQL Server-exemplaren Hallo momenteel eigenaar is van Hallo beschikbaarheidsgroep-listener. Azure-tests Hallo-service op basis van Hallo IP-adres op een poort die u bij het maken van de test Hallo definiëren.

1. Op Hallo netwerktaakverdeler **instellingen** blade, klikt u op **statuscontroles**. 

2. Op Hallo **statuscontroles** blade, klikt u op **toevoegen**.

3. Hallo test configureren op Hallo **toevoegen test** blade. Gebruik Hallo waarden tooconfigure Hallo test te volgen:

   | Instelling | Waarde |
   | --- | --- |
   | **Naam** |De tekstnaam van een hello test die vertegenwoordigt. Bijvoorbeeld: **SQLAlwaysOnEndPointProbe**. |
   | **Protocol** |**TCP** |
   | **Poort** |U kunt een beschikbare poort gebruiken. Bijvoorbeeld: *59999*. |
   | **Interval** |*5* |
   | **Drempelwaarde voor onjuiste status** |*2* |

4.  Klik op **OK**. 

> [!NOTE]
> Zorg ervoor dat Hallo poort die u opgeeft geopend op de firewall Hallo van beide exemplaren van SQL Server is. Beide exemplaren vereisen een inkomende regel voor Hallo TCP-poort die u gebruikt. Zie voor meer informatie [toevoegen of bewerken firewallregel](http://technet.microsoft.com/library/cc753558.aspx). 
> 
> 

Azure Hallo test maakt en gebruikt vervolgens tootest welke SQL Server-exemplaar Hallo-listener voor de beschikbaarheidsgroep Hallo heeft.

### <a name="step-4-set-hello-load-balancing-rules"></a>Stap 4: Stel Hallo load-balancingregels
regels voor taakverdeling Hallo configureren hoe Hallo load balancer doorgestuurd voor verkeer toohello SQL Server-exemplaren. Voor deze load balancer inschakelen u direct server return omdat slechts één van de twee SQL Server-exemplaren Hallo eigenaar is van Hallo listener beschikbaarheidsgroepresource tegelijk.

1. Op Hallo netwerktaakverdeler **instellingen** blade, klikt u op **Taakverdelingsregels**. 

2. Op Hallo **Taakverdelingsregels** blade, klikt u op **toevoegen**.

3. Op Hallo **taakverdelingsregels toevoegen** blade Hallo taakverdelingsregel configureren. Gebruik Hallo volgende instellingen: 

   | Instelling | Waarde |
   | --- | --- |
   | **Naam** |De tekstnaam van een hello taakverdelingsregels die vertegenwoordigt. Bijvoorbeeld: **SQLAlwaysOnEndPointListener**. |
   | **Protocol** |**TCP** |
   | **Poort** |*1433* |
   | **Back-Endpoort** |*1433*. Deze waarde wordt genegeerd omdat deze regel maakt gebruik van **zwevend IP (direct server return)**. |
   | **Test** |Hallo-naam van Hallo-test die u hebt gemaakt voor deze load balancer gebruiken. |
   | **Sessiepersistentie** |**Geen** |
   | **Time-out voor inactiviteit (minuten)** |*4* |
   | **Zwevend IP (direct server return)** |**Ingeschakeld** |

   > [!NOTE]
   > U wellicht tooscroll omlaag Hallo blade tooview alle Hallo-instellingen.
   > 

4. Klik op **OK**. 
5. Azure configureert Hallo taakverdelingsregel. Hallo load balancer is nu geconfigureerd tooroute verkeer toohello exemplaar van SQL Server die als host Hallo-listener voor de beschikbaarheidsgroep Hallo fungeert. 

Op dit moment is Hallo-resourcegroep een load balancer die verbinding tooboth SQL Server-machines maakt. Hallo load balancer bevat ook een IP-adres voor Hallo SQL Server Always On beschikbaarheidsgroeplistener, zodat beide machine toorequests voor beschikbaarheidsgroepen Hallo kan reageren.

> [!NOTE]
> Als uw SQL Server-exemplaren in twee afzonderlijke regio's, stappen Hallo in Hallo andere regio. Elke regio vereist een load balancer. 
> 
> 

## <a name="configure-hello-cluster-toouse-hello-load-balancer-ip-address"></a>Hallo cluster toouse Hallo load balancer IP-adres configureren
de volgende stap Hallo tooconfigure Hallo listener op Hallo cluster en Hallo listener online brengen. Hallo te volgen: 

1. Hallo beschikbaarheidsgroep-listener op Hallo failover-cluster maken. 

2. Hallo-listener online brengen.

### <a name="step-5-create-hello-availability-group-listener-on-hello-failover-cluster"></a>Stap 5: Hallo beschikbaarheidsgroep-listener op Hallo failover-cluster maken
In deze stap moet u handmatig Hallo beschikbaarheidsgroep-listener in Failoverclusterbeheer en SQL Server Management Studio maken.

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

### <a name="verify-hello-configuration-of-hello-listener"></a>Hallo-configuratie van Hallo listener controleren

Als de clusterbronnen Hallo en afhankelijkheden juist zijn geconfigureerd, moet u kunnen tooview Hallo-listener in SQL Server Management Studio. tooset Hallo listener-poort, Hallo te volgen:

1. Start SQL Server Management Studio en maak verbinding toohello primaire replica.

2. Ga te**AlwaysOn hoge beschikbaarheid** > **beschikbaarheidsgroepen** > **beschikbaarheid Beschikbaarheidsgroeplisteners**.  
    U ziet nu Hallo-listener-naam die u hebt gemaakt in Failoverclusterbeheer. 

3. Met de rechtermuisknop op de naam van de beschikbaarheidsgroeplistener hello en klik vervolgens op **eigenschappen**.

4. In Hallo **poort** Geef Hallo-poortnummer voor Hallo beschikbaarheidsgroep-listener met behulp van Hallo $EndpointPort u eerder hebt gebruikt (1433 was Hallo standaard), en klik vervolgens op **OK**.

U hebt nu een beschikbaarheidsgroep in Azure virtuele machines die worden uitgevoerd in de modus Resource Manager. 

## <a name="test-hello-connection-toohello-listener"></a>Test Hallo verbinding toohello listener
Hallo-testverbinding door Hallo volgende te doen:

1. RDP tooa SQL Server-exemplaar dat in Hallo hetzelfde virtuele netwerk, maar niet eigen Hallo replica. Deze server kunnen worden Hallo andere SQL Server-exemplaar in Hallo-cluster.

2. Gebruik **sqlcmd** hulpprogramma tootest Hallo verbinding. Bijvoorbeeld Hallo script volgen stelt een **sqlcmd** verbinding toohello primaire replica via het Hallo-listener met de Windows-verificatie:
   
        sqlcmd -S <listenerName> -E

Hallo SQLCMD-verbinding verbinding automatisch toohello SQL Server-exemplaar dat als host fungeert voor de primaire replica Hallo. 

## <a name="create-an-ip-address-for-an-additional-availability-group"></a>Een IP-adres voor een extra beschikbaarheidsgroep maken

Elke beschikbaarheidsgroep een listener afzonderlijke gebruikt. Elke listener beschikt over een eigen IP-adres. Gebruik dezelfde Hallo load balancer toohold Hallo IP-adres voor extra listeners. Nadat u een beschikbaarheidsgroep hebt gemaakt, Hallo IP-adres toohello load balancer toevoegen en configureer vervolgens Hallo listener.

een IP-adres tooa load balancer Hello Azure-portal tooadd Hallo te volgen:

1. Open Hallo-resourcegroep met de Hallo load balancer in hello Azure-portal, en klik op Hallo load balancer. 

2. Onder **instellingen**, klikt u op **Frontend-IP adresgroep**, en klik vervolgens op **toevoegen**. 

3. Onder **frontend-IP-adres toevoegen**, wijs een naam voor het Hallo-front-end. 

4. Controleer of deze Hallo **virtueel netwerk** en Hallo **Subnet** zijn hetzelfde als het SQL Server-exemplaren Hallo Hallo.

5. Hallo IP-adres voor de listener Hallo ingesteld. 
   
   >[!TIP]
   >U kunt Hallo IP-adres toostatic en typ een adres dat wordt momenteel niet gebruikt in Hallo subnet. U kunt ook Hallo IP-adres toodynamic en opslaan van Hallo nieuwe front-end-IP-adresgroep. Als u doet dit, wordt een beschikbare IP-adres toohello groep automatisch toegewezen door hello Azure-portal. Vervolgens kunt u Open Hallo front-end-IP-adresgroep en Hallo toewijzing toostatic wijzigen. 

6. Hallo IP-adres voor de listener Hallo opslaan. 

7. Een health test toevoegen met behulp van Hallo volgende instellingen:

   |Instelling |Waarde
   |:-----|:----
   |**Naam** |Een naam tooidentify Hallo-test.
   |**Protocol** |TCP
   |**Poort** |Een niet-gebruikte TCP-poort, die beschikbaar zijn op alle virtuele machines. Het kan niet worden gebruikt voor andere doeleinden. Er zijn geen twee listeners kunnen hello gebruiken dezelfde poort-test. 
   |**Interval** |Hallo hoeveelheid tijd tussen test probeert. Hallo-standaard (5) gebruiken.
   |**Drempelwaarde voor onjuiste status** |Hallo aantal opeenvolgende drempelwaarden die moet worden gemist voordat een virtuele machine is in orde beschouwd.

8. Klik op **OK** toosave Hallo test. 

9. Maak een regel voor taakverdeling. Klik op **Taakverdelingsregels**, en klik vervolgens op **toevoegen**.

10. Hallo nieuwe taakverdelingsregel met behulp van Hallo volgende instellingen configureren:

   |Instelling |Waarde
   |:-----|:----
   |**Naam** |Een naam tooidentify hello balancingregel laden. 
   |**Frontend IP-adres** |Selecteer Hallo IP-adres dat u hebt gemaakt. 
   |**Protocol** |TCP
   |**Poort** |Hallo-poort die van SQL Server-exemplaren hello gebruikmaken gebruiken. Een standaardexemplaar gebruikt poort 1433, tenzij u deze hebt gewijzigd. 
   |**Back-endpoort** |Gebruik Hallo dezelfde als waarde **poort**.
   |**Back-endpool** |Hallo-pool met Hallo virtuele machines met Hallo SQL Server-exemplaren. 
   |**De statuscontrole** |Kies Hallo-test die u hebt gemaakt.
   |**Sessiepersistentie** |Geen
   |**Time-out voor inactiviteit (minuten)** |Standaard (4)
   |**Zwevend IP (direct server return)** | Ingeschakeld

### <a name="configure-hello-availability-group-toouse-hello-new-ip-address"></a>Hallo beschikbaarheid groep toouse Hallo nieuwe IP-adres configureren

toofinish Hallo-cluster, herhaaldelijk Hallo stappen die u wanneer u de eerste beschikbaarheidsgroep Hallo gevolgd configureren. Dat wil zeggen configureren Hallo [toouse Hallo nieuwe IP-adres van cluster](#configure-the-cluster-to-use-the-load-balancer-ip-address). 

Wanneer u een IP-adres voor de listener Hallo hebt toegevoegd, kunt u de Hallo aanvullende-beschikbaarheidsgroep configureren door Hallo volgende te doen: 

1. Controleer of Hallo testpoort voor het nieuwe IP-adres Hallo geopend zijn op beide virtuele machines van SQL Server. 

2. [In de Cluster-beheer toevoegen Hallo clienttoegangspunt](#addcap).

3. [Hallo IP-resource voor de beschikbaarheidsgroep Hallo configureren](#congroup).

   >[!IMPORTANT]
   >Wanneer u Hallo IP-adres, gebruiken Hallo IP-adres dat u toohello load balancer toegevoegd.  

4. [Maak Hallo SQL Server-beschikbaarheidsgroepresource afhankelijk van clienttoegangspunt hello](#dependencyGroup).

5. [Hallo-client toegang afhankelijk Hallo IP-adres van bron wijzen](#listname).
 
6. [Hallo Clusterparameters instellen in PowerShell](#setparam).

Nadat u Hallo beschikbaarheid toouse Hallo nieuwe IP-groepadres configureert, configureert u Hallo verbinding toohello listener. 

## <a name="next-steps"></a>Volgende stappen

- [Een SQL Server Always On-beschikbaarheidsgroep configureren op virtuele Azure-machines in verschillende regio 's](virtual-machines-windows-portal-sql-availability-group-dr.md)
