---
title: aaaSQL Server FCI - Azure Virtual Machines | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe toocreate Failover-Cluster van SQL Server-instantie op Azure Virtual Machines.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a>Exemplaar van SQL Server-failovercluster configureren op virtuele Machines in Azure

Dit artikel wordt uitgelegd hoe toocreate een SQL Serverfailover Cluster Instance (FCI) op Azure virtuele machines in de Resource Manager-model. Deze oplossing gebruikt [Windows Server 2016 Datacenter edition opslagruimten Direct \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) als een op software gebaseerde virtueel SAN waarmee Hallo opslag (gegevensschijven) gesynchroniseerd tussen Hallo knooppunten (virtuele Azure-machines) in een Windows-Cluster. S2D is nieuw in Windows Server 2016.

Hallo volgende diagram ziet u de volledige oplossing Hallo op Azure virtuele machines:

![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

Hallo voorgaande diagram laat zien welke:

- Twee virtuele Azure-machines in een Windows-failovercluster. Wanneer een virtuele machine in een failovercluster wordt ook wel een *clusterknooppunt*, of *knooppunten*.
- Elke virtuele machine heeft twee of meer gegevensschijven.
- S2D hello gegevens op Hallo gegevensschijf gesynchroniseerd en geeft de opslag Hallo gesynchroniseerd als een opslaggroep.
- Hallo opslaggroep geeft een cluster shared volume (CSV) toohello failover-cluster.
- functie Hallo FCI van SQL Server-cluster maakt gebruik van Hallo CSV voor Hallo gegevensstations.
- Een Azure-load balancer toohold Hallo IP-adres voor Hallo FCI van SQL Server.
- Een Azure beschikbaarheidsset bevat alle Hallo-resources.

   >[!NOTE]
   >Alle Azure-resources zijn in Hallo diagram zijn in Hallo dezelfde resourcegroep.

Zie voor meer informatie over S2D [Windows Server 2016 Datacenter edition opslagruimten Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).

S2D ondersteunt twee soorten architecturen - geconvergeerde en hyper-geconvergeerde. Hallo-architectuur in dit document is hyper-geconvergeerde. Een hyper-geconvergeerde infrastructuur plaatsen Hallo opslag op Hallo van dezelfde servers die host Hallo geclusterde toepassing. In deze architectuur is Hallo opslag op elk knooppunt FCI van SQL Server.

### <a name="example-azure-template"></a>Voorbeeld van de Azure-sjabloon

U kunt Hallo hele oplossing in Azure maken van een sjabloon. Een voorbeeld van een sjabloon is beschikbaar in GitHub hello [Azure-Snelstartsjablonen](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad). In dit voorbeeld is niet ontworpen of getest voor een specifieke werkbelasting. U kunt op een SQL Server-FCI Hallo sjabloon toocreate uitvoeren met S2D opslag verbonden tooyour domein. U kunt evalueren Hallo sjabloon en aanpassen voor uw doeleinden.

## <a name="before-you-begin"></a>Voordat u begint

Er zijn enkele dingen die u moet tooknow en een aantal dingen die u nodig hebt voldaan voordat u doorgaat.

### <a name="what-tooknow"></a>Welke tooknow
U hebt een operationeel inzicht in Hallo technologieën te volgen:

- [Windows cluster-technologieën](http://technet.microsoft.com/library/hh831579.aspx)
-  [Exemplaren van SQL Server-failovercluster](http://msdn.microsoft.com/library/ms189134.aspx).

Bovendien hebt u een algemeen begrip van Hallo technologieën te volgen:

- [Hyper-geconvergeerde oplossing met behulp van opslagruimten Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [Azure-resourcegroepen](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a>Welke toohave

Voordat u Hallo-instructies in dit artikel, hebt u al:

- Een Microsoft Azure-abonnement.
- Een Windows-domein op virtuele machines in Azure.
- Een account met machtigingen toocreate objecten in hello Azure virtuele machine.
- Een virtuele Azure-netwerk en subnet met voldoende IP-adresruimte voor Hallo volgende onderdelen:
   - Beide virtuele machines.
   - IP-adres voor Hallo failover-cluster.
   - Een IP-adres voor elke FCI.
- DNS wordt geconfigureerd op Hallo Azure-netwerk, wijzen toohello-domeincontrollers.

Met deze vereisten is voldaan, kunt u doorgaan met het bouwen van uw failover-cluster. de eerste stap Hallo is toocreate Hallo virtuele machines.

## <a name="step-1-create-virtual-machines"></a>Stap 1: Virtuele machines maken

1. Meld u bij toohello [Azure-portal](http://portal.azure.com) met uw abonnement.

1. [Maken van een Azure beschikbaarheidsset](../tutorial-availability-sets.md).

   Hallo beschikbaarheid instellen groepen virtuele machines tussen domeinen met fouten en domeinen bijwerken. Hallo beschikbaarheidsset zorgt ervoor dat uw toepassing is niet van invloed op een individuele foutpunten, zoals het Hallo-netwerkswitch of Hallo power-eenheid van een rek met servers.

   Als u geen Hallo resourcegroep hebt gemaakt voor uw virtuele machines, moet u het doen wanneer u een Azure beschikbaarheidsset maakt. Als u hello Azure portal toocreate hello beschikbaarheidsset, Hallo volgende stappen:

   - Klik in hello Azure-portal, op  **+**  tooopen hello Azure Marketplace. Zoeken naar **beschikbaarheidsset**.
   - Klik op **beschikbaarheidsset**.
   - Klik op **Create**.
   - Op Hallo **beschikbaarheidsset maken** blade set Hallo volgende waarden:
      - **Naam**: een naam voor de beschikbaarheidsset Hallo.
      - **Abonnement**: uw Azure-abonnement.
      - **Resourcegroep**: als u wilt dat toouse een bestaande groep, klikt u op **gebruik bestaande** en selecteer Hallo groep uit de vervolgkeuzelijst Hallo. Kies anders **nieuw** en typ een naam voor de groep Hallo.
      - **Locatie**: Stel Hallo locatie waar u van plan toocreate bent in uw virtuele machines.
      - **Fault-domeinen**: Hallo-standaard (3).
      - **Bijwerken van domeinen**: Hallo-standaard (5).
   - Klik op **maken** toocreate hello beschikbaarheidsset.

1. Hallo virtuele machines maken in beschikbaarheidsset Hallo.

   Twee SQL Server virtuele machines inrichten in hello Azure beschikbaarheidsset. Zie voor instructies [een SQL Server-machine inrichten in hello Azure-portal](virtual-machines-windows-portal-sql-server-provision.md).

   Plaats beide virtuele machines:

   - In Hallo is dezelfde Azure-resourcegroep die uw beschikbaarheidsset.
   - Op Hallo netwerk als uw domeincontroller.
   - In een subnet met voldoende IP-adresruimte voor virtuele machines en alle Failoverclusterinstanties die u uiteindelijk op dit cluster kan gebruiken.
   - In hello Azure beschikbaarheidsset.   

      >[!IMPORTANT]
      >U niet instellen of wijzigen van de beschikbaarheidsset nadat een virtuele machine is gemaakt.

   Een afbeelding kiezen uit hello Azure Marketplace. U kunt een Marketplace installatiekopie met die Windows Server en SQL Server of alleen Hallo Windows Server bevat. Zie voor meer informatie [overzicht van SQL Server op Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)

   Hallo officiële SQL Server-installatiekopieën in hello Azure-galerie omvatten een geïnstalleerde SQL Server-exemplaar plus Hallo SQL Server-installatie van software en Hallo sleutel.

   Hallo juiste installatiekopie volgens toohow gewenste toopay voor SQL Server-licentie Hallo kiezen:

   - **Betalen per gebruik licentieverlening**: Hallo per minuut kosten van deze installatiekopieën omvat Hallo SQL Server-licentieverlening:
      - **SQL Server 2016 Enterprise op Windows Server Datacenter 2016**
      - **SQL Server 2016 Standard op Windows Server Datacenter 2016**
      - **SQL Server 2016 Developer op Windows Server Datacenter 2016**

   - **Bring-your-eigenaar-license (BYOL)**

      - **{BYOL} SQL Server 2016 Enterprise op Windows Server Datacenter 2016**
      - **{BYOL} SQL Server 2016 Standard op Windows Server Datacenter 2016**

   >[!IMPORTANT]
   >Nadat u Hallo virtuele machine hebt gemaakt, verwijdert u Hallo vooraf geïnstalleerde zelfstandige SQL Server-exemplaar. U gebruikt Hallo vooraf geïnstalleerde SQL Server media toocreate Hallo FCI van SQL Server nadat u Hallo failover-cluster en S2D configureren.

   U kunt ook Azure Marketplace-installatiekopieën gebruiken met NET Hallo-besturingssysteem. Kies een **Windows Server 2016 Datacenter** installatiekopie en Hallo FCI van SQL Server te installeren nadat u het failovercluster Hallo en S2D configureren. Deze installatiekopie bevat geen SQL Server-installatiemedia. Hallo-installatiemedia plaatsen op een locatie waar u Hallo SQL Server-installatie voor elke server kunt uitvoeren.

1. Nadat uw virtuele machines is gemaakt in Azure, moet u tooeach virtuele machine verbinden met RDP.

   Als u tooa virtuele machine voor het eerst verbinding met RDP, desgewenst Hallo computer tooallow deze PC toobe op Hallo netwerk kunnen worden gedetecteerd. Klik op **Ja**.

1. Als u van een virtuele machine op basis van SQL Server-installatiekopieën hello gebruikmaakt, verwijdert u Hallo SQL Server-exemplaar.

   - In **programma's en onderdelen**, met de rechtermuisknop op **Microsoft SQL Server 2016 (64-bits)** en klik op **verwijderen/wijzigen**.
   - Klik op **verwijderen**.
   - Selecteer het standaardexemplaar Hallo.
   - Verwijder alle onderdelen onder **Database Engine-Services**. Verwijder niet **gedeelde onderdelen**. Zie de volgende afbeelding Hallo:

      ![Onderdelen verwijderen](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - Klik op **volgende**, en klik vervolgens op **verwijderen**.

1. <a name="ports"></a>Open Hallo firewall-poorten.

   Open op elke virtuele machine, Hallo poorten op Hallo Windows Firewall te volgen.

   | Doel | TCP-poort | Opmerkingen
   | ------ | ------ | ------
   | SQL Server | 1433 | Normale poort voor standaardexemplaren van SQL Server. Als u een installatiekopie van het uit de galerie Hallo gebruikt, worden deze poort wordt automatisch geopend.
   | De statuscontrole | 59999 | Een open TCP-poort. In een later stadium Hallo load balancer configureren [health test](#probe) en Hallo cluster toouse deze poort.  

1. Opslag toohello virtuele machine toevoegen. Zie voor gedetailleerde informatie [opslag toevoegen](../../../storage/common/storage-premium-storage.md).

   Beide virtuele machines nodig ten minste twee schijven.

   Koppel onbewerkte schijven - geen NTFS-geformatteerde schijven.
      >[!NOTE]
      >Als u NTFS-geformatteerde schijven koppelt, kunt u alleen S2D inschakelen met geen controle van de schijf in aanmerking komt.  

   Koppel een minimum van twee Premium-opslag (SSD-schijven) tooeach VM. Het is raadzaam ten minste P30 schijven (1 TB).

   Set-hostcaching te**alleen-lezen**.

   Hallo opslagcapaciteit die u gebruik in productieomgevingen, is afhankelijk van uw workload. Hallo-waarden die worden beschreven in dit artikel zijn voor de demonstratie en testen.

1. [Hallo virtuele machines tooyour vooraf bestaande domein toevoegen](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

Nadat het Hallo virtuele machines worden gemaakt en geconfigureerd, kunt u Hallo failover-cluster configureren.

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a>Stap 2: Hallo Windows Failover Cluster met S2D configureren

de volgende stap Hallo is tooconfigure Hallo-failovercluster met S2D. In deze stap doet u Hallo volgende substappen:

1. Windows Failover Clustering-functie toevoegen
1. Hallo cluster valideren
1. Hallo failover-cluster maken
1. Hallo cloud witness maken
1. Opslag toevoegen

### <a name="add-windows-failover-clustering-feature"></a>Windows Failover Clustering-functie toevoegen

1. toobegin, toohello eerste virtuele machine verbinden met RDP met een domeinaccount dat lid is van de lokale groep administrators en machtigingen toocreate objecten heeft in Active Directory. Dit account wordt gebruikt voor de rest Hallo van Hallo-configuratie.

1. [Failover Clustering functie tooeach virtuele machine toevoegen](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

   tooinstall functie Failover Clustering van Hallo-gebruikersinterface Hallo volgende stappen uit op beide virtuele machines.
   - In **Serverbeheer**, klikt u op **beheren**, en klik vervolgens op **functies en onderdelen toevoegen**.
   - In **Wizard Functies toevoegen en onderdelen**, klikt u op **volgende** totdat u te**onderdelen selecteren**.
   - In **onderdelen selecteren**, klikt u op **Failoverclustering**. Alle vereiste onderdelen en Hallo beheerhulpprogramma's bevatten. Klik op **functies toevoegen**.
   - Klik op **volgende** en klik vervolgens op **voltooien** tooinstall Hallo functies.

   tooinstall hello functie Failover Clustering met PowerShell Hallo script van een beheerder PowerShell-sessie te volgen op een van de Hallo virtuele machines worden uitgevoerd.

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

Voor een verwijzing naar de volgende stappen Hallo instructies Hallo onder stap 3 van [Hyper-geconvergeerde oplossing met behulp van opslagruimten Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).

### <a name="validate-hello-cluster"></a>Hallo cluster valideren

Deze handleiding verwijst tooinstructions onder [cluster valideren](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).

Hallo-clusters in Hallo gebruikersinterface of met PowerShell valideren.

toovalidate hello cluster met Hallo-gebruikersinterface Hallo volgende stappen uit een van Hallo virtuele machines.

1. In **Serverbeheer**, klikt u op **extra**, klikt u vervolgens op **Failoverclusterbeheer**.
1. In **Failoverclusterbeheer**, klikt u op **actie**, klikt u vervolgens op **configuratie valideren...** .
1. Klik op **Volgende**.
1. Op **Servers selecteren of een Cluster**, Hallo-typenaam van beide virtuele machines.
1. Op **testopties**, kies **alleen mij geselecteerde tests uitvoeren**. Klik op **Volgende**.
1. Op **selectie testen**, nemen alle tests uit behalve **opslag**. Zie de volgende afbeelding Hallo:

   ![Valideren van Tests](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. Klik op **Volgende**.
1. Op **bevestiging**, klikt u op **volgende**.

Hallo **Wizard een configuratie valideren** wordt uitgevoerd Hallo validatietests.

toovalidate hello cluster PowerShell Hallo script van een beheerder PowerShell-sessie te volgen op een van de Hallo virtuele machines worden uitgevoerd.

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

Nadat u Hallo cluster valideren, Hallo failover-cluster maken.

### <a name="create-hello-failover-cluster"></a>Hallo failover-cluster maken

Deze handleiding verwijst te[Hallo failover-cluster maken](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).

toocreate hello failover-cluster, moet u de:
- Hallo-namen van Hallo virtuele machines die Hallo clusterknooppunten worden.
- Een naam op voor Hallo failover-cluster
- Een IP-adres voor Hallo failover-cluster. U kunt een IP-adres dat niet wordt gebruikt op Hallo gebruiken hetzelfde virtuele Azure-netwerk en subnet als Hallo clusterknooppunten.

Hallo PowerShell na maakt een failover-cluster. Hallo-script met Hallo namen van Hallo knooppunten (namen Hallo virtuele machine) en een beschikbaar IP-adres uit hello Azure VNET bijwerken:

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a>Maken van een cloud-witness

Cloud-Witness is een nieuw type clusterquorum-witness is opgeslagen in een Azure Storage-Blob. Hiermee verwijdert u Hallo behoeften van een afzonderlijke virtuele machine die als host fungeert voor een witness-share.

1. [Maken van een cloud-witness voor het failovercluster Hallo](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).

1. Maak een blob-container.

1. Hallo toegangstoetsen en de URL van de opslagcontainer Hallo opslaan.

1. Hallo failover cluster clusterquorum-witness configureren. Zie, [configureren Hallo quorumwitness in de gebruikersinterface Hallo]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in Hallo gebruikersinterface.

### <a name="add-storage"></a>Opslag toevoegen

Hallo-schijven voor S2D moeten toobe leeg en zonder partities of andere gegevens. Volg tooclean schijven [Hallo stappen in deze handleiding](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).

1. [Store inschakelen opslagruimten Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).

   Hallo na PowerShell kunt opslagruimten direct.  

   ```PowerShell
   Enable-ClusterS2D
   ```

   In **Failoverclusterbeheer**, ziet u nu Hallo-opslaggroep.

1. [Een volume maken](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).

   Een van de functies Hallo van S2D is dat er een opslaggroep automatisch gemaakt wanneer u dit inschakelen. U bent nu klaar toocreate een volume. PowerShell-commandlet Hallo `New-Volume` automatiseert Hallo volume maken, met inbegrip van de opmaak, toohello cluster toe te voegen en het maken van een gedeeld clustervolume (CSV). Hallo volgende voorbeeld maakt een 800 GB (Gigabyte) CSV.

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   Nadat u deze opdracht is voltooid, wordt een 800 GB-volume als clusterbron gekoppeld. Hallo volume loopt `C:\ClusterStorage\Volume1\`.

   Hallo volgende diagram ziet u een gedeeld clustervolume met S2D:

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a>Stap 3: Failover clusterfailover testen

In Failoverclusterbeheer, Controleer of dat u Hallo storage resource toohello andere clusterknooppunt verplaatsen kunt. Als u verbinding kunt maken toohello failover-cluster met **Failoverclusterbeheer** en Hallo opslag verplaatsen van één knooppunt toohello andere, bent u klaar tooconfigure Hallo FCI.

## <a name="step-4-create-sql-server-fci"></a>Stap 4: SQL Server FCI maken

Nadat u Hallo failover-cluster en alle clusteronderdelen inclusief opslag hebt geconfigureerd, kunt u Hallo FCI van SQL Server maken.

1. Toohello eerste virtuele machine verbinden met RDP.

1. In **Failoverclusterbeheer**, zorg ervoor dat alle clusterkernresources op Hallo eerste virtuele machine zijn. Indien nodig, verplaatst u alle resources toothis virtuele machine.

1. Zoek Hallo-installatiemedia. Als Hallo virtuele machine gebruikmaakt van een van de hello Azure Marketplace-installatiekopieën, Hallo media bevindt zich op `C:\SQLServer_<version number>_Full`. Klik op **Setup**.

1. In Hallo **Installatiecentrum van SQL Server**, klikt u op **installatie**.

1. Klik op **New SQL Server failover cluster installation**. Volg de instructies Hallo in Hallo wizard tooinstall Hallo FCI van SQL Server.

   Hallo FCI gegevensmappen moeten toobe op geclusterde opslag. Met S2D is het niet een gedeelde schijf, maar een volume koppelen punt tooa op elke server. S2D synchroniseert Hallo volume tussen beide knooppunten. Hallo-volume wordt gepresenteerd toohello cluster een cluster shared volume. Hallo CSV koppelpunt voor gegevensmappen hello gebruiken.

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. Nadat u Hallo wizard hebt voltooid, installeert Setup een FCI SQL Server op Hallo eerste knooppunt.

1. Nadat Setup is Hallo FCI is geïnstalleerd op het eerste knooppunt hello, verbinding maken met het tweede knooppunt toohello met RDP.

1. Open Hallo **Installatiecentrum van SQL Server**. Klik op **installatie**.

1. Klik op **toevoegen knooppunt tooa SQL Server-failovercluster**. Volg de instructies Hallo in Hallo wizard tooinstall SQL server en voeg deze server toohello FCI.

   >[!NOTE]
   >Als u een installatiekopie van de galerie van Azure Marketplace met SQL Server gebruikt, zijn SQL Server-hulpprogramma's opgenomen in de installatiekopie van het Hallo. Als u deze installatiekopie niet gebruikt, afzonderlijk Hallo SQL Server-hulpprogramma's installeren. Zie [downloaden van SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="step-5-create-azure-load-balancer"></a>Stap 5: Azure load balancer maken

Clusters gebruik op virtuele machines in Azure, een load balancer toohold een IP-adres dat toobe op één clusterknooppunt tegelijk moet. In deze oplossing bevat Hallo load balancer Hallo IP-adres voor Hallo FCI van SQL Server.

[Maken en configureren van een Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a>Hallo load balancer maken in hello Azure-portal

toocreate hello load balancer:

1. Ga in de Azure-portal hello, toohello resourcegroep met Hallo virtuele machines.

1. Klik op **+ toevoegen**. Zoeken Hallo Marketplace voor **Load Balancer**. Klik op **Load Balancer**.

1. Klik op **Create**.

1. Hallo load balancer met configureren:

   - **Naam**: een naam waarmee Hallo load balancer.
   - **Type**: Hallo load balancer mag openbare of particuliere. Een persoonlijke load balancer toegankelijk is vanuit Hallo hetzelfde VNET. De meeste Azure toepassingen kunnen gebruikmaken van een persoonlijke load balancer. Als uw toepassing toegang tooSQL Server rechtstreeks via Internet hello moet, gebruikt u een openbare load balancer.
   - **Virtueel netwerk**: Hallo netwerk als Hallo virtuele machines.
   - **Subnet**: Hallo hetzelfde subnet als Hallo virtuele machines.
   - **Privé IP-adres**: Hallo hetzelfde IP-adres dat u toohello FCI van SQL Server-clusterbron in het netwerk worden toegewezen.
   - **abonnement**: uw Azure-abonnement.
   - **Resourcegroep**: gebruik Hallo dezelfde resourcegroep als uw virtuele machines.
   - **Locatie**: gebruik dezelfde hello Azure-locatie als uw virtuele machines.
   Zie de volgende afbeelding Hallo:

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a>Back-endpool van Hallo load balancer configureren

1. Toohello Azure-resourcegroep met Hallo virtuele machines retourneren en Ga naar Hallo nieuwe load balancer. Wellicht hebt u toorefresh Hallo weergave op Hallo resourcegroep. Klik op Hallo load balancer.

1. Klik op Hallo load balancer blade **back-endpools**.

1. Klik op **+ toevoegen** tooadd een back-endpool.

1. Typ een naam voor de back-endpool Hallo.

1. Klik op **toevoegen van een virtuele machine**.

1. Op Hallo **virtuele machines kiezen** blade, klikt u op **een beschikbaarheidsset kiezen**.

1. Kies Hallo beschikbaarheidsset u Hallo SQL Server-virtuele machines in hebt geplaatst.

1. Op Hallo **virtuele machines kiezen** blade, klikt u op **Hallo virtuele machines kiezen**.

   Uw Azure-portal moet eruitzien als Hallo volgende afbeelding:

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. Klik op **Selecteer** op Hallo **virtuele machines kiezen** blade.

1. Klik op **OK** twee keer.

### <a name="configure-a-load-balancer-health-probe"></a>Een load balancer-test health configureren

1. Klik op Hallo load balancer blade **statuscontroles**.

1. Klik op **+ toevoegen**.

1. Op Hallo **toevoegen health test** blade <a name="probe"> </a>Hallo health test parameters instellen:

   - **Naam**: een naam voor de Hallo health test.
   - **Protocol**: TCP.
   - **Poort**: tooan beschikbare TCP-poort ingesteld. Deze poort moet een firewallpoort worden geopend. Gebruik Hallo [dezelfde poort](#ports) u instellen voor de Hallo health test op Hallo firewall.
   - **Interval**: 5 seconden.
   - **Drempelwaarde voor onjuiste status**: 2 achtereenvolgende mislukte pogingen.

1. Klik op OK.

### <a name="set-load-balancing-rules"></a>Taakverdelingsregels instellen

1. Klik op Hallo load balancer blade **Taakverdelingsregels**.

1. Klik op **+ toevoegen**.

1. Hallo load balancing regels parameters instellen:

   - **Naam**: een naam op voor Hallo load-balancingregels.
   - **Frontend IP-adres**: Hallo IP-adres gebruiken voor Hallo netwerkbron FCI van SQL Server-cluster.
   - **Poort**: ingesteld voor Hallo SQL Server FCI TCP-poort. Hallo exemplaar standaardpoort is 1433.
   - **Back-endpoort**: deze waarde gebruikt Hallo dezelfde poort als Hallo **poort** waarde wanneer u inschakelt **zwevend IP (direct server return)**.
   - **Back-endpool**: gebruik Hallo back-end Poolnaam die u eerder hebt geconfigureerd.
   - **De statuscontrole van**: gebruik Hallo health test op die u eerder hebt geconfigureerd.
   - **Sessiepersistentie**: geen.
   - **Time-out (minuten)**: 4.
   - **Zwevend IP (direct server return)**: ingeschakeld

1. Klik op **OK**.

## <a name="step-6-configure-cluster-for-probe"></a>Stap 6: Configureren voor de test-cluster

Stel Hallo cluster test poortparameter in PowerShell.

tooset Hallo cluster test poortparameter, update variabelen in het volgende script uit uw omgeving Hallo.

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a>Stap 7: Testen FCI failover

Failover van Hallo FCI toovalidate clusterfunctionaliteit wilt testen. Hallo volgende stappen:

1. Tooone van clusterknooppunten voor SQL Server FCI Hallo met RDP verbinding.

1. Open **Failoverclusterbeheer**. Klik op **rollen**. De aankondiging welk knooppunt eigenaar van Hallo FCI van SQL Server-rol.

1. Met de rechtermuisknop op Hallo FCI van SQL Server-rol.

1. Klik op **verplaatsen** en klik op **Best mogelijke knooppunt**.

**Failover Cluster Manager** toont Hallo rol en de daarbij behorende bronnen offline gaan. Hallo resources Verplaats en online komen op Hallo andere knooppunt.

### <a name="test-connectivity"></a>Connectiviteit testen

tootest connectiviteit, log in tooanother virtuele machine in Hallo hetzelfde virtuele netwerk. Open **SQL Server Management Studio** en verbinding maken met de naam van de SQL Server FCI toohello.

>[!NOTE]
>Zo nodig u kunt [SQL Server Management Studio downloaden](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="limitations"></a>Beperkingen
Op virtuele machines in Azure, wordt Microsoft Distributed Transaction Coordinator (DTC) niet ondersteund op Failoverclusterinstanties omdat Hallo RPC-poort wordt niet ondersteund door Hallo load balancer.

## <a name="see-also"></a>Zie ook

[Setup S2D met extern bureaublad (Azure)](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

[Hyper-geconvergeerde oplossing met opslagruimten direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).

[Directe opslag ruimte-overzicht](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[SQL Server-ondersteuning voor S2D](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
