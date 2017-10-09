---
title: aaaSet van replicatie-instellingen voor Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven hoe clouds tooAzure toodeploy siteherstel tooorchestrate replicatie, failovers en herstel van Hyper-V-machines in VMM.
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a>Replicatiebeleid voor voor VMware tooAzure beheren


## <a name="create-a-replication-policy"></a>Een replicatiebeleid maken

1. Selecteer **Beheren** > **Infrastructuur voor Site Recovery**.
2. Selecteer **Replicatiebeleid** onder **Voor VMware en fysieke machines**.
3. Selecteer **+Replicatiebeleid**.

    ![Replicatiebeleid maken](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. Voer de beleidsnaam Hallo.

5. In **RPO drempelwaarde**, Hallo RPO grootte opgeven. Wanneer de continue replicatie deze limiet overschrijdt, worden er waarschuwingen gegenereerd.
6. In **herstel bewaarperiode**, geef (in uren) Hallo duur van de bewaarperiode Hallo voor elk herstelpunt. Beveiligde machines kunnen worden hersteld tooany punt binnen een bewaarperiode.

    > [!NOTE]
    > Too24 uur retentieperiode wordt ondersteund voor de opslag van de gerepliceerde toopremium machines. Too72 uur retentieperiode wordt ondersteund voor de opslag van de gerepliceerde toostandard machines.

    > [!NOTE]
    > Er wordt automatisch een replicatiebeleid voor failback gemaakt.

7. Geef in **Frequentie van de app-consistente momentopname** op hoe vaak (in minuten) er herstelpunten moeten worden gemaakt met toepassingsconsistente momentopnamen.

8. Klik op **OK**. Hallo-beleid moet worden gemaakt in 30 too60 seconden.

![Replicatiebeleid genereren](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a>Een configuratieserver koppelen aan het replicatiebeleid
1. Kies Hallo replicatie beleid toowhich gewenste tooassociate Hallo configuratieserver.
2. Klik op **Koppelen**.
![Configuratieserver koppelen](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)

3. Selecteer Hallo configuratieserver uit Hallo lijst met servers.
4. Klik op **OK**. Hallo configuratieserver moet worden gekoppeld in één tootwo minuten.

![Configuratieserver koppelen](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a>Een replicatiebeleid bewerken
1. Hallo replicatiebeleid waarvoor u tooedit replicatie-instellingen wilt kiezen.
![Replicatiebeleid bewerken](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)

2. Klik op **Instellingen bewerken**.
![Instellingen van replicatiebeleid bewerken](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)

3. Hallo wijzigen op basis van uw behoeften.
4. Klik op **Opslaan**. Hallo-beleid moet worden opgeslagen in twee toofive minuten, afhankelijk van hoeveel virtuele machines die replicatiebeleid gebruikt.

![Replicatiebeleid opslaan](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a>Een configuratieserver loskoppelen van een replicatiebeleid
1. Kies Hallo replicatie beleid toowhich gewenste tooassociate Hallo configuratieserver.
2. Klik op **Ontkoppelen**.
3. Selecteer Hallo configuratieserver uit Hallo lijst met servers.
4. Klik op **OK**. Hallo configuratieserver moet worden ontkoppeld in één tootwo minuten.

    > [!NOTE]
    > U kunt een configuratieserver kan niet ontkoppelen als er ten minste één gerepliceerde item met behulp van Hallo-beleid. Zorg ervoor dat er zijn geen gerepliceerde items met behulp van Hallo beleid voordat u de configuratieserver Hallo ontkoppelen.

## <a name="delete-a-replication-policy"></a>Een replicatiebeleid verwijderen

1. Hallo replicatiebeleid kiezen dat u wilt dat toodelete.
2. Klik op **Verwijderen**. Hallo-beleid moet worden verwijderd in 30 too60 seconden.

    > [!NOTE]
    > U kunt een beleid voor wachtwoordreplicatie niet verwijderen als er ten minste één tooit voor configuratie-server die is gekoppeld. Controleer of er zijn geen gerepliceerde items met behulp van beleid Hallo en verwijder die alle Hallo configuratieservers gekoppeld voordat u Hallo beleid verwijderen.
