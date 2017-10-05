---
title: Doel (VMware naar Azure) voorbereiden | Microsoft Docs
description: Dit artikel wordt beschreven hoe u uw Azure-omgeving om te virtuele VMware-machines repliceren naar Azure voorbereidt.
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: c84a775564769ddc796aa9d75add019ef1003175
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-target-vmware-to-azure"></a><span data-ttu-id="da2d1-103">Doel (VMware naar Azure) voorbereiden</span><span class="sxs-lookup"><span data-stu-id="da2d1-103">Prepare target (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="da2d1-104">VMware naar Azure</span><span class="sxs-lookup"><span data-stu-id="da2d1-104">VMware to Azure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="da2d1-105">Fysieke naar Azure</span><span class="sxs-lookup"><span data-stu-id="da2d1-105">Physical to Azure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="da2d1-106">Dit artikel wordt beschreven hoe u uw Azure-omgeving om te virtuele VMware-machines repliceren naar Azure voorbereidt.</span><span class="sxs-lookup"><span data-stu-id="da2d1-106">This article describes how to prepare your Azure environment to start replicating VMware virtual machines to Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da2d1-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="da2d1-107">Prerequisites</span></span>

<span data-ttu-id="da2d1-108">Het artikel wordt ervan uitgegaan:</span><span class="sxs-lookup"><span data-stu-id="da2d1-108">The article assumes the following:</span></span>
- <span data-ttu-id="da2d1-109">U kunt een Recovery Services-kluis ter bescherming van uw virtuele VMware-machines hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="da2d1-109">You have created a Recovery Services Vault to protect your VMware virtual machines.</span></span> <span data-ttu-id="da2d1-110">Kunt u een Recovery Services-kluis uit de [Azure-portal](http://portal.azure.com "Azure-portal").</span><span class="sxs-lookup"><span data-stu-id="da2d1-110">You can create a Recovery Services Vault from the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="da2d1-111">U hebt [instellen van uw on-premises omgeving](./site-recovery-set-up-vmware-to-azure.md) virtuele VMware-machines repliceren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="da2d1-111">You have [setup your on-premises environment](./site-recovery-set-up-vmware-to-azure.md) to replicate VMware virtual machines to Azure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="da2d1-112">Doel voorbereiden</span><span class="sxs-lookup"><span data-stu-id="da2d1-112">Prepare target</span></span>

<span data-ttu-id="da2d1-113">Na het voltooien van de **stap 1: Selecteer beveiligingsdoel** en **stap 2: bereid bron**, gaat u naar **stap 3: doel**</span><span class="sxs-lookup"><span data-stu-id="da2d1-113">After completing the **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken to **Step 3: Target**</span></span>

![Doel voorbereiden](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. <span data-ttu-id="da2d1-115">**Abonnement:** in de vervolgkeuzelijst, selecteer het abonnement dat u wilt repliceren van uw virtuele machines naar.</span><span class="sxs-lookup"><span data-stu-id="da2d1-115">**Subscription:** From the drop down menu, select the Subscription that you want to replicate your virtual machines to.</span></span>
2. <span data-ttu-id="da2d1-116">**Implementatiemodel:** selecteren van het implementatiemodel (klassiek of Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="da2d1-116">**Deployment Model:** Select the deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="da2d1-117">Op basis van het gekozen implementatiemodel, wordt een validatie uitgevoerd om ervoor te zorgen dat er ten minste één compatibel storage-account en het virtuele netwerk in het doelabonnement voor replicatie en failover uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="da2d1-117">Based on the chosen deployment model, a validation is run to ensure that you have at least one compatible storage account and virtual network in the target subscription to replicate and failover your virtual machine to.</span></span>

<span data-ttu-id="da2d1-118">Zodra de validaties wordt voltooid, klikt u op OK om door te gaan met de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="da2d1-118">Once the validations complete successfully, click OK to go to the next step.</span></span>

<span data-ttu-id="da2d1-119">Als u geen compatibel Resource Manager-opslagaccount of virtueel netwerk hebt of wilt meer toevoegen, kunt u doen door te klikken op de **+ Opslagaccount** of **+ netwerk** knoppen boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="da2d1-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like to add more, you can do so by clicking the **+ Storage Account** or **+ Network** buttons on the top of the blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da2d1-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="da2d1-120">Next steps</span></span>
<span data-ttu-id="da2d1-121">[Replicatie-instellingen configureren](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="da2d1-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
