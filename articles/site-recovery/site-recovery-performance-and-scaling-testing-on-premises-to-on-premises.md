---
title: aaaTest resultaten voor Hyper-V-replicatie tussen sites met Azure Site Recovery | Microsoft Docs
description: In dit artikel bevat informatie over de prestatietests voor de lokale tooon-premises replicatie van Hyper-V-machines met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 96ff404f-0d88-43fa-a00b-2dffde93d192
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: raynew
ms.openlocfilehash: 3b37542fc88e0af05e05cee78183983667618816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="test-results-for-on-premises-tooon-premises-hyper-v-replication-with-site-recovery"></a>Testresultaten voor lokale tooon-premises Hyper-V-replicatie met Site Recovery

U kunt Microsoft Azure Site Recovery tooorchestrate gebruiken en beheren van replicatie van virtuele machines en fysieke servers tooAzure of tooa secundair datacenter. Dit artikel bevat Hallo-resultaten van de prestatietests toen het repliceren van Hyper-V virtuele machines tussen twee lokale datacenters.

## <a name="test-goals"></a>Doelstellingen testen

Hallo-doel van de testen is tooexamine hoe Azure Site Recovery tijdens de replicatie van de actieve status uitvoert. Actieve status replicatie treedt op wanneer virtuele machines eerste replicatie is voltooid en deltawijzigingen synchroniseert. Het is belangrijk toomeasure prestaties met behulp van de actieve status omdat het Hallo-status waarin de meeste virtuele machines blijven, tenzij er onverwachte storingen optreden.

Testimplementatie Hallo bestond uit twee lokale sites met een VMM-server op elke site. Deze testimplementatie is standaard van een head office/branch office-implementatie met hoofdkantoor fungeert als de primaire site Hallo en Hallo filiaal als Hallo secundaire of herstel de site.

## <a name="what-we-did"></a>Wat er gedaan

Dit is wat er is in Hallo test geslaagd:

1. Virtuele machines met VMM-sjablonen gemaakt.
2. Virtuele machines en maatstaven voor prestaties van vastleggen basislijn meer dan 12 uur gestart.
3. Gemaakte clouds op primaire en herstelsites VMM-servers.
4. Geconfigureerde cloudbeveiliging in Azure Site Recovery, met inbegrip van de toewijzing van de bron- en herstelinstellingen clouds.
5. Beveiliging voor virtuele machines is ingeschakeld en kunnen ze toocomplete initiële replicatie.
6. Een paar uur voor systeem stabilization gewacht.
7. Vastgelegd maatstaven voor prestaties meer dan 12 uur ervoor te zorgen dat alle virtuele machines bleef een verwachte replicatiestatus voor deze 12 uur.
8. Meting Hallo verschillen tussen maatstaven voor prestaties Hallo-basislijn en maatstaven voor prestaties Hallo-replicatie.


## <a name="primary-server-performance"></a>Prestaties van de primaire server

* Hyper-V Replica houdt asynchroon wijzigingen tooa logboekbestand met minimale opslagoverhead op Hallo primaire server.
* Hyper-V Replica maakt gebruik van zelf handhaven cache toominimize IOPS geheugenoverhead voor bijhouden. Schrijfbewerkingen toohello VHDX van geheugen en deze in het logboekbestand Hallo voordat Hallo Hallo logboek tijd leegmaakacties toohello herstelsite wordt verzonden, worden opgeslagen. Een schijf leegmaken gebeurt ook als een vooraf vastgestelde limiet bereikt, wordt Hallo schrijfbewerkingen.
* Hallo grafiek hieronder toont Hallo gereedstatus IOPS overhead voor replicatie. U ziet dat Hallo overhead vanwege tooreplication IOP's is ongeveer 5% die is te klein.

![Primaire resultaten](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744913.png)

Hyper-V Replica maakt gebruik van geheugen op Hallo primaire server toooptimize schijfprestaties. Zoals u in de volgende grafiek hello, is geheugen overhead op alle servers in de primaire cluster Hallo marginale. Hallo-geheugen overhead is Hallo percentage van geheugen gebruikt door replicatie vergeleken toohello totale geïnstalleerd geheugen op Hallo Hyper-V-server.

![Primaire resultaten](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744914.png)

Hyper-V Replica heeft minimale CPU-overhead. Zoals u in de grafiek hello, ligt replicatieoverhead Hallo bereik van % 2-3.

![Primaire resultaten](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744915.png)

## <a name="secondary-recovery-server-performance"></a>Prestaties van de secundaire (herstel)-server

Hyper-V Replica gebruikt een kleine hoeveelheid geheugen op Hallo herstel server toooptimize Hallo aantal opslagbewerkingen. Hallo-grafiek bevat een overzicht van Hallo geheugengebruik op de herstelserver Hallo. Hallo-geheugen overhead is Hallo percentage van geheugen gebruikt door replicatie vergeleken toohello totale geïnstalleerd geheugen op Hallo Hyper-V-server.

![Secundaire resultaten](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744916.png)

Hallo hoeveelheid i/o-bewerkingen op Hallo herstelsite is een functie van het aantal schrijfbewerkingen op de primaire site Hallo Hallo. Laten we bekijkt hello totale i/o-bewerkingen op de herstelsite Hallo ten opzichte van de totale i/o-bewerkingen Hallo- en schrijfbewerkingen op Hallo primaire site. Hallo-grafieken wordt aangegeven die Hallo totale die IOP 's op de herstelsite Hallo is

* Hallo circa 1,5 keer IOPS op Hallo primaire schrijven.
* 37% van Hallo totaal ongeveer IOPS op Hallo primaire site.

![Secundaire resultaten](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744917.png)

![Secundaire resultaten](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744918.png)

## <a name="effect-on-network-utilization"></a>Effect op netwerkgebruik

Een gemiddelde van 275 Mb per seconde van de netwerkbandbreedte is tussen primaire Hallo en herstel knooppunten gebruikt (met gebruik van compressie) op basis van een bestaande bandbreedte van 5 Gb per seconde.

![Netwerkgebruik resultaten](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744919.png)

## <a name="effect-on-vm-performance"></a>Effect op de prestaties van de virtuele machine

Een belangrijk aandachtspunt is Hallo impact van replicatie op de productie-workloads uitvoeren op Hallo virtuele machines. Als de primaire site Hallo voldoende voor replicatie ingericht is, mogen er zich niet invloed op Hallo werkbelastingen. Hyper-V-Replica lightweight bijhouden mechanisme zorgt ervoor werkbelastingen op Hallo virtuele machines niet negatief beïnvloed tijdens de replicatie van de actieve status. Dit wordt geïllustreerd in Hallo grafieken te volgen.

Deze grafiek toont IOPS uitgevoerd door virtuele machines met verschillende werkbelastingen voordat en nadat de replicatie is ingeschakeld. U kunt zien dat er geen verschil tussen twee Hallo is.

![Replica effect resultaten](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744920.png)

Hallo ziet volgende grafiek Hallo doorvoer van virtuele machines die verschillende werkbelasting voordat en nadat de replicatie is ingeschakeld. U kunt zien dat de replicatie heeft geen aanzienlijke invloed.

![Resultaten replica effecten](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744921.png)

## <a name="conclusion"></a>Conclusie

Hallo resultaten duidelijk dat Azure Site Recovery, samen met Hyper-V Replica ook met minimale overhead voor een grote cluster schaalt.  Azure Site Recovery biedt eenvoudige implementatie, replicatie, beheer en bewaking. Hyper-V Replica bevat de benodigde infrastructuur Hallo voor het schalen van geslaagde replicatie. Voor het plannen van de implementatie van een optimale we raden u Hallo downloaden [Hyper-V Replica Capacity Planner](https://www.microsoft.com/download/details.aspx?id=39057).

## <a name="test-environment-details"></a>Details van de omgeving

### <a name="primary-site"></a>Primaire site

* Hallo primaire site heeft een cluster met vijf Hyper-V-servers 470 virtuele machines worden uitgevoerd.
* Hallo virtuele machines verschillende werkbelastingen worden uitgevoerd en alle is de Azure Site Recovery-beveiliging ingeschakeld.
* Opslag voor Hallo clusterknooppunt wordt verstrekt door een iSCSI-SAN. Model – Hitachi HUS130.
* Elke clusterserver heeft vier netwerkkaarten (NIC's) van een Gbps.
* Twee netwerkkaarten Hallo zijn verbonden tooan iSCSI-particulier netwerk en twee verbonden tooan externe bedrijfsnetwerk zijn. Een van de externe netwerken Hallo is gereserveerd voor alleen-clustercommunicatie is ingericht.

![Primaire hardwarevereisten](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744922.png)

| Server | RAM | Model | Processor | Aantal processors | NIC | Software |
| --- | --- | --- | --- | --- | --- | --- |
| Hyper-V-servers in het cluster: <br />ESTLAB HOST11<br />ESTLAB HOST12<br />ESTLAB HOST13<br />ESTLAB HOST14<br />ESTLAB HOST25 |128ESTLAB HOST25 is 256 |Dell™ PowerEdge™ R820 |Intel(R) Xeon(R) CPU E5-4620 0 @ 2,20 GHz |4 |Ik x 4 Gbps |Windows Server Datacenter 2012 R2 (x64) + Hyper-V-functie |
| VMM-Server |2 | | |2 |1 Gbps |Windows Server-Database 2012 R2 (x 64) + VMM 2012 R2 |

### <a name="secondary-recovery-site"></a>(Herstel) voor secundaire site

* Hallo secundaire site heeft een failovercluster met zes knooppunten.
* Opslag voor Hallo clusterknooppunt wordt verstrekt door een iSCSI-SAN. Model – Hitachi HUS130.

![Primaire hardwarespecificaties](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744923.png)

| Server | RAM | Model | Processor | Aantal processors | NIC | Software |
| --- | --- | --- | --- | --- | --- | --- |
| Hyper-V-servers in het cluster: <br />ESTLAB HOST07<br />ESTLAB HOST08<br />ESTLAB HOST09<br />ESTLAB HOST10 |96 |Dell™ PowerEdge™ R720 |Intel(R) Xeon(R) CPU E5-2630 0 @ 2.30GHz |2 |Ik x 4 Gbps |Windows Server Datacenter 2012 R2 (x64) + Hyper-V-functie |
| ESTLAB HOST17 |128 |Dell™ PowerEdge™ R820 |Intel(R) Xeon(R) CPU E5-4620 0 @ 2,20 GHz |4 | |Windows Server Datacenter 2012 R2 (x64) + Hyper-V-functie |
| ESTLAB HOST24 |256 |Dell™ PowerEdge™ R820 |Intel(R) Xeon(R) CPU E5-4620 0 @ 2,20 GHz |2 | |Windows Server Datacenter 2012 R2 (x64) + Hyper-V-functie |
| VMM-Server |2 | | |2 |1 Gbps |Windows Server-Database 2012 R2 (x 64) + VMM 2012 R2 |

### <a name="server-workloads"></a>Server-werkbelastingen

* We gekozen workloads die vaak worden gebruikt in zakelijke klant scenario's voor testdoeleinden.
* We gebruiken [IOMeter](http://www.iometer.org) met Hallo werkbelasting kenmerk samengevat in de tabel Hallo voor de simulatie.
* Alle IOMeter profielen zijn ingesteld toowrite willekeurige bytes toosimulate slechtste schrijven patronen voor werkbelastingen.

| Workload | I/o-grootte (KB) | % Toegang | % Lezen | Openstaande i/o 's | I/o-patroon |
| --- | --- | --- | --- | --- | --- |
| Bestandsserver |48163264 |60%20%5%5%10% |80%80%80%80%80% |88888 |Alle 100% willekeurige |
| SQL Server (volume 1) SQL Server (volume 2) |864 |100%100% |70%0% |88 |100% random100% sequentiële |
| Exchange |32 |100% |67% |8 |100% willekeurige |
| Werkstation/VDI |464 |66%34% |70%95% |11 |Beide willekeurige 100% |
| Web-bestandsserver |4864 |33%34%33% |95%95%95% |888 |Alle 75% willekeurige |

### <a name="vm-configuration"></a>VM-configuratie

* 470 virtuele machines op de primaire Hallo-cluster.
* Alle virtuele machines met VHDX-schijf.
* Virtuele machines waarop werkbelastingen samengevat in de tabel Hallo worden uitgevoerd. Alle zijn gemaakt met de VMM-sjablonen.

| Workload | # Virtuele machines | Minimale hoeveelheid RAM (GB) | Maximum-RAM (GB) | Grootte van logische schijf (GB) per VM | Maximale IOPS |
| --- | --- | --- | --- | --- | --- |
| SQL Server |51 |1 |4 |167 |10 |
| Exchange Server |71 |1 |4 |552 |10 |
| Bestandsserver |50 |1 |2 |552 |22 |
| VDI |149 |.5 |1 |80 |6 |
| Webserver |149 |.5 |1 |80 |6 |
| TOTAAL |470 | | |96.83 TB |4108 |

### <a name="site-recovery-settings"></a>Site Recovery-instellingen

* Azure Site Recovery is geconfigureerd voor on-premises tooon-premises beveiliging
* Hallo VMM-server heeft vier clouds zijn geconfigureerd, met de Hallo Hyper-V-clusterservers en hun virtuele machines.

| Primaire VMM-cloud | Beveiligde virtuele machines in de cloud Hallo | Replicatiefrequentie | Extra herstelpunten |
| --- | --- | --- | --- |
| PrimaryCloudRpo15m |142 |15 minuten |Geen |
| PrimaryCloudRpo30s |47 |30 seconden |Geen |
| PrimaryCloudRpo30sArp1 |47 |30 seconden |1 |
| PrimaryCloudRpo5m |235 |5 minuten |Geen |

### <a name="performance-metrics"></a>Maatstaven voor prestaties

Hallo tabel ziet u Hallo-maatstaven voor prestaties en de items die zijn gemeten in Hallo-implementatie.

| Gegevens | Prestatiemeteritems |
| --- | --- |
| CPU |\Processor(_Total)\% Processor Time |
| Beschikbaar geheugen |\Memory\Available megabytes (MB) |
| IOPS |\PhysicalDisk (_Totaal) \Disk Schijfoverdrachten per seconde |
| Virtuele machine lezen (IOPS)-bewerkingen per seconde |\Hyper-V virtueel opslagapparaat (<VHD>) \Read bewerkingen per seconde |
| VM geschreven (IOPS)-bewerkingen per seconde |\Hyper-V virtueel opslagapparaat (<VHD>) \Write Operations/S |
| VM doorvoer lezen |\Hyper-V virtueel opslagapparaat (<VHD>) \Read Bytes per seconde |
| VM-schrijfbewerkingen |\Hyper-V virtueel opslagapparaat (<VHD>) \Write Bytes per seconde |

## <a name="next-steps"></a>Volgende stappen

[De replicatie tussen twee lokale VMM-sites instellen](site-recovery-vmm-to-vmm.md)
