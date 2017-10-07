---
title: Back-up van Azure Linux VM's | Microsoft Docs
description: Uw virtuele Linux-machines beveiligen door deze back-ups van maken met Azure Backup.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a>Back-up van Linux virtuele machines in Azure

U kunt uw gegevens beschermen door regelmatig back-ups te maken. Azure Backup maakt herstelpunten die zijn opgeslagen in een geografisch redundante recovery kluizen. Wanneer u vanaf een herstelpunt herstelt, kunt u herstellen Hallo hele virtuele machine of alleen specifieke bestanden. Dit artikel wordt uitgelegd hoe toorestore één tooa Linux VM actieve nginx-bestand. Als u een VM-toouse nog geen hebt, kunt u een maken met behulp van Hallo [Linux Quick Start](quick-create-cli.md). In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Maak een back-up van een virtuele machine
> * Een dagelijkse back-up plannen
> * Een bestand te herstellen vanaf een back-up



## <a name="backup-overview"></a>Overzicht van Backup

Wanneer hello Azure Backup-service een back-up begint, activeert het Hallo Backup-extensie tootake een momentopname van een punt in tijd. Hello Azure Backup-service gebruikt Hallo _VMSnapshotLinux_ extensie in Linux. Hallo-extensie wordt geïnstalleerd tijdens Hallo eerste VM back-up als Hallo VM wordt uitgevoerd. Als hello VM niet wordt uitgevoerd, wordt Hallo Backup-service een momentopname van Hallo onderliggende opslag (omdat er geen schrijfbewerkingen toepassing tijdens het Hallo die VM is gestopt optreden).

Standaard Azure Backup heeft een bestand system consistente back-up voor Linux VM maar het kan geconfigureerde tootake [toepassing consistente back-up met script voor vóór en na-framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). Zodra hello Azure Backup-service Hallo momentopname maakt, is Hallo gegevens overgedragen toohello kluis. toomaximize-efficiëntie Hallo service identificeert en alleen Hallo blokken met gegevens die zijn gewijzigd sinds de vorige back-up Hallo overdraagt.

Hallo-gegevensoverdracht is voltooid, Hallo momentopname wordt verwijderd als een herstelpunt wordt gemaakt.


## <a name="create-a-backup"></a>Maak een back-up
Maak een eenvoudige geplande dagelijkse back-tooa Recovery Services-kluis. 

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Selecteer in het menu aan de linkerkant Hallo Hallo **virtuele machines**. 
3. Selecteer een VM-tooback uit Hallo-lijst.
4. Op Hallo VM blade in Hallo **instellingen** sectie, klikt u op **back-up**. Hallo **back-up** blade wordt geopend.
5. In **Recovery Services-kluis**, klikt u op **nieuw** en geef de naam Hallo voor Hallo nieuwe kluis. Een nieuwe kluis is gemaakt in Hallo dezelfde resourcegroep en locatie als Hallo virtuele machine.
6. Klik op **back-up maken van beleid**. In dit voorbeeld blijven Hallo standaardwaarden en klik op **OK**.
7. Op Hallo **back-up** blade, klikt u op **back-up inschakelen**. Hiermee maakt u een dagelijkse back-up op basis van het standaardschema Hallo.
10. een eerste herstelpunt op Hallo toocreate **back-up** Klik op de blade **back-up nu**.
11. Op Hallo **back-up nu** blade, klikt u op het pictogram Kalender Hallo, gebruikt u Hallo kalender besturingselement tooselect Hallo laatste dag van dit herstelpunt wordt bewaard en op **back-up**.
12. In Hallo **back-up** blade voor uw virtuele machine, ziet u Hallo aantal herstelpunten die voltooid zijn.

    ![Herstelpunten](./media/tutorial-backup-vms/backup-complete.png)

de eerste back-up Hallo duurt ongeveer 20 minuten. Toohello volgende deel van deze zelfstudie worden voortgezet nadat de back-up is voltooid.

## <a name="restore-a-file"></a>Een bestand te herstellen

Als u per ongeluk verwijdert of wijzigingen tooa bestand maken, kunt u bestandsherstel toorecover Hallo bestand vanuit uw back-upkluis. Bestandsherstel maakt gebruik van een script dat wordt uitgevoerd op virtuele machine, Hallo toomount Hallo herstelpunt als lokale schijf. Deze stations blijft gekoppelde 12 uur zodat u kunt bestanden vanaf Hallo herstelpunt kopiëren en herstel deze toohello VM.  

In dit voorbeeld laten we zien hoe toorecover standaard nginx webpagina /var/www/html/index.nginx-debian.html Hallo. Hallo openbare IP-adres van de virtuele machine in dit voorbeeld is *13.69.75.209*. U vindt Hallo IP-adres van uw virtuele machine met:

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. Open een browser en typ Hallo openbare IP-adres van uw VM toosee hello nginx standaardwebpagina op uw lokale computer.

    ![Standaard nginx-webpagina](./media/tutorial-backup-vms/nginx-working.png)

1. SSH in uw virtuele machine.

    ```bash
    ssh 13.69.75.209
    ```
2. /Var/www/html/index.nginx-debian.html verwijderen.

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. Op de lokale computer, vernieuwt u Hallo browser kunt u door op CTRL + F5 toosee die standaard nginx-pagina is verwijderd.

    ![Standaard nginx-webpagina](./media/tutorial-backup-vms/nginx-broken.png)
    
1. Meld u op uw lokale computer aan toohello [Azure-portal](https://portal.azure.com/).
6. Selecteer in het menu aan de linkerkant Hallo Hallo **virtuele machines**. 
7. Selecteer in Hallo lijst Hallo VM.
8. Op Hallo VM blade in Hallo **instellingen** sectie, klikt u op **back-up**. Hallo **back-up** blade wordt geopend. 
9. Selecteer in het menu Hallo Hallo boven aan het Hallo-blade **bestandsherstel**. Hallo **bestandsherstel** blade wordt geopend.
10. In **stap 1: Selecteer herstelpunt**, selecteer een herstelpunt in de vervolgkeuzelijst Hallo.
11. In **stap 2: downloaden script toobrowse en bestanden herstellen**, klikt u op Hallo **uitvoerbaar bestand downloaden** knop. Hallo gedownloade bestand tooyour lokale computer opslaan.
7. Klik op **script downloaden** toodownload Hallo scriptbestand lokaal.
8. Open een Bash-prompt en type hello te volgen en vervangt *Linux_myVM_05-05-2017.sh* met Hallo de juiste pad en bestandsnaam voor Hallo-script dat u hebt gedownload, *azureuser* met Hallo gebruikersnaam voor Hallo VM en *13.69.75.209* Hallo openbare IP-adres voor uw virtuele machine.
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. Open op uw lokale computer, een SSH-verbinding toohello VM.

    ```bash
    ssh 13.69.75.209
    ```
    
10. Voeg op de virtuele machine, machtigingen toohello scriptbestand uitvoeren.

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. Op de virtuele machine, Hallo herstelpunt voor Hallo script toomount worden uitgevoerd als een bestandssysteem.

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. Hallo de uitvoer van Hallo script geeft dat u het pad naar het koppelpunt Hallo Hallo. Hallo-uitvoer ziet er vergelijkbare toothis:

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. Op de virtuele machine, kopieert u Hallo nginx-standaardwebpagina van Hallo koppelpunt punt back toowhere u Hallo bestand verwijderd.

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. Open op uw lokale computer Hallo browsertabblad waar u bent verbonden toohello IP-adres van Hallo VM van Hallo nginx standaard de pagina. Druk op CTRL + F5 toorefresh Hallo browserpagina. U ziet nu dat Hallo standaardpagina weer werkt.

    ![Standaard nginx-webpagina](./media/tutorial-backup-vms/nginx-working.png)

18. Op de lokale computer, gaat u terug toohello browsertabblad voor hello Azure-portal en in **stap 3: Hallo schijven ontkoppelen na het herstel** klikt u op Hallo **schijven ontkoppelen** knop. Als u toodo deze stap vergeet, wordt na 12 uur Hallo verbinding toohello koppelpunt automatisch sluiten. Na deze 12 uur moet u een nieuwe script toocreate een nieuwe koppelpunt toodownload.


## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]
> * Maak een back-up van een virtuele machine
> * Een dagelijkse back-up plannen
> * Een bestand te herstellen vanaf een back-up

Ga toohello volgende zelfstudie toolearn over het bewaken van virtuele machines.

> [!div class="nextstepaction"]
> [Virtuele machines bewaken](tutorial-monitoring.md)

