---
title: Replicatie-instellingen voor Azure Site Recovery instellen | Microsoft Docs
description: Dit artikel beschrijft hoe u Site Recovery implementeert om replicatie, failovers en herstel van virtuele Hyper-V-machines in VMM-clouds naar Azure te beheren.
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
ms.openlocfilehash: 73a1f19177f23441f5f7165cf2bc92ba85e62aa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-replication-policy-for-vmware-to-azure"></a><span data-ttu-id="11a43-103">Replicatiebeleid voor VMware naar Azure beheren</span><span class="sxs-lookup"><span data-stu-id="11a43-103">Manage replication policy for VMware to Azure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="11a43-104">Een replicatiebeleid maken</span><span class="sxs-lookup"><span data-stu-id="11a43-104">Create a replication policy</span></span>

1. <span data-ttu-id="11a43-105">Selecteer **Beheren** > **Infrastructuur voor Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="11a43-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="11a43-106">Selecteer **Replicatiebeleid** onder **Voor VMware en fysieke machines**.</span><span class="sxs-lookup"><span data-stu-id="11a43-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="11a43-107">Selecteer **+Replicatiebeleid**.</span><span class="sxs-lookup"><span data-stu-id="11a43-107">Select **+Replication policy**.</span></span>

    ![Replicatiebeleid maken](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="11a43-109">Voer de naam van het beleid in.</span><span class="sxs-lookup"><span data-stu-id="11a43-109">Enter the policy name.</span></span>

5. <span data-ttu-id="11a43-110">Geef de limiet voor de RPO op bij **RPO-drempelwaarde**.</span><span class="sxs-lookup"><span data-stu-id="11a43-110">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="11a43-111">Wanneer de continue replicatie deze limiet overschrijdt, worden er waarschuwingen gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="11a43-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="11a43-112">Geef in **Bewaarperiode van het herstelpunt** de duur (in uren) op dat elk herstelpunt moet worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="11a43-112">In **Recovery point retention**, specify (in hours) the duration of the retention window for each recovery point.</span></span> <span data-ttu-id="11a43-113">Beveiligde machines kunnen binnen een bepaald tijdsvenster te allen tijde worden hersteld naar een willekeurig punt.</span><span class="sxs-lookup"><span data-stu-id="11a43-113">Protected machines can be recovered to any point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="11a43-114">Een bewaarperiode van maximaal 24 uur wordt ondersteund voor computers die worden gerepliceerd naar Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="11a43-114">Up to 24 hours of retention is supported for machines replicated to premium storage.</span></span> <span data-ttu-id="11a43-115">Een bewaarperiode van maximaal 72 uur wordt ondersteund voor computers die worden gerepliceerd naar Standard Storage.</span><span class="sxs-lookup"><span data-stu-id="11a43-115">Up to 72 hours of retention is supported for machines replicated to standard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="11a43-116">Er wordt automatisch een replicatiebeleid voor failback gemaakt.</span><span class="sxs-lookup"><span data-stu-id="11a43-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="11a43-117">Geef in **Frequentie van de app-consistente momentopname** op hoe vaak (in minuten) er herstelpunten moeten worden gemaakt met toepassingsconsistente momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="11a43-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="11a43-118">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="11a43-118">Click **OK**.</span></span> <span data-ttu-id="11a43-119">Het beleid wordt binnen 30 seconden tot 60 minuut gemaakt.</span><span class="sxs-lookup"><span data-stu-id="11a43-119">The policy should be created in 30 to 60 seconds.</span></span>

![Replicatiebeleid genereren](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="11a43-121">Een configuratieserver koppelen aan het replicatiebeleid</span><span class="sxs-lookup"><span data-stu-id="11a43-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="11a43-122">Kies het replicatiebeleid waaraan u de configuratieserver wilt koppelen.</span><span class="sxs-lookup"><span data-stu-id="11a43-122">Choose the replication policy to which you want to associate the configuration server.</span></span>
2. <span data-ttu-id="11a43-123">Klik op **Koppelen**.</span><span class="sxs-lookup"><span data-stu-id="11a43-123">Click **Associate**.</span></span>
<span data-ttu-id="11a43-124">![Configuratieserver koppelen](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="11a43-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="11a43-125">Selecteer de configuratieserver in de lijst met servers.</span><span class="sxs-lookup"><span data-stu-id="11a43-125">Select the configuration server from the list of servers.</span></span>
4. <span data-ttu-id="11a43-126">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="11a43-126">Click **OK**.</span></span> <span data-ttu-id="11a43-127">De configuratieserver wordt binnen één tot twee minuten gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="11a43-127">The configuration server should be associated in one to two minutes.</span></span>

![Configuratieserver koppelen](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="11a43-129">Een replicatiebeleid bewerken</span><span class="sxs-lookup"><span data-stu-id="11a43-129">Edit a replication policy</span></span>
1. <span data-ttu-id="11a43-130">Kies het replicatiebeleid waarvan u de replicatie-instellingen wilt bewerken.</span><span class="sxs-lookup"><span data-stu-id="11a43-130">Choose the replication policy for which you want to edit replication settings.</span></span>
<span data-ttu-id="11a43-131">![Replicatiebeleid bewerken](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="11a43-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="11a43-132">Klik op **Instellingen bewerken**.</span><span class="sxs-lookup"><span data-stu-id="11a43-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="11a43-133">![Instellingen van replicatiebeleid bewerken](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="11a43-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="11a43-134">Wijzig de instellingen op basis van uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="11a43-134">Change the settings based on your need.</span></span>
4. <span data-ttu-id="11a43-135">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="11a43-135">Click **Save**.</span></span> <span data-ttu-id="11a43-136">Het beleid wordt binnen twee tot vijf minuten opgeslagen. Dit is afhankelijk van hoeveel virtuele machines gebruikmaken van dit replicatiebeleid.</span><span class="sxs-lookup"><span data-stu-id="11a43-136">The policy should be saved in two to five minutes, depending on how many VMs are using that replication policy.</span></span>

![Replicatiebeleid opslaan](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="11a43-138">Een configuratieserver loskoppelen van een replicatiebeleid</span><span class="sxs-lookup"><span data-stu-id="11a43-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="11a43-139">Kies het replicatiebeleid waaraan u de configuratieserver wilt koppelen.</span><span class="sxs-lookup"><span data-stu-id="11a43-139">Choose the replication policy to which you want to associate the configuration server.</span></span>
2. <span data-ttu-id="11a43-140">Klik op **Ontkoppelen**.</span><span class="sxs-lookup"><span data-stu-id="11a43-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="11a43-141">Selecteer de configuratieserver in de lijst met servers.</span><span class="sxs-lookup"><span data-stu-id="11a43-141">Select the configuration server from the list of servers.</span></span>
4. <span data-ttu-id="11a43-142">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="11a43-142">Click **OK**.</span></span> <span data-ttu-id="11a43-143">De configuratieserver wordt binnen één tot twee minuten ontkoppeld.</span><span class="sxs-lookup"><span data-stu-id="11a43-143">The configuration server should be dissociated in one to two minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="11a43-144">U kunt een configuratieserver niet ontkoppelen als het beleid door een of meer gerepliceerde items wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="11a43-144">You cannot dissociate a configuration server if there is at least one replicated item using the policy.</span></span> <span data-ttu-id="11a43-145">Voordat u de configuratieserver ontkoppelt, moet u ervoor zorgen dat het beleid niet door gerepliceerde items wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="11a43-145">Make sure there are no replicated items using the policy before you dissociate the configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="11a43-146">Een replicatiebeleid verwijderen</span><span class="sxs-lookup"><span data-stu-id="11a43-146">Delete a replication policy</span></span>

1. <span data-ttu-id="11a43-147">Kies het replicatiebeleid dat u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="11a43-147">Choose the replication policy that you want to delete.</span></span>
2. <span data-ttu-id="11a43-148">Klik op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="11a43-148">Click **Delete**.</span></span> <span data-ttu-id="11a43-149">Het beleid wordt binnen 30 seconden tot 60 minuut verwijderd.</span><span class="sxs-lookup"><span data-stu-id="11a43-149">The policy should be deleted in 30 to 60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="11a43-150">U kunt een replicatiebeleid niet verwijderen als er een of meer configuratieservers aan zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="11a43-150">You cannot delete a replication policy if it has at least one configuration server associated to it.</span></span> <span data-ttu-id="11a43-151">Zorg ervoor dat het beleid niet door gerepliceerde items wordt gebruikt en verwijder alle gekoppelde configuratieservers voordat u het beleid verwijdert.</span><span class="sxs-lookup"><span data-stu-id="11a43-151">Make sure there are no replicated items using the policy and delete all the associated configuration servers before you delete the policy.</span></span>
