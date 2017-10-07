---
title: aaaDelete een Site Recovery-kluis
description: Meer informatie over hoe toodelete een Azure Site Recovery-kluis op basis van Hallo Site Recovery scenario.
service: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: 36db202d8b790bb5d31d1348fb72f51acb5d559c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-site-recovery-vault"></a>Een Site Recovery-kluis verwijderen
Afhankelijkheden kunnen voorkomen dat u een Azure Site Recovery-kluis verwijderen. Hallo acties u moet tootake variëren, afhankelijk van Site Recovery-scenario Hallo: VMware-tooAzure tooAzure Hyper-V (met en zonder System Center Virtual Machine Manager) en Azure Backup. Zie een gebruikt in Azure Backup-kluis toodelete [verwijderen van een back-upkluis in Azure](../backup/backup-azure-delete-vault.md).

>[!Important]
>Als u test Hallo product en worden niet betrokken zijn bij verlies van gegevens, verwijder gebruik Hallo geforceerd verwijderen methode toorapidly Hallo kluis en de afhankelijkheden ervan.

> Hallo PowerShell-opdracht worden alle Hallo inhoud van het Hallo-kluis verwijderd en is niet omkeerbaar.

## <a name="use-powershell-tooforce-delete-hello-vault"></a>Gebruik PowerShell tooforce Hallo kluis verwijderen 

toodelete hello Site Recovery-kluis zelfs als er beveiligde items, deze opdrachten gebruiken:

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a>Een Site Recovery-kluis verwijderen 
toodelete hello kluis, volg Hallo aanbevolen stappen voor uw scenario.

### <a name="vmware-vms-tooazure"></a>Virtuele VMware-machines tooAzure

1. Verwijder alle virtuele machines beveiligd door de stappen te volgen Hallo in [Schakel de beveiliging voor een VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Alle beleidsregels voor replicatie verwijderen door de stappen te volgen Hallo in [verwijderen van een beleid voor wachtwoordreplicatie](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Verwijzingen toovCenter door de volgende Hallo stappen voor het verwijderen [verwijderen van een vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).

4. Hallo configuratieserver verwijderen door de stappen te volgen Hallo in [een configuratieserver buiten gebruik stellen](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).

5. Hallo kluis verwijderen.


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a>Hyper-V-machines (met Virtual Machine Manager) tooAzure
1. Verwijder alle virtuele machines beveiligd door de stappen te volgen Hallo in [Schakel de beveiliging voor een VMware-VM of de fysieke server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Alle beleidsregels voor replicatie verwijderen door de stappen te volgen Hallo in [verwijderen van een beleid voor wachtwoordreplicatie](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3.  Delete verwijst naar tooVirtual Machine Manager-servers door de stappen te volgen Hallo in [Hef de registratie van een VMM-server verbonden](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).

4.  Hallo kluis verwijderen.

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a>Hyper-V-machines (zonder Virtual Machine Manager) tooAzure
1. Verwijder alle virtuele machines beveiligd door de stappen te volgen Hallo in [Schakel de beveiliging voor een VMware-VM of de fysieke server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Alle beleidsregels voor replicatie verwijderen door de stappen te volgen Hallo in [verwijderen van een beleid voor wachtwoordreplicatie](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Delete verwijst naar tooHyper-V-servers door de stappen te volgen Hallo in [Hef de registratie van een Hyper-V-host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).

4. Hallo Hyper-V-site verwijderen.

5. Hallo kluis verwijderen.
