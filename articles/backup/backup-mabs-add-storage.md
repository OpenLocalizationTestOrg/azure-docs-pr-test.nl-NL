---
title: aaaUse moderne Backup Storage met Azure Backup-Server v2 | Microsoft Docs
description: Meer informatie over nieuwe functies in Azure Backup-Server v2 Hallo. Dit artikel wordt beschreven hoe tooupgrade uw back-up-Server-installatie.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a>Toevoegen van opslag tooAzure back-upserver van v2

Azure Backup Server v2 wordt geleverd met System Center 2016 Data Protection Manager moderne back-up opslag. Moderne back-up Storage biedt opslagbesparing van 50 procent van de back-ups die drie keer snellere en efficiëntere opslag. Biedt ook werkbelasting-bewuste opslag. 

> [!NOTE]
> toouse moderne back-up-opslag, moet u back-upserver van v2 uitvoeren op Windows Server 2016. Als u een back-upserver van v2 op een eerdere versie van Windows Server uitvoert, kan niet Azure Backup-Server profiteren van moderne back-up-opslag. In plaats daarvan beveiligt het werkbelastingen zoals met back-upserver van v1. Zie voor meer informatie, Hallo back-upserver versie [beveiliging matrix](backup-mabs-protection-matrix.md).

## <a name="volumes-in-backup-server-v2"></a>Volumes in de back-upserver v2

Back-Server v2 accepteert opslagvolumes. Wanneer u een volume toevoegt, indelingen back-upserver Hallo volume tooResilient File System (ReFS), waarvoor moderne back-up-opslag is vereist. een volume tooadd en tooexpand later als u wilt het is raadzaam dat u deze werkstroom:

1.  Back-upserver van v2 op een virtuele machine instellen.
2.  Maak een volume op een virtuele schijf in een opslaggroep:
    1.  Voeg een schijf tooa-opslaggroep en een virtuele schijf maken met eenvoudige indeling.
    2.  Voeg eventuele extra schijven en Hallo virtuele schijf uitbreiden.
    3.  Volumes op Hallo virtuele schijf maken.
3.  Hallo volumes tooBackup Server toevoegen.
4.  Werkbelasting-bewuste opslag configureren.

## <a name="create-a-volume-for-modern-backup-storage"></a>Een volume maken voor moderne back-up-opslag

Met behulp van back-upserver van v2 met volumes als schijfopslag kunt u controle over opslag. Een volume kan één schijf zijn. Als u wilt dat toekomstige tooextend opslag in hello, echter een volume buiten een schijf die is gemaakt met behulp van opslagruimten maken. Zo kunt u indien tooexpand Hallo volume voor back-up gewenst. Deze sectie vindt u aanbevolen procedures voor het maken van een volume met deze instellingen.

1. Selecteer in Serverbeheer **File and Storage Services** > **Volumes** > **opslaggroepen**. Onder **fysieke schijven**, selecteer **nieuwe opslaggroep**. 

    ![Een nieuwe opslaggroep maken](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. In Hallo **taken** vervolgkeuzelijst, selecteer **nieuwe virtuele schijf**.

    ![Een virtuele schijf toevoegen](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. Selecteer de opslaggroep Hallo en selecteer vervolgens **fysieke schijf toevoegen**.

    ![Toevoegen van een fysieke schijf](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. Selecteer de fysieke schijf Hallo en selecteer vervolgens **virtuele schijf uitbreiden**.

    ![Hallo virtuele schijf uitbreiden](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. Selecteer Hallo virtuele schijf en selecteer vervolgens **NieuwVolume**.

    ![Maak een nieuw volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. In Hallo **Hallo-server en schijf selecteren** dialoogvenster, selecteer Hallo-server en de nieuwe schijf Hallo. Selecteer **volgende**.

    ![Hallo-server en schijf selecteren](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a>Volumes tooBackup Server schijfopslag toevoegen

een volume tooBackup-Server in Hallo tooadd **Management** deelvenster Hallo opslag opnieuw scannen en selecteer vervolgens **toevoegen**. Er verschijnt een lijst met alle Hallo volumes beschikbaar toobe toegevoegd voor de opslag van back-up-Server. Nadat beschikbare volumes zijn toegevoegd toohello lijst met geselecteerde volumes, kunt u ze een beschrijvende naam toohelp u ze beheren geven. deze volumes tooReFS zodat back-upserver Hallo voordelen van moderne back-up-opslag kunt, selecteer tooformat **OK**.

![Toevoegen van de beschikbare Volumes](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a>Werkbelasting-bewuste opslag instellen

Met de werkbelasting-bewuste opslag, kunt u Hallo volumes waarop bepaalde soorten belasting bij voorkeur zijn opgeslagen. U kunt bijvoorbeeld dure volumes die ondersteuning bieden voor een groot aantal i/o-bewerkingen per tweede (IOPS) toostore alleen Hallo werkbelastingen waarvoor frequente, hoog volume back-ups instellen. Een voorbeeld is SQL Server met de transactielogboeken. Andere werkbelastingen zijn back-ups minder vaak, zoals virtuele machines, kunnen worden back-up toolow kosten volumes.

### <a name="update-dpmdiskstorage"></a>Update DPMDiskStorage

U kunt de werkbelasting-bewuste opslag instellen met behulp van PowerShell-cmdlet Hallo Update-DPMDiskStorage die Hallo eigenschappen van een volume in de opslaggroep Hallo op een server met Data Protection Manager-updates.

Syntaxis:

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
Hallo volgende schermafbeelding ziet u Hallo Update DPMDiskStorage cmdlet in Hallo PowerShell-venster.

![Hallo Update DPMDiskStorage opdracht in Hallo PowerShell-venster](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

Hallo-wijzigingen die u aanbrengt met behulp van PowerShell worden doorgevoerd in Hallo back-up Server Administrator-Console.

![Schijven en volumes in Hallo Administrator-Console](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a>Volgende stappen
Nadat u de back-up-Server hebt geïnstalleerd, informatie over hoe tooprepare uw server, of met het beveiligen van een werkbelasting beginnen.

- [Back-upserver van werkbelastingen voorbereiden](backup-azure-microsoft-azure-backup.md)
- [Back-upserver tooback van een VMware-server gebruiken](backup-azure-backup-server-vmware.md)
- [Back-upserver tooback van SQL Server gebruiken](backup-azure-sql-mabs.md)

