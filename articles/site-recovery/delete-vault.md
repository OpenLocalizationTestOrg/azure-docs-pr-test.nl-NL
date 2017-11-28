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
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="12ddc-103">Een Site Recovery-kluis verwijderen</span><span class="sxs-lookup"><span data-stu-id="12ddc-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="12ddc-104">Afhankelijkheden kunnen voorkomen dat u een Azure Site Recovery-kluis verwijderen.</span><span class="sxs-lookup"><span data-stu-id="12ddc-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="12ddc-105">Hallo acties u moet tootake variëren, afhankelijk van Site Recovery-scenario Hallo: VMware-tooAzure tooAzure Hyper-V (met en zonder System Center Virtual Machine Manager) en Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="12ddc-105">hello actions you need tootake vary based on hello Site Recovery scenario: VMware tooAzure, Hyper-V (with and without System Center Virtual Machine Manager) tooAzure, and Azure Backup.</span></span> <span data-ttu-id="12ddc-106">Zie een gebruikt in Azure Backup-kluis toodelete [verwijderen van een back-upkluis in Azure](../backup/backup-azure-delete-vault.md).</span><span class="sxs-lookup"><span data-stu-id="12ddc-106">toodelete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="12ddc-107">Als u test Hallo product en worden niet betrokken zijn bij verlies van gegevens, verwijder gebruik Hallo geforceerd verwijderen methode toorapidly Hallo kluis en de afhankelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="12ddc-107">If you're testing hello product and aren't concerned about data loss, use hello force delete method toorapidly remove hello vault and all its dependencies.</span></span>

> <span data-ttu-id="12ddc-108">Hallo PowerShell-opdracht worden alle Hallo inhoud van het Hallo-kluis verwijderd en is niet omkeerbaar.</span><span class="sxs-lookup"><span data-stu-id="12ddc-108">hello PowerShell command deletes all hello contents of hello vault and is not reversible.</span></span>

## <a name="use-powershell-tooforce-delete-hello-vault"></a><span data-ttu-id="12ddc-109">Gebruik PowerShell tooforce Hallo kluis verwijderen</span><span class="sxs-lookup"><span data-stu-id="12ddc-109">Use PowerShell tooforce delete hello vault</span></span> 

<span data-ttu-id="12ddc-110">toodelete hello Site Recovery-kluis zelfs als er beveiligde items, deze opdrachten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="12ddc-110">toodelete hello Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="12ddc-111">Een Site Recovery-kluis verwijderen</span><span class="sxs-lookup"><span data-stu-id="12ddc-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="12ddc-112">toodelete hello kluis, volg Hallo aanbevolen stappen voor uw scenario.</span><span class="sxs-lookup"><span data-stu-id="12ddc-112">toodelete hello vault, follow hello recommended steps for your scenario.</span></span>

### <a name="vmware-vms-tooazure"></a><span data-ttu-id="12ddc-113">Virtuele VMware-machines tooAzure</span><span class="sxs-lookup"><span data-stu-id="12ddc-113">VMware VMs tooAzure</span></span>

1. <span data-ttu-id="12ddc-114">Verwijder alle virtuele machines beveiligd door de stappen te volgen Hallo in [Schakel de beveiliging voor een VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="12ddc-114">Delete all protected VMs by following hello steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="12ddc-115">Alle beleidsregels voor replicatie verwijderen door de stappen te volgen Hallo in [verwijderen van een beleid voor wachtwoordreplicatie](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="12ddc-115">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="12ddc-116">Verwijzingen toovCenter door de volgende Hallo stappen voor het verwijderen [verwijderen van een vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span><span class="sxs-lookup"><span data-stu-id="12ddc-116">Delete references toovCenter by following hello steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="12ddc-117">Hallo configuratieserver verwijderen door de stappen te volgen Hallo in [een configuratieserver buiten gebruik stellen](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="12ddc-117">Delete hello configuration server by following hello steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="12ddc-118">Hallo kluis verwijderen.</span><span class="sxs-lookup"><span data-stu-id="12ddc-118">Delete hello vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a><span data-ttu-id="12ddc-119">Hyper-V-machines (met Virtual Machine Manager) tooAzure</span><span class="sxs-lookup"><span data-stu-id="12ddc-119">Hyper-V VMs (with Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="12ddc-120">Verwijder alle virtuele machines beveiligd door de stappen te volgen Hallo in [Schakel de beveiliging voor een VMware-VM of de fysieke server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="12ddc-120">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="12ddc-121">Alle beleidsregels voor replicatie verwijderen door de stappen te volgen Hallo in [verwijderen van een beleid voor wachtwoordreplicatie](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="12ddc-121">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="12ddc-122">Delete verwijst naar tooVirtual Machine Manager-servers door de stappen te volgen Hallo in [Hef de registratie van een VMM-server verbonden](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span><span class="sxs-lookup"><span data-stu-id="12ddc-122">Delete references tooVirtual Machine Manager servers by following hello steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="12ddc-123">Hallo kluis verwijderen.</span><span class="sxs-lookup"><span data-stu-id="12ddc-123">Delete hello vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a><span data-ttu-id="12ddc-124">Hyper-V-machines (zonder Virtual Machine Manager) tooAzure</span><span class="sxs-lookup"><span data-stu-id="12ddc-124">Hyper-V VMs (without Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="12ddc-125">Verwijder alle virtuele machines beveiligd door de stappen te volgen Hallo in [Schakel de beveiliging voor een VMware-VM of de fysieke server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="12ddc-125">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="12ddc-126">Alle beleidsregels voor replicatie verwijderen door de stappen te volgen Hallo in [verwijderen van een beleid voor wachtwoordreplicatie](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="12ddc-126">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="12ddc-127">Delete verwijst naar tooHyper-V-servers door de stappen te volgen Hallo in [Hef de registratie van een Hyper-V-host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span><span class="sxs-lookup"><span data-stu-id="12ddc-127">Delete references tooHyper-V servers by following hello steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="12ddc-128">Hallo Hyper-V-site verwijderen.</span><span class="sxs-lookup"><span data-stu-id="12ddc-128">Delete hello Hyper-V site.</span></span>

5. <span data-ttu-id="12ddc-129">Hallo kluis verwijderen.</span><span class="sxs-lookup"><span data-stu-id="12ddc-129">Delete hello vault.</span></span>
