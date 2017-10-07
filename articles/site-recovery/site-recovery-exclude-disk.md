---
title: schijven uit de beveiliging met behulp van Azure Site Recovery aaaExclude | Microsoft Docs
description: Hierin wordt beschreven waarom en hoe tooexclude VM van replicatie voor scenario's van VMware tooAzure en Hyper-V tooAzure schijven.
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: f47146bc57aeab3fce90123d0894fa86dde93417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="exclude-disks-from-replication"></a>Schijven uitsluiten van replicatie
Dit artikel wordt beschreven hoe tooexclude schijven van replicatie. Met deze uitsluiting kunt optimaliseren Hallo verbruikt replicatie bandbreedte of Hallo doelzijde resources die gebruikmaken van dergelijke schijven optimaliseren. Hallo-functie wordt ondersteund voor scenario's van VMware tooAzure en Hyper-V tooAzure.

## <a name="prerequisites"></a>Vereisten

Standaard worden alle schijven op een machine gerepliceerd. tooexclude een schijf van replicatie, moet u handmatig installeren Hallo Mobility-service op Hallo machine voordat u replicatie inschakelen als u van VMware tooAzure repliceert.


## <a name="why-exclude-disks-from-replication"></a>Waarom is het nodig om schijven uit te sluiten van replicatie?
Schijven uitsluiten van replicatie is vaak nodig, omdat:

- Hallo-gegevens die wordt churned op Hallo uitgesloten schijf is niet van belang of toobe gerepliceerd niet nodig.

- De opslag- en netwerkbronnen toosave wilt u deze verloop niet repliceren.

## <a name="what-are-hello-typical-scenarios"></a>Wat zijn typische Hallo-scenario's?
Er zijn specifieke voorbeelden van gegevensverloop die in aanmerking komen voor uitsluiting. Voorbeelden hiervan zijn schrijft tooa wisselbestand (pagefile.sys) en schrijft toohello tempdb-bestand van Microsoft SQL Server. Afhankelijk van werkbelasting Hallo en Hallo opslagsubsysteem kunt Hallo wisselbestand een aanzienlijke hoeveelheid verloop registreren. Deze gegevens van Hallo primaire site tooAzure repliceren is echter veel bronnen. U kunt dus hello te volgen stappen toooptimize replicatie van een virtuele machine met een virtuele schijf die zowel Hallo-besturingssysteem als het wisselbestand Hallo is gebruiken:

1. Hallo één virtuele schijf gesplitst in twee virtuele schijven. Één virtuele schijf heeft Hallo-besturingssysteem en andere Hallo Hallo wisselbestand.
2. Hallo paginering schijf uitsluiten van replicatie.

Op deze manier kunt u gebruiken hello te volgen stappen toooptimize een schijf met beide Hallo Microsoft SQL Server tempdb ve en Hallo system-databasebestand:

1. Houd de systeemdatabase Hallo en tempdb op twee verschillende schijven.
2. Hallo tempdb schijf uitsluiten van replicatie.

## <a name="how-tooexclude-disks-from-replication"></a>Hoe tooexclude schijven van replicatie?

### <a name="vmware-tooazure"></a>VMware tooAzure
Ga als volgt Hallo [replicatie inschakelen](site-recovery-vmware-to-azure.md) werkstroom tooprotect een virtuele machine van hello Azure Site Recovery-portal. Gebruik in vierde stap van de werkstroom Hallo HALLO hallo **schijf tooREPLICATE** kolom tooexclude schijven van replicatie. Standaard worden alle schijven geselecteerd voor replicatie. Schakel het selectievakje Hallo van schijven die u wilt dat tooexclude van replicatie, en vervolgens voltooit Hallo stappen tooenable replicatie.

![Schijven uitsluiten van replicatie en -replicatie voor VMware tooAzure failback inschakelen](./media/site-recovery-exclude-disk/v2a-enable-replication-exclude-disk1.png)


>[!NOTE]
>
> * U kunt alleen de schijven die al Hallo Mobility-service geïnstalleerd uitsluiten. Toomanually installatie Hallo Mobility-service, moet u omdat Hallo Mobility-service alleen wordt geïnstalleerd met behulp van push-mechanisme Hallo nadat replicatie is ingeschakeld.
> * Alleen standaardschijven kunnen worden uitgesloten van replicatie. Besturingssystemen en dynamische schijven kunt u niet uitsluiten.
> * Nadat u de replicatie hebt ingeschakeld, kunt u geen schijven meer toevoegen of verwijderen voor replicatie. Als u wilt dat tooadd of uitsluiten van een schijf, kunt u toodisable beveiliging voor Hallo-apparaat nodig en vervolgens opnieuw inschakelen.
> * Als u deze uitsluiten van een schijf die nodig is voor een toooperate toepassing na failover tooAzure, moet u toocreate Hallo schijf handmatig in Azure zodat de toepassing hello gerepliceerd kunt uitvoeren. U kunt ook Azure automation integreren in een plan toocreate Hallo herstelschijf op tijdens de failover van Hallo-machine.
> * Virtuele Windows-machines: voor schijven die u handmatig hebt gemaakt in Azure, wordt geen failback uitgevoerd. Als u bijvoorbeeld een failover hebt uitgevoerd voor drie schijven en er twee rechtstreeks in virtuele Azure-machines maakt, wordt alleen voor de drie schijven waarvoor een failover is uitgevoerd, een failback uitgevoerd. U kunt geen schijven die u handmatig hebt gemaakt in de failback of beveiligt van lokale tooAzure opnemen.
> * Virtuele Linux-machines: voor schijven die u handmatig hebt gemaakt in Azure, wordt een failback uitgevoerd. Als u bijvoorbeeld een failover hebt uitgevoerd voor drie schijven en er twee rechtstreeks in virtuele Azure-machines maakt, wordt voor alle vijf een failback uitgevoerd. U kunt geen schijven die handmatig zijn gemaakt, uitsluiten van failback.
>

### <a name="hyper-v-tooazure"></a>Hyper-V tooAzure
Ga als volgt Hallo [replicatie inschakelen](site-recovery-hyper-v-site-to-azure.md) werkstroom tooprotect een virtuele machine van hello Azure Site Recovery-portal. Gebruik in vierde stap van de werkstroom Hallo HALLO hallo **schijf tooREPLICATE** kolom tooexclude schijven van replicatie. Standaard worden alle schijven geselecteerd voor replicatie. Schakel het selectievakje Hallo van schijven die u wilt dat tooexclude van replicatie, en vervolgens voltooit Hallo stappen tooenable replicatie.

![Schijven uitsluiten van replicatie en -replicatie voor Hyper-V tooAzure failback inschakelen](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

>[!NOTE]
>
> * U kunt alleen standaardschijven uitsluiten van replicatie. Besturingssysteemschijven kunt u niet uitsluiten. We raden u aan geen dynamische schijven uit te sluiten. Azure Site Recovery kan niet vaststellen welke virtuele harde schijf (VHD) is basisschijven of dynamische in Hallo virtuele gastmachine.  Als niet alle afhankelijke dynamisch volume schijven zijn uitgesloten, Hallo beveiligde dynamische schijf wordt een niet-werkende schijf op een failover-virtuele machine en hello gegevens op de schijf is niet toegankelijk.
> * Nadat u de replicatie hebt ingeschakeld, kunt u geen schijven meer toevoegen of verwijderen voor replicatie. Als u wilt dat tooadd of uitsluiten van een schijf, kunt u toodisable beveiliging nodig voor Hallo virtuele machine en vervolgens opnieuw inschakelen.
> * Als u een schijf die nodig is voor een toepassing toooperate uitsluit, na failover tooAzure moet u toocreate Hallo schijf handmatig in Azure zodat de toepassing hello gerepliceerd kunt uitvoeren. U kunt ook Azure automation integreren in een plan toocreate Hallo herstelschijf op tijdens de failover van Hallo-machine.
> * Voor schijven die u handmatig hebt gemaakt in Azure, wordt geen failback uitgevoerd. Als u meer dan drie schijven mislukken en maken van twee schijven rechtstreeks in Azure Virtual Machines, wordt bijvoorbeeld slechts drie schijven met failover zijn mislukt door Azure tooHyper-V. U kunt geen schijven die handmatig zijn gemaakt in de failback of in de omgekeerde replicatie van Hyper-V tooAzure opnemen.



## <a name="end-to-end-scenarios-of-exclude-disks"></a>End-to-end scenario's voor het uitsluiten van schijven
Laten we eens twee scenario's toounderstand Hallo uitsluiten schijf functie:

- tempdb-schijf in SQL Server
- Schijf van het wisselbestand (pagefile.sys)

### <a name="exclude-hello-sql-server-tempdb-disk"></a>Hallo SQL Server tempdb-schijf uitsluiten
We gaan uit van een virtuele SQL Server-machine met een tempdb die kan worden uitgesloten.

Hallo-naam van de virtuele schijf Hallo is SalesDB.

Schijven op de virtuele bronmachine Hallo zijn als volgt:


**Schijfnaam** | **Gastbesturingssysteemschijf#** | **Stationsletter** | **Gegevenstype op Hallo-schijf**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Besturingssysteemschijf
DB-Disk1| Disk1 | D:\ | SQL-systeemdatabase en gebruikersdatabase1
DB-Disk2 (Hallo schijf uitgesloten van beveiliging) | Disk2 | E:\ | Tijdelijke bestanden
DB-Disk3 (Hallo schijf uitgesloten van beveiliging) | Disk3 | F:\ | SQL-tempdb-database (mappad (F:\MSSQL\Data\) < /br/>< /br/> Schrijf Hallo mappad voordat failover wordt uitgevoerd.
DB-Disk4 | Disk4 |G:\ |Gebruikersdatabase2

Omdat gegevensverloop op twee schijven van Hallo virtuele machine tijdelijk, is terwijl u Hallo SalesDB virtuele machine beveiligen, sluit u Disk2 en Disk3 van replicatie. Azure Site Recovery repliceert deze schijven niet. Failover, deze schijven worden niet aanwezig op Hallo failover-virtuele machine in Azure.

Schijven op virtuele machine na een failover van Azure Hallo zijn als volgt:

**Gastbesturingssysteemschijf#** | **Stationsletter** | **Gegevenstype op Hallo-schijf**
--- | --- | ---
DISK0 | C:\ | Besturingssysteemschijf
Disk1 | E:\ | Tijdelijke opslag < /br / >< /br / > Azure voegt van deze schijf en wijst Hallo eerste beschikbare letter.
Disk2 | D:\ | SQL-systeemdatabase en gebruikersdatabase1
Disk3 | G:\ | Gebruikersdatabase2

Omdat Disk2 en Disk3 zijn uitgesloten van Hallo SalesDB virtuele machine, is het E: Hallo eerste letter van de lijst met beschikbare Hallo. Azure toegewezen E: toohello tijdelijke opslagvolume. Voor alle Hallo gerepliceerd schijven Hallo Hallo station letters blijven hetzelfde.

Disk3 die Hallo SQL tempdb schijf was (tempdb mappad F:\MSSQL\Data\), is uitgesloten van replicatie. Hallo-schijf is niet beschikbaar op Hallo failover-virtuele machine. Als gevolg hiervan Hallo SQL-service is gestopt en moet Hallo F:\MSSQL\Data pad.

Er zijn twee manieren toocreate dit pad:

- Voeg een nieuwe schijf toe en wijs een tempdb-mappad toe.
- Gebruik een bestaande schijf van de tijdelijke opslag voor Hallo tempdb mappad.

#### <a name="add-a-new-disk"></a>Een nieuwe schijf toevoegen:

1. Schrijf Hallo paden van de SQL-tempdb.mdf en tempdb.ldf voordat failover wordt uitgevoerd.
2. Van hello Azure-portal, een nieuwe schijf toohello failover-virtuele machine toevoegen Hello dezelfde of meer grootte als die van Hallo SQL tempdb bronschijf (Disk3).
3. Meld u aan toohello virtuele machine van Azure. Van Hallo Schijfbeheer (diskmgmt.msc) management console toegevoegde initialiseren en formatteren Hallo schijf.
4. Toewijzen hello dezelfde stationsletter dat werd gebruikt door Hallo SQL tempdb schijf (F:).
5. Maak een tempdb-map op Hallo volume F: (F:\MSSQL\Data).
6. Hallo SQL-service niet starten vanaf Hallo service-console.

#### <a name="use-an-existing-temporary-storage-disk-for-hello-sql-tempdb-folder-path"></a>Gebruik een bestaande schijf van de tijdelijke opslag voor Hallo SQL tempdb mappad:

1. Open een opdrachtprompt.
2. SQL Server worden uitgevoerd in herstelmodus vanaf de opdrachtprompt Hallo.

        Net start MSSQLSERVER /f / T3608

3. Hallo sqlcmd toochange Hallo tempdb pad toohello nieuwe pad worden uitgevoerd.

        sqlcmd -A -S SalesDB        **Use your SQL DBname**
        USE master;     
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = tempdev, FILENAME = 'E:\MSSQL\tempdata\tempdb.mdf');
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = templog, FILENAME = 'E:\MSSQL\tempdata\templog.ldf');       
        GO


4. Hallo-Microsoft SQL Server-service niet stoppen.

        Net stop MSSQLSERVER
5. Hallo-Microsoft SQL Server-service starten.

        Net start MSSQLSERVER

Raadpleeg toohello Azure richtlijn voor tijdelijke opslagschijf te volgen:

* [Gebruik van SSD's in Azure Virtual machines toostore SQL Server TempDB en -extensies voor Buffer-groep](https://blogs.technet.microsoft.com/dataplatforminsider/2014/09/25/using-ssds-in-azure-vms-to-store-sql-server-tempdb-and-buffer-pool-extensions/)
* [Aanbevolen procedures voor prestaties voor SQL Server op virtuele machines van Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)

### <a name="failback-from-azure-tooan-on-premises-host"></a>Failback (vanaf Azure tooan lokale host)
Nu gaan we begrijpen Hallo-schijven die worden gerepliceerd wanneer u een failover van Azure tooyour lokale VMware of Hyper-V-host. Schijven die u handmatig hebt gemaakt in Azure, worden niet gerepliceerd. Als u bijvoorbeeld een failover hebt uitgevoerd voor drie schijven en twee rechtstreeks op virtuele Azure-machines maakt, wordt alleen voor de drie schijven waarvoor een failover is uitgevoerd, een failback uitgevoerd. U kunt geen schijven die handmatig zijn gemaakt in de failback of beveiligt van lokale tooAzure opnemen. Deze ook repliceert niet Hallo tijdelijke opslag schijf tooon-premises hosts.

#### <a name="failback-toooriginal-location-recovery"></a>Herstel van failback toooriginal locatie

In het vorige voorbeeld hello is schijfconfiguratie voor virtuele machine van Azure Hallo als volgt uit:

**Gastbesturingssysteemschijf#** | **Stationsletter** | **Gegevenstype op Hallo-schijf**
--- | --- | ---
DISK0 | C:\ | Besturingssysteemschijf
Disk1 | E:\ | Tijdelijke opslag < /br / >< /br / > Azure voegt van deze schijf en wijst Hallo eerste beschikbare letter.
Disk2 | D:\ | SQL-systeemdatabase en gebruikersdatabase1
Disk3 | G:\ | Gebruikersdatabase2


#### <a name="vmware-tooazure"></a>VMware tooAzure
Wanneer de failback wordt de oorspronkelijke locatie toohello uitgevoerd, is schijfconfiguratie van Hallo failback van virtuele machine heeft geen uitgesloten schijven. Schijven die zijn uitgesloten van VMware tooAzure wordt niet beschikbaar zijn op Hallo failback van virtuele machine.

Na de geplande failover van Azure tooon-premises VMware zijn schijven op Hallo VMWare virtuele machine (oorspronkelijke locatie) als volgt uit:

**Gastbesturingssysteemschijf#** | **Stationsletter** | **Gegevenstype op Hallo-schijf**
--- | --- | ---
DISK0 | C:\ | Besturingssysteemschijf
Disk1 | D:\ | SQL-systeemdatabase en gebruikersdatabase1
Disk2 | G:\ | Gebruikersdatabase2

#### <a name="hyper-v-tooazure"></a>Hyper-V tooAzure
Als de oorspronkelijke locatie toohello failback is Hallo Hallo failback van virtuele machine schijf configuratie blijft hetzelfde als die van de oorspronkelijke virtuele machine de schijfconfiguratie voor Hyper-V. Schijven die zijn uitgesloten van Hyper-V-site tooAzure zijn beschikbaar op Hallo failback van virtuele machine.

Na een geplande failover naar Azure tooon-premises Hyper-V-zijn schijven op Hallo Hyper-V virtuele machine (oorspronkelijke locatie) als volgt uit:

**Schijfnaam** | **Gastbesturingssysteemschijf#** | **Stationsletter** | **Gegevenstype op Hallo-schijf**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 |   C:\ | Besturingssysteemschijf
DB-Disk1 | Disk1 | D:\ | SQL-systeemdatabase en gebruikersdatabase1
DB-Disk2 (uitgesloten schijf) | Disk2 | E:\ | Tijdelijke bestanden
DB-Disk3 (uitgesloten schijf) | Disk3 | F:\ | SQL-tempdb-database (mappad (F:\MSSQL\Data\)
DB-Disk4 | Disk4 | G:\ | Gebruikersdatabase2


#### <a name="exclude-hello-paging-file-pagefilesys-disk"></a>(Pagefile.sys) schijf Hallo van wisselbestand uitsluiten

We gaan uit van een virtuele machine met een wisselbestandschijf die kan worden uitgesloten.
Er zijn twee mogelijke situaties.

#### <a name="case-1-hello-paging-file-is-configured-on-hello-d-drive"></a>Voorbeeld 1: het wisselbestand Hallo is geconfigureerd op Hallo station D:
Hier volgt de schijfconfiguratie Hallo:


**Schijfnaam** | **Gastbesturingssysteemschijf#** | **Stationsletter** | **Gegevenstype op Hallo-schijf**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Besturingssysteemschijf
DB-diskette 1 (Hallo schijf uitgesloten van beveiliging Hallo) | Disk1 | D:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | Gebruikersgegevens 1
DB-Disk3 | Disk3 | F:\ | Gebruikersgegevens 2

Hier volgen Hallo instellingen voor het wisselbestand op de virtuele bronmachine Hallo:

![Instellingen voor het wisselbestand op de virtuele bronmachine](./media/site-recovery-exclude-disk/pagefile-on-d-drive-sourceVM.png)


Na een failover van Hallo virtuele machine van VMware tooAzure of Hyper-V tooAzure zijn schijven op virtuele machine van Azure Hallo als volgt uit:

**Schijfnaam** | **Gastbesturingssysteemschijf#** | **Stationsletter** | **Gegevenstype op Hallo-schijf**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Besturingssysteemschijf
DB-Disk1 | Disk1 | D:\ | Tijdelijke opslag</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | Gebruikersgegevens 1
DB-Disk3 | Disk3 | F:\ | Gebruikersgegevens 2

Omdat diskette 1 (D:) is uitgesloten, is het D: Hallo eerste letter van de lijst met beschikbare Hallo. Azure toegewezen D: toohello tijdelijke opslagvolume. Omdat D: beschikbaar is op Hallo virtuele machine van Azure, Hallo Hallo instelling voor het wisselbestand van Hallo virtuele machine blijft hetzelfde.

Hier volgen Hallo instellingen voor het wisselbestand op Hallo virtuele machine van Azure:

![Instellingen voor het wisselbestand op de virtuele Azure-machine](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover.png)

#### <a name="case-2-hello-paging-file-is-configured-on-another-drive-other-than-d-drive"></a>Voorbeeld 2: het wisselbestand Hallo is geconfigureerd op een ander station (met uitzondering van station D:)

Hier volgt een schijfconfiguratie van Hallo bron virtuele machine:

**Schijfnaam** | **Gastbesturingssysteemschijf#** | **Stationsletter** | **Gegevenstype op Hallo-schijf**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Besturingssysteemschijf
DB-diskette 1 (Hallo schijf uitgesloten van beveiliging) | Disk1 | G:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | Gebruikersgegevens 1
DB-Disk3 | Disk3 | F:\ | Gebruikersgegevens 2

Hier volgen Hallo instellingen voor het wisselbestand op Hallo on-premises virtuele machine:

![Wisselbestand op Hallo on-premises virtuele machine](./media/site-recovery-exclude-disk/pagefile-on-g-drive-sourceVM.png)

Na een failover van Hallo virtuele machine van VMware/Hyper-V tooAzure zijn schijven op virtuele machine van Azure Hallo als volgt uit:

**Schijfnaam**| **Gastbesturingssysteemschijf#**| **Stationsletter** | **Gegevenstype op Hallo-schijf**
--- | --- | --- | ---
DB-Disk0-OS | DISK0  |C:\ |Besturingssysteemschijf
DB-Disk1 | Disk1 | D:\ | Tijdelijke opslag</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | Gebruikersgegevens 1
DB-Disk3 | Disk3 | F:\ | Gebruikersgegevens 2

Omdat D: Hallo eerste letter in de lijst beschikbare hello, wijst Azure D: toohello tijdelijke opslagvolume. Voor alle Hallo gerepliceerd schijven Hallo Hallo stationsletter blijft hetzelfde. Omdat Hallo G: schijf niet beschikbaar is, wordt system Hallo voor Hallo wisselbestand Hallo C: station gebruiken.

Hier volgen Hallo instellingen voor het wisselbestand op Hallo virtuele machine van Azure:

![Instellingen voor het wisselbestand op de virtuele Azure-machine](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover-2.png)

## <a name="next-steps"></a>Volgende stappen
Wanneer uw implementatie actief is, kunt u [hier](site-recovery-failover.md) meer lezen over de verschillende soorten failovers.
