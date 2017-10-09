---
title: aaaBackup VM's van Windows Azure | Microsoft-Docs
description: Uw Windows-VM's beveiligen door deze back-ups van maken met Azure Backup.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a>Back-up van Windows virtuele machines in Azure

U kunt uw gegevens beschermen door regelmatig back-ups te maken. Azure Backup maakt herstelpunten die zijn opgeslagen in een geografisch redundante recovery kluizen. Wanneer u vanaf een herstelpunt herstelt, kunt u herstellen Hallo hele virtuele machine of alleen specifieke bestanden. Dit artikel wordt uitgelegd hoe toorestore één bestand tooa virtuele machine met Windows Server- en IIS. Als u een VM-toouse nog geen hebt, kunt u een maken met behulp van Hallo [Windows-snelstartgids](quick-create-portal.md). In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Maak een back-up van een virtuele machine
> * Een dagelijkse back-up plannen
> * Een bestand te herstellen vanaf een back-up




## <a name="backup-overview"></a>Overzicht van Backup

Wanneer hello Azure Backup-service een back-uptaak initieert, activeert het Hallo Backup-extensie tootake een momentopname van een punt in tijd. Hello Azure Backup-service gebruikt Hallo _VMSnapshot_ extensie. Hallo-extensie wordt geïnstalleerd tijdens Hallo eerste VM back-up als Hallo VM wordt uitgevoerd. Als hello VM niet wordt uitgevoerd, wordt Hallo Backup-service een momentopname van Hallo onderliggende opslag (omdat er geen schrijfbewerkingen toepassing tijdens het Hallo die VM is gestopt optreden).

Bij het nemen van een momentopname van VM's van Windows coördineert hello Backup-service met Hallo Volume Shadow Copy Service (VSS) tooget een consistente momentopname te maken van schijven Hallo virtuele machine. Zodra hello Azure Backup-service Hallo momentopname maakt, is Hallo gegevens overgedragen toohello kluis. toomaximize-efficiëntie Hallo service identificeert en alleen Hallo blokken met gegevens die zijn gewijzigd sinds de vorige back-up Hallo overdraagt.

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

## <a name="recover-a-file"></a>Herstellen van een bestand

Als u per ongeluk verwijdert of wijzigingen tooa bestand maken, kunt u bestandsherstel toorecover Hallo bestand vanuit uw back-upkluis. Bestandsherstel maakt gebruik van een script dat wordt uitgevoerd op virtuele machine, Hallo toomount Hallo herstelpunt als lokale schijf. Deze stations blijft gekoppelde 12 uur zodat u kunt bestanden vanaf Hallo herstelpunt kopiëren en herstel deze toohello VM.  

In dit voorbeeld laten we zien hoe toorecover Hallo installatiekopiebestand op dat wordt gebruikt in Hallo standaardwebpagina voor IIS. 

1. Open een browser en maak verbinding toohello IP-adres van Hallo VM tooshow Hallo standaard IIS-pagina.

    ![IIS-standaardwebpagina](./media/tutorial-backup-vms/iis-working.png)

2. Verbinding maken met toohello VM.
3. Open op Hallo VM, **Verkenner** en navigeer too\inetpub\wwwroot en verwijder het Hallo-bestand **iisstart.png**.
4. Vernieuwen Hallo browser toosee die de installatiekopie op de standaardpagina IIS Hallo Hallo is op de lokale computer verwijderd.

    ![IIS-standaardwebpagina](./media/tutorial-backup-vms/iis-broken.png)

5. Open op uw lokale computer, een nieuw tabblad en ga Hallo Hallo [Azure-portal](https://portal.azure.com).
6. Selecteer in het menu aan de linkerkant Hallo Hallo **virtuele machines** en selecteer Hallo VM formulier Hallo lijst.
8. Op Hallo VM blade in Hallo **instellingen** sectie, klikt u op **back-up**. Hallo **back-up** blade wordt geopend. 
9. Selecteer in het menu Hallo Hallo boven aan het Hallo-blade **bestandsherstel**. Hallo **bestandsherstel** blade wordt geopend.
10. In **stap 1: Selecteer herstelpunt**, selecteer een herstelpunt in de vervolgkeuzelijst Hallo.
11. In **stap 2: downloaden script toobrowse en bestanden herstellen**, klikt u op Hallo **uitvoerbaar bestand downloaden** knop. Hallo bestand tooyour opslaan **downloadt** map.
12. Open op uw lokale computer **Verkenner** en navigeer tooyour **downloadt** map en kopieer Hallo .exe-bestand hebt gedownload. Hallo filename wordt voorafgegaan door de naam van uw virtuele machine. 
13. Plak Hallo .exe-bestand toohello bureaublad van uw virtuele machine op de virtuele machine (via Hallo RDP-verbinding). 
14. Ga toohello bureaublad van uw virtuele machine en dubbelklik op Hallo .exe. Hiermee wordt een opdrachtprompt en koppel vervolgens Hallo herstelpunt worden gemaakt als een bestandsshare die u toegang hebt tot. Wanneer deze is voltooid maken Hallo share, typt u **q** tooclose Hallo-opdrachtprompt.
15. Open op uw virtuele machine, **Verkenner** en navigeer toohello stationsletter is die is gebruikt voor het Hallo-bestandsshare.
16. Navigeer too\inetpub\wwwroot en kopieer **iisstart.png** uit Hallo-bestand delen en plak deze in \inetpub\wwwroot. Bijvoorbeeld: F:\inetpub\wwwroot\iisstart.png Kopieer en plak deze in c:\inetpub\wwwroot toorecover Hallo-bestand.
17. Open op uw lokale computer Hallo browsertabblad waar u bent verbonden toohello IP-adres van Hallo VM van Hallo IIS standaard de pagina. Druk op CTRL + F5 toorefresh Hallo browserpagina. U ziet nu dat Hallo afbeelding is hersteld.
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









