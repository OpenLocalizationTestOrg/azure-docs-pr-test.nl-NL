---
title: aaaAdd Azure Automation-runbooks toorecovery plannen in de Azure Site Recovery | Microsoft Docs
description: Meer informatie over hoe Azure Site Recovery kunt herstelplannen met behulp van Azure Automation uitbreiden. Meer informatie over hoe toocomplete complexe taken tijdens herstel tooAzure.
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a><span data-ttu-id="5b6b6-104">Toevoegen van Azure Automation-runbooks toorecovery plannen</span><span class="sxs-lookup"><span data-stu-id="5b6b6-104">Add Azure Automation runbooks toorecovery plans</span></span>
<span data-ttu-id="5b6b6-105">In dit artikel wordt beschreven hoe Azure Site Recovery kan worden geïntegreerd met Azure Automation toohelp uitbreiden van uw plannen voor herstel.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation toohelp you extend your recovery plans.</span></span> <span data-ttu-id="5b6b6-106">Plannen voor herstel kunnen herstel van virtuele machines die zijn beveiligd met Site Recovery indelen.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="5b6b6-107">Plannen voor herstel werkt zowel voor replicatie tooa secundaire cloud, en voor replicatie tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-107">Recovery plans work both for replication tooa secondary cloud, and for replication tooAzure.</span></span> <span data-ttu-id="5b6b6-108">Herstelplannen ook zorgt u ervoor dat Hallo herstel **accuraat**, **herhaalbare**, en **geautomatiseerde**.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-108">Recovery plans also help make hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="5b6b6-109">Als u uw virtuele machines tooAzure failover, uitgebreid integratie met Azure Automation uw plannen voor herstel.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-109">If you fail over your VMs tooAzure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="5b6b6-110">U kunt deze gebruiken tooexecute runbooks die krachtige automatiseringstaken bieden.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-110">You can use it tooexecute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="5b6b6-111">Als u nieuwe tooAzure Automation bent, kunt u [aanmelden](https://azure.microsoft.com/services/automation/) en [voorbeeldscripts downloaden](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="5b6b6-111">If you are new tooAzure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="5b6b6-112">Voor meer informatie en toolearn hoe tooorchestrate herstel tooAzure met behulp van [herstelplannen](https://azure.microsoft.com/blog/?p=166264), Zie [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="5b6b6-112">For more information, and toolearn how tooorchestrate recovery tooAzure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="5b6b6-113">In dit artikel wordt beschreven hoe u Azure Automation-runbooks kunt integreren in uw plannen voor herstel.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="5b6b6-114">We gebruiken voorbeelden tooautomate basistaken die voorheen handmatige interventie nodig.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-114">We use examples tooautomate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="5b6b6-115">We beschrijven ook hoe tooconvert een herstel van meerdere stappen tooa één-op-herstelbewerking.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-115">We also describe how tooconvert a multi-step recovery tooa single-click recovery action.</span></span>

## <a name="customize-hello-recovery-plan"></a><span data-ttu-id="5b6b6-116">Hallo herstelplan aanpassen</span><span class="sxs-lookup"><span data-stu-id="5b6b6-116">Customize hello recovery plan</span></span>
1. <span data-ttu-id="5b6b6-117">Ga toohello **siteherstel** recovery plan resource-blade.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-117">Go toohello **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="5b6b6-118">In dit voorbeeld heeft Hallo herstelplan twee virtuele machines toegevoegd tooit, voor herstel.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-118">For this example, hello recovery plan has two VMs added tooit, for recovery.</span></span> <span data-ttu-id="5b6b6-119">toobegin toevoegen van een runbook, klikt u op Hallo **aanpassen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-119">toobegin adding a runbook, click hello **Customize** tab.</span></span>

    ![Klik op de knop aanpassen Hallo](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="5b6b6-121">Met de rechtermuisknop op **groep 1: Start**, en selecteer vervolgens **post actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![Klik met de rechtermuisknop groep 1: Start en post actie toevoegen](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="5b6b6-123">Klik op **kiest u een script**.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="5b6b6-124">Op Hallo **bijwerken actie** blade, naam Hallo script **Hallo wereld**.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-124">On hello **Update action** blade, name hello script **Hello World**.</span></span>

    ![Hallo Update actie blade](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="5b6b6-126">Voer de naam van een Automation-account.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="5b6b6-127">Hallo Automation-account kan zich in een Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-127">hello Automation account can be in any Azure region.</span></span> <span data-ttu-id="5b6b6-128">Hallo Automation-account moet zich in Hallo hetzelfde abonnement als hello Azure Site Recovery-kluis.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-128">hello Automation account must be in hello same subscription as hello Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="5b6b6-129">Selecteer een runbook in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="5b6b6-130">Dit runbook is Hallo-script dat wordt uitgevoerd tijdens de uitvoering van de Hallo van het herstelplan hello, na het herstel van de eerste groep Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-130">This runbook is hello script that runs during hello execution of hello recovery plan, after hello recovery of hello first group.</span></span>

7. <span data-ttu-id="5b6b6-131">toosave hello script, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-131">toosave hello script, click **OK**.</span></span> <span data-ttu-id="5b6b6-132">Hallo-script wordt toegevoegd, te**groep 1: na stappen**.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-132">hello script is added too**Group 1: Post-steps**.</span></span>

    ![Groep na acties 1:Start](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="5b6b6-134">Overwegingen voor het toevoegen van een script</span><span class="sxs-lookup"><span data-stu-id="5b6b6-134">Considerations for adding a script</span></span>

* <span data-ttu-id="5b6b6-135">Voor opties te**verwijderen van een stap** of **Hallo updatescript**, met de rechtermuisknop op het Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-135">For options too**delete a step** or **update hello script**, right-click hello script.</span></span>
* <span data-ttu-id="5b6b6-136">Een script kunt uitvoeren in Azure tijdens de failover vanuit een lokale machine tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-136">A script can run on Azure during failover from an on-premises machine tooAzure.</span></span> <span data-ttu-id="5b6b6-137">Deze kunt ook uitvoeren op Azure als een primaire site script voordat wordt afgesloten, tijdens de failback vanuit Azure tooan lokale machine.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure tooan on-premises machine.</span></span>
* <span data-ttu-id="5b6b6-138">Wanneer een script wordt uitgevoerd, injects deze de context van een herstel plan.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="5b6b6-139">Hallo volgende voorbeeld ziet u een variabele context:</span><span class="sxs-lookup"><span data-stu-id="5b6b6-139">hello following example shows a context variable:</span></span>

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    <span data-ttu-id="5b6b6-140">Hallo volgende tabel geeft een lijst Hallo naam en beschrijving van iedere variabele in het Hallo-context.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-140">hello following table lists hello name and description of each variable in hello context.</span></span>

    | <span data-ttu-id="5b6b6-141">**Naam variabele**</span><span class="sxs-lookup"><span data-stu-id="5b6b6-141">**Variable name**</span></span> | <span data-ttu-id="5b6b6-142">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="5b6b6-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="5b6b6-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="5b6b6-143">RecoveryPlanName</span></span> |<span data-ttu-id="5b6b6-144">Hallo-naam van Hallo-planning wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-144">hello name of hello plan being run.</span></span> <span data-ttu-id="5b6b6-145">Deze variabele kunt u verschillende acties op basis van naam Hallo herstel uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-145">This variable helps you take different actions based on hello recovery plan name.</span></span> <span data-ttu-id="5b6b6-146">U kunt ook Hallo script hergebruiken.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-146">You also can reuse hello script.</span></span> |
    | <span data-ttu-id="5b6b6-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="5b6b6-147">FailoverType</span></span> |<span data-ttu-id="5b6b6-148">Hiermee geeft u op of Hallo failover een test is, gepland of ongepland.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-148">Specifies whether hello failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="5b6b6-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="5b6b6-149">FailoverDirection</span></span> |<span data-ttu-id="5b6b6-150">Geeft aan of herstel tooa primaire of secundaire site.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-150">Specifies whether recovery is tooa primary or secondary site.</span></span> |
    | <span data-ttu-id="5b6b6-151">Groeps-id</span><span class="sxs-lookup"><span data-stu-id="5b6b6-151">GroupID</span></span> |<span data-ttu-id="5b6b6-152">Identificeert in het herstelplan Hallo Hallo groepsnummer wanneer Hallo plan wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-152">Identifies hello group number in hello recovery plan when hello plan is running.</span></span> |
    | <span data-ttu-id="5b6b6-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="5b6b6-153">VmMap</span></span> |<span data-ttu-id="5b6b6-154">Een matrix met alle VM's in het Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-154">An array of all VMs in hello group.</span></span> |
    | <span data-ttu-id="5b6b6-155">VMMap sleutel</span><span class="sxs-lookup"><span data-stu-id="5b6b6-155">VMMap key</span></span> |<span data-ttu-id="5b6b6-156">Een unieke sleutel (GUID) voor elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="5b6b6-157">De Hallo zelfde als ID van Azure Virtual Machine Manager (VMM) Hallo Hallo VM, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-157">It's hello same as hello Azure Virtual Machine Manager (VMM) ID of hello VM, where applicable.</span></span> |
    | <span data-ttu-id="5b6b6-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="5b6b6-158">SubscriptionId</span></span> |<span data-ttu-id="5b6b6-159">Hello Azure-abonnement-ID in welke Hallo VM is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-159">hello Azure subscription ID in which hello VM was created.</span></span> |
    | <span data-ttu-id="5b6b6-160">Rolnaam</span><span class="sxs-lookup"><span data-stu-id="5b6b6-160">RoleName</span></span> |<span data-ttu-id="5b6b6-161">Hallo-naam van hello Azure virtuele machine die wordt hersteld.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-161">hello name of hello Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="5b6b6-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="5b6b6-162">CloudServiceName</span></span> |<span data-ttu-id="5b6b6-163">Hello Azure cloud servicenaam waaronder Hallo VM is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-163">hello Azure cloud service name under which hello VM was created.</span></span> |
    | <span data-ttu-id="5b6b6-164">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="5b6b6-164">ResourceGroupName</span></span>|<span data-ttu-id="5b6b6-165">Hello Azure Resourcegroepnaam waaronder Hallo VM is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-165">hello Azure resource group name under which hello VM was created.</span></span> |
    | <span data-ttu-id="5b6b6-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="5b6b6-166">RecoveryPointId</span></span>|<span data-ttu-id="5b6b6-167">Hallo tijdstempel voor wanneer Hallo VM is hersteld.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-167">hello timestamp for when hello VM is recovered.</span></span> |

* <span data-ttu-id="5b6b6-168">Zorg ervoor dat Hallo Automation-account heeft Hallo modules te volgen:</span><span class="sxs-lookup"><span data-stu-id="5b6b6-168">Ensure that hello Automation account has hello following modules:</span></span>
    * <span data-ttu-id="5b6b6-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="5b6b6-169">AzureRM.profile</span></span>
    * <span data-ttu-id="5b6b6-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="5b6b6-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="5b6b6-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="5b6b6-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="5b6b6-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="5b6b6-172">AzureRM.Network</span></span>
    * <span data-ttu-id="5b6b6-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="5b6b6-173">AzureRM.Compute</span></span>

<span data-ttu-id="5b6b6-174">Alle modules moeten van compatibele versies.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="5b6b6-175">Een eenvoudige manier tooensure alle modules zijn compatibel is toouse Hallo nieuwste versies van alle Hallo-modules.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-175">An easy way tooensure that all modules are compatible is toouse hello latest versions of all hello modules.</span></span>

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a><span data-ttu-id="5b6b6-176">Toegang tot alle virtuele machines van Hallo VMMap in een lus</span><span class="sxs-lookup"><span data-stu-id="5b6b6-176">Access all VMs of hello VMMap in a loop</span></span>
<span data-ttu-id="5b6b6-177">Hallo code tooloop volgen over alle VM's van Microsoft VMMap hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5b6b6-177">Use hello following code tooloop across all VMs of hello Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="5b6b6-178">Hallo resource groep en de rol naamwaarden zijn leeg als Hallo-script een groep van de opstartinstallatiekopie tooa vooraf in te grijpen is.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-178">hello resource group name and role name values are empty when hello script is a pre-action tooa boot group.</span></span> <span data-ttu-id="5b6b6-179">Hallo-waarden worden ingevuld alleen als Hallo VM van die groep tijdens failover slaagt.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-179">hello values are populated only if hello VM of that group succeeds in failover.</span></span> <span data-ttu-id="5b6b6-180">Hallo-script is een na actie van Hallo opstarten groep.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-180">hello script is a post-action of hello boot group.</span></span>

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="5b6b6-181">Gebruik dezelfde Hallo Automation-runbook in meerdere herstelplannen</span><span class="sxs-lookup"><span data-stu-id="5b6b6-181">Use hello same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="5b6b6-182">U kunt één script gebruiken in meerdere herstelplannen met behulp van externe variabelen.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="5b6b6-183">U kunt [Azure Automation-variabelen](../automation/automation-variables.md) toostore parameters die u voor een herstel doorgeven kunt uitvoeren plannen.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-183">You can use [Azure Automation variables](../automation/automation-variables.md) toostore parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="5b6b6-184">U kunt afzonderlijke variabelen voor elke herstelplan maken door Hallo herstelnaam als een voorvoegsel toohello variabele toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-184">By adding hello recovery plan name as a prefix toohello variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="5b6b6-185">Gebruik vervolgens Hallo variabelen als parameters.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-185">Then, use hello variables as parameters.</span></span> <span data-ttu-id="5b6b6-186">U kunt een parameter wijzigen zonder het Hallo-script wijzigen, maar wijziging Hallo Hallo nog steeds manier werkt.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-186">You can change a parameter without changing hello script, but still change hello way hello script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="5b6b6-187">Een eenvoudige string-variabele in een runbookscript gebruiken</span><span class="sxs-lookup"><span data-stu-id="5b6b6-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="5b6b6-188">In dit voorbeeld wordt een script Hallo invoer van een Netwerkbeveiligingsgroep (NSG) en toegepast toohello VM's van een herstelplan.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-188">In this example, a script takes hello input of a Network Security Group (NSG) and applies it toohello VMs of a recovery plan.</span></span>

<span data-ttu-id="5b6b6-189">Gebruik voor Hallo script toodetect welk herstelplan wordt uitgevoerd, Hallo recovery plan context:</span><span class="sxs-lookup"><span data-stu-id="5b6b6-189">For hello script toodetect which recovery plan is running, use hello recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="5b6b6-190">een bestaande NSG tooapply, u moet weten Hallo NSG naam en het Hallo NSG Resourcegroepnaam.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-190">tooapply an existing NSG, you must know hello NSG name and hello NSG resource group name.</span></span> <span data-ttu-id="5b6b6-191">Deze variabelen gebruiken als invoer voor herstel plan scripts.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="5b6b6-192">toodo deze twee variabelen in Hallo activa van Automation-account maken.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-192">toodo this, create two variables in hello Automation account assets.</span></span> <span data-ttu-id="5b6b6-193">Hallo-naam van het herstelplan Hallo die u Hallo parameters voor als voorvoegsel toohello variabelenaam maakt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-193">Add hello name of hello recovery plan that you are creating hello parameters for as a prefix toohello variable name.</span></span>

1. <span data-ttu-id="5b6b6-194">Maak een variabele toostore hello NSG-naam.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-194">Create a variable toostore hello NSG name.</span></span> <span data-ttu-id="5b6b6-195">Voorvoegsel toohello naam van een variabele toevoegen met behulp van de naam van het herstelplan Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-195">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Maak een NSG naamvariabele](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="5b6b6-197">Naam van een variabele toostore hello NSG een resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-197">Create a variable toostore hello NSG's resource group name.</span></span> <span data-ttu-id="5b6b6-198">Voorvoegsel toohello naam van een variabele toevoegen met behulp van de naam van het herstelplan Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-198">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![De groepsnaam van een NSG-resource maken](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="5b6b6-200">In Hallo-script gebruiken Hallo verwijzing code tooget Hallo waarden van variabelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5b6b6-200">In hello script, use hello following reference code tooget hello variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="5b6b6-201">Gebruik Hallo variabelen in Hallo runbook tooapply hello NSG toohello netwerkinterface Hallo failover VM:</span><span class="sxs-lookup"><span data-stu-id="5b6b6-201">Use hello variables in hello runbook tooapply hello NSG toohello network interface of hello failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="5b6b6-202">Voor elke herstelplan onafhankelijke variabelen te maken zodat u Hallo script opnieuw kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-202">For each recovery plan, create independent variables so that you can reuse hello script.</span></span> <span data-ttu-id="5b6b6-203">Een voorvoegsel toevoegen met behulp van naam Hallo recovery-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-203">Add a prefix by using hello recovery plan name.</span></span> <span data-ttu-id="5b6b6-204">Zie voor een script is voltooid, end-to-end voor dit scenario, [toevoegen van een openbare IP-adres en het NSG tooVMs tijdens de testfailover van een herstelplan Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span><span class="sxs-lookup"><span data-stu-id="5b6b6-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG tooVMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-toostore-more-information"></a><span data-ttu-id="5b6b6-205">Gebruik een complex variabele toostore meer informatie</span><span class="sxs-lookup"><span data-stu-id="5b6b6-205">Use a complex variable toostore more information</span></span>

<span data-ttu-id="5b6b6-206">Overweeg een scenario waarin u wilt dat een tooturn één script op een openbaar IP-adres op specifieke virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-206">Consider a scenario in which you want a single script tooturn on a public IP on specific VMs.</span></span> <span data-ttu-id="5b6b6-207">In een ander scenario kunt u tooapply verschillende nsg's op verschillende virtuele machines (niet op alle VM's).</span><span class="sxs-lookup"><span data-stu-id="5b6b6-207">In another scenario, you might want tooapply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="5b6b6-208">U kunt een script dat opnieuw kan worden gebruikt voor een herstelplan maken.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="5b6b6-209">Elke herstelplan kan een variabele aantal VM's hebben.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="5b6b6-210">Een SharePoint-herstelbewerking heeft bijvoorbeeld twee front-ends.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="5b6b6-211">Een basic line-of-business (LOB)-toepassing heeft slechts één front-end.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="5b6b6-212">U kunt afzonderlijke variabelen voor elke herstelplan kan niet maken.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="5b6b6-213">In Hallo voorbeeld te volgen, wordt een nieuwe techniek gebruiken en maak een [complex variabele](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in hello Azure Automation-account activa.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-213">In hello following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in hello Azure Automation account assets.</span></span> <span data-ttu-id="5b6b6-214">U doet dit door geven meerdere waarden.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="5b6b6-215">U moet Azure PowerShell toocomplete Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5b6b6-215">You must use Azure PowerShell toocomplete hello following steps:</span></span>

1. <span data-ttu-id="5b6b6-216">Aanmelden tooyour Azure-abonnement in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5b6b6-216">In PowerShell, sign in tooyour Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="5b6b6-217">Hallo complex variabele maken toostore Hallo-parameters, met behulp van de naam van het herstelplan Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="5b6b6-217">toostore hello parameters, create hello complex variable by using hello name of hello recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="5b6b6-218">In deze variabele complex **VMDetails** Hallo VM-ID is voor de Hallo beveiligd VM.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-218">In this complex variable, **VMDetails** is hello VM ID for hello protected VM.</span></span> <span data-ttu-id="5b6b6-219">tooget hello VM-ID in de Azure-portal Hallo Hallo VM-eigenschappen weergeven.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-219">tooget hello VM ID, in hello Azure portal, view hello VM properties.</span></span> <span data-ttu-id="5b6b6-220">Hallo volgende schermafbeelding ziet u een variabele die in details op Hallo van twee virtuele machines worden opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="5b6b6-220">hello following screenshot shows a variable that stores hello details of two VMs:</span></span>

    ![Hallo VM-ID gebruiken zoals Hallo GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="5b6b6-222">Gebruik deze variabele in uw runbook.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-222">Use this variable in your runbook.</span></span> <span data-ttu-id="5b6b6-223">Als Hallo dat VM GUID is gevonden in de context van Hallo recovery plan aangegeven, van toepassing hello NSG op Hallo VM:</span><span class="sxs-lookup"><span data-stu-id="5b6b6-223">If hello indicated VM GUID is found in hello recovery plan context, apply hello NSG on hello VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="5b6b6-224">Doorlopen Hallo VM's van Hallo recovery plan context in uw runbook.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-224">In your runbook, loop through hello VMs of hello recovery plan context.</span></span> <span data-ttu-id="5b6b6-225">Controleer of Hallo VM bestaat in **$VMDetailsObj**.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-225">Check whether hello VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="5b6b6-226">Als dit bestaat, toegang tot de eigenschappen Hallo Hallo variabele tooapply Hallo NSG:</span><span class="sxs-lookup"><span data-stu-id="5b6b6-226">If it exists, access hello properties of hello variable tooapply hello NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

<span data-ttu-id="5b6b6-227">U kunt Hallo dezelfde script gebruiken voor andere herstelplannen.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-227">You can use hello same script for different recovery plans.</span></span> <span data-ttu-id="5b6b6-228">Geef andere parameters door op te slaan Hallo-waarde die overeenkomt met het herstelplan tooa in verschillende variabelen.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-228">Enter different parameters by storing hello value that corresponds tooa recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="5b6b6-229">Voorbeeldscripts</span><span class="sxs-lookup"><span data-stu-id="5b6b6-229">Sample scripts</span></span>

<span data-ttu-id="5b6b6-230">toodeploy voorbeeld scripts tooyour Automation-account, klikt u op Hallo **tooAzure implementeren** knop.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-230">toodeploy sample scripts tooyour Automation account, click hello **Deploy tooAzure** button.</span></span>

<span data-ttu-id="5b6b6-231">[![TooAzure implementeren](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="5b6b6-231">[![Deploy tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="5b6b6-232">Zie voor een ander voorbeeld Hallo video te volgen.</span><span class="sxs-lookup"><span data-stu-id="5b6b6-232">For another example, see hello following video.</span></span> <span data-ttu-id="5b6b6-233">Dit laat zien hoe toorecover een tooAzure met twee lagen WordPress toepassing:</span><span class="sxs-lookup"><span data-stu-id="5b6b6-233">It demonstrates how toorecover a two-tier WordPress application tooAzure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="5b6b6-234">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="5b6b6-234">Additional resources</span></span>
* [<span data-ttu-id="5b6b6-235">Azure Automation-service uitvoeren als-account</span><span class="sxs-lookup"><span data-stu-id="5b6b6-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="5b6b6-236">Overzicht van Azure Automation</span><span class="sxs-lookup"><span data-stu-id="5b6b6-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure Automation-overzicht")
* [<span data-ttu-id="5b6b6-237">Azure Automation-voorbeeldscripts</span><span class="sxs-lookup"><span data-stu-id="5b6b6-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure Automation-voorbeeldscripts")
