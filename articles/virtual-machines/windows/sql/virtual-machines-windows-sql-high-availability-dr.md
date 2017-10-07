---
title: aaaHigh beschikbaarheid en herstel na noodgevallen voor SQL Server | Microsoft Docs
description: "Een beschrijving van de hello verschillende soorten HADR strategieën voor SQL Server wordt uitgevoerd in Azure Virtual Machines."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 53981f7e-8370-4979-b26a-93a5988d905f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: mikeray
ms.openlocfilehash: 2b62d8b30520952ba6b7da7177a2c2de95bea8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-and-disaster-recovery-for-sql-server-in-azure-virtual-machines"></a>Maximale beschikbaarheid en herstel na noodgeval voor SQL Server in SQL Server Virtual Machine

Microsoft Azure virtuele machines (VM's) met SQL Server kunt lagere Hallo kosten van een hoge beschikbaarheid en noodherstel (HADR) database hersteloplossing. De meeste HADR van SQL Server-oplossingen worden ondersteund in Azure virtuele machines, als Azure alleen-lezen en als de hybride-oplossingen. In een Azure-only-oplossing, Hallo gehele HADR systeem wordt uitgevoerd in Azure. In een hybride-configuratie van Hallo oplossing wordt uitgevoerd in Azure en Hallo andere onderdeel wordt uitgevoerd op lokale in uw organisatie. Hallo flexibiliteit van hello Azure-omgeving kunt u toomove geheel of gedeeltelijk tooAzure toosatisfy Hallo budget en HADR vereisten van uw SQL Server-database systemen.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="understanding-hello-need-for-an-hadr-solution"></a>Understanding Hallo behoefte aan een oplossing HADR
Is tooyou tooensure dat uw databasesysteem bezit Hallo HADR mogelijkheden die Hallo service level agreement (SLA) vereist. Hallo feit die Azure mechanismen voor hoge beschikbaarheid biedt, zoals service herstel voor cloudservices en herstel foutdetectie voor virtuele Machines, kan niet zichzelf garanderen u voldoen aan de SLA Hallo gewenst. Deze mechanismen beveiligen Hallo hoge beschikbaarheid van virtuele machines hello, maar niet Hallo beschikbaarheid van SQL Server uitgevoerd binnen Hallo virtuele machines. Is het mogelijk voor Hallo SQL Server-exemplaar toofail Hallo VM is online en in orde. Bovendien zelfs Hallo hoge beschikbaarheid mechanismen verstrekt door Azure toestaan uitvaltijd Hallo VMs vanwege tooevents zoals het herstellen van de software- of hardwarestoringen en updates van besturingssystemen.

Bovendien geografisch redundante opslag (GRS) in Azure, dit wordt geïmplementeerd met een functie geo-replicatie, mogelijk niet een voldoende noodherstel voor uw databases. Omdat geo-replicatie worden gegevens asynchroon verzendt, kunnen u recente updates verloren in Hallo-gebeurtenis van noodherstel. Meer informatie over de beperkingen van geo-replicatie worden behandeld in Hallo [Geo-replicatie wordt niet ondersteund voor gegevens en logboekbestanden op afzonderlijke schijven](#geo-replication-support) sectie.

## <a name="hadr-deployment-architectures"></a>HADR implementatie architecturen
SQL Server HADR technologieën die worden ondersteund in Azure omvatten:

* [Altijd op beschikbaarheidsgroepen](https://technet.microsoft.com/library/hh510230.aspx)
* [Altijd op de failovercluster-exemplaren](https://technet.microsoft.com/library/ms189134.aspx)
* [Back-upfunctie voor logboekbestanden](https://technet.microsoft.com/library/ms187103.aspx)
* [SQL Server-back-up en herstel met Azure Blob Storage-Service](https://msdn.microsoft.com/library/jj919148.aspx)
* [Databasespiegeling](https://technet.microsoft.com/library/ms189852.aspx) - in SQL Server 2016 afgeschaft

Het is mogelijk toocombine Hallo technologieën bij elkaar tooimplement een SQL Server-oplossing met hoge beschikbaarheid en -mogelijkheden voor herstel na noodgevallen. Afhankelijk van het Hallo-technologie die u gebruikt, moet een hybride implementatie mogelijk een VPN-tunnel Hello virtuele Azure-netwerk. Hallo in de volgende secties ziet u enkele Hallo voorbeeld implementatie architecturen.

## <a name="azure-only-high-availability-solutions"></a>Azure alleen-lezen: oplossingen voor hoge beschikbaarheid

U kunt een oplossing voor hoge beschikbaarheid hebben voor SQL Server op het databaseniveau van een met AlwaysOn-beschikbaarheidsgroepen - beschikbaarheidsgroepen aangeroepen. U kunt ook maken een oplossing voor hoge beschikbaarheid op het niveau van een exemplaar met altijd op Failover Cluster Instances - failover cluster-exemplaren. Voor aanvullende redundantie, kunt u redundantie op beide niveaus maken door het maken van beschikbaarheidsgroepen op failover cluster-exemplaren. 

| Technologie | Voorbeeld architecturen |
| --- | --- |
| **Beschikbaarheidsgroepen** |Beschikbaarheidsreplica's uitgevoerd in de virtuele machines in Azure Hallo dezelfde regio bieden hoge beschikbaarheid. U moet tooconfigure een domeincontroller VM, omdat Windows failover clustering een Active Directory-domein vereist.<br/> ![Beschikbaarheidsgroepen](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_ha_always_on.gif)<br/>Zie voor meer informatie [beschikbaarheidsgroepen configureren in Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups.md). |
| **Failover cluster-exemplaren** |Failover Cluster exemplaren (FCI), die gedeelde opslag is vereist, kunnen op verschillende manieren 3 worden gemaakt.<br/><br/>1. Een failovercluster met twee knooppunten met behulp van gekoppelde opslag in Azure VM's met [Windows Server 2016 opslagruimten Direct \(S2D\) ](virtual-machines-windows-portal-sql-create-failover-cluster.md) tooprovide een op software gebaseerde virtueel SAN.<br/><br/>2. Twee knooppunten failovercluster uitgevoerd in Azure VM's met opslag ondersteund door een clustering oplossing van derden. Zie voor een specifieke voorbeeld die gebruikmaakt van SIOS DataKeeper [hoge beschikbaarheid voor een bestandsshare met behulp van failover clustering en 3e softwareleveranciers SIOS DataKeeper](https://azure.microsoft.com/blog/high-availability-for-a-file-share-using-wsfc-ilb-and-3rd-party-software-sios-datakeeper/).<br/><br/>3. Een failovercluster met twee knooppunten uitgevoerd in Azure VM's met externe iSCSI-doel gedeelde blokopslag via ExpressRoute. NetApp persoonlijke opslag (NPS) wordt bijvoorbeeld een iSCSI-doel via ExpressRoute met Equinix tooAzure virtuele machines.<br/><br/>Voor gedeelde opslag van derden en oplossingen voor replicatie van gegevens, moet u contact op met leverancier van de Hallo voor alle gegevens van de gerelateerde tooaccessing problemen op failover.<br/><br/>Houd er rekening mee dat als u met FCI boven [Azure File storage](https://azure.microsoft.com/services/storage/files/) wordt nog niet ondersteund, omdat deze oplossing geen gebruik van Premium-opslag. Wij werken toosupport dit snel. |

## <a name="azure-only-disaster-recovery-solutions"></a>Azure alleen-lezen: oplossingen voor herstel na noodgevallen
U kunt een noodherstel voor uw SQL Server-databases in Azure met behulp van beschikbaarheidsgroepen, databasespiegeling of back-up en herstellen met de storage-blobs.

| Technologie | Voorbeeld architecturen |
| --- | --- |
| **Beschikbaarheidsgroepen** |De beschikbaarheidsreplica is uitgevoerd in meerdere datacenters in Azure VM's voor herstel na noodgevallen. Deze oplossing regio-overschrijdende beschermd tegen storing van de volledige site. <br/> ![Beschikbaarheidsgroepen](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_alwayson.png)<br/>Binnen een regio moeten alle replica's binnen Hallo dezelfde cloudservice en Hallo hetzelfde VNet. Omdat elke regio een afzonderlijk VNet, vereist deze oplossingen VNet tooVNet connectiviteit. Zie voor meer informatie [Azure-portal configureren een VNet-naar-VNet-verbinding gebruikt Hallo](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md). Zie voor gedetailleerde instructies [een SQL Server-beschikbaarheidsgroep configureren op Azure Virtual Machines in verschillende regio's](virtual-machines-windows-portal-sql-availability-group-dr.md).|
| **Databasespiegeling** |Principal en gespiegelde en servers die in verschillende datacenters voor herstel na noodgevallen. U moet implementeren met behulp van servercertificaten omdat active directory-domein kan niet meerdere datacenters omvatten.<br/>![Databasespiegeling](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_dbmirroring.gif) |
| **Back-up en herstel met Azure Blob Storage-Service** |Productiedatabases back-ups rechtstreeks tooblob opslag in een ander datacenter voor herstel na noodgevallen.<br/>![Back-up en herstel](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_backup_restore.gif)<br/>Zie voor meer informatie [back-up en herstel voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="hybrid-it-disaster-recovery-solutions"></a>Hybride IT: Noodhersteloplossingen
Als u beschikt over van een noodherstel voor uw SQL Server-databases in een hybride IT-omgeving met beschikbaarheidsgroepen, databasespiegeling-upfunctie voor logboekbestanden en back-up en herstellen met de opslag van de Azure-blog.

| Technologie | Voorbeeld architecturen |
| --- | --- |
| **Beschikbaarheidsgroepen** |Sommige beschikbaarheidsreplica's uitgevoerd in de Azure VM's en andere replica's met on-premises voor herstel na noodgevallen voor cross-site. Hallo productiesite kan worden on-premises of in een Azure-datacenter.<br/>![Beschikbaarheidsgroepen](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_alwayson.gif)<br/>Omdat alle beschikbaarheidsreplica's moeten in Hallo hetzelfde failovercluster hello cluster moet span beide netwerken (een meerdere subnetten failover-cluster). Deze configuratie is vereist voor een VPN-verbinding tussen Azure en Hallo on-premises netwerk.<br/><br/>Voor geslaagde noodherstel van uw database, moet u ook een replicadomeincontroller op Hallo disaster recovery site installeren.<br/><br/>Het is mogelijk toouse Hallo Replica Wizard toevoegen in SSMS tooadd een Azure replica tooan bestaande AlwaysOn-beschikbaarheidsgroep. Zie voor meer informatie, zelfstudie: uw tooAzure AlwaysOn-beschikbaarheidsgroep uitbreiden. |
| **Databasespiegeling** |Een partner uitgevoerd in een virtuele machine van Azure en Hallo andere on-premises voor noodherstel van cross-site met behulp van servercertificaten uitgevoerd. Partners hoeft geen toobe in hetzelfde Active Directory-domein Hallo en er is geen VPN-verbinding vereist.<br/>![Databasespiegeling](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_dbmirroring.gif)<br/>Een andere database mirroring scenario omvat één partner uitgevoerd in een virtuele machine van Azure en hello andere uitgevoerd on-premises in Hallo dezelfde Active Directory-domein voor herstel na noodgevallen voor cross-site. Een [VPN-verbinding tussen hello Azure virtuele netwerk en Hallo on-premises netwerk](../../../vpn-gateway/vpn-gateway-site-to-site-create.md) is vereist.<br/><br/>Voor geslaagde noodherstel van uw database, moet u ook een replicadomeincontroller op Hallo disaster recovery site installeren. |
| **Back-upfunctie voor logboekbestanden** |Één server worden uitgevoerd in een virtuele machine van Azure en Hallo andere on-premises voor herstel na noodgevallen voor cross-site uitgevoerd. Back-upfunctie voor logboekbestanden hangt af van het Windows-bestanden delen, zodat een VPN-verbinding tussen Hallo virtuele Azure-netwerk en Hallo lokale netwerk is vereist.<br/>![Back-upfunctie voor logboekbestanden](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_log_shipping.gif)<br/>Voor geslaagde noodherstel van uw database, moet u ook een replicadomeincontroller op Hallo disaster recovery site installeren. |
| **Back-up en herstel met Azure Blob Storage-Service** |Een on-premises productiedatabases back-ups rechtstreeks tooAzure blob storage voor herstel na noodgevallen.<br/>![Back-up en herstel](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_backup_restore.gif)<br/>Zie voor meer informatie [back-up en herstel voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="important-considerations-for-sql-server-hadr-in-azure"></a>Belangrijke aandachtspunten voor SQL Server HADR in Azure
Azure virtuele machines, opslag en netwerken hebben andere operationele kenmerken dan een on-premises, niet-gevirtualiseerde IT-infrastructuur. Een succesvolle implementatie van een oplossing voor HADR SQL Server in Azure, moet u inzicht in deze verschillen en ontwerp van uw oplossing tooaccommodate ze.

### <a name="high-availability-nodes-in-an-availability-set"></a>Knooppunten voor hoge beschikbaarheid in een beschikbaarheidsset
Beschikbaarheidssets in Azure, kunt u tooplace Hallo hoge beschikbaarheid knooppunten in afzonderlijke domeinen met fouten (FDs) en Update-domeinen (UDs). Voor Azure Virtual machines toobe geplaatst in Hallo dezelfde beschikbaarheidsset, moet u implementeren ze Hallo moeten dezelfde cloudservice. Alleen knooppunten in dezelfde cloudservice kan deelnemen Hallo Hallo dezelfde beschikbaarheidsset. Zie voor meer informatie [beheren Hallo beschikbaarheid van virtuele Machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="failover-cluster-behavior-in-azure-networking"></a>Gedrag van de failover-cluster in Azure-netwerken
niet-RFC-compatibele DHCP-service in Azure Hallo kan leiden tot Hallo maken van een bepaalde toofail failover cluster configuraties, vanwege toohello clusternetwerknaam een dubbel IP-adres wordt toegewezen, zoals Hallo hetzelfde IP-adressen als een van de clusterknooppunten Hallo. Dit is een probleem wanneer u beschikbaarheidsgroepen gebruikt, die afhankelijk van de functie failover clustering van Hallo Windows is implementeren.

Houd rekening met Hallo scenario als een cluster met twee knooppunten wordt gemaakt en online is gekomen:

1. Hallo-cluster online komt en vervolgens knooppunt1 een dynamisch toegewezen IP-adres voor de clusternetwerknaam Hallo-aanvragen.
2. Er is geen IP-adres behalve knooppunt1 eigen IP-adres wordt bepaald door Hallo DHCP-service, omdat de DHCP-service Hallo herkent die Hallo aanvraag afkomstig is van knooppunt1 zelf.
3. Windows detecteert dat een dubbel adres tooNODE1 zowel toohello netwerknaam van failover-cluster is toegewezen en toocome online clustergroep Hallo-standaard is mislukt.
4. Hallo standaardclustergroep verplaatst tooNODE2 die wordt beschouwd knooppunt1 van IP-adres als Hallo cluster-IP-adres en Hallo standaardclustergroep online brengt.
5. Wanneer Knooppunt2 tooestablish connectiviteit met knooppunt1 probeert, laat pakketten die gericht zijn op knooppunt1 nooit Knooppunt2 omdat hiermee het knooppunt1 van IP-adres tooitself wordt opgelost. Knooppunt2 kan geen verbinding maken met knooppunt1, vervolgens quorum verliest en Hallo cluster wordt afgesloten.
6. In de tussentijd Hallo knooppunt1 pakketten tooNODE2 kunt verzenden, maar Knooppunt2 kan niet antwoorden. Knooppunt1 quorum verliest en Hallo cluster wordt afgesloten.

Dit scenario kunt u voorkomen door het toewijzen van een ongebruikt statische IP-adres, zoals een link-local IP-adres zoals 169.254.1.1, toohello clusternetwerknaam in volgorde toobring Hallo clusternetwerknaam online. toosimplify dit verwerken, Zie [Windows configureren van failover-cluster in Azure voor beschikbaarheidsgroepen](http://social.technet.microsoft.com/wiki/contents/articles/14776.configuring-windows-failover-cluster-in-windows-azure-for-alwayson-availability-groups.aspx).

Zie voor meer informatie [beschikbaarheidsgroepen configureren in Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups.md).

### <a name="availability-group-listener-support"></a>Beschikbaarheid van groep listener-ondersteuning
Beschikbaarheid beschikbaarheidsgroeplisteners worden ondersteund op Azure VM's met Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 en Windows Server 2016. Deze ondersteuning wordt mogelijk gemaakt door Hallo gebruik van netwerktaakverdeling-eindpunten die zijn ingeschakeld op Hallo Azure Virtual machines die beschikbaarheid groepsknooppunten. U moet stappen speciale configuratie voor Hallo listeners toowork voor zowel clienttoepassingen die worden uitgevoerd in Azure, evenals die lokaal wordt uitgevoerd.

Er zijn twee manieren voor het instellen van de listener: externe (openbaar) of interne. Hallo externe (openbare)-listener gebruikt een internetverbinding de load balancer en is gekoppeld met een openbare virtuele IP-adres (VIP) die toegankelijk is via internet Hallo. Een interne listener maakt gebruik van een interne load balancer en alleen ondersteunt clients binnen hetzelfde virtuele netwerk Hallo. Voor een load balancer type, moet u Direct Server Return inschakelen. 

Als Hallo beschikbaarheidsgroep omvat meerdere Azure subnetten (zoals een implementatie die over Azure-regio's), verbindingsreeks Hallo-client moet bevatten '**MultisubnetFailover = True**'. Dit resulteert in parallelle verbinding pogingen toohello replica's in verschillende subnetten Hallo. Zie voor instructies over het instellen van een listener

* [Een ILB-listener voor beschikbaarheidsgroepen configureren in Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md).
* [Een externe-listener voor beschikbaarheidsgroepen configureren in Azure](../classic/ps-sql-ext-listener.md).

U kunt nog steeds tooeach beschikbaarheidsreplica afzonderlijk verbinden door verbinding te maken rechtstreeks toohello service-exemplaar. Bovendien aangezien beschikbaarheidsgroepen achterwaarts compatibel met databasespiegeling clients, kunt u toohello beschikbaarheidsreplica's zoals partners voor databasespiegeling, zolang het Hallo-replica's zijn geconfigureerd vergelijkbare toodatabase spiegelen:

* Eén primaire replica en één secundaire replica
* Hallo secundaire replica is geconfigureerd als niet-leesbare (**leesbare secundaire** optie ingesteld te**Nee**)

Een voorbeeld van de client-verbindingsreeks die overeenkomt met toothis database mirroring-achtige configuratie met behulp van de ADO.NET- of SQL Server Native Client lager is dan:

    Data Source=ReplicaServer1;Failover Partner=ReplicaServer2;Initial Catalog=AvailabilityDatabase;

Zie voor meer informatie over clientverbindingen controleren:

* [Met behulp van Connection String trefwoorden met SQL Server Native Client](https://msdn.microsoft.com/library/ms130822.aspx)
* [Verbinding maken met Clients tooa Database Mirroring sessie (SQL Server)](https://technet.microsoft.com/library/ms175484.aspx)
* [Verbinding maken met tooAvailability Listener in hybride IT-groep](http://blogs.msdn.com/b/sqlalwayson/archive/2013/02/14/connecting-to-availability-group-listener-in-hybrid-it.aspx)
* [Beschikbaarheidsgroep-Listeners, clientconnectiviteit en Failover van de toepassing (SQL Server)](https://technet.microsoft.com/library/hh213417.aspx)
* [Met behulp van verbindingsreeksen Database Mirroring met beschikbaarheidsgroepen](https://technet.microsoft.com/library/hh213417.aspx)

### <a name="network-latency-in-hybrid-it"></a>Netwerklatentie in hybride IT
U moet uw oplossing HADR met Hallo verondersteld dat er perioden met hoge netwerklatentie tussen uw on-premises netwerk en Azure implementeren. Bij het implementeren van replica's tooAzure, moet u asynchrone doorvoer in plaats van synchrone doorvoer voor Hallo Synchronisatiemodus. Wanneer database mirroring servers implementeren zowel on-premises en in Azure, kunt u Hallo krachtige modus gebruiken in plaats van Hallo hoge veiligheid modus.

### <a name="geo-replication-support"></a>Geo-replicatie-ondersteuning
Geo-replicatie in Azure-schijven biedt geen ondersteuning voor het Hallo-gegevensbestand en logboekbestand Hallo dezelfde database toobe op afzonderlijke schijven opgeslagen. GRS repliceert wijzigingen op elke schijf afzonderlijk en asynchroon. Dit mechanisme zorgt ervoor dat Hallo schrijven volgorde binnen een enkele schijf op Hallo geogerepliceerde kopie, maar niet tussen geogerepliceerde kopieën van meerdere schijven. Als u een database toostore het gegevensbestand en een logboekbestand op afzonderlijke schijven configureert, hersteld Hallo schijven na een noodgeval kan een meer recente kopie van het gegevensbestand Hallo dan Hallo-logboekbestand, welke einden Hallo vooraf geschreven logboek in SQL Server en Hallo ACID bevatten Eigenschappen van transacties. Als u geen Hallo optie toodisable geo-replicatie op Hallo storage-account, moet u alle gegevens behouden en logboekbestanden voor een bepaalde database op Hallo dezelfde schijf. Als u meer dan één schijf vanwege de grootte van de database Hallo toohello gebruiken moet, moet u een van de noodhersteloplossingen hello tooensure gegevensredundantie bovenstaande toodeploy.

## <a name="next-steps"></a>Volgende stappen
Als u een virtuele machine van Azure met SQL Server toocreate nodig hebt, raadpleegt u [inrichten van een virtuele Machine van SQL Server op Azure](virtual-machines-windows-portal-sql-server-provision.md).

tooget hello optimale prestaties van SQL Server wordt uitgevoerd op een Azure-VM Zie Hallo richtlijnen in [Best Practices prestaties for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).

Voor andere onderwerpen die betrekking toorunning SQL-Server in Azure VM's hebben, Zie [SQL Server op Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).

### <a name="other-resources"></a>Meer informatie
* [Een nieuw Active Directory-forest installeren in Azure](../../../active-directory/active-directory-new-forest-virtual-machine.md)
* [Failover-Cluster maken voor beschikbaarheidsgroepen in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a)

