---
title: Server-beschikbaarheidsgroepen - virtuele Machines van de Azure - noodherstel aaaSQL | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe tooconfigure de beschikbaarheid van een SQL Server op Azure virtuele machines met een replica in een andere regio groepeert.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: df6238dc61c5a56879c75c9bf7314c618f43c0ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a>Een AlwaysOn-beschikbaarheidsgroep configureren op virtuele Azure-machines in verschillende regio 's

Dit artikel wordt uitgelegd hoe tooconfigure een SQL Server Always On availability replica op de virtuele Azure-machines op een externe locatie Azure groepeert. Gebruik deze configuratie toosupport-noodherstel.

In dit artikel is van toepassing tooAzure virtuele Machines in de modus Resource Manager.

Hallo volgende afbeelding toont een algemene implementatie van een beschikbaarheidsgroep op Azure virtuele machines:

   ![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

In deze implementatie worden alle virtuele machines in een Azure-regio. replica's Hallo van beschikbaarheidsgroepen kunnen synchrone doorvoer met automatische failover op de SQL-1 en SQL-2 hebben. toobuild deze architectuur Zie [beschikbaarheidsgroep sjabloon of zelfstudie](virtual-machines-windows-portal-sql-availability-group-overview.md).

Deze architectuur is kwetsbaar toodowntime als ontoegankelijk hello Azure-regio. tooovercome deze kwetsbaarheid, het toevoegen van een replica in een andere Azure-regio. Hallo volgende diagram toont de nieuwe architectuur Hallo zou als volgt uitzien:

   ![Beschikbaarheid van groep DR](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

Hallo voorgaande diagram ziet u een nieuwe virtuele machine SQL 3 genoemd. SQL-3 is in een andere Azure-regio. SQL-3 wordt toohello Windows Server Failover Cluster toegevoegd. SQL-3 kan een beschikbaarheidsreplica van de groep host. Ten slotte ziet dat die hello Azure-regio voor de SQL-3 heeft een nieuwe Azure load balancer.

>[!NOTE]
> Een Azure beschikbaarheidsset is vereist wanneer meer dan één virtuele machine bevindt zich in dezelfde regio Hallo. Hallo beschikbaarheidsset is niet vereist als er slechts één virtuele machine zich in de regio hello. U kunt alleen een virtuele machine in een beschikbaarheidsset tijdens de aanmaak plaatsen. Als Hallo virtuele machine staat al in een beschikbaarheidsset bevindt, kunt u een virtuele machine voor een extra replica later toevoegen.

In deze architectuur wordt Hallo replica in de externe regio Hallo normaal gesproken geconfigureerd met asynchrone doorvoermodus voor beschikbaarheid en handmatige failover-modus.

Als replica's van beschikbaarheidsgroepen op Azure virtuele machines in verschillende Azure-regio's, moet elke regio:

* Een virtuele netwerkgateway
* Een verbinding met virtual network gateway

Hallo volgende diagram toont hoe Hallo netwerken communiceren tussen datacenters.

   ![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
>Deze architectuur leidt ertoe dat kosten voor uitgaande gegevens voor gegevens gerepliceerd tussen Azure-regio's. Zie [bandbreedte prijzen](http://azure.microsoft.com/pricing/details/bandwidth/).  

## <a name="create-remote-replica"></a>Externe replica maken

een replica in een externe Datacenter toocreate Hallo volgende stappen:

1. [Een virtueel netwerk maken in de nieuwe regio Hallo](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

1. [Een VNet-naar-VNet-verbinding configureren met hello Azure-portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).

   >[!NOTE]
   >In sommige gevallen mogelijk hebt u toouse PowerShell toocreate hello VNet-naar-VNet-verbinding. Als u verschillende Azure-accounts kan niet u Hallo verbinding configureren in Hallo-portal. In dit geval ziet, [Azure-portal configureren een VNet-naar-VNet-verbinding gebruikt Hallo](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

1. [Maken van een domeincontroller in de nieuwe regio Hallo](../../../active-directory/active-directory-new-forest-virtual-machine.md).

   Deze domeincontroller biedt verificatie als de domeincontroller Hallo in Hallo primaire site niet beschikbaar is.

1. [Maken van een virtuele machine van SQL Server in de nieuwe regio Hallo](virtual-machines-windows-portal-sql-server-provision.md).

1. [Maak een Azure load balancer in Hallo-netwerk op Hallo nieuw gebied](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

   Deze load balancer moet:

   - Zich in hetzelfde netwerk en subnet Hallo zoals Hallo van nieuwe virtuele machine.
   - Een statisch IP-adres voor Hallo beschikbaarheidsgroep-listener hebben.
   - Een back-endpool die bestaan uit alleen Hallo virtuele machines in dezelfde regio Hallo zoals Hallo load balancer bevatten.
   - Gebruik een TCP-poort test specifieke toohello IP-adres.
   - Een load balancing-regel specifieke toohello SQL Server in Hallo hebben dezelfde regio.  

1. [Toevoegen van Failover Clustering functie toohello nieuwe SQL-Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

1. [Lid worden van domein van Hallo nieuwe SQL Server toohello](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

1. [Stel Hallo nieuwe SQL Server-service-account toouse een domeinaccount](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).

1. [Hallo nieuwe SQL Server toohello Windows Server Failover Cluster toevoegen](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).

1. Maak een bron van de IP-adres op Hallo-cluster.

   U kunt Hallo IP-adres resource maken in Failoverclusterbeheer. Met de rechtermuisknop op de rol van Hallo beschikbaarheid groep, klikt u op **Resource toevoegen**, **meer bronnen**, en klik op **IP-adres**.

   ![IP-adres maken](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   Dit IP-adres als volgt configureren:

   - Hallo-netwerk van Hallo remote Datacenter gebruiken.
   - Hallo IP-adres van de nieuwe Azure load balancer Hallo toewijzen. 

1. Hallo op nieuwe SQL-Server in SQL Server Configuration Manager [inschakelen altijd op beschikbaarheidsgroepen](http://msdn.microsoft.com/library/ff878259.aspx).

1. [Open firewallpoorten op de nieuwe SQL-Server Hallo](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

   Hallo poortnummers moet u tooopen is afhankelijk van uw omgeving. Open poorten voor Hallo mirroring-eindpunt en Azure load balancer health test.

1. [Toevoegen van een beschikbaarheidsgroep van de replica-toohello op Hallo nieuwe SQL-Server](http://msdn.microsoft.com/library/hh213239.aspx).

   Voor een replica in een externe Azure-regio, moet u deze voor asynchrone replicatie met handmatige failover instellen.  

1. Hallo IP-adres resource toevoegen als een afhankelijkheid voor Hallo listener client access point (netwerknaam) cluster.

   Hallo volgende schermafbeelding ziet u een correct geconfigureerde clusterbron voor IP-adres:

   ![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   >Hallo clusterbrongroep bevat beide IP-adressen. Beide IP-adressen zijn afhankelijkheden voor het Hallo-listener client access point. Gebruik Hallo **of** operator in Hallo afhankelijkheid clusterconfiguratie.

1. [Hallo Clusterparameters instellen in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).

Hallo PowerShell-script uitvoeren met de clusternetwerknaam hello, IP-adres en testpoort die u hebt geconfigureerd op Hallo load balancer in de nieuwe regio Hallo.

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a>Set-verbinding voor meerdere subnetten

Hallo replica in de externe Datacenter Hallo is onderdeel van de beschikbaarheidsgroep hello, maar het is in een ander subnet. Als deze replica de primaire replica hello wordt, optreden verbindingstime toepassing. Dit gedrag is hetzelfde als een lokale beschikbaarheidsgroep in een implementatie met meerdere subnetten Hallo. tooallow verbindingen van clienttoepassingen, Hallo clientverbinding bijwerken of cachegebruik op Hallo cluster netwerknaambron naamomzetting configureren.

Bij voorkeur bijwerken Hallo client verbinding tekenreeksen tooset `MultiSubnetFailover=Yes`. Zie [verbinding te maken met MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).

Als u verbindingsreeksen Hallo niet wijzigen, kunt u de naam resolutie caching kunt configureren. Zie [time-outs voor verbindingen in meerdere subnetten beschikbaarheidsgroep](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).

## <a name="fail-over-tooremote-region"></a>Failover tooremote regio

tootest listener connectiviteit toohello externe regio, u kunt een failover Hallo replica toohello externe regio. Hallo replica asynchroon is, is failover kwetsbaar toopotential gegevens verloren gaan. toofail via zonder gegevensverlies, Hallo beschikbaarheid modus toosynchronous wijzigen en Hallo failover-modus tooautomatic ingesteld. Gebruik Hallo stappen te volgen:

1. In **Objectverkenner**, verbinding toohello exemplaar van SQL Server die als host fungeert voor de primaire replica Hallo.
1. Onder **AlwaysOn Availability Groups**, **beschikbaarheidsgroepen**, met de rechtermuisknop op de beschikbaarheidsgroep en klik op **eigenschappen**.
1. Op Hallo **algemene** pagina onder **Beschikbaarheidsreplica**, set Hallo secundaire replica in Hallo DR site toouse **synchroon doorvoeren** beschikbaarheidsmodus en **Automatische** failover-modus.
1. Als u een secundaire replica in dezelfde site als de primaire replica voor hoge beschikbaarheid, stelt u deze replica te**asynchrone doorvoeren** en **handmatige**.
1. Klik op OK.
1. In **Objectverkenner**, met de rechtermuisknop op het Hallo-beschikbaarheidsgroep en klikt u op **Dashboard weergeven**.
1. Controleer op Hallo dashboard dat Hallo replica op Hallo DR-site is gesynchroniseerd.
1. In **Objectverkenner**, met de rechtermuisknop op het Hallo-beschikbaarheidsgroep en klikt u op **Failover...** . SQL Server Management Studios Hiermee opent u een wizard toofail via SQL Server.  
1. Klik op **volgende**, en selecteer Hallo SQL Server-exemplaar op Hallo DR-site. Klik op **volgende** opnieuw.
1. Verbinding maken met SQL Server-exemplaar toohello op Hallo DR-site en klik op **volgende**.
1. Op Hallo **samenvatting** pagina, Hallo instellingen controleren en klikt u op **voltooien**.

Nadat de verbinding test, Hallo primaire replica back tooyour primaire gegevens center en instellingen voor het Hallo beschikbaarheid modus back tootheir normale operationele te verplaatsen. Hallo ziet volgende tabel u Hallo normale operationele instellingen voor Hallo-architectuur in dit document beschreven:

| Locatie | Server-exemplaar | Rol | De Beschikbaarheidsmodus | Failover-modus
| ----- | ----- | ----- | ----- | -----
| Primaire Datacenter | SQL-1 | Primair | Synchrone | Automatisch
| Primaire Datacenter | SQL-2 | Secundair | Synchrone | Automatisch
| Secundaire of door de externe Datacenter | SQL-3 | Secundair | Asynchrone | Handmatig


### <a name="more-information-about-planned-and-forced-manual-failover"></a>Meer informatie over de geplande en geforceerde handmatige failover

Zie de volgende onderwerpen Hallo voor meer informatie:

- [Voer een geplande handmatige Failover van een beschikbaarheidsgroep (SQL Server)](http://msdn.microsoft.com/library/hh231018.aspx)
- [Voer een geforceerde handmatige Failover van een beschikbaarheidsgroep (SQL Server)](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a>Aanvullende koppelingen

* [Altijd op beschikbaarheidsgroepen](http://msdn.microsoft.com/library/hh510230.aspx)
* [Virtuele Machines in Azure](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [Azure Load Balancers](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [Azure Beschikbaarheidssets](../manage-availability.md)
