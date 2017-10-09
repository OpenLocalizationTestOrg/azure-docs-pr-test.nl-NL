---
title: aaaBack van Azure Virtual machines | Microsoft Docs
description: Back-up van virtuele machines in Azure recovery services-kluis tooa detecteren en registreren.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: back-up van virtuele machine. back-up van virtuele machine; back-up en herstel na noodgevallen; back-up van arm vm
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a>Maak een back-up van virtuele machines in Azure tooa Recovery Services-kluis
> [!div class="op_single_selector"]
> * [Back-up van virtuele machines tooRecovery Services-kluis](backup-azure-arm-vms.md)
> * [Back-up van virtuele machines tooBackup kluis](backup-azure-vms.md)
>
>

Dit artikel wordt uitgelegd hoe tooback van Azure Virtual machines (geïmplementeerd met Resource Manager en Classic geïmplementeerd) tooa Recovery Services-kluis. De meeste Hallo werk voor back-ups van virtuele machines is Hallo voorbereiding. Voordat u kunt back-up of een virtuele machine te beveiligen, moet u Hallo [vereisten](backup-azure-arm-vms-prepare.md) tooprepare uw omgeving voor het beveiligen van uw virtuele machines. Nadat u Hallo vereisten hebt voltooid, kunt u Hallo back-upbewerking tootake momentopnamen van uw virtuele machine starten.


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

Zie voor meer informatie Hallo artikelen op [plannen van uw back-upinfrastructuur VM in Azure](backup-azure-vms-introduction.md) en [virtuele Azure-machines](https://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="triggering-hello-backup-job"></a>Activering van de back-uptaak Hallo
Hallo back-upbeleid gekoppeld Hallo die Recovery Services-kluis wordt gedefinieerd hoe vaak en wanneer Hallo back-upbewerking wordt uitgevoerd. Hallo eerste geplande back-up is standaard Hallo eerste back-up. Totdat de eerste back-up Hallo optreedt, Hallo Status van de laatste back-up op Hallo **back-uptaken** blade wordt weergegeven als **waarschuwing (eerste back-up in behandeling)**.

![Back-up in behandeling](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

Tenzij u uw eerste back-up toobegin binnenkort is het raadzaam dat u uitvoert **Back-up nu**. Hallo begint volgende procedure bij Hallo kluisdashboard. Deze procedure fungeert voor het uitvoeren van de eerste back-uptaak Hallo nadat u alle vereisten hebt voltooid. Deze procedure is niet beschikbaar als de eerste back-uptaak Hallo al is uitgevoerd. Hallo bepaalt gekoppeld back-upbeleid Hallo volgende back-uptaak.  

toorun hello eerste back-uptaak:

1. Op het kluisdashboard hello, klikt u op Hallo onder **back-Upitems**, of klik op Hallo **back-Upitems** tegel. <br/>
  ![Pictogram Instellingen](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  Hallo **back-Upitems** blade wordt geopend.

  ![Back-upitems](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. Op Hallo **back-Upitems** blade, selecteer Hallo artikel.

  ![Het pictogram Instellingen](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  Hallo **back-Upitems** lijst wordt geopend. <br/>

  ![Geactiveerde back-uptaak](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. Op Hallo **back-Upitems** lijst, klikt u op de weglatingstekens Hallo **...**  tooopen Hallo contextmenu.

  ![Contextmenu](./media/backup-azure-vms-first-look-arm/context-menu.png)

  Hallo contextmenu wordt weergegeven.

  ![Contextmenu](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. Klik in het contextmenu hello, **back-up nu**.

  ![Contextmenu](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  back-up nu Hallo-blade wordt geopend.

  ![ziet u nu back-up Hallo-blade](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. Klik op Hallo nu back-up blade op Hallo kalenderpictogram, gebruikt u Hallo kalender besturingselement tooselect Hallo laatste dag van dit herstelpunt wordt bewaard, en klik op **back-up**.

  ![set Hallo laatste dag Hallo nu back-up een herstelpunt wordt bewaard](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Meldingen van de implementatie kunnen u weten Hallo back-uptaak is geactiveerd en dat u kunt voortgang Hallo van Hallo-taak op de pagina Hallo back-up-taken. Afhankelijk van de grootte van de Hallo van uw virtuele machine, kan Hallo eerste back-up maken duren.

6. tooview of bijhouden Hallo-status van Hallo eerste back-up, op Hallo kluisdashboard op Hallo **back-uptaken** Klik op de tegel **Bezig**.

  ![Tegel Back-uptaken](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  de blade back-uptaken Hello wordt geopend.

  ![Tegel Back-uptaken](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  In Hallo **back-uptaken** blade ziet u Hallo status van alle taken. Controleer als Hallo back-uptaak voor uw virtuele machine wordt nog uitgevoerd of als het is voltooid. Wanneer een back-uptaak is voltooid, is het Hallo-status *voltooid*.

  > [!NOTE]
  > Als onderdeel van de back-upbewerking Hallo verstrekt hello Azure Backup-service een toohello opdracht Backup-extensie in elke VM tooflush alle schrijft en een consistente momentopname.
  >
  >

## <a name="troubleshooting-errors"></a>Het oplossen van problemen
Als u problemen tijdens het back-ups maken van uw virtuele machine, Zie Hallo [VM probleemoplossingsartikel](backup-azure-vms-troubleshoot.md) voor hulp.

## <a name="next-steps"></a>Volgende stappen
Nu u uw virtuele machine hebt beveiligd, gaat u naar Hallo na toolearn artikelen over VM beheertaken, en hoe toorestore virtuele machines.

* [Uw virtuele machines beheren en controleren](backup-azure-manage-vms.md)
* [Virtuele machines herstellen](backup-azure-arm-restore-vms.md)
