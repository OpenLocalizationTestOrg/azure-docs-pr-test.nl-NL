---
title: hoge beschikbaarheid van de virtuele Machines voor SAP NetWeaver aaaAzure | Microsoft Docs
description: Hoge beschikbaarheid-handleiding voor SAP NetWeaver op Azure Virtual Machines
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 662dd793390d7f6138b160ed86259d13391336aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a>Azure virtuele Machines hoge beschikbaarheid voor SAP NetWeaver

[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



Virtuele Machines in Azure is Hallo-oplossing voor organisaties die berekenings-, opslag- en netwerkbronnen, in de minimale tijd en zonder langdurige inkoop cycli moeten. U kunt Azure Virtual Machines toodeploy klassieke toepassingen zoals SAP NetWeaver gebaseerde ABAP, Java en een ABAP + Java-stack gebruiken. Betrouwbaarheid en beschikbaarheid zonder dat extra on-premises resources uitbreiden. Virtuele Machines in Azure ondersteunt cross-premises connectiviteit, zodat u kunt Azure Virtual Machines integreren in uw organisatie lokale domeinen, privéclouds en SAP system Liggend.

In dit artikel wordt uitgelegd we Hallo stappen die u toodeploy SAP-systemen voor hoge beschikbaarheid in Azure ondernemen kunt met hello Azure Resource Manager-implementatiemodel. We helpt u bij deze belangrijke taken:

* Hallo zoeken rechts SAP-opmerkingen en installatie implementatiehandleidingen, die worden vermeld in Hallo [Resources] [ sap-ha-guide-2] sectie. In dit artikel is een aanvulling op de documentatie voor SAP-installatie en SAP-opmerkingen, de primaire Hallo-bronnen waarmee u kunnen installeren en SAP software implementeren op specifieke platforms.
* Meer informatie over Hallo verschillen tussen hello Azure Resource Manager-implementatiemodel en hello Azure klassieke implementatiemodel.
* Meer informatie over Windows Server Failover Clustering quorum-modi, zodat u Hallo model dat geschikt is voor uw Azure-implementatie kunt selecteren.
* Meer informatie over Windows Server Failover Clustering gedeelde opslag in Azure-services.
* Meer informatie over hoe de onderdelen van één punt van fout zoals geavanceerde Business Application Programming (ABAP) SAP centrale Services (ASC's) voor het beveiligen van toohelp / SAP centrale Services (SCS) en databasebeheersystemen (DBMS) en redundante componenten zoals SAP Toepassingsserver in Azure.
* Ga als volgt een voorbeeld van een stapsgewijze van een installatie en configuratie van een SAP-systeem voor hoge beschikbaarheid in een cluster met Windows Server Failover Clustering in Azure met Azure Resource Manager.
* Meer informatie over extra stappen vereist toouse Windows Server Failover Clustering in Azure, maar die niet nodig zijn in een on-premises implementatie.

toosimplify implementatie en configuratie in dit artikel gebruiken we Hallo SAP drie lagen hoge beschikbaarheid Resource Manager-sjablonen. Hallo sjablonen automatisering van Hallo gehele infrastructuur die u nodig hebt voor een hoge beschikbaarheid SAP-systeem. Hallo-infrastructuur ondersteunt ook het formaat van uw systeem SAP SAP toepassing prestaties Standard (SAP's).

## <a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a>Vereisten
Zorg voordat u begint, dat u voldoet aan de Hallo vereisten die worden beschreven in Hallo uit te voeren. Wees ook zeker toocheck alle resources die worden vermeld in Hallo [Resources] [ sap-ha-guide-2] sectie.

In dit artikel gebruiken we Azure Resource Manager-sjablonen voor [drie lagen SAP NetWeaver schijven beheerd](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/). Zie voor een handig overzicht van sjablonen [SAP Azure Resource Manager-sjablonen](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).

## <a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a>Resources
Deze artikelen omvatten SAP-implementaties in Azure:

* [Azure virtuele Machines, planning en implementatie voor SAP NetWeaver][planning-guide]
* [Azure virtuele Machines-implementatie voor SAP NetWeaver][deployment-guide]
* [Azure virtuele Machines DBMS-implementatie voor SAP NetWeaver][dbms-guide]
* [Azure virtuele Machines hoge beschikbaarheid voor SAP NetWeaver (deze handleiding)][sap-ha-guide]

> [!NOTE]
> Waar mogelijk, geven wij u een koppeling toohello SAP installatiehandleiding verwijzen (Zie Hallo [SAP installatiehandleidingen][sap-installation-guides]). Voor vereisten en informatie over het Hallo-installatieproces, het een goed idee tooread Hallo SAP NetWeaver installatie zorgvuldig leidt. Dit artikel behandelt alleen specifieke taken voor SAP NetWeaver-gebaseerde computers die u met Azure Virtual Machines gebruiken kunt.
>
>

Deze opmerkingen SAP zijn verwante toohello onderwerp van SAP in Azure:

| Het nummer | Titel |
| --- | --- |
| [1928533] |SAP-toepassingen in Azure: ondersteunde producten en schaling |
| [2015553] |SAP op Microsoft Azure: ondersteuning voor vereisten |
| [1999351] |Verbeterde Azure bewaking voor SAP |
| [2178632] |Sleutel bewaking van metrische gegevens voor SAP op Microsoft Azure |
| [1999351] |Virtualisatie in Windows: uitgebreide bewaking |
| [2243692] |Gebruik van Azure Premium-SSD-opslag voor SAP DBMS exemplaar |

Meer informatie over Hallo [beperkingen van de Azure-abonnementen][azure-subscription-service-limits-subscription], waaronder algemene standaardbeperkingen en maximale beperkingen.

## <a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>Hoge beschikbaarheid SAP met Azure Resource Manager versus hello Azure klassieke implementatiemodel
Hello Azure Resource Manager en Azure klassieke implementatiemodel zijn verschillende in Hallo gebieden te volgen:

- Resourcegroepen
- Azure interne load balancer-afhankelijkheid van hello Azure-resourcegroep
- Ondersteuning voor SAP multi-SID-scenario 's

### <a name="f76af273-1993-4d83-b12d-65deeae23686"></a>Resourcegroepen
In Azure Resource Manager kunt u resource groepen toomanage alle Hallo toepassingsresources in uw Azure-abonnement. Een geïntegreerde benadering, in een resourcegroep van alle resources hebben Hallo dezelfde levenscyclus. Bijvoorbeeld, alle resources worden gemaakt op Hallo dezelfde tijd en ze worden verwijderd op Hallo hetzelfde moment. Meer informatie over [resourcegroepen](../../../azure-resource-manager/resource-group-overview.md#resource-groups).

### <a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure interne load balancer-afhankelijkheid van hello Azure-resourcegroep

Hello Azure klassieke implementatiemodel is er een afhankelijkheid tussen hello Azure interne load balancer (Azure Load Balancer-service) en het Hallo-cloudservice. Elke interne load balancer moet een service in de cloud.

In Azure Resource Manager elk Azure-resource moet toobe in een Azure-resourcegroep geplaatst en dit is ook geldig voor de Load Balancer van Azure. Maar er is geen groep nodig toohave één Azure-resource per Azure-load balancer, bijvoorbeeld één Azure-resourcegroep meerdere Azure Load Balancers kan bevatten. Hallo-omgeving is eenvoudiger en flexibeler. 

### <a name="support-for-sap-multi-sid-scenarios"></a>Ondersteuning voor SAP multi-SID-scenario 's

In Azure Resource Manager kunt u meerdere SAP systeem-id (SID) ASC's / SCS exemplaren in één cluster installeren. Multi-SID-exemplaren zijn mogelijk vanwege ondersteuning voor meerdere IP-adressen voor elke Azure interne load balancer.

toouse hello Azure klassieke implementatiemodel, voert u de procedures op Hallo van [SAP NetWeaver in Azure: Clustering SAP ASC's / SCS exemplaren met behulp van Windows Server Failover Clustering in Azure met SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).

> [!IMPORTANT]
> Het is raadzaam dat u hello Azure Resource Manager-implementatiemodel voor uw SAP-installaties. Dit biedt veel voordelen die niet beschikbaar in het klassieke implementatiemodel Hallo. Meer informatie over Azure [implementatiemodellen][virtual-machines-azure-resource-manager-architecture-benefits-arm].   
>
>

## <a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a>Windows Serverfailover Clustering
Windows Server Failover Clustering is Hallo-basis van een hoge beschikbaarheid SAP ASC's / SCS installatie en DBMS in Windows.

Een failovercluster is een groep 1 + n onafhankelijke servers (knooppunten) die samenwerken tooincrease Hallo beschikbaarheid van toepassingen en services. Als een knooppuntfout optreedt, Windows Server Failover Clustering berekent het aantal fouten die zich voordoen kunnen tijdens het onderhoud van een gezonde Hallo cluster tooprovide toepassingen en services. U kunt kiezen uit andere quorum-modi tooachieve Failoverclustering.

### <a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a>Quorum-modi
U kunt kiezen uit vier quorum-modi wanneer u Windows Server Failover Clustering:

* **Knooppuntmeerderheid**. Elk knooppunt van Hallo kunt stemmen. Hallo cluster werkt alleen met een meerderheid van stemmen, dat wil zeggen, met meer dan de helft Hallo stemmen. U wordt aangeraden deze optie voor clusters met een oneven aantal knooppunten. Bijvoorbeeld drie knooppunten in een cluster met zeven knooppunten kunnen mislukken en Hallo cluster tussen beelden meerderheid bereikt en toorun blijft.  
* **Knooppunt en schijfmeerderheid**. Elk knooppunt en een aangewezen schijf (een schijfwitness) in de clusteropslag Hallo kunnen stemmen wanneer ze beschikbaar zijn en in de communicatie. Hallo cluster werkt alleen met een meerderheid van Hallo stemmen, dat wil zeggen, met meer dan de helft Hallo stemmen. Deze modus is wel zinvol in een clusteromgeving met een even aantal knooppunten. Als Hallo schijf en half Hallo knooppunten online zijn, blijft Hallo-cluster in een foutloze toestand bevindt.
* **Knooppunt en de meeste bestandsshare**. Elk knooppunt plus een aangewezen bestandsshare (een bestandssharewitness) die Hallo beheerder maakt kunt stemmen, ongeacht of Hallo knooppunten en bestandsshare beschikbaar zijn en bij communicatie. Hallo cluster werkt alleen met een meerderheid van Hallo stemmen, dat wil zeggen, met meer dan de helft Hallo stemmen. Deze modus is wel zinvol in een clusteromgeving met een even aantal knooppunten. Het is vergelijkbaar toohello knooppunt en schijfmeerderheid modus, maar een witness-bestandsshare wordt gebruikt in plaats van een witness-schijf. Deze modus is eenvoudig tooimplement, maar als het Hallo-bestandsshare zelf is niet maximaal beschikbaar, het mogelijk een potentieel risico.
* **Geen meerderheid: Alleen schijf**. Hallo-cluster heeft quorum als één knooppunt beschikbaar en communicatie met een specifieke schijf in de clusteropslag Hallo is. Alleen Hallo knooppunten die ook in de communicatie met die schijf kunnen Hallo-cluster toevoegen. Het is raadzaam dat u deze modus niet gebruiken.
 

## <a name="fdfee875-6e66-483a-a343-14bbaee33275"></a>Windows Serverfailover Clustering van on-premises
Afbeelding 1 ziet u een cluster met twee knooppunten. Als hello netwerkverbinding tussen de knooppunten Hallo mislukt en beide knooppunten blijven en wordt uitgevoerd, een quorum schijf of bestandsshare bepaalt welk knooppunt blijft tooprovide Hallo cluster toepassingen en services. Hallo-knooppunt dat toegang toohello quorumschijf of de bestandsshare is Hallo-knooppunt dat ervoor zorgt dat services kunnen blijven.

Omdat in dit voorbeeld een cluster met twee knooppunten wordt, gebruiken we Hallo knooppunt en bestandssharemeerderheid quorum-modus. Hallo knooppunt en schijfmeerderheid is ook een geldige optie. U wordt aangeraden dat u een quorumschijf in een productieomgeving. U kunt system technologie toomake van netwerk- en deze maximaal beschikbaar.

![Afbeelding 1: Voorbeeld van een configuratie voor Windows Server Failover Clustering voor SAP ASC's / SCS in Azure][sap-ha-guide-figure-1000]

_**Afbeelding 1:** voorbeeld van een configuratie voor Windows Server Failover Clustering voor SAP ASC's / SCS in Azure_

### <a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a>Gedeelde opslag
Afbeelding 1 wordt ook een cluster met twee knooppunten gedeelde opslag. Alle knooppunten in cluster Hallo detecteren in een cluster van de gedeelde opslag lokale gedeelde opslag. Een vergrendelingsfout mechanisme beschermt Hallo gegevens tegen beschadiging. Alle knooppunten kunnen detecteren als een ander knooppunt mislukt. Als een knooppunt is mislukt, wordt het resterende knooppunt hello wordt eigenaar van opslagbronnen Hallo en zorgt ervoor Hallo beschikbaarheid van services.

> [!NOTE]
> U hoeft geen gedeelde schijven voor hoge beschikbaarheid bij sommige toepassingen DBMS zoals met SQL Server. SQL Server Always On repliceert DBMS gegevens en logboekbestanden bestanden van de lokale schijf Hallo van één cluster knooppunt toohello lokale schijf van een ander clusterknooppunt. Configuratie van het cluster Windows hello hoeft in dat geval niet een gedeelde schijf.
>
>

### <a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a>Netwerk- en naamomzetting
Clientcomputers bereiken Hallo-cluster via een virtueel IP-adres en de naam van een virtuele host op die Hallo DNS-server biedt. Hallo on-premises knooppunten en Hallo DNS-server kan meerdere IP-adressen verwerken.

In een typische installatie gebruikt u twee of meer netwerkverbindingen:

* Een speciale verbinding toohello opslag
* Een cluster interne netwerkverbinding voor Hallo heartbeat
* Een openbaar netwerk dat clients tooconnect toohello cluster gebruiken

## <a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a>Windows Serverfailover Clustering in Azure
Vergeleken toobare metal of privécloud implementaties, Azure Virtual Machines vereist extra stappen tooconfigure Windows Server Failover Clustering. Als u een gedeelde clusterschijf bouwen, moet u de namen van verschillende IP-adressen en virtuele host tooset voor Hallo SAP ASC's / SCS exemplaar.

In dit artikel hoofdconcepten bespreken we en Hallo extra stappen vereist toobuild een SAP-services met hoge beschikbaarheid centrale cluster in Azure. We zien u hoe tooset up Hallo hulpprogramma van derden SIOS DataKeeper en hoe tooconfigure hello Azure interne load balancer. U kunt deze hulpprogramma's voor toocreate een failover-cluster van Windows gebruiken met een bestandsshare-witness in Azure.

![Afbeelding 2: Windows Server Failover Clustering configuratie in Azure zonder een gedeelde schijf][sap-ha-guide-figure-1001]

_**Afbeelding 2:** configuratie Windows Server Failover Clustering in Azure zonder een gedeelde schijf_

### <a name="1a464091-922b-48d7-9d08-7cecf757f341"></a>Gedeelde schijf in Azure met SIOS DataKeeper
U moet gedeelde opslag voor een hoge beschikbaarheid SAP ASC's / SCS-exemplaar in de cluster. Zoals van September 2016 Azure niet gedeelde opslag die biedt kunt u toocreate een cluster met gedeelde opslag gebruiken. U kunt software van derden SIOS DataKeeper Cluster Edition toocreate een gespiegelde opslagruimte die gedeelde clusteropslag simuleert. Hallo SIOS oplossing biedt realtime synchrone gegevensreplicatie. Dit is hoe u een gedeelde schijfbron voor een cluster kunt maken:

1. Koppel een extra schijf tooeach van Hallo virtuele machines (VM's) in de configuratie van een Windows-cluster.
2. SIOS DataKeeper Cluster Edition wordt uitgevoerd op beide knooppunten van de virtuele machine.
3. SIOS DataKeeper Cluster Edition configureren zodat deze overeenkomt met inhoud van Hallo extra schijf die is gekoppeld volume van Hallo bron virtuele machine toohello extra schijf die is gekoppeld volume van de virtuele doelmachine Hallo Hallo. SIOS DataKeeper isoleert Hallo bron en doel lokale volumes en geeft ze tooWindows Server Failover Clustering als één gedeelde schijf.

Vindt u meer informatie over [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).

![Afbeelding 3: Configuratie van Windows Server Failover Clustering in Azure met SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Afbeelding 3:** configuratie Windows Server Failover Clustering in Azure met SIOS DataKeeper_

> [!NOTE]
> U hoeft geen gedeelde schijven voor hoge beschikbaarheid met sommige DBMS-producten, zoals SQL Server. SQL Server Always On repliceert DBMS gegevens en logboekbestanden bestanden van de lokale schijf Hallo van één cluster knooppunt toohello lokale schijf van een ander clusterknooppunt. Hallo Windows cluster-configuratie nodig niet in dit geval een gedeelde schijf.
>
>

### <a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a>Naamomzetting in Azure
Hello Azure-cloud-platform biedt geen Hallo optie tooconfigure virtuele IP-adressen, zoals zwevend IP-adressen te bieden. U moet een alternatieve oplossing tooset van een virtueel IP-adres tooreach Hallo clusterbron in Hallo cloud.
Azure heeft een interne load balancer in hello Azure Load Balancer-service. Met Hallo interne load balancer bereiken clients Hallo cluster via Hallo cluster virtuele IP-adres.
U moet toodeploy Hallo interne load balancer in Hallo resourcegroep die de clusterknooppunten Hallo bevat. Configureer vervolgens alle benodigde poorttoewijzing regels met Hallo test poorten van Hallo interne load balancer.
Hallo-clients kunnen verbinding maken via de naam van de virtuele host Hallo. Hallo DNS-server wordt omgezet Hallo cluster IP-adres en Hallo interne load balancer-ingangen poorttoewijzing toohello actieve knooppunt van Hallo-cluster.

## <a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a>SAP NetWeaver hoge beschikbaarheid in een Azure-infrastructuur-as-a-Service (IaaS)
tooachieve SAP-toepassing hoge beschikbaarheid, zoals SAP-softwareonderdelen, moet u tooprotect Hallo volgende onderdelen:

* SAP Application Server-exemplaar
* SAP ASC's / SCS-exemplaar
* DBMS-server

Zie voor meer informatie over het beveiligen van SAP-onderdelen in scenario's voor hoge beschikbaarheid [Azure Virtual Machines planning en implementatie voor SAP NetWeaver][planning-guide-11].

### <a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a>Hoge beschikbaarheid SAP-toepassingsserver
Normaal gesproken hoeft u niet een bepaalde oplossing voor hoge beschikbaarheid voor Hallo SAP-toepassingsserver en dialoogvenster exemplaren. Een maximale beschikbaarheid realiseren door redundantie en configureert u meerdere exemplaren van het dialoogvenster in verschillende exemplaren van Azure Virtual Machines. U hebt ten minste twee SAP exemplaren van een toepassing in twee exemplaren van Azure Virtual Machines geïnstalleerd.

![Afbeelding 4: Hoge beschikbaarheid SAP-toepassingsserver][sap-ha-guide-figure-2000]

_**Afbeelding 4:** hoge beschikbaarheid SAP-toepassingsserver_

U moet alle virtuele machines dat SAP-toepassingsserver instanties van hosts in dezelfde Azure beschikbaarheidsset Hallo plaatsen. Een Azure beschikbaarheidsset zorgt ervoor dat:

* Alle virtuele machines deel uitmaken van Hallo dezelfde upgradedomein. Een upgradedomein bijvoorbeeld zorgt ervoor dat Hallo virtuele machines zijn niet op Hallo bijgewerkt hetzelfde moment tijdens gepland onderhoud uitval.
* Alle virtuele machines deel uitmaken van Hallo hetzelfde foutdomein. Een foutdomein bijvoorbeeld ervoor zorgt dat virtuele machines zodat er geen storingspunt is van invloed op Hallo beschikbaarheid van alle virtuele machines zijn geïmplementeerd.

Meer informatie over het te[Hallo beschikbaarheid van virtuele machines beheren][virtual-machines-manage-availability].

Alleen niet-beheerde schijf: omdat hello Azure storage-account een potentieel storingspunt is, is het belangrijk toohave ten minste twee Azure storage-accounts, waarbij ten minste twee virtuele machines worden gedistribueerd. In een ideaal setup wordt Hallo schijven van elke virtuele machine die wordt uitgevoerd een SAP-dialoogvenster-exemplaar geïmplementeerd in een ander opslagaccount.

### <a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a>Hoge beschikbaarheid SAP ASC's / SCS exemplaar
Afbeelding 5 is een voorbeeld van een exemplaar van de SAP ASC's / SCS hoge beschikbaarheid.

![Afbeelding 5: Hoge beschikbaarheid SAP ASC's / SCS exemplaar][sap-ha-guide-figure-2001]

_**Afbeelding 5:** hoge beschikbaarheid SAP ASC's / SCS-exemplaar_

#### <a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a>SAP ASC's / SCS exemplaar hoge beschikbaarheid met Windows Server Failover Clustering in Azure
Vergeleken toobare metal of privécloud implementaties, Azure Virtual Machines vereist extra stappen tooconfigure Windows Server Failover Clustering. toobuild een failover-cluster van Windows, moet u een gedeelde clusterschijf, verschillende IP-adressen, verschillende namen van de virtuele host en een Azure interne load balancer voor een exemplaar SAP ASC's / SCS clustering. Dit bespreken we in meer detail verderop in Hallo artikel.

![Afbeelding 6: Windows Server Failover Clustering voor een SAP ASC's / SCS-configuratie in Azure met behulp van SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Afbeelding 6:** Windows Server Failover Clustering voor een SAP ASC's / SCS-configuratie in Azure met SIOS DataKeeper_

### <a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Hoge beschikbaarheid DBMS exemplaar
Hallo DBMS is ook een aanspreekpunt in een SAP-systeem. U moet tooprotect deze met behulp van een oplossing voor hoge beschikbaarheid. Afbeelding 7 toont een hoge beschikbaarheid SQL Server Always On oplossing in Azure, met Windows Server Failover Clustering en hello Azure interne load balancer. SQL Server Always On repliceert DBMS gegevens en logboekbestanden bestanden met behulp van een eigen DBMS-replicatie. In dit geval nodig u niet clusteren gedeelde schijven die vereenvoudigt Hallo volledige installatie.

![Afbeelding 7: Voorbeeld van een hoge beschikbaarheid SAP DBMS, met SQL Server Always On][sap-ha-guide-figure-2003]

_**Afbeelding 7:** voorbeeld van een hoge beschikbaarheid SAP DBMS, met SQL Server Always On_

Zie voor meer informatie over SQL Server in Azure met Azure Resource Manager-implementatiemodel Hallo clustering deze artikelen:

* [AlwaysOn-beschikbaarheidsgroep in Azure Virtual Machines handmatig configureren met behulp van Resource Manager] [virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]
* [Een Azure interne load balancer voor een AlwaysOn-beschikbaarheidsgroep configureren in Azure] [virtual-machines-windows-portal-sql-alwayson-int-listener]

## <a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a>End-to-end hoge beschikbaarheid implementatiescenario 's

### <a name="deployment-scenario-using-architectural-template-1"></a>Implementatiescenario met architectuur sjabloon 1

Afbeelding 8 toont een voorbeeld van een SAP NetWeaver hoge beschikbaarheid-architectuur in Azure voor **één** SAP-systeem. Dit scenario is als volgt instellen:

- Een speciale cluster wordt gebruikt voor Hallo SAP ASC's / SCS exemplaar.
- Een speciale cluster wordt gebruikt voor Hallo DBMS exemplaar.
- SAP Application Server-exemplaren zijn in hun eigen toegewezen virtuele machines geïmplementeerd.

![Afbeelding 8: Hoge beschikbaarheid architectuur sjabloon 1, met speciale cluster voor ASC's / SCS en DBMS SAP][sap-ha-guide-figure-2004]

_**Afbeelding 8:** SAP-architectuur sjabloon 1 hoge beschikbaarheid, speciale clusters voor ASC's / SCS en DBMS_

### <a name="deployment-scenario-using-architectural-template-2"></a>Implementatiescenario met behulp van architectuur sjabloon 2

Afbeelding 9 toont een voorbeeld van een SAP NetWeaver hoge beschikbaarheid-architectuur in Azure voor **één** SAP-systeem. Dit scenario is als volgt instellen:

- Een speciale cluster wordt gebruikt voor **beide** Hallo SAP ASC's / SCS-instantie en Hallo DBMS.
- SAP Application Server-exemplaren zijn in de eigen toegewezen virtuele machines geïmplementeerd.

![Afbeelding 9: Hoge beschikbaarheid architectuur sjabloon 2, met een speciale voor ASC's / SCS als een cluster toegewezen voor DBMS SAP][sap-ha-guide-figure-2005]

_**Afbeelding 9:** hoge beschikbaarheid architectuur sjabloon 2, met een speciale voor ASC's / SCS als een cluster toegewezen voor DBMS SAP_

### <a name="deployment-scenario-using-architectural-template-3"></a>Implementatiescenario met architectuur sjabloon 3

Afbeelding 10 toont een voorbeeld van een SAP NetWeaver hoge beschikbaarheid-architectuur in Azure voor **twee** SAP-systemen, met &lt;SID1&gt; en &lt;SID2&gt;. Dit scenario is als volgt instellen:

- Een speciale cluster wordt gebruikt voor **beide** Hallo SAP ASC's / SCS SID1 exemplaar *en* Hallo SAP ASC's / SCS SID2 exemplaar (één cluster).
- Een speciale cluster wordt gebruikt voor DBMS SID1 en een ander toegewezen cluster wordt gebruikt voor DBMS SID2 (twee clusters).
- SAP Application Server-exemplaren voor Hallo SAP-systeem SID1 hebben hun eigen toegewezen virtuele machines.
- SAP Application Server-exemplaren voor Hallo SAP-systeem SID2 hebben hun eigen toegewezen virtuele machines.

![Afbeelding 10: SAP hoge beschikbaarheid architectuur sjabloon 3, met een cluster toegewezen voor verschillende ASC's / SCS-exemplaren][sap-ha-guide-figure-6003]

_**Afbeelding 10:** SAP-hoge beschikbaarheid architectuur sjabloon 3, met een cluster toegewezen voor verschillende ASC's / SCS-exemplaren_

## <a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Hallo-infrastructuur voorbereiden

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a>Hallo-infrastructuur voorbereiden voor architecturale sjabloon 1
Azure Resource Manager-sjablonen voor SAP vereenvoudigen implementatie van de vereiste resources.

Hallo drie lagen sjablonen in Azure Resource Manager ondersteunen ook scenario's met hoge beschikbaarheid, zoals in de architectuur sjabloon 1, met twee clusters. Elk cluster is een SAP storingspunt voor SAP ASC's / SCS en DBMS.

Dit is waarop u Azure Resource Manager-sjablonen kunt ophalen voor Hallo voorbeeldscenario die in dit artikel worden beschreven:

* [Azure Marketplace-installatiekopie](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [Azure Marketplace-installatiekopie met schijven beheerd](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [Aangepaste installatiekopie](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [Aangepaste installatiekopie met schijven beheerd](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

tooprepare hello infrastructuur voor architecturale sjabloon 1:

- In de Azure-portal op Hallo Hallo **Parameters** blade in Hallo **SYSTEMAVAILABILITY** de optie **HA**.

  ![Afbeelding 11: Stel SAP-parameters voor hoge beschikbaarheid Azure Resource Manager][sap-ha-guide-figure-3000]

_**Afbeelding 11:** ingesteld SAP-parameters voor hoge beschikbaarheid Azure Resource Manager_


  Hallo-sjablonen maken:

  * **Virtuele machines**:
    * SAP-toepassingsserver virtuele machines: <*SAPSystemSID*> - di - <*getal*>
    * ASC's / SCS cluster virtuele machines: <*SAPSystemSID*> - ASC - 's <*getal*>
    * DBMS-cluster: <*SAPSystemSID*> - db - <*getal*>

  * **Netwerkkaarten voor alle virtuele machines met bijbehorende IP-adressen**:
    * <*SAPSystemSID*> - nic - di - <*getal*>
    * <*SAPSystemSID*> - nic - ASC's - <*getal*>
    * <*SAPSystemSID*> - nic - db - <*getal*>

  * **Azure storage-accounts (alleen niet-beheerde schijven)**

  * **Beschikbaarheidsgroepen** voor:
    * SAP-toepassingsserver virtuele machines: <*SAPSystemSID*> - avset - di
    * SAP ASC's / SCS cluster virtuele machines: <*SAPSystemSID*> - avset - ASC's
    * DBMS cluster virtuele machines: <*SAPSystemSID*> - avset - db

  * **Azure interne load balancer**:
    * Met alle poorten voor Hallo ASC's / SCS exemplaar en IP-adres <*SAPSystemSID*> - lb - ASC's
    * Met alle poorten voor de SQL Server-DBMS en IP-adres Hallo <*SAPSystemSID*> - lb - db

  * **Netwerkbeveiligingsgroep**: <*SAPSystemSID*> - nsg - ASC's-0  
    * Met een open externe Remote Desktop Protocol (RDP)-poort toohello <*SAPSystemSID*> - ASC's - 0 virtuele machine

> [!NOTE]
> Alle IP-adressen van Hallo netwerkkaarten en Azure interne load balancers zijn **dynamische** standaard. Ze ook wijzigen**statische** IP-adressen. We beschrijven hoe toodo dit later op Hallo artikel.
>
>

### <a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Virtuele machines implementeren met het bedrijfsnetwerk connectiviteit (cross-premises) toouse in productie
Voor productiesystemen SAP, Azure virtuele machines implementeren met [bedrijfsnetwerk connectiviteit (cross-premises)] [ planning-guide-2.2] met behulp van Azure Site-naar-Site VPN- of Azure ExpressRoute.

> [!NOTE]
> U kunt uw Azure Virtual Network-exemplaar gebruiken. Hallo virtueel netwerk en subnet zijn al gemaakt en voorbereid.
>
>

1.  In de Azure-portal op Hallo Hallo **Parameters** blade in Hallo **NEWOREXISTINGSUBNET** de optie **bestaande**.
2.  In Hallo **SUBNETID** Voeg Hallo volledige tekenreeks van het voorbereide Azure netwerk SubnetID waar u van plan toodeploy uw virtuele machines in Azure bent.
3.  een lijst met alle Azure-netwerksubnetten tooget deze PowerShell-opdracht uitvoeren:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  Hallo **ID** veld bevat Hallo **SUBNETID**.
4. een lijst met alle tooget **SUBNETID** waarden, deze PowerShell-opdracht uitvoeren:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  Hallo **SUBNETID** ziet er als volgt:

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a>Alleen in de cloud SAP-exemplaren voor test- en demo implementeren
U kunt uw SAP-systeem voor hoge beschikbaarheid in een cloudconfiguratie implementatiemodel implementeren. Dit type implementatie is vooral nuttig voor demo en test gebruiksvoorbeelden. Het niet geschikt voor gebruiksvoorbeelden voor productie.

- In de Azure-portal op Hallo Hallo **Parameters** blade in Hallo **NEWOREXISTINGSUBNET** de optie **nieuwe**. Hallo laat **SUBNETID** veld leeg.

  Hallo SAP Azure Resource Manager sjabloon automatisch maakt Hallo virtuele Azure-netwerk en subnet.

> [!NOTE]
> U moet ook toodeploy ten minste één virtuele machine specifiek zijn voor Active Directory en DNS-server in Hallo hetzelfde exemplaar van Azure Virtual Network. Hallo-sjabloon maakt geen deze virtuele machines.
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a>Hallo-infrastructuur voorbereiden voor architecturale sjabloon 2

U kunt deze Azure Resource Manager-sjabloon gebruiken voor toohelp SAP-implementatie van resources van de vereiste infrastructuur voor SAP architectuur sjabloon 2 vereenvoudigen.

Dit is waarop u Azure Resource Manager-sjablonen kunt ophalen voor deze implementatiescenario:

* [Azure Marketplace-installatiekopie](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [Azure Marketplace-installatiekopie met schijven beheerd](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [Aangepaste installatiekopie](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [Aangepaste installatiekopie met schijven beheerd](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a>Hallo-infrastructuur voorbereiden voor architecturale sjabloon 3

U kunt Hallo infrastructuur voorbereiden en configureren van SAP voor **multi-SID**. U kunt bijvoorbeeld een extra exemplaar SAP ASC's / SCS in toevoegen een *bestaande* clusterconfiguratie. Zie voor meer informatie [configureren van een extra exemplaar SAP ASC's / SCS in een bestaand cluster configuratie toocreate een SAP multi-SID-configuratie in Azure Resource Manager][sap-ha-multi-sid-guide].

Als u een nieuw cluster met meerdere SID toocreate wilt, kunt u Hallo multi-SID [Quick Start-sjablonen op GitHub](https://github.com/Azure/azure-quickstart-templates).
een nieuw cluster met meerdere SID toocreate, moet u toodeploy Hallo drie sjablonen te volgen:

* [ASC's / SCS-sjabloon](#ASCS-SCS-template)
* [Database-sjabloon](#database-template)
* [Toepassingssjabloon voor servers](#application-servers-template)

Hallo hebben volgende secties meer informatie over het Hallo-sjablonen en moet u tooprovide in sjablonen Hallo Hallo-parameters.

#### <a name="ASCS-SCS-template"></a>ASC's / SCS-sjabloon

Hallo ASC's / SCS sjabloon implementeert twee virtuele machines dat u een failover-cluster van Windows Server die als host fungeert voor meerdere exemplaren van ASC's / SCS toocreate kunt gebruiken.

tooset van de sjabloon Hallo ASC's / SCS multi-SID in Hallo [ASC's / SCS multi-SID sjabloon] [ sap-templates-3-tier-multisid-xscs-marketplace-image] of [ASC's / SCS multi-SID-sjabloon met gebruik van schijven beheerd] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], voer waarden in voor Hallo volgende parameters:

  - **Resource-voorvoegsel**.  Hallo resource voorvoegsel, namelijk gebruikte tooprefix alle resources die zijn gemaakt tijdens de implementatie van Hallo ingesteld. Omdat Hallo bronnen geen deel van een SAP-systeem tooonly uitmaken, is Hallo-voorvoegsel van Hallo resource niet Hallo SID van een SAP-systeem.  Hallo-voorvoegsel moet liggen tussen **drie tot zes tekens**.
  - **Stack is Type**. Selecteer Hallo stack type Hallo SAP-systeem. Afhankelijk van het type van de stack hello heeft Azure Load Balancer een (ABAP of alleen Java) of twee (ABAP + Java) privé IP-adressen per SAP-systeem.
  -  **Type besturingssysteem**. Selecteer de besturingssysteem Hallo Hallo virtuele machines.
  -  **SAP System aantal**. Selecteer Hallo nummer SAP-systemen dat u wilt dat tooinstall in dit cluster.
  -  **Beschikbaarheid van het systeem**. Selecteer **HA**.
  -  **Gebruikersnaam en het beheerder beheerderswachtwoord**. Maak een nieuwe gebruiker die gebruikt toosign in toohello machine worden kan.
  -  **Nieuwe of bestaande Subnet**. Instellen of een nieuw virtueel netwerk en subnet moeten worden gemaakt of een bestaand subnet moet worden gebruikt. Als u al een virtueel netwerk dat is verbonden tooyour on-premises netwerk hebt, selecteert u **bestaande**.
  -  **Subnet-Id**. Set Hallo-ID van Hallo subnet toowhich Hallo virtuele machines moet zijn verbonden. Selecteer subnet Hallo van uw virtueel particulier netwerk (VPN) of ExpressRoute virtueel netwerk tooconnect Hallo virtuele machine tooyour on-premises netwerk. Hallo-ID ziet er meestal als volgt uit:

   /Subscriptions/ <*abonnements-id*> /resourceGroups/ <*Resourcegroepnaam*> /providers/Microsoft.Network/virtualNetworks/ <*virtuele-netwerknaam*> /subnets/ <*subnetnaam*>

Hallo sjabloon implementeert één Load Balancer van Azure-instantie, die ondersteuning biedt voor meerdere SAP-systemen.

- Hallo ASC's exemplaren worden geconfigureerd voor exemplaarnummer 00, 10, 20...
- Hallo SCS exemplaren worden geconfigureerd voor exemplaarnummer 01, 11, 21...
- Hallo ASC's in de wachtrij plaatsen replicatie Server (gebruikers) (alleen voor Linux) exemplaren worden geconfigureerd voor exemplaarnummer 02, 12, 22...
- Hallo SCS Ebruikers (alleen voor Linux) exemplaren worden geconfigureerd voor exemplaarnummer 03, 13, 23...

Hallo load balancer bevat 1 (2 voor Linux) VIP(s), 1 x-VIP voor ASC's / SCS en 1 x-VIP voor Ebruikers (alleen voor Linux).

Hallo bevat volgende lijst alle load-balancingregels (waarbij x staat voor Hallo aantal Hallo SAP-systeem, bijvoorbeeld 1, 2, 3...):
- Windows-specifieke poorten voor elke SAP-systeem: 445, 5985
- ASC's poorten (exemplaarnummer x0): 32 x 0, 36 x 0, 39 x 0, 81 x 0, 5 x 013, 5 x 014, 5 x 016
- SCS-poorten (exemplaarnummer x1): 32 x 1 33 x 1, 39 x 1, 81 x 1, 5 x 113, 5 x 114, 5 x 116
- ASCS ERS poorten op Linux (exemplaarnummer x2): 33 x 2, 5 x 213, 5 x 214, 5 x 216
- SCS ERS poorten op Linux (exemplaarnummer x3): 33 x 3, 5 x 313, 5 x 314, 5 x 316

Hallo load balancer is geconfigureerde toouse Hallo test-poorten (waarbij x staat voor Hallo aantal Hallo SAP-systeem, bijvoorbeeld 1, 2, 3...) te volgen:
- ASC's / SCS interne load balancer-testpoort: 620 0 x
- Ebruikers interne load balancer-testpoort (alleen voor Linux): 621 x 2

#### <a name="database-template"></a>Database-sjabloon

Hallo databasesjabloon implementeert een of twee virtuele machines waarmee u tooinstall kunt Hallo relationele databasebeheersysteem (RDBMS) voor een SAP-systeem. Bijvoorbeeld, als u een sjabloon ASC's / SCS voor vijf SAP-systemen implementeert, moet u toodeploy deze sjabloon vijf keer.

tooset up Hallo database multi-SID sjabloon in Hallo [multi-SID databasesjabloon] [ sap-templates-3-tier-multisid-db-marketplace-image] of [multi-SID databasesjabloon beheerd schijven] [ sap-templates-3-tier-multisid-db-marketplace-image-md], voer waarden in voor Hallo volgende parameters:

  -  **SAP-Id van het systeem**. Voer Hallo SAP systeem-ID van Hallo gewenste tooinstall SAP-systeem. Hallo-ID wordt als voorvoegsel worden gebruikt voor Hallo-resources die zijn geïmplementeerd.
  -  **Type besturingssysteem**. Selecteer de besturingssysteem Hallo Hallo virtuele machines.
  -  **DbType**. Selecteer Hallo type Hallo database dat u wilt dat tooinstall op Hallo-cluster. Selecteer **SQL** als u wilt dat tooinstall Microsoft SQL Server. Selecteer **HANA** als u van plan tooinstall SAP HANA Hallo virtuele machines bent. Zorg ervoor dat tooselect Hallo juiste operationele systeemtype: Selecteer **Windows** voor SQL, en selecteer een Linux-distributiepunt voor HANA. Hello Azure Load Balancer die is verbonden toohello virtuele machines worden geconfigureerd toosupport Hallo geselecteerd databasetype:
    * **SQL**. Hallo load balancer wordt verdelen poort 1433. Zorg ervoor dat toouse deze poort voor de installatie van SQL Server Always On.
    * **HANA**. Hallo load balancer wordt verdelen poorten 35015 en 35017. Zorg ervoor dat tooinstall SAP HANA met exemplaarnummer **50**.
    Hallo load balancer wordt testpoort 62550 gebruiken.
  -  **Grootte van het SAP**. Set Hallo aantal nieuwe Hallo-systeem SAP's bieden. Als u niet zeker hoeveel SAP's Hallo systeem is vereist weet, vraagt u uw SAP-technologie Partner of System Integrator.
  -  **Beschikbaarheid van het systeem**. Selecteer **HA**.
  -  **Gebruikersnaam en het beheerder beheerderswachtwoord**. Maak een nieuwe gebruiker die gebruikt toosign in toohello machine worden kan.
  -  **Subnet-Id**. Hallo-ID van het Hallo-subnet dat u hebt gebruikt tijdens de implementatie van Hallo ASC's / SCS sjabloon Hallo of Hallo-ID van Hallo-subnet dat is gemaakt als onderdeel van Hallo ASC's / SCS sjabloonimplementatie invoeren.

#### <a name="application-servers-template"></a>Toepassingssjabloon voor servers

Hallo-toepassingssjabloon servers implementeert twee of meer virtuele machines die kan worden gebruikt als SAP-toepassingsserver exemplaren voor een SAP-systeem. Bijvoorbeeld, als u een sjabloon ASC's / SCS voor vijf SAP-systemen implementeert, moet u toodeploy deze sjabloon vijf keer.

tooset up Hallo servers multi-SID toepassingssjabloon, in Hallo [toepassingssjabloon servers multi-SID] [ sap-templates-3-tier-multisid-apps-marketplace-image] of [servers multi-SID toepassingssjabloon beheerd schijven] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], voer waarden in voor Hallo volgende parameters:

  -  **SAP-Id van het systeem**. Voer Hallo SAP systeem-ID van Hallo gewenste tooinstall SAP-systeem. Hallo-ID wordt als voorvoegsel worden gebruikt voor Hallo-resources die zijn geïmplementeerd.
  -  **Type besturingssysteem**. Selecteer de besturingssysteem Hallo Hallo virtuele machines.
  -  **Grootte van het SAP**. Hallo aantal nieuwe Hallo-systeem SAP's bieden. Als u niet zeker hoeveel SAP's Hallo systeem is vereist weet, vraagt u uw SAP-technologie Partner of System Integrator.
  -  **Beschikbaarheid van het systeem**. Selecteer **HA**.
  -  **Gebruikersnaam en het beheerder beheerderswachtwoord**. Maak een nieuwe gebruiker die gebruikt toosign in toohello machine worden kan.
  -  **Subnet-Id**. Hallo-ID van het Hallo-subnet dat u hebt gebruikt tijdens de implementatie van Hallo ASC's / SCS sjabloon Hallo of Hallo-ID van Hallo-subnet dat is gemaakt als onderdeel van Hallo ASC's / SCS sjabloonimplementatie invoeren.


### <a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a>Virtuele Azure-netwerk
In ons voorbeeld is de adresruimte Hallo Hallo virtuele Azure-netwerk 10.0.0.0/16. Er is één subnet met de naam **Subnet**, met een adresbereik van 10.0.0.0/24. Alle virtuele machines en interne load balancers worden geïmplementeerd in dit virtuele netwerk.

> [!IMPORTANT]
> Breng geen wijzigingen toohello netwerkinstellingen in het gastbesturingssysteem Hallo. Dit omvat het IP-adressen, DNS-servers en subnet. De netwerkinstellingen configureren in Azure. Hallo Dynamic Host Configuration Protocol (DHCP)-service geeft uw instellingen.
>
>

### <a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a>DNS IP-adressen

Hallo tooset vereist dat DNS IP-adressen, Hallo stappen te volgen.

1.  In de Azure-portal op Hallo Hallo **DNS-servers** blade, zorg ervoor dat het virtuele netwerk **DNS-servers** optie is ingesteld, te**aangepaste DNS**.
2.  Selecteer uw instellingen op basis van Hallo type netwerk die u hebben. Zie voor meer informatie Hallo resources te volgen:
    * [Zakelijke netwerkverbinding (cross-premises)][planning-guide-2.2]: Hallo IP-adressen van Hallo lokale DNS-servers toevoegen.  
    U kunt de lokale DNS-servers toohello virtuele machines die worden uitgevoerd in Azure uitbreiden. In dit scenario, voegt u toe Hallo IP-adressen van hello Azure virtuele machines waarop u Hallo DNS-service uitvoert.
    * [Cloud-implementatie][planning-guide-2.1]: een extra virtuele machine implementeren in Hallo hetzelfde virtuele netwerk-exemplaar dat als een DNS-server fungeert. Toevoegen van Hallo IP-adressen van hello Azure virtuele machines die u toorun DNS-service hebt ingesteld.

    ![Afbeelding 12: DNS-servers configureren voor Azure Virtual Network][sap-ha-guide-figure-3001]

    _**Afbeelding 12:** configureren DNS-servers voor Azure Virtual Network_

  > [!NOTE]
  > Als u Hallo IP-adressen van Hallo DNS-servers wijzigt, moet u toorestart hello Azure virtuele machines tooapply Hallo wijzigen en propageren Hallo nieuwe DNS-servers.
  >
  >

Hallo DNS-service is geïnstalleerd en geconfigureerd op deze virtuele machines van Windows in ons voorbeeld:

| De rol virtuele machine | Hostnaam van de virtuele machine | Naam van de netwerk-kaart | Statisch IP-adres |
| --- | --- | --- | --- |
| Eerste DNS-server |domcontr 0 |PR1-nic-domcontr-0 |10.0.0.10 |
| Tweede DNS-server |domcontr-1 |PR1-nic-domcontr-1 |10.0.0.11 |

### <a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Hostnamen en statische IP-adressen voor Hallo SAP ASC's / SCS geclusterde exemplaar en DBMS geclusterd exemplaar

Voor on-premises implementatie moet u deze gereserveerde hostnamen en IP-adressen:

| Virtuele host naam rol | De naam van de virtuele host | Virtuele vaste IP-adres |
| --- | --- | --- |
| SAP ASC's / SCS eerste virtuele host clusternaam (voor cluster) |PR1-ASC's-vir |10.0.0.42 |
| Naam van de virtuele host op het exemplaar van SAP ASC's / SCS |PR1 ASC's sap |10.0.0.43 |
| SAP DBMS tweede virtuele host clusternaam (cluster management) |PR1-dbms-vir |10.0.0.32 |

Wanneer u Hallo-cluster maakt, maakt u Hallo virtuele hostnamen **pr1-ASC's-vir** en **pr1-dbms-vir** en Hallo bijbehorende IP-adressen die Hallo cluster zelf beheren. Voor informatie over het toodo deze, Zie [verzamelen clusterknooppunten in een clusterconfiguratie][sap-ha-guide-8.12.1].

U kunt Hallo handmatig maken andere twee virtuele hostnamen **pr1 ASC's sap** en **pr1 dbms sap**, en Hallo bijbehorende IP-adressen op Hallo DNS-server. Hallo geclusterde SAP ASC's / SCS-instantie en Hallo geclusterde DBMS instantie deze resources gebruiken. Voor informatie over het toodo deze, Zie [maken van een virtuele host-naam voor een geclusterd exemplaar van de SAP ASC's / SCS][sap-ha-guide-9.1.1].

### <a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Statische IP-adressen voor virtuele machines die Hallo SAP instellen
Nadat u Hallo virtuele machines toouse in uw cluster implementeert, moet u tooset statische IP-adressen voor alle virtuele machines. Dit doen in hello Azure Virtual Network-configuratie en niet in het gastbesturingssysteem Hallo.

1.  Selecteer in de Azure-portal hello, **resourcegroep** > **netwerkkaart** > **instellingen** > **IP-adres** .
2.  Op Hallo **IP-adressen** blade onder **toewijzing**, selecteer **statische**. In Hallo **IP-adres** Voer Hallo IP-adres dat u wilt dat toouse.

  > [!NOTE]
  > Als u Hallo IP-adres van de netwerkkaart Hallo wijzigt, moet u toorestart hello Azure virtuele machines tooapply Hallo wijzigen.  
  >
  >

  ![Afbeelding 13: Statische IP-adressen voor de netwerkkaart Hallo van elke virtuele machine instellen][sap-ha-guide-figure-3002]

  _**Afbeelding 13:** statische IP-adressen voor de netwerkkaart Hallo van elke virtuele machine instellen_

  Herhaal deze stap voor alle netwerkinterfaces, dat wil zeggen, voor alle virtuele machines, met inbegrip van virtuele machines wilt u toouse voor uw Active Directory en DNS-service.

In ons voorbeeld hebben we deze virtuele machines en statische IP-adressen:

| De rol virtuele machine | Hostnaam van de virtuele machine | Naam van de netwerk-kaart | Statisch IP-adres |
| --- | --- | --- | --- |
| Eerste SAP Application Server-exemplaar |PR1-di-0 |PR1-nic-di-0 |10.0.0.50 |
| Tweede SAP Application Server-exemplaar |PR1-di-1 |PR1-nic-di-1 |10.0.0.51 |
| ... |... |... |... |
| Laatste SAP Application Server-exemplaar |PR1-di-5 |PR1-nic-di-5 |10.0.0.55 |
| Eerste clusterknooppunt voor ASC's / SCS-exemplaar |PR1-ASC's-0 |PR1-nic-ASC's-0 |10.0.0.40 |
| Tweede clusterknooppunt voor ASC's / SCS-exemplaar |PR1-ASC's-1 |PR1-nic-ASC's-1 |10.0.0.41 |
| Eerste clusterknooppunt voor DBMS-exemplaar |PR1-db-0 |PR1-nic-db-0 |10.0.0.30 |
| Tweede clusterknooppunt voor DBMS-exemplaar |PR1-db-1 |PR1-nic-db-1 |10.0.0.31 |

### <a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Een statisch IP-adres instellen voor hello Azure interne load balancer

Hallo SAP Azure Resource Manager-sjabloon maakt u een Azure interne load balancer die wordt gebruikt voor Hallo SAP ASC's / SCS exemplaar als Hallo DBMS-cluster.

> [!IMPORTANT]
> Hallo IP-adres van de naam van de virtuele host Hallo Hallo SAP ASC's / SCS is Hallo dezelfde als de IP-adres Hallo Hallo SAP ASC's / SCS interne load balancer: **pr1-lb-ASC's**.
> Hallo IP-adres van de virtuele naam Hallo Hallo DBMS is Hallo dezelfde als de IP-adres Hallo Hallo DBMS interne load balancer: **pr1-lb-dbms**.
>
>

tooset een statisch IP-adres voor hello Azure interne load balancer:

1.  Hallo initiële implementatie ingesteld Hallo interne load balancer IP-adres te**dynamische**. In de Azure-portal op Hallo Hallo **IP-adressen** blade onder **toewijzing**, selecteer **statische**.
2.  Stel Hallo IP-adres van Hallo interne load balancer **pr1-lb-ASC's** toohello IP-adres van de naam van de virtuele host Hallo van Hallo SAP ASC's / SCS-exemplaar.
3.  Stel Hallo IP-adres van Hallo interne load balancer **pr1-lb-dbms** toohello IP-adres van de naam van de virtuele host Hallo van Hallo DBMS-exemplaar.

  ![Afbeelding 14: Statische IP-adressen voor interne load balancer Hallo voor Hallo SAP ASC's / SCS exemplaar instellen][sap-ha-guide-figure-3003]

  _**Afbeelding 14:** statische IP-adressen voor interne load balancer Hallo voor Hallo SAP ASC's / SCS exemplaar instellen_

In ons voorbeeld hebben we twee Azure interne load balancers die deze statische IP-adressen:

| Azure interne load balancer-rol | Naam Azure interne load balancer | Statisch IP-adres |
| --- | --- | --- |
| SAP ASC's / SCS exemplaar interne load balancer |PR1-lb-ASC 's |10.0.0.43 |
| SAP DBMS interne load balancer |PR1-lb-dbms |10.0.0.33 |


### <a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Standaard ASC's / SCS taakverdelingsregels voor hello Azure interne load balancer

Hallo SAP Azure Resource Manager-sjabloon maakt Hallo-poorten die u nodig:
* Een exemplaar ABAP ASCS met Hallo standaard exemplaarnummer **00**
* Een Java-SCS-exemplaar, met Hallo standaard exemplaarnummer **01**

Wanneer u uw exemplaar SAP ASC's / SCS installeert, moet u Hallo standaard exemplaarnummer **00** voor uw ABAP ASCS exemplaar en het Hallo standaard exemplaar **01** voor uw Java-SCS-exemplaar.

Vervolgens maakt u een vereiste voor de interne load balancer-eindpunten voor Hallo SAP NetWeaver poorten.

toocreate vereist interne load balancing eindpunten, maakt u eerst deze taakverdeling eindpunten voor Hallo SAP NetWeaver ABAP ASC's poorten:

| Service/load balancing regelnaam | Standaardpoortnummers | Concrete poorten voor (ASC's exemplaar met exemplaarnummer 00) (uit met 10) |
| --- | --- | --- |
| In de wachtrij plaatsen Server / *lbrule3200* |32 <*InstanceNumber*> |3200 |
| ABAP berichtenserver / *lbrule3600* |36 <*InstanceNumber*> |3600 |
| Interne ABAP bericht / *lbrule3900* |39 <*InstanceNumber*> |3900 |
| Server-HTTP-bericht / *Lbrule8100* |81 <*InstanceNumber*> |8100 |
| SAP Start Service ASC's HTTP / *Lbrule50013* |5 <*InstanceNumber*> 13 |50013 |
| SAP Start Service ASC's HTTPS / *Lbrule50014* |5 <*InstanceNumber*> 14 |50014 |
| Replicatie van de wachtrij plaatsen / *Lbrule50016* |5 <*InstanceNumber*> 16 |50016 |
| SAP Start Service Ebruikers HTTP *Lbrule51013* |5 <*InstanceNumber*> 13 |51013 |
| SAP Start Service Ebruikers HTTP *Lbrule51014* |5 <*InstanceNumber*> 14 |51014 |
| Win RM *Lbrule5985* | |5985 |
| Bestandsshare *Lbrule445* | |445 |

_**Tabel 1:** poortnummers van Hallo SAP NetWeaver ABAP ASC's exemplaren_

Vervolgens maakt u deze load balancing-eindpunten voor Hallo SAP NetWeaver Java SCS poorten:

| Service/load balancing regelnaam | Standaardpoortnummers | Concrete poorten voor (exemplaar met exemplaarnummer 01 SCS) (Ebruikers met 11) |
| --- | --- | --- |
| In de wachtrij plaatsen Server / *lbrule3201* |32 <*InstanceNumber*> |3201 |
| Gateway-Server / *lbrule3301* |33 <*InstanceNumber*> |3301 |
| Java berichtenserver / *lbrule3900* |39 <*InstanceNumber*> |3901 |
| Server-HTTP-bericht / *Lbrule8101* |81 <*InstanceNumber*> |8101 |
| SAP Start Service SCS HTTP / *Lbrule50113* |5 <*InstanceNumber*> 13 |50113 |
| SAP Start Service SCS HTTPS / *Lbrule50114* |5 <*InstanceNumber*> 14 |50114 |
| Replicatie van de wachtrij plaatsen / *Lbrule50116* |5 <*InstanceNumber*> 16 |50116 |
| SAP Start Service Ebruikers HTTP *Lbrule51113* |5 <*InstanceNumber*> 13 |51113 |
| SAP Start Service Ebruikers HTTP *Lbrule51114* |5 <*InstanceNumber*> 14 |51114 |
| Win RM *Lbrule5985* | |5985 |
| Bestandsshare *Lbrule445* | |445 |

_**Tabel 2:** poortnummers van Hallo SAP NetWeaver Java SCS exemplaren_

![Afbeelding 15: Standaard ASC's / SCS taakverdelingsregels voor hello Azure interne load balancer][sap-ha-guide-figure-3004]

_**Afbeelding 15:** standaard ASC's / SCS load-balancingregels voor hello Azure interne load balancer_

Stel IP-adres Hallo Hallo load balancer **pr1-lb-dbms** toohello IP-adres van de naam van de virtuele host Hallo van Hallo DBMS-exemplaar.

### <a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Hallo ASC's / SCS standaard load-balancingregels voor hello Azure interne load balancer wijzigen

Als u verschillende aantallen toouse voor Hallo SAP ASC's of SCS exemplaren wilt, moet u Hallo namen en waarden van de poorten wijzigen van standaardwaarden.

1.  Selecteer in de Azure-portal hello,  **<* SID*> - lb - ASC's load balancer ** > **Load Balancing regels**.
2.  Voor alle load-balancingregels die deel uitmaken van toohello SAP ASC's of SCS exemplaar, deze waarden te wijzigen:

  * Naam
  * Poort
  * Back-end-poort

  Bijvoorbeeld, als u toochange Hallo ASC's exemplaar standaardnummer van 00 too31 wilt, moet u toomake Hallo wijzigingen voor alle poorten die worden vermeld in tabel 1.

  Hier volgt een voorbeeld van een update voor poort *lbrule3200*.

  ![Afbeelding 16: Hallo ASC's / SCS standaard load-balancingregels voor hello Azure interne load balancer wijzigen][sap-ha-guide-figure-3005]

  _**Afbeelding 16:** wijziging Hallo ASC's / SCS standaard load-balancingregels voor hello Azure interne load balancer_

### <a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Windows virtuele machines toohello domein toevoegen

Nadat u een statisch IP-adres toohello virtuele machines toegewezen, voegt u Hallo virtuele machines toohello domein toe.

![Afbeelding 17: Een virtuele machine tooa-domein toevoegen][sap-ha-guide-figure-3006]

_**Afbeelding 17:** een virtuele machine tooa domein toevoegen_

### <a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Registervermeldingen op beide clusterknooppunten van Hallo SAP ASC's / SCS exemplaar toe te voegen

Azure Load Balancer heeft een interne load balancer die wordt gesloten verbindingen als Hallo verbindingen niet actief gedurende een bepaalde zijn time (niet-actieve time-out). SAP werkprocessen in de wachtrij plaatsen van dialoogvenster exemplaren geopende verbindingen toohello SAP verwerken zodra Hallo eerste in de wachtrij plaatsen/in wachtrij behoeften toobe verzonden aanvragen. Deze verbindingen meestal blijven tot stand gebrachte tot Hallo werkproces of Hallo in de wachtrij plaatsen proces opnieuw wordt opgestart. Echter, als Hallo verbinding gedurende een bepaalde tijd inactief is, hello Azure interne load balancer wordt gesloten Hallo verbindingen. Dit geen probleem omdat Hallo SAP-werkproces toohello Hallo-wachtrij plaatsen verbindingsproces herstelt als het niet meer bestaat. Deze activiteiten zijn gedocumenteerd in Hallo developer traceringen SAP-processen, maar ze een grote hoeveelheid extra inhoud in deze traceringen maken. Het is een goed idee toochange Hallo TCP/IP `KeepAliveTime` en `KeepAliveInterval` op beide clusterknooppunten. Deze wijzigingen in Hallo TCP/IP-parameters met SAP profiel parameters, dat wordt beschreven in artikel hello later worden gecombineerd.

op beide clusterknooppunten Windows toevoegen tooadd registervermeldingen op beide clusterknooppunten van Hallo SAP ASC's / SCS instantie eerst deze registervermeldingen Windows voor SAP ASC's / SCS:

| Pad | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Naam variabele |`KeepAliveTime` |
| Type variabele |REG_DWORD (decimaal) |
| Waarde |120000 |
| Koppeling toodocumentation |[https://technet.Microsoft.com/en-us/library/cc957549.aspx](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

_**Tabel 3:** wijziging Hallo eerste TCP/IP-parameter_

Voegt u deze Windows-registervermeldingen op beide clusterknooppunten Windows voor SAP ASC's / SCS:

| Pad | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Naam variabele |`KeepAliveInterval` |
| Type variabele |REG_DWORD (decimaal) |
| Waarde |120000 |
| Koppeling toodocumentation |[https://technet.Microsoft.com/en-us/library/cc957548.aspx](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

_**Tabel 4:** wijziging Hallo tweede TCP/IP-parameter_

**tooapply hello verandert, opnieuw opstarten van beide clusterknooppunten**.

### <a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a>Een cluster met Windows Server Failover Clustering voor een SAP ASC's / SCS-instantie instellen

Instellen van een cluster met Windows Server Failover Clustering voor een SAP ASC's / SCS-exemplaar, moet deze taken uitvoeren:

- Hallo clusterknooppunten in een clusterconfiguratie verzamelen
- Een cluster bestandsshare-witness configureren

#### <a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Hallo clusterknooppunten in een clusterconfiguratie verzamelen

1.  In Hallo functie toevoegen en de Wizard Functies toevoegen voor failover clustering tooboth clusterknooppunten.
2.  Hallo failover-cluster instellen met behulp van Failoverclusterbeheer. Selecteer in Failoverclusterbeheer **Cluster maken**, en voegt u alleen Hallo naam van de eerste cluster hello, knooppunt A. Voeg het tweede knooppunt Hallo nog; het tweede knooppunt Hallo voegt u in een later stadium.

  ![Afbeelding 18: Hallo-server of de naam van de virtuele machine van de eerste clusterknooppunt Hallo toevoegen][sap-ha-guide-figure-3007]

  _**Afbeelding 18:** toevoegen Hallo server of de virtuele machine de naam van het eerste clusterknooppunt Hallo_

3.  Voer Hallo netwerknaam (virtuele host-naam) van Hallo-cluster.

  ![Afbeelding 19: Voer de clusternaam Hallo][sap-ha-guide-figure-3008]

  _**Afbeelding 19:** Enter Hallo clusternaam_

4.  Nadat u Hallo cluster hebt gemaakt, voert u een clustervalidatietest.

  ![Afbeelding van 20: Hallo cluster validatiecontrole uitvoeren][sap-ha-guide-figure-3009]

  _**Afbeelding van 20:** Hallo cluster validatiecontrole uitvoeren_

  U kunt waarschuwingen met betrekking tot schijven op dit moment in Hallo proces negeren. U voegt dat een bestandssharewitness en Hallo SIOS gedeelde schijven later. In dit stadium hoeft u geen tooworry over het hebben van een quorum.

  ![Afbeelding 21: Er is geen quorumschijf is gevonden.][sap-ha-guide-figure-3010]

  _**Afbeelding 21:** geen quorumschijf is gevonden_

  ![Afbeelding 22: Core cluster-bron moet een nieuw IP-adres][sap-ha-guide-figure-3011]

  _**Afbeelding 22:** Core cluster-bron moet een nieuw IP-adres_

5.  Hallo IP-adres van Hallo core cluster-service wijzigen. Hallo-cluster starten niet totdat u Hallo IP-adres van de clusterservice Hallo-core, wijzigt omdat Hallo IP-adres van de server Hallo tooone van knooppunten van de virtuele machine Hallo verwijst. Dit doen op Hallo **eigenschappen** pagina van Hallo core cluster-service van IP-resource.

  Bijvoorbeeld, moeten we tooassign een IP-adres (in ons voorbeeld **10.0.0.42**) voor de naam van de virtuele host cluster Hallo **pr1-ASC's-vir**.

  ![Afbeelding 23: In Hallo eigenschappen in het dialoogvenster Hallo IP-adres wijzigen][sap-ha-guide-figure-3012]

  _**Afbeelding 23:** In Hallo **eigenschappen** in het dialoogvenster, wijziging Hallo IP-adres_

  ![Afbeelding 24: Hallo IP-adres dat is gereserveerd voor Hallo cluster toewijzen][sap-ha-guide-figure-3013]

  _**Afbeelding 24:** Hallo IP-adres dat is gereserveerd voor Hallo cluster toewijzen_

6.  Hallo virtuele host clusternaam online brengen.

  ![Afbeelding 25: Core de clusterservice actief is en uitgevoerd en Hello Corrigeer IP-adres][sap-ha-guide-figure-3014]

  _**Afbeelding 25:** core de clusterservice actief is en uitgevoerd, en met Hallo Corrigeer IP-adres_

7.  De tweede clusterknooppunt Hallo toevoegen.

  Nu Hallo core cluster-service actief is, kunt u de tweede clusterknooppunt Hallo toevoegen.

  ![Afbeelding 26: Hallo tweede clusterknooppunt toevoegen][sap-ha-guide-figure-3015]

  _**Afbeelding 26:** toevoegen Hallo tweede clusterknooppunt_

8.  Voer een naam voor Hallo tweede knooppunt clusterhost.

  ![Afbeelding 27: Voer Hallo tweede hostnaam voor het clusterknooppunt][sap-ha-guide-figure-3016]

  _**Afbeelding 27:** Enter Hallo tweede hostnaam voor het clusterknooppunt_

  > [!IMPORTANT]
  > Zorg dat Hallo **Voeg alle in aanmerking komende opslag toohello cluster** selectievakje **niet** geselecteerde.  
  >
  >

  ![Afbeelding 28: Schakel niet Hallo selectievakje][sap-ha-guide-figure-3017]

  _**Afbeelding 28:** doen **niet** Selecteer Hallo selectievakje_

  U kunt waarschuwingen over quorum en schijven negeren. Stelt u Hallo quorum en -share Hallo schijf later, zoals beschreven in [SIOS DataKeeper Cluster Edition installeren voor de clusterschijf share SAP ASC's / SCS][sap-ha-guide-8.12.3].

  ![Afbeelding 29: Negeren van waarschuwingen over Hallo schijf quorum][sap-ha-guide-figure-3018]

  _**Afbeelding 29:** negeren van waarschuwingen over Hallo schijf quorum_


#### <a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a>Een cluster bestandsshare-witness configureren

Een cluster bestandsshare-witness configureren, moet deze taken uitvoeren:

- Een bestandsshare maken
- Instelling Hallo bestand bestandsshare-witness quorum in Failoverclusterbeheer

##### <a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a>Een bestandsshare maken

1.  Selecteer een bestandssharewitness in plaats van een quorumschijf. SIOS DataKeeper ondersteunt deze optie.

  In Hallo voorbeelden in dit artikel is het Hallo bestandssharewitness op Hallo Active Directory en DNS-server die wordt uitgevoerd in Azure. Hallo bestandsshare-witness wordt aangeroepen **domcontr 0**. Omdat u zou een VPN-verbinding tooAzure (via Site-naar-Site VPN- of Azure ExpressRoute) hebt geconfigureerd, kunt u met uw Active Directory en DNS-service is on-premises en is niet geschikt toorun een bestand witness delen.

  > [!NOTE]
  > Als uw Active Directory en DNS-service wordt uitgevoerd alleen lokale, niet de bestandsshare-witness configureren op Hallo Active Directory en DNS-Windows-besturingssysteem die lokaal wordt uitgevoerd. Netwerklatentie tussen clusterknooppunten uitgevoerd in Azure en Active Directory en DNS-on-premises mogelijk te groot zijn en leiden tot problemen met de netwerkverbinding. Worden ervoor tooconfigure Hallo bestandssharewitness op een virtuele machine van Azure met sluiten toohello clusterknooppunt.  
  >
  >

  Hallo quorumstation moet ten minste 1024 MB vrije ruimte. We raden 2048 MB aan vrije ruimte voor Hallo quorum-station aan.

2.  Hallo clusternaamobject toevoegen.

  ![Afbeelding 30: Hallo-machtigingen op Hallo share voor Hallo clusternaamobject toewijzen][sap-ha-guide-figure-3019]

  _**Afbeelding 30:** Hallo-machtigingen op Hallo share voor Hallo clusternaamobject toewijzen_

  Zorg dat Hallo machtigingen Hallo autoriteit toochange gegevens in Hallo share voor Hallo clusternaamobject bevatten (in ons voorbeeld **pr1-ASC's-vir$**).

3.  tooadd hello cluster naam toohello objectenlijst, selecteer **toevoegen**. Hallo filter toocheck voor computerobjecten in toevoeging toothose wordt weergegeven in afbeelding 31 wijzigen.

  ![Afbeelding 31: Hallo objecttypen tooinclude computers wijzigen][sap-ha-guide-figure-3020]

  _**Afbeelding 31:** Hallo objecttypen tooinclude computers wijzigen_

  ![Afbeelding 32: Selectievakje Hallo Computers][sap-ha-guide-figure-3021]

  _**Afbeelding 32:** Selecteer Hallo **Computers** selectievakje_

4.  Voer Hallo clusternaamobject zoals in afbeelding 31. Omdat Hallo record al is gemaakt, kunt u Hallo-machtigingen kunt wijzigen, zoals wordt weergegeven in afbeelding 30.

5.  Selecteer Hallo **beveiliging** tabblad van het Hallo-share- en vervolgens moet u meer gedetailleerde machtigingen voor Hallo clusternaamobject.

  ![Afbeelding 33: Hallo beveiligingskenmerken instellen voor clusternaamobject Hallo Hallo file share quorum][sap-ha-guide-figure-3022]

  _**Afbeelding 33:** Hallo beveiligingskenmerken instellen voor clusternaamobject Hallo Hallo file share quorum_

##### <a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Set Hallo bestand bestandsshare-witness quorum in Failoverclusterbeheer

1.  Open Hallo Wizard configureren Quorum-instelling.

  ![Afbeelding 34: Start Hallo Wizard instelling clusterquorum configureren][sap-ha-guide-figure-3023]

  _**Afbeelding 34:** Start de Wizard clusterquorum configureren instelling Hallo_

2.  Op Hallo **quorumconfiguratie selecteren** pagina **hello quorumwitness selecteren**.

  ![Afbeelding 35: Quorumconfiguraties u kunt kiezen uit][sap-ha-guide-figure-3024]

  _**Afbeelding 35:** quorumconfiguraties kunt u kiezen uit_

3.  Op Hallo **Quorumwitness selecteren** pagina **een bestandssharewitness configureren**.

  ![Afbeelding 36: Selecteer Hallo bestandsshare-witness][sap-ha-guide-figure-3025]

  _**Afbeelding 36:** Hallo bestandssharewitness selecteren_

4.  Voer Hallo UNC-pad toohello bestandsshare (in ons voorbeeld \\domcontr 0\FSW). een lijst met Hallo wijzigingen kunt u, selecteer toosee **volgende**.

  ![Afbeelding 37: Hallo bestandsshare-locatie voor de witness-share Hallo definiëren][sap-ha-guide-figure-3026]

  _**Afbeelding 37:** Hallo bestandsshare-locatie voor de witness-share Hallo definiëren_

5.  Selecteer Hallo wijzigingen die u wilt en selecteer vervolgens **volgende**. U moet toosuccessfully Hallo clusterconfiguratie configureren zoals wordt weergegeven in afbeelding 38.  

  ![Afbeelding 38: Bevestiging dat u opnieuw hebt geconfigureerd Hallo-cluster][sap-ha-guide-figure-3027]

  _**Afbeelding 38:** bevestiging dat u opnieuw hebt geconfigureerd Hallo-cluster_

Na de installatie is Windows Failover Cluster hello, moeten de wijzigingen toobe toosome drempelwaarden tooadapt failover detectie tooconditions aangebracht in Azure. Hallo parameters toobe gewijzigd, worden beschreven in deze blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/. Ervan uitgaande dat uw twee virtuele machines die bouwen Hallo zijn Windows Cluster-configuratie voor ASC's / SCS in hetzelfde SubNet hello, hello volgende parameters moeten toobe gewijzigd toothese waarden:
- SameSubNetDelay = 2
- SameSubNetThreshold = 15

Deze instellingen zijn getest met klanten en een goede inbreuk toobe robuust genoeg opgegeven Hallo-een-zijde. Op Hallo daarentegen deze instellingen zijn bieden snel genoeg failover in een echte foutcondities op SAP-software of het knooppunt/VM-fout. 

### <a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>SIOS DataKeeper Cluster Edition voor Hallo SAP ASC's / SCS clusterschijf delen installeren

U hebt nu een werkende configuratie van Windows Server Failover Clustering in Azure. Maar tooinstall een SAP ASC's / SCS-exemplaar, moet u een gedeelde schijf-resource. U kunt Hallo gedeelde schijfbronnen die u nodig in Azure maken. SIOS DataKeeper Cluster Edition is een oplossing van derden, kunt u de schijfbronnen toocreate gedeeld.

Het installeren van SIOS DataKeeper Cluster Edition voor Hallo SAP ASC's / SCS omvat share clusterschijf deze taken:

- Hallo .NET Framework 3.5 toevoegen
- SIOS DataKeeper installeren
- SIOS DataKeeper instellen

#### <a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Hallo .NET Framework 3.5 toevoegen
Hallo Microsoft .NET Framework 3.5 is niet automatisch geactiveerd of Windows Server 2012 R2 is geïnstalleerd. Omdat SIOS DataKeeper Hallo .NET Framework toobe op alle knooppunten die u vereist op DataKeeper installeert, moet u Hallo .NET Framework 3.5 installeren op Hallo gastbesturingssysteem van alle virtuele machines in het Hallo-cluster.

Er zijn twee manieren tooadd Hallo .NET Framework 3.5:

- Gebruik Wizard Hallo toevoegen functies en onderdelen in Windows zoals in afbeelding 39.

  ![Afbeelding 39: Hallo .NET Framework 3.5 installeren met behulp van de Wizard Hallo toevoegen functies en onderdelen][sap-ha-guide-figure-3028]

  _**Afbeelding 39:** installeren Hallo .NET Framework 3.5 met behulp van de Wizard Hallo toevoegen functies en onderdelen_

  ![Afbeelding 40: Installatie van de voortgangsbalk wanneer u Hallo .NET Framework 3.5 installeren met behulp van de Wizard Hallo toevoegen functies en onderdelen][sap-ha-guide-figure-3029]

  _**Afbeelding 40:** installatie van de voortgangsbalk wanneer u Hallo .NET Framework 3.5 installeren met behulp van de Wizard Hallo toevoegen functies en onderdelen_

- Gebruik Hallo opdrachtregelprogramma dism.exe. Voor dit type installatie moet u tooaccess Hallo SxS-map op de installatiemedia voor Windows hello. Typ bij een opdrachtprompt met verhoogde bevoegdheid:

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <a name="dd41d5a2-8083-415b-9878-839652812102"></a>SIOS DataKeeper installeren

SIOS DataKeeper Cluster Edition installeren op elk knooppunt in het Hallo-cluster. toocreate virtuele gedeelde opslag met SIOS DataKeeper, maakt u een gesynchroniseerde mirror en vervolgens simuleren gedeelde clusteropslag.

Voordat u Hallo SIOS software installeert, maken de domeingebruiker Hallo **DataKeeperSvc**.

> [!NOTE]
> Hallo toevoegen **DataKeeperSvc** gebruiker toohello **lokale beheerder** groep op beide clusterknooppunten.
>
>

tooinstall SIOS DataKeeper:

1.  Hallo SIOS software installeren op beide clusterknooppunten.

  ![SIOS installatieprogramma][sap-ha-guide-figure-3030]

  ![Afbeelding 41: Eerste pagina van Hallo SIOS DataKeeper installatie][sap-ha-guide-figure-3031]

  _**Afbeelding 41:** eerste pagina van Hallo SIOS DataKeeper installatie_

2.  Selecteer Hallo in het dialoogvenster wordt weergegeven in afbeelding 42 **Ja**.

  ![Afbeelding 42: DataKeeper informeert u dat een service wordt uitgeschakeld][sap-ha-guide-figure-3032]

  _**Afbeelding 42:** DataKeeper informeert u dat een service wordt uitgeschakeld_

3.  Hallo in het dialoogvenster wordt weergegeven in afbeelding 43 wordt aangeraden dat u selecteert **domein of de Server account**.

  ![Afbeelding 43: Selectie van de de gebruiker voor SIOS DataKeeper][sap-ha-guide-figure-3033]

  _**Afbeelding 43:** gebruikersselectie voor SIOS DataKeeper_

4.  Voer Hallo account domeingebruikersnaam en wachtwoorden op dat u hebt gemaakt voor SIOS DataKeeper.

  ![Afbeelding 44: Hallo domeingebruikersnaam en wachtwoord invoeren voor Hallo SIOS DataKeeper installatie][sap-ha-guide-figure-3034]

  _**Afbeelding 44:** Hallo domeingebruikersnaam en wachtwoord invoeren voor Hallo SIOS DataKeeper installatie_

5.  De licentiesleutel Hallo voor uw exemplaar SIOS DataKeeper zoals in afbeelding 45 installeren.

  ![Afbeelding 45: Voer uw licentiecode SIOS DataKeeper][sap-ha-guide-figure-3035]

  _**Afbeelding 45:** uw licentiesleutel SIOS DataKeeper invoeren_

6.  Wanneer u wordt gevraagd, moet u Hallo virtuele machine opnieuw opstarten.

#### <a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a>SIOS DataKeeper instellen

Nadat u SIOS DataKeeper op beide knooppunten hebt geïnstalleerd, moet u toostart Hallo configuratie. Hallo-doel van Hallo-configuratie is toohave synchrone gegevensreplicatie tussen Hallo extra schijven tooeach van Hallo virtuele machines die zijn gekoppeld.

1.  Hallo DataKeeper beheer en hulpprogramma voor serverconfiguratie starten en selecteer vervolgens **verbinding maken met Server**. (In de afbeelding 46 deze optie is met een rode cirkel.)

  ![46 afbeelding: De SIOS DataKeeper beheer en het hulpprogramma voor serverconfiguratie][sap-ha-guide-figure-3036]

  _**Afbeelding 46:** SIOS DataKeeper beheer en de configuratie-hulpprogramma_

2.  Hallo naam invoeren of TCP/IP-adres van Hallo eerste knooppunt Hallo beheer en de configuratie-hulpprogramma moet verbinding maken, en, in een tweede stap van de tweede Hallo-knooppunt.

  ![Afbeelding 47: Insert Hallo naam of TCP/IP-adres van Hallo eerste knooppunt Hallo beheer en de configuratie-hulpprogramma moet verbinding maken, en in een tweede stap van het tweede knooppunt Hallo][sap-ha-guide-figure-3037]

  _**Afbeelding 47:** Insert Hallo naam of TCP/IP-adres van Hallo eerste knooppunt Hallo beheer en de configuratie-hulpprogramma verbinding moet maken, en in een tweede stap van het tweede knooppunt Hallo_

3.  Hallo replicatie taak tussen twee knooppunten Hallo maken.

  ![Afbeelding van 48: Een replicatie-taak maken][sap-ha-guide-figure-3038]

  _**Afbeelding van 48:** een replicatie-taak maken_

  Een wizard leidt u door het Hallo-proces voor het maken van een taak voor replicatie.
4.  Hallo-naam, de TCP/IP-adres en de schijfvolume van het bronknooppunt Hallo definiëren.

  ![Afbeelding 49: Hallo-naam van Hallo replicatie taak definiëren][sap-ha-guide-figure-3039]

  _**Afbeelding 49:** definiëren Hallo-naam van Hallo replicatie taak_

  ![Afbeelding 50: Basisgegevens voor Hallo-knooppunt, de huidige bronknooppunt Hallo moet Hallo definiëren][sap-ha-guide-figure-3040]

  _**Afbeelding 50:** basisgegevens voor Hallo-knooppunt, de huidige bronknooppunt Hallo moet Hallo definiëren_

5.  Hallo-naam, de TCP/IP-adres en de schijfvolume van het doelknooppunt Hallo definiëren.

  ![Afbeelding 51: Basisgegevens voor Hallo-knooppunt, de huidige doelknooppunt Hallo moet Hallo definiëren][sap-ha-guide-figure-3041]

  _**Afbeelding 51:** basisgegevens voor Hallo-knooppunt, de huidige doelknooppunt Hallo moet Hallo definiëren_

6.  Hallo compressie algoritmen definiëren. In ons voorbeeld is het raadzaam dat u Hallo replicatiestroom comprimeren. Met name in situaties hersynchronisatie minder Hallo-compressie van Hallo replicatiestroom aanzienlijk hersynchronisatie-tijd. Houd er rekening mee dat compressie Hallo CPU en RAM-geheugen van een virtuele machine verbruikt. Als Hallo compressie snelheid toeneemt, dus Hallo volume aan CPU-resources die worden gebruikt. Ook kunt u aanpassen deze instelling later.

7.  Een andere instelling die u moet toocheck is of Hallo replicatie synchroon of asynchroon. *Wanneer u SAP ASC's / SCS configuraties beveiligt, moet u synchrone replicatie*.  

  ![Afbeelding 52: Replicatiedetails definiëren][sap-ha-guide-figure-3042]

  _**Afbeelding 52:** replicatiedetails definiëren_

8.  Definieer of Hallo volume die is gerepliceerd door Hallo taak vertegenwoordigde tooa Windows Server Failover Clustering clusterconfiguratie als gedeelde schijf moet zijn. Hallo SAP ASC's / SCS configuratie, selecteert u **Ja** zodat Hallo Windows cluster ziet Hallo gerepliceerde volume als een gedeelde schijf die kan worden gebruikt als een clustervolume.

  ![Afbeelding 53: Selecteer Ja tooset Hallo gerepliceerd volume als een clustervolume][sap-ha-guide-figure-3043]

  _**Afbeelding 53:** Selecteer **Ja** tooset Hallo gerepliceerd volume als een clustervolume_

  Nadat Hallo volume is gemaakt, ziet u Hallo DataKeeper beheer en de configuratie-hulpprogramma dat taak Hallo-replicatie is actief.

  ![Afbeelding 54: Synchroon spiegelen van DataKeeper voor Hallo SAP ASC's / SCS share schijf actief is.][sap-ha-guide-figure-3044]

  _**Afbeelding 54:** DataKeeper synchroon spiegelen voor hello SAP ASC's / SCS schijf delen is actief_

  Hallo-schijf als een schijf DataKeeper weergegeven Failoverclusterbeheer nu zoals in afbeelding 55.

  ![Afbeelding 55: Failover Cluster Manager toont Hallo-schijf die DataKeeper gerepliceerd][sap-ha-guide-figure-3045]

  _**Afbeelding 55:** Failover Cluster Manager toont Hallo schijf die is gerepliceerd DataKeeper_

## <a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Hallo SAP NetWeaver systeem installeert

Hallo DBMS setup won't worden beschreven omdat instellingen variëren, afhankelijk van Hallo DBMS systeem u gebruikt. Echter, gaan we ervan uit dat hoge beschikbaarheid weergegeven met de Hallo DBMS worden aangepakt met Hallo functionaliteiten Hallo verschillende DBMS leveranciers ondersteuning voor Azure. Bijvoorbeeld altijd op of database mirroring voor SQL Server en Oracle Data Guard voor Oracle-databases. We toevoegen niet meer bescherming toohello DBMS in Hallo scenario we in dit artikel gebruiken.

Er zijn geen speciale overwegingen bij verschillende DBMS services met dit soort clusterconfiguratie SAP ASC's / SCS in Azure communiceren.

> [!NOTE]
> Hallo installatieprocedures van SAP NetWeaver ABAP systemen, Java-systemen en ABAP + Java systemen zijn bijna identiek. Hallo belangrijkste verschil is dat een SAP ABAP systeem een exemplaar van de ASC's heeft. Hallo SAP Java systeem heeft een SCS-exemplaar. Hallo SAP ABAP + Java systeem heeft een exemplaar van de ASC's en één SCS-exemplaar in Hallo dezelfde Microsoft failover cluster-groep. Eventuele verschillen installatie voor elke installatie SAP NetWeaver stack worden expliciet vermeld. Alle andere onderdelen zijn dezelfde hello, kunt u aannemen.  
>
>

### <a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a>SAP installeren met een hoge beschikbaarheid ASC's / SCS-exemplaar

> [!IMPORTANT]
> Zorg ervoor dat geen tooplace uw pagina bestand op DataKeeper gespiegelde volumes. DataKeeper biedt geen ondersteuning voor gespiegelde volumes. U kunt uw wisselbestand op Hallo tijdelijke station D van een virtuele machine van Azure, laten Hallo standaardinstelling. Als deze nog niet is gebeurd, verplaatst u Hallo Windows pagina bestand toodrive D: van uw Azure-machine.
>
>

SAP installeren met een exemplaar van de ASC's / SCS hoge beschikbaarheid, moet deze taken uitvoeren:

- Maken van een virtuele host-naam voor geclusterde Hallo SAP ASC's / SCS exemplaar
- Eerste Hallo SAP-clusterknooppunt installeren
- Hallo SAP-profiel van Hallo ASC's / SCS-exemplaar wijzigen
- Een testpoort toevoegen
- Hallo Windows firewall-testpoort openen

#### <a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Een virtuele host-naam voor geclusterde Hallo SAP ASC's / SCS exemplaar maken

1.  Maak een DNS-vermelding voor de naam van de virtuele host Hallo van Hallo ASC's / SCS exemplaar in Hallo Windows DNS-beheer.

  > [!IMPORTANT]
  > Hallo IP-adres dat u de naam van de virtuele host toohello Hallo ASC's / SCS-exemplaar moet toewijzen Hallo dezelfde als Hallo IP-adres dat aan u toegewezen tooAzure Load Balancer (**<*SID*> - lb - ASC's **).  
  >
  >

  Hallo IP-adres van de virtuele SAP ASC's / SCS Hallo-hostnaam (**pr1 ASC's sap**) is dezelfde als Hallo IP-adres van de Load Balancer van Azure Hallo (**pr1-lb-ASC's**).

  ![Afbeelding 56: Definieer Hallo DNS-vermelding voor de virtuele clusternaam Hallo SAP ASC's / SCS en TCP/IP-adres][sap-ha-guide-figure-3046]

  _**Afbeelding 56:** Hallo DNS-vermelding voor de virtuele clusternaam Hallo SAP ASC's / SCS en TCP/IP-adres definiëren_

2.  toodefine hello IP-adres is toegewezen toohello naam virtuele host op, selecteer **DNS-beheer** > **domein**.

  ![57 afbeelding: De nieuwe virtuele naam en het TCP/IP-adres voor de clusterconfiguratie SAP ASC's / SCS][sap-ha-guide-figure-3047]

  _**Afbeelding 57:** nieuwe virtuele naam en het TCP/IP-adres voor SAP ASC's / SCS-clusterconfiguratie_

#### <a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Eerste Hallo SAP-clusterknooppunt installeren

1.  Hallo eerste cluster knooppunt optie op clusterknooppunt A. uitvoeren Bijvoorbeeld: op Hallo **pr1-ASC's-0** host.
2.  tookeep Hallo-standaardpoorten voor hello Azure interne load balancer, selecteren:

  * **ABAP system**: **ASC's** exemplaar nummer **00**
  * **Java-systeem**: **SCS** exemplaar nummer **01**
  * **ABAP + Java system**: **ASC's** exemplaar nummer **00** en **SCS** exemplaar nummer **01**

  toouse exemplaar getallen andere dan 00 voor Hallo ABAP ASCS exemplaar en 01 voor Hallo Java SCS exemplaar, moet u eerst toochange hello Azure interne load balancer standaard load-balancingregels beschreven in [wijziging Hallo ASC's / SCS standaard laden regels voor hello Azure interne load balancer Balancing][sap-ha-guide-8.9].

Hello worden niet volgende enkele taken beschreven in Hallo standaard SAP documentatie voor de installatie.

> [!NOTE]
> Hallo SAP installatie documentatie wordt beschreven hoe tooinstall Hallo eerste ASC's / SCS-clusterknooppunt.
>
>

#### <a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Hallo SAP-profiel van Hallo ASC's / SCS-exemplaar wijzigen

U moet een nieuwe profiel-parameter tooadd. Hallo profiel parameter voorkomt dat verbindingen tussen processen SAP en Hallo in de wachtrij plaatsen server af te sluiten wanneer ze niet actief is te lang zijn. Gezegd Hallo probleem scenario in [registervermeldingen toe te voegen op beide clusterknooppunten van Hallo SAP ASC's / SCS exemplaar][sap-ha-guide-8.11]. In deze sectie geïntroduceerd we ook twee wijzigingen toosome eenvoudige TCP/IP-verbindingsparameters. In een tweede stap moet u tooset Hallo in de wachtrij plaatsen server toosend een `keep_alive` signaal zodat Hallo verbindingen niet hello Azure interne load balancer niet-actieve drempelwaarde bereikt.

toomodify hello SAP-profiel van Hallo ASC's / SCS exemplaar:

1.  Dit profiel parameter toohello SAP ASC's / SCS exemplaar profiel toevoegen:

  ```
  enque/encni/set_so_keepalive = true
  ```
  In ons voorbeeld Hallo pad als volgt:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  Bijvoorbeeld toohello SAP SCS exemplaar profiel en het bijbehorende pad:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  tooapply hello wijzigingen, Hallo SAP ASC's /SCS exemplaar opnieuw starten.

#### <a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a>Een testpoort toevoegen

Hallo interne load balancer-test functionaliteit toomake Hallo clusteroplossing configuratiewerk gebruiken met Azure Load Balancer. Hello Azure interne load balancer distribueert meestal Hallo binnenkomende werkbelasting gelijkmatig tussen deelnemende virtuele machines. Echter werkt dat niet in bepaalde clusterconfiguraties omdat er slechts één exemplaar actief is. Hallo andere exemplaar is passieve en kan niet alle Hallo werkbelasting accepteren. Een test-functionaliteit helpt wanneer hello Azure interne load balancer wordt toegewezen alleen tooan actieve sessie werkt. Hallo interne load balancer kan met Hallo test functionaliteit detecteren welke exemplaren actief zijn en vervolgens de doelinstantie alleen Hallo met Hallo werklast.

tooadd een testpoort:

1.  Controleer de huidige Hallo **ProbePort** instellen door het volgende PowerShell-opdracht Hallo uitvoeren. Deze niet binnen één Hallo virtuele machines worden uitgevoerd in Hallo clusterconfiguratie.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  Definieer een testpoort. Hallo test standaardpoortnummer is **0**. In ons voorbeeld gebruiken we de testpoort **62000**.

  ![Afbeelding 58: Hallo cluster configuratie de testpoort is 0 standaard][sap-ha-guide-figure-3048]

  _**Afbeelding 58:** Hallo cluster configuration test standaardpoort is 0_

  Hallo-poortnummer is gedefinieerd in SAP Azure Resource Manager-sjablonen. U kunt Hallo poortnummer in PowerShell kunt toewijzen.

  een nieuwe ProbePort-waarde voor Hallo tooset  **SAP <*SID*> IP-** clusterbron, Hallo volgende PowerShell-script uitvoeren. Hallo PowerShell variabelen voor uw omgeving bijwerken. Nadat het Hallo-script wordt uitgevoerd, moet u na vragen aan gebruiker toorestart Hallo SAP cluster tooactivate Hallo wijzigingen.

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  Nadat u Hallo brengt  **SAP <*SID*> ** cluster online rol, Controleer **ProbePort** toohello nieuwe waarde is ingesteld.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Afbeelding 59: Test Hallo cluster poort nadat u de nieuwe waarde Hallo instellen][sap-ha-guide-figure-3049]

  _**Afbeelding 59:** Probe Hallo cluster poort nadat u de nieuwe waarde Hallo instellen_

#### <a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Hallo Windows firewall-testpoort openen

U moet een Windows firewall-test poort op beide clusterknooppunten tooopen. Gebruik Hallo script tooopen een test-poort van Windows firewall te volgen. Hallo PowerShell variabelen voor uw omgeving bijwerken.

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

Hallo **ProbePort** te is ingesteld,**62000**. Nu u toegang hebt tot de bestandsshare Hallo  **\\\ascsha-clsap\sapmnt** met andere hosts, zoals als van **ascsha-DBA's**.

### <a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Hallo-database-exemplaar installeren

tooinstall hello database-exemplaar, voert u de Hallo-proces dat wordt beschreven in Hallo SAP-documentatie voor installatie.

### <a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>De tweede clusterknooppunt Hallo installeren

tooinstall hello tweede cluster, volg de stappen Hallo in Hallo SAP installatiehandleiding.

### <a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Hallo het starttype Hallo SAP Ebruikers Windows service-exemplaar wijzigen

Het starttype Hallo Hallo SAP Ebruikers Windows-service ook wijzigen**automatisch (vertraagd starten)** op beide clusterknooppunten.

![Afbeelding 60: Hallo servicetype voor Hallo SAP Ebruikers exemplaar toodelayed automatische wijzigen][sap-ha-guide-figure-3050]

_**Afbeelding 60:** Hallo servicetype voor Hallo SAP Ebruikers exemplaar toodelayed automatische wijzigen_

### <a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Hallo SAP primaire toepassingsserver installeren

Hallo primaire Application Server (PAS)-exemplaar installeren <*SID*> - di - 0 op Hallo virtuele machine die u hebt opgegeven toohost Hallo Pa's. Er zijn geen afhankelijkheden op Azure of DataKeeper-specifieke instellingen.

### <a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Hallo SAP aanvullende toepassingsserver installeren

Een SAP aanvullende Application Server (AAS) installeren op alle Hallo virtuele machines dat u hebt aangewezen toohost een SAP Application Server-exemplaar. Bijvoorbeeld: op <*SID*> - di - 1 te <*SID*> - di -&lt;n&gt;.

> [!NOTE]
> Dit is voltooid Hallo-installatie van een hoge beschikbaarheid SAP NetWeaver-systeem. Vervolgens gaat u verder met het testen van failover.
>


## <a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Hallo SAP ASC's / SCS exemplaar failover en SIOS replicatie testen
Het is gemakkelijk tootest en een SAP ASC's / SCS exemplaar failover en SIOS schijfreplicatie bewaken met behulp van Failoverclusterbeheer en Hallo SIOS DataKeeper beheer en de configuratie-hulpprogramma.

### <a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a>SAP ASC's / SCS-exemplaar wordt uitgevoerd op een clusterknooppunt A

Hallo **SAP PR1** clustergroep wordt uitgevoerd op een clusterknooppunt A. Bijvoorbeeld: op **pr1-ASC's-0**. Toewijzen van gedeelde Hallo schijfstation S, die deel uitmaakt van Hallo **SAP PR1** cluster groep en welk Hallo ASC's / SCS-exemplaar gebruikt, toocluster knooppunt A.

![Afbeelding 61: Failover Cluster Manager: Hallo SAP < SID > clustergroep wordt uitgevoerd op een clusterknooppunt A][sap-ha-guide-figure-5000]

_**Afbeelding 61:** Failoverclusterbeheer: SAP Hallo <*SID*> clustergroep wordt uitgevoerd op een clusterknooppunt A_

In het Hallo SIOS DataKeeper beheer en hulpprogramma voor serverconfiguratie ziet u dat Hallo gedeelde schijf gegevens synchroon worden gerepliceerd vanaf Hallo bron volume station S op clusterknooppunt een toohello volume doelstation S op clusterknooppunt B. Bijvoorbeeld, worden gerepliceerd van **pr1 ASC's 0 [10.0.0.40]** te**pr1-ASC's-1 [10.0.0.41]**.

![Afbeelding 62: In SIOS DataKeeper, repliceert u Hallo lokaal volume van het clusterknooppunt een knooppunt toocluster B][sap-ha-guide-figure-5001]

_**Afbeelding 62:** repliceren In SIOS DataKeeper, Hallo lokaal volume van het clusterknooppunt een knooppunt toocluster B_

### <a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Failover van knooppunt A toonode B

1.  Kies een van deze opties tooinitiate een failover van Hallo SAP <*SID*> clustergroep van knooppunt A toocluster clusterknooppunt B:
  - Gebruik Failoverclusterbeheer  
  - Failover-Cluster PowerShell gebruiken

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  Start opnieuw op een van de cluster-knooppunt in Hallo Windows-gastbesturingssysteem (Hiermee initieert u een automatische failover Hallo SAP <*SID*> clustergroep van knooppunt A toonode B).  
3.  Start opnieuw op een van de cluster-knooppunt van hello Azure-portal (Hiermee initieert u een automatische failover Hallo SAP <*SID*> clustergroep van knooppunt A toonode B).  
4.  Cluster-knooppunt een starten met Azure PowerShell (Hiermee initieert u een automatische failover Hallo SAP <*SID*> clustergroep van knooppunt A toonode B).

  Na een failover Hallo SAP <*SID*> clustergroep wordt uitgevoerd op een clusterknooppunt B. Bijvoorbeeld, deze wordt uitgevoerd op **pr1-ASC's-1**.

  ![Afbeelding 63: In Failoverclusterbeheer Hallo SAP < SID > clustergroep wordt uitgevoerd op het clusterknooppunt B][sap-ha-guide-figure-5002]

  _**Afbeelding 63**: In Failoverclusterbeheer, Hallo SAP <*SID*> clustergroep wordt uitgevoerd op een clusterknooppunt B_

  Hallo gedeelde schijf is nu gekoppeld op cluster knooppunt B. SIOS DataKeeper is repliceren van gegevens vanaf bron volume station S op knooppunt B tootarget volume clusterstation S op clusterknooppunt A. Bijvoorbeeld, van repliceren **pr1-ASC's-1 [10.0.0.41]** te**pr1 ASC's 0 [10.0.0.40]**.

  ![Afbeelding 64: SIOS DataKeeper repliceert Hallo lokaal volume van knooppunt B toocluster clusterknooppunt A][sap-ha-guide-figure-5003]

  _**Afbeelding 64:** SIOS DataKeeper repliceert Hallo lokaal volume van knooppunt B toocluster clusterknooppunt A_
