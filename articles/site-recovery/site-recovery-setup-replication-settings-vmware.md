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
# <a name="manage-replication-policy-for-vmware-tooazure"></a><span data-ttu-id="42ba4-103">Replicatiebeleid voor voor VMware tooAzure beheren</span><span class="sxs-lookup"><span data-stu-id="42ba4-103">Manage replication policy for VMware tooAzure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="42ba4-104">Een replicatiebeleid maken</span><span class="sxs-lookup"><span data-stu-id="42ba4-104">Create a replication policy</span></span>

1. <span data-ttu-id="42ba4-105">Selecteer **Beheren** > **Infrastructuur voor Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="42ba4-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="42ba4-106">Selecteer **Replicatiebeleid** onder **Voor VMware en fysieke machines**.</span><span class="sxs-lookup"><span data-stu-id="42ba4-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="42ba4-107">Selecteer **+Replicatiebeleid**.</span><span class="sxs-lookup"><span data-stu-id="42ba4-107">Select **+Replication policy**.</span></span>

    ![Replicatiebeleid maken](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="42ba4-109">Voer de beleidsnaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="42ba4-109">Enter hello policy name.</span></span>

5. <span data-ttu-id="42ba4-110">In **RPO drempelwaarde**, Hallo RPO grootte opgeven.</span><span class="sxs-lookup"><span data-stu-id="42ba4-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="42ba4-111">Wanneer de continue replicatie deze limiet overschrijdt, worden er waarschuwingen gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="42ba4-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="42ba4-112">In **herstel bewaarperiode**, geef (in uren) Hallo duur van de bewaarperiode Hallo voor elk herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="42ba4-112">In **Recovery point retention**, specify (in hours) hello duration of hello retention window for each recovery point.</span></span> <span data-ttu-id="42ba4-113">Beveiligde machines kunnen worden hersteld tooany punt binnen een bewaarperiode.</span><span class="sxs-lookup"><span data-stu-id="42ba4-113">Protected machines can be recovered tooany point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="42ba4-114">Too24 uur retentieperiode wordt ondersteund voor de opslag van de gerepliceerde toopremium machines.</span><span class="sxs-lookup"><span data-stu-id="42ba4-114">Up too24 hours of retention is supported for machines replicated toopremium storage.</span></span> <span data-ttu-id="42ba4-115">Too72 uur retentieperiode wordt ondersteund voor de opslag van de gerepliceerde toostandard machines.</span><span class="sxs-lookup"><span data-stu-id="42ba4-115">Up too72 hours of retention is supported for machines replicated toostandard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="42ba4-116">Er wordt automatisch een replicatiebeleid voor failback gemaakt.</span><span class="sxs-lookup"><span data-stu-id="42ba4-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="42ba4-117">Geef in **Frequentie van de app-consistente momentopname** op hoe vaak (in minuten) er herstelpunten moeten worden gemaakt met toepassingsconsistente momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="42ba4-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="42ba4-118">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="42ba4-118">Click **OK**.</span></span> <span data-ttu-id="42ba4-119">Hallo-beleid moet worden gemaakt in 30 too60 seconden.</span><span class="sxs-lookup"><span data-stu-id="42ba4-119">hello policy should be created in 30 too60 seconds.</span></span>

![Replicatiebeleid genereren](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="42ba4-121">Een configuratieserver koppelen aan het replicatiebeleid</span><span class="sxs-lookup"><span data-stu-id="42ba4-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="42ba4-122">Kies Hallo replicatie beleid toowhich gewenste tooassociate Hallo configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="42ba4-122">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="42ba4-123">Klik op **Koppelen**.</span><span class="sxs-lookup"><span data-stu-id="42ba4-123">Click **Associate**.</span></span>
<span data-ttu-id="42ba4-124">![Configuratieserver koppelen](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="42ba4-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="42ba4-125">Selecteer Hallo configuratieserver uit Hallo lijst met servers.</span><span class="sxs-lookup"><span data-stu-id="42ba4-125">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="42ba4-126">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="42ba4-126">Click **OK**.</span></span> <span data-ttu-id="42ba4-127">Hallo configuratieserver moet worden gekoppeld in één tootwo minuten.</span><span class="sxs-lookup"><span data-stu-id="42ba4-127">hello configuration server should be associated in one tootwo minutes.</span></span>

![Configuratieserver koppelen](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="42ba4-129">Een replicatiebeleid bewerken</span><span class="sxs-lookup"><span data-stu-id="42ba4-129">Edit a replication policy</span></span>
1. <span data-ttu-id="42ba4-130">Hallo replicatiebeleid waarvoor u tooedit replicatie-instellingen wilt kiezen.</span><span class="sxs-lookup"><span data-stu-id="42ba4-130">Choose hello replication policy for which you want tooedit replication settings.</span></span>
<span data-ttu-id="42ba4-131">![Replicatiebeleid bewerken](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="42ba4-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="42ba4-132">Klik op **Instellingen bewerken**.</span><span class="sxs-lookup"><span data-stu-id="42ba4-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="42ba4-133">![Instellingen van replicatiebeleid bewerken](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="42ba4-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="42ba4-134">Hallo wijzigen op basis van uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="42ba4-134">Change hello settings based on your need.</span></span>
4. <span data-ttu-id="42ba4-135">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="42ba4-135">Click **Save**.</span></span> <span data-ttu-id="42ba4-136">Hallo-beleid moet worden opgeslagen in twee toofive minuten, afhankelijk van hoeveel virtuele machines die replicatiebeleid gebruikt.</span><span class="sxs-lookup"><span data-stu-id="42ba4-136">hello policy should be saved in two toofive minutes, depending on how many VMs are using that replication policy.</span></span>

![Replicatiebeleid opslaan](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="42ba4-138">Een configuratieserver loskoppelen van een replicatiebeleid</span><span class="sxs-lookup"><span data-stu-id="42ba4-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="42ba4-139">Kies Hallo replicatie beleid toowhich gewenste tooassociate Hallo configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="42ba4-139">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="42ba4-140">Klik op **Ontkoppelen**.</span><span class="sxs-lookup"><span data-stu-id="42ba4-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="42ba4-141">Selecteer Hallo configuratieserver uit Hallo lijst met servers.</span><span class="sxs-lookup"><span data-stu-id="42ba4-141">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="42ba4-142">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="42ba4-142">Click **OK**.</span></span> <span data-ttu-id="42ba4-143">Hallo configuratieserver moet worden ontkoppeld in één tootwo minuten.</span><span class="sxs-lookup"><span data-stu-id="42ba4-143">hello configuration server should be dissociated in one tootwo minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="42ba4-144">U kunt een configuratieserver kan niet ontkoppelen als er ten minste één gerepliceerde item met behulp van Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="42ba4-144">You cannot dissociate a configuration server if there is at least one replicated item using hello policy.</span></span> <span data-ttu-id="42ba4-145">Zorg ervoor dat er zijn geen gerepliceerde items met behulp van Hallo beleid voordat u de configuratieserver Hallo ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="42ba4-145">Make sure there are no replicated items using hello policy before you dissociate hello configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="42ba4-146">Een replicatiebeleid verwijderen</span><span class="sxs-lookup"><span data-stu-id="42ba4-146">Delete a replication policy</span></span>

1. <span data-ttu-id="42ba4-147">Hallo replicatiebeleid kiezen dat u wilt dat toodelete.</span><span class="sxs-lookup"><span data-stu-id="42ba4-147">Choose hello replication policy that you want toodelete.</span></span>
2. <span data-ttu-id="42ba4-148">Klik op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="42ba4-148">Click **Delete**.</span></span> <span data-ttu-id="42ba4-149">Hallo-beleid moet worden verwijderd in 30 too60 seconden.</span><span class="sxs-lookup"><span data-stu-id="42ba4-149">hello policy should be deleted in 30 too60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="42ba4-150">U kunt een beleid voor wachtwoordreplicatie niet verwijderen als er ten minste één tooit voor configuratie-server die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="42ba4-150">You cannot delete a replication policy if it has at least one configuration server associated tooit.</span></span> <span data-ttu-id="42ba4-151">Controleer of er zijn geen gerepliceerde items met behulp van beleid Hallo en verwijder die alle Hallo configuratieservers gekoppeld voordat u Hallo beleid verwijderen.</span><span class="sxs-lookup"><span data-stu-id="42ba4-151">Make sure there are no replicated items using hello policy and delete all hello associated configuration servers before you delete hello policy.</span></span>
