---
title: Een Site Recovery-kluis verwijderen
description: Informatie over het verwijderen van een Azure Site Recovery-kluis op basis van de Site Recovery-scenario.
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
ms.openlocfilehash: b95b9defa0a037f7d7d3ef36b99bc7c53c751050
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="9d447-103">Een Site Recovery-kluis verwijderen</span><span class="sxs-lookup"><span data-stu-id="9d447-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="9d447-104">Afhankelijkheden kunnen voorkomen dat u een Azure Site Recovery-kluis verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9d447-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="9d447-105">De acties die u moet nemen afhankelijk van het scenario met Site Recovery: VMware naar Azure, Hyper-V (met en zonder System Center Virtual Machine Manager) voor Azure en Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="9d447-105">The actions you need to take vary based on the Site Recovery scenario: VMware to Azure, Hyper-V (with and without System Center Virtual Machine Manager) to Azure, and Azure Backup.</span></span> <span data-ttu-id="9d447-106">Zie het verwijderen van een gebruikt in Azure Backup-kluis [verwijderen van een back-upkluis in Azure](../backup/backup-azure-delete-vault.md).</span><span class="sxs-lookup"><span data-stu-id="9d447-106">To delete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="9d447-107">Als u het product test en niet betrokken zijn bij verlies van gegevens, gebruikt u de delete-methode force snel de kluis en de afhankelijkheden ervan verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9d447-107">If you're testing the product and aren't concerned about data loss, use the force delete method to rapidly remove the vault and all its dependencies.</span></span>

> <span data-ttu-id="9d447-108">De PowerShell-opdracht wordt de inhoud van de kluis verwijderd en is niet omkeerbaar.</span><span class="sxs-lookup"><span data-stu-id="9d447-108">The PowerShell command deletes all the contents of the vault and is not reversible.</span></span>

## <a name="use-powershell-to-force-delete-the-vault"></a><span data-ttu-id="9d447-109">Gebruik PowerShell om af te dwingen de kluis verwijderen</span><span class="sxs-lookup"><span data-stu-id="9d447-109">Use PowerShell to force delete the vault</span></span> 

<span data-ttu-id="9d447-110">Voor het verwijderen van de Site Recovery-kluis zelfs als er beveiligde items, moet u deze opdrachten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9d447-110">To delete the Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="9d447-111">Een Site Recovery-kluis verwijderen</span><span class="sxs-lookup"><span data-stu-id="9d447-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="9d447-112">Volg de aanbevolen stappen voor uw scenario voor het verwijderen van de kluis.</span><span class="sxs-lookup"><span data-stu-id="9d447-112">To delete the vault, follow the recommended steps for your scenario.</span></span>

### <a name="vmware-vms-to-azure"></a><span data-ttu-id="9d447-113">VMware-VM’s naar Azure</span><span class="sxs-lookup"><span data-stu-id="9d447-113">VMware VMs to Azure</span></span>

1. <span data-ttu-id="9d447-114">Verwijder alle virtuele machines beveiligd door de stappen in [Schakel de beveiliging voor een VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="9d447-114">Delete all protected VMs by following the steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="9d447-115">Beleidsregels voor alle replicatie verwijderen door de stappen in [verwijderen van een beleid voor wachtwoordreplicatie](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="9d447-115">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="9d447-116">Verwijzingen naar vCenter verwijderen door de stappen in [verwijderen van een vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span><span class="sxs-lookup"><span data-stu-id="9d447-116">Delete references to vCenter by following the steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="9d447-117">De configuratieserver verwijderen door de stappen in [een configuratieserver buiten gebruik stellen](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="9d447-117">Delete the configuration server by following the steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="9d447-118">Verwijder de kluis.</span><span class="sxs-lookup"><span data-stu-id="9d447-118">Delete the vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-to-azure"></a><span data-ttu-id="9d447-119">Hyper-V-machines (met Virtual Machine Manager) naar Azure</span><span class="sxs-lookup"><span data-stu-id="9d447-119">Hyper-V VMs (with Virtual Machine Manager) to Azure</span></span>
1. <span data-ttu-id="9d447-120">Verwijder alle virtuele machines beveiligd door de stappen in [Schakel de beveiliging voor een VMware-VM of de fysieke server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="9d447-120">Delete all protected VMs by following the steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="9d447-121">Beleidsregels voor alle replicatie verwijderen door de stappen in [verwijderen van een beleid voor wachtwoordreplicatie](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="9d447-121">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="9d447-122">Verwijzingen naar Virtual Machine Manager-servers verwijderen door de stappen in [Hef de registratie van een VMM-server verbonden](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span><span class="sxs-lookup"><span data-stu-id="9d447-122">Delete references to Virtual Machine Manager servers by following the steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="9d447-123">Verwijder de kluis.</span><span class="sxs-lookup"><span data-stu-id="9d447-123">Delete the vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-to-azure"></a><span data-ttu-id="9d447-124">Hyper-V-machines (zonder Virtual Machine Manager) naar Azure</span><span class="sxs-lookup"><span data-stu-id="9d447-124">Hyper-V VMs (without Virtual Machine Manager) to Azure</span></span>
1. <span data-ttu-id="9d447-125">Verwijder alle virtuele machines beveiligd door de stappen in [Schakel de beveiliging voor een VMware-VM of de fysieke server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="9d447-125">Delete all protected VMs by following the steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="9d447-126">Beleidsregels voor alle replicatie verwijderen door de stappen in [verwijderen van een beleid voor wachtwoordreplicatie](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="9d447-126">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="9d447-127">Verwijzingen naar Hyper-V-servers verwijderen door de stappen in [Hef de registratie van een Hyper-V-host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span><span class="sxs-lookup"><span data-stu-id="9d447-127">Delete references to Hyper-V servers by following the steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="9d447-128">De Hyper-V-site verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9d447-128">Delete the Hyper-V site.</span></span>

5. <span data-ttu-id="9d447-129">Verwijder de kluis.</span><span class="sxs-lookup"><span data-stu-id="9d447-129">Delete the vault.</span></span>
