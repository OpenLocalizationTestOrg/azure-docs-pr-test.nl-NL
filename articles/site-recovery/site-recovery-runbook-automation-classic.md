---
title: aaaAdd Azure automation-runbooks toorecovery plannen in de klassieke portal Hallo | Microsoft Docs
description: Dit artikel wordt beschreven hoe Azure Site Recovery kunt u nu tooextend herstelplannen met behulp van Azure Automation toocomplete complexe taken tijdens herstel tooAzure
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a><span data-ttu-id="46e79-103">Azure automation-runbooks toorecovery plannen in de klassieke portal Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="46e79-103">Add Azure automation runbooks toorecovery plans in hello classic portal</span></span>
<span data-ttu-id="46e79-104">Deze zelfstudie wordt beschreven hoe Azure Site Recovery kan worden geïntegreerd met Azure Automation tooprovide uitbreidbaarheid toorecovery plannen.</span><span class="sxs-lookup"><span data-stu-id="46e79-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation tooprovide extensibility toorecovery plans.</span></span> <span data-ttu-id="46e79-105">Plannen voor herstel kunnen herstel van uw virtuele machines die zijn beveiligd met Azure Site Recovery voor replicatie toosecondary cloud- en replicatie tooAzure scenario's te organiseren.</span><span class="sxs-lookup"><span data-stu-id="46e79-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication toosecondary cloud and replication tooAzure scenarios.</span></span> <span data-ttu-id="46e79-106">Ze ook helpen bij het maken van Hallo herstel **accuraat**, **herhaalbare**, en **geautomatiseerde**.</span><span class="sxs-lookup"><span data-stu-id="46e79-106">They also help in making hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="46e79-107">Als u via uw virtuele machines tooAzure mislukken, worden de integratie met Azure Automation breidt de herstelplannen en biedt u de mogelijkheid tooexecute runbooks, zodat krachtige automatiseringstaken.</span><span class="sxs-lookup"><span data-stu-id="46e79-107">If you are failing over your virtual machines tooAzure, integration with Azure Automation extends the recovery plans and gives you capability tooexecute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="46e79-108">Als u niet gehoord over Azure Automation nog, meldt u [hier](https://azure.microsoft.com/services/automation/) en hun voorbeeldscripts downloaden [hier](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="46e79-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="46e79-109">Lees meer over [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) en hoe tooorchestrate herstel tooAzure met recovery plan [hier](https://azure.microsoft.com/blog/?p=166264).</span><span class="sxs-lookup"><span data-stu-id="46e79-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how tooorchestrate recovery tooAzure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="46e79-110">In deze korte zelfstudie kijken we hoe u Azure Automation-runbooks in herstelplannen integreren kunt.</span><span class="sxs-lookup"><span data-stu-id="46e79-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="46e79-111">We eenvoudige taken die eerder handmatige interventie vereist automatiseren en Zie hoe een multi-tooconvert herstel stap in een herstelactie met één klik.</span><span class="sxs-lookup"><span data-stu-id="46e79-111">We will automate simple tasks that earlier required manual intervention and see how tooconvert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="46e79-112">Ook kijken we hoe u een eenvoudig script oplossen kunt, als deze fout gaat.</span><span class="sxs-lookup"><span data-stu-id="46e79-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-hello-application-tooazure"></a><span data-ttu-id="46e79-113">Hallo toepassing tooAzure beveiligen</span><span class="sxs-lookup"><span data-stu-id="46e79-113">Protect hello application tooAzure</span></span>
<span data-ttu-id="46e79-114">Laten we beginnen met een eenvoudige toepassing die bestaat uit twee virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="46e79-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="46e79-115">Hier, hebben we een HRweb-toepassing van Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="46e79-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="46e79-116">Fabrikam-HRweb-front-end- en Fabrikam-Hrweb-back-end zijn Hallo twee virtuele machines beveiligd tooAzure met Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="46e79-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are hello two virtual machines protected tooAzure using Azure Site Recovery.</span></span> <span data-ttu-id="46e79-117">tooprotect hello virtuele machines met Azure Site Recovery stappen Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="46e79-117">tooprotect hello virtual machines using Azure Site Recovery, follow hello steps below.</span></span>

1. <span data-ttu-id="46e79-118">Schakel de beveiliging voor uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="46e79-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="46e79-119">Zorg ervoor dat Hallo virtuele machines eerste replicatie is voltooid en repliceert.</span><span class="sxs-lookup"><span data-stu-id="46e79-119">Ensure that hello virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="46e79-120">Wacht tot Hallo initiële replicatie is voltooid en Hallo replicatiestatus beveiligd zegt.</span><span class="sxs-lookup"><span data-stu-id="46e79-120">Wait till hello initial replication completes and hello Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="46e79-121">We gaan een herstelplan voor Hallo Fabrikam HRweb toepassing toofailover Hallo toepassing tooAzure maken in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="46e79-121">In this tutorial, we will create a recovery plan for hello Fabrikam HRweb application toofailover hello application tooAzure.</span></span> <span data-ttu-id="46e79-122">We gaan deze vervolgens integreren met een runbook dat een eindpunt op Hallo failover van virtuele machine van Azure tooserve webpagina's op poort 80, wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="46e79-122">Then we will integrate it with a runbook that will create an endpoint on hello failed over Azure virtual machine tooserve web pages at port 80.</span></span>

<span data-ttu-id="46e79-123">Eerst gaan we een herstelplan voor onze toepassing maken.</span><span class="sxs-lookup"><span data-stu-id="46e79-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-hello-recovery-plan"></a><span data-ttu-id="46e79-124">Hallo herstelplan maken</span><span class="sxs-lookup"><span data-stu-id="46e79-124">Create hello recovery plan</span></span>
<span data-ttu-id="46e79-125">toorecover hello toepassing tooAzure, moet u een herstelplan toocreate.</span><span class="sxs-lookup"><span data-stu-id="46e79-125">toorecover hello application tooAzure, you need toocreate a recovery plan.</span></span>
<span data-ttu-id="46e79-126">Met behulp van een herstelplan dat kunt u de volgorde Hallo van herstel van de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="46e79-126">Using a recovery plan you can specify hello order of recovery of the virtual machines.</span></span> <span data-ttu-id="46e79-127">Hallo virtuele machine in de groep 1 geplaatst worden herstellen eerst worden gestart en vervolgens Hallo virtuele machine in de groep 2 opvolgt.</span><span class="sxs-lookup"><span data-stu-id="46e79-127">hello virtual machine placed in group 1 will recover and start first, and then hello virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="46e79-128">Maak een herstelplan dat op hieronder lijkt.</span><span class="sxs-lookup"><span data-stu-id="46e79-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="46e79-129">meer informatie over plannen voor herstel, documentatie te lezen tooread [hier](https://msdn.microsoft.com/library/azure/dn788799.aspx "hier").</span><span class="sxs-lookup"><span data-stu-id="46e79-129">tooread more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="46e79-130">Vervolgens maken we Hallo nodig artefacten in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="46e79-130">Next, let's create hello necessary artifacts in Azure Automation.</span></span>

## <a name="create-hello-automation-account-and-its-assets"></a><span data-ttu-id="46e79-131">Hallo automation-account en bijbehorende assets maken</span><span class="sxs-lookup"><span data-stu-id="46e79-131">Create hello automation account and its assets</span></span>
<span data-ttu-id="46e79-132">U moet een Azure Automation-account toocreate-runbooks.</span><span class="sxs-lookup"><span data-stu-id="46e79-132">You need an Azure Automation account toocreate runbooks.</span></span> <span data-ttu-id="46e79-133">Als u nog geen account, gaat u tooAzure Automation tabblad aangegeven met ![](media/site-recovery-runbook-automation/02.png)en maak een nieuwe account.</span><span class="sxs-lookup"><span data-stu-id="46e79-133">If you do not already have an account, navigate tooAzure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="46e79-134">Hallo-account een naam tooidentify met geven.</span><span class="sxs-lookup"><span data-stu-id="46e79-134">Give hello account a name tooidentify with.</span></span>
2. <span data-ttu-id="46e79-135">Geef een geografische regio waar u tooplace Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="46e79-135">Specify a geographical region where you want tooplace hello account.</span></span>

<span data-ttu-id="46e79-136">Het verdient aanbeveling tooplace Hallo-account in Hallo dezelfde regio bevinden als Hallo ASR kluis.</span><span class="sxs-lookup"><span data-stu-id="46e79-136">It is recommended tooplace hello account in hello same region as hello ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="46e79-137">Maak vervolgens Hallo activa in Hallo Account te volgen.</span><span class="sxs-lookup"><span data-stu-id="46e79-137">Next, create hello following assets in hello Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="46e79-138">De naam van een abonnement toevoegen als asset</span><span class="sxs-lookup"><span data-stu-id="46e79-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="46e79-139">Voeg een nieuwe instelling ![](media/site-recovery-runbook-automation/04.png) Hallo in Azure Automation activa en te selecteren![](media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="46e79-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select too![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="46e79-140">Selecteer Hallo variabeletype als **tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="46e79-140">Select hello variable type as **String**</span></span>
3. <span data-ttu-id="46e79-141">Geef een naam op als **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="46e79-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="46e79-142">Geef de werkelijke naam van uw Azure-abonnement als Hallo variabelewaarde.</span><span class="sxs-lookup"><span data-stu-id="46e79-142">Specify your actual Azure Subscription name as hello variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="46e79-143">Hallo-naam van uw abonnement op de instellingenpagina Hallo van uw account op Hallo Azure-portal, kunt u identificeren.</span><span class="sxs-lookup"><span data-stu-id="46e79-143">You can identify hello name of your subscription from hello settings page of your account on hello Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="46e79-144">Toevoegen van een referentie voor de Azure-aanmelding als asset</span><span class="sxs-lookup"><span data-stu-id="46e79-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="46e79-145">Azure Automation maakt gebruik van Azure PowerShell tooconnect toothe abonnement en werkt met er Hallo-artefacten.</span><span class="sxs-lookup"><span data-stu-id="46e79-145">Azure Automation uses Azure PowerShell tooconnect toothe subscription and operates on hello artifacts there.</span></span> <span data-ttu-id="46e79-146">Hiervoor moet u verifiëren met behulp van uw Microsoft-account of een werk- of schoolaccount.</span><span class="sxs-lookup"><span data-stu-id="46e79-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="46e79-147">U kunt Hallo accountreferenties opslaan in een asset toobe veilig door Hallo runbook gebruikt.</span><span class="sxs-lookup"><span data-stu-id="46e79-147">You can store hello account credentials in an asset toobe used securely by hello runbook.</span></span>

1. <span data-ttu-id="46e79-148">Voeg een nieuwe instelling ![](media/site-recovery-runbook-automation/04.png) hello Azure Automation activa in en selecteer![](media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="46e79-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="46e79-149">Selecteer Hallo referentietype als **Windows PowerShell-referentie**</span><span class="sxs-lookup"><span data-stu-id="46e79-149">Select hello Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="46e79-150">Geef de naam Hallo als **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="46e79-150">Specify hello name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="46e79-151">Hallo-gebruikersnaam en wachtwoord toosign in met opgeven.</span><span class="sxs-lookup"><span data-stu-id="46e79-151">Specify hello username and password toosign-in with.</span></span>

<span data-ttu-id="46e79-152">Beide deze instellingen zijn nu beschikbaar in uw assets.</span><span class="sxs-lookup"><span data-stu-id="46e79-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="46e79-153">Meer informatie over hoe tooconnect tooyour abonnement via PowerShell krijgt [hier](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="46e79-153">More information about how tooconnect tooyour subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="46e79-154">Vervolgens maakt u een runbook in Azure Automation die een eindpunt voor Hallo front-virtuele machine na een failover kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="46e79-154">Next, you will create a runbook in Azure Automation that can add an endpoint for hello front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="46e79-155">Azure automation-context</span><span class="sxs-lookup"><span data-stu-id="46e79-155">Azure automation context</span></span>
<span data-ttu-id="46e79-156">ASR geeft een context variabele toohello runbook toohelp u deterministische scripts schrijven.</span><span class="sxs-lookup"><span data-stu-id="46e79-156">ASR passes a context variable toohello runbook toohelp you write deterministic scripts.</span></span> <span data-ttu-id="46e79-157">Een kan stellen Hallo namen van Hallo Cloudservice en Hallo virtuele Machine zijn voorspelbaar, maar er gebeurt dat is het niet altijd Hallo geval ten gevolge van toocertain scenario's zoals Hallo een waar Hallo-naam van de naam van de virtuele machine Hallo mogelijk gewijzigd vanwege toounsupported tekens in Azure.</span><span class="sxs-lookup"><span data-stu-id="46e79-157">One could argue that hello names of hello Cloud Service and hello Virtual Machine are predictable, but happens that it is not always hello case owing toocertain scenarios such as hello one where hello name of hello virtual machine name might have changed due toounsupported characters in Azure.</span></span> <span data-ttu-id="46e79-158">Deze informatie is daarom toohello ASR herstelplan doorgegeven als onderdeel van Hallo *context*.</span><span class="sxs-lookup"><span data-stu-id="46e79-158">Hence this information is passed toohello ASR recovery plan as part of hello *context*.</span></span>

<span data-ttu-id="46e79-159">Hieronder volgt een voorbeeld van hoe Hallo context variabele eruitziet.</span><span class="sxs-lookup"><span data-stu-id="46e79-159">Below is an example of how hello context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="46e79-160">Hallo in de volgende tabel bevat de naam en beschrijving voor iedere variabele in het Hallo-context.</span><span class="sxs-lookup"><span data-stu-id="46e79-160">hello table below contains name and description for each variable in hello context.</span></span>

| <span data-ttu-id="46e79-161">**Naam variabele**</span><span class="sxs-lookup"><span data-stu-id="46e79-161">**Variable name**</span></span> | <span data-ttu-id="46e79-162">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="46e79-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="46e79-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="46e79-163">RecoveryPlanName</span></span> |<span data-ttu-id="46e79-164">Naam van de planning wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="46e79-164">Name of plan being run.</span></span> <span data-ttu-id="46e79-165">Helpt u maatregelen nemen op basis van de naam met behulp van dezelfde Hallo script</span><span class="sxs-lookup"><span data-stu-id="46e79-165">Helps you take action based on name using hello same script</span></span> |
| <span data-ttu-id="46e79-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="46e79-166">FailoverType</span></span> |<span data-ttu-id="46e79-167">Hiermee geeft u op of Hallo failover is testen, gepland of ongepland.</span><span class="sxs-lookup"><span data-stu-id="46e79-167">Specifies whether hello failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="46e79-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="46e79-168">FailoverDirection</span></span> |<span data-ttu-id="46e79-169">Geef op of herstel tooprimary of secundaire site</span><span class="sxs-lookup"><span data-stu-id="46e79-169">Specify whether recovery is tooprimary or secondary</span></span> |
| <span data-ttu-id="46e79-170">Groeps-id</span><span class="sxs-lookup"><span data-stu-id="46e79-170">GroupID</span></span> |<span data-ttu-id="46e79-171">Hallo groepsnummer binnen Hallo herstelplan identificeren wanneer Hallo plan wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="46e79-171">Identify hello group number within hello recovery plan when hello plan is running</span></span> |
| <span data-ttu-id="46e79-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="46e79-172">VmMap</span></span> |<span data-ttu-id="46e79-173">Matrix van alle Hallo virtuele machines in de groep Hallo</span><span class="sxs-lookup"><span data-stu-id="46e79-173">Array of all hello virtual machines in hello group</span></span> |
| <span data-ttu-id="46e79-174">VMMap sleutel</span><span class="sxs-lookup"><span data-stu-id="46e79-174">VMMap key</span></span> |<span data-ttu-id="46e79-175">Unieke sleutel (GUID) voor elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="46e79-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="46e79-176">Deze heeft Hallo hetzelfde zijn als de VMM-ID van de VM Hallo Hallo indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="46e79-176">It's hello same as hello VMM ID of hello virtual machine where applicable.</span></span> |
| <span data-ttu-id="46e79-177">Rolnaam</span><span class="sxs-lookup"><span data-stu-id="46e79-177">RoleName</span></span> |<span data-ttu-id="46e79-178">Naam van de virtuele machine van Azure die wordt hersteld Hallo</span><span class="sxs-lookup"><span data-stu-id="46e79-178">Name of hello Azure VM that's being recovered</span></span> |
| <span data-ttu-id="46e79-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="46e79-179">CloudServiceName</span></span> |<span data-ttu-id="46e79-180">Azure Cloud Service-naam onder welke Hallo virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="46e79-180">Azure Cloud Service name under which hello virtual machine is created.</span></span> |

<span data-ttu-id="46e79-181">tooidentify hello VmMap Key in de context van Hallo u kan ook toohello VM eigenschappenpagina in ASR en bekijkt hello VM GUID-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="46e79-181">tooidentify hello VmMap Key in hello context you could also go toohello VM properties page in ASR and look at hello VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="46e79-182">De auteur van een Automation-runbook</span><span class="sxs-lookup"><span data-stu-id="46e79-182">Author an Automation runbook</span></span>
<span data-ttu-id="46e79-183">Hallo runbook tooopen poort 80 op Hallo front-virtuele machine nu gemaakt.</span><span class="sxs-lookup"><span data-stu-id="46e79-183">Now create hello runbook tooopen port 80 on hello front-end virtual machine.</span></span>

1. <span data-ttu-id="46e79-184">Een nieuw runbook maken in Azure Automation-account met de naam van de Hallo Hallo **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="46e79-184">Create a new runbook in hello Azure Automation account with hello name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="46e79-185">Navigeer toohello weergave van Hallo runbook auteur en Hallo conceptmodus invoeren.</span><span class="sxs-lookup"><span data-stu-id="46e79-185">Navigate toohello Author view of hello runbook and enter hello draft mode.</span></span>
3. <span data-ttu-id="46e79-186">Geef eerst Hallo variabele toouse als Hallo recovery plan context</span><span class="sxs-lookup"><span data-stu-id="46e79-186">First specify hello variable toouse as hello recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="46e79-187">Toohello abonnement Hallo referentie en abonnement op met de volgende keer verbinding</span><span class="sxs-lookup"><span data-stu-id="46e79-187">Next connect toohello subscription using hello credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="46e79-188">Let erop dat u hello Azure gebruikt activa – **AzureCredential** en **AzureSubscriptionName** hier.</span><span class="sxs-lookup"><span data-stu-id="46e79-188">Note that you use hello Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="46e79-189">Nu Hallo endpoint details opgeven en Hallo GUID van Hallo virtuele machine waarvoor u tooexpose Hallo eindpunt wilt.</span><span class="sxs-lookup"><span data-stu-id="46e79-189">Now specify hello endpoint details and hello GUID of hello virtual machine for which you want tooexpose hello endpoint.</span></span> <span data-ttu-id="46e79-190">Case Hallo front-virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="46e79-190">In this case hello front-end virtual machine.</span></span>

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="46e79-191">Hiermee geeft u hello Azure-eindpunt protocol, lokale poort op Hallo VM en de bijbehorende toegewezen openbare poort.</span><span class="sxs-lookup"><span data-stu-id="46e79-191">This specifies hello Azure endpoint protocol, local port on hello VM and its mapped public port.</span></span> <span data-ttu-id="46e79-192">Deze variabelen zijn parameters vereist zijn voor hello Azure opdrachten die eindpunten tooVMs toevoegt.</span><span class="sxs-lookup"><span data-stu-id="46e79-192">These variables are parameters     required by hello Azure commands that add endpoints tooVMs.</span></span> <span data-ttu-id="46e79-193">Hallo VMGUID bevat Hallo GUID van Hallo virtuele machine, moet u toooperate op.</span><span class="sxs-lookup"><span data-stu-id="46e79-193">hello VMGUID holds hello GUID of hello virtual machine you need toooperate on.</span></span>
6. <span data-ttu-id="46e79-194">Hallo script wordt nu Hallo context voor Hallo VM GUID opgegeven uitpakken en een eindpunt op Hallo virtuele machine waarnaar wordt verwezen door deze te maken.</span><span class="sxs-lookup"><span data-stu-id="46e79-194">hello script will now extract hello context for hello given VM GUID and create an endpoint on hello virtual machine referenced by it.</span></span>

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="46e79-195">Zodra dit voltooid is, klik op publiceren ![](media/site-recovery-runbook-automation/20.png) tooallow uw script toobe beschikbaar voor uitvoering.</span><span class="sxs-lookup"><span data-stu-id="46e79-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) tooallow your script toobe available for execution.</span></span>

<span data-ttu-id="46e79-196">Hallo volledige script hieronder voor referentiedoeleinden</span><span class="sxs-lookup"><span data-stu-id="46e79-196">hello complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a><span data-ttu-id="46e79-197">Hallo script toohello herstelplan toevoegen</span><span class="sxs-lookup"><span data-stu-id="46e79-197">Add hello script toohello recovery plan</span></span>
<span data-ttu-id="46e79-198">Zodra Hallo script gereed is, kunt u deze toevoegen toohello herstelplan die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="46e79-198">Once hello script is ready, you can add it toohello recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="46e79-199">In de Hallo herstelplan die u hebt gemaakt, kiest u tooadd een script achter de groep 2.</span><span class="sxs-lookup"><span data-stu-id="46e79-199">In hello recovery plan you created, choose tooadd a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="46e79-200">Geef de scriptnaam van een.</span><span class="sxs-lookup"><span data-stu-id="46e79-200">Specify a script name.</span></span> <span data-ttu-id="46e79-201">Dit is slechts een beschrijvende naam voor dit script voor weergeven in het herstelplan Hallo.</span><span class="sxs-lookup"><span data-stu-id="46e79-201">This is just a friendly name for this script for showing within hello Recovery plan.</span></span>
3. <span data-ttu-id="46e79-202">Selecteer in de Hallo failover tooAzure script – hello Azure Automation-accountnaam.</span><span class="sxs-lookup"><span data-stu-id="46e79-202">In hello failover tooAzure script – Select hello Azure Automation Account name.</span></span>
4. <span data-ttu-id="46e79-203">Hallo Azure Runbooks, selecteer Hallo runbook die u geschreven.</span><span class="sxs-lookup"><span data-stu-id="46e79-203">In hello Azure Runbooks, select hello runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="46e79-204">Scripts op de primaire</span><span class="sxs-lookup"><span data-stu-id="46e79-204">Primary side scripts</span></span>
<span data-ttu-id="46e79-205">Wanneer u een failover-tooAzure uitvoert, kunt u ook kiezen tooexecute scripts op de primaire.</span><span class="sxs-lookup"><span data-stu-id="46e79-205">When you are executing a failover tooAzure, you can also choose tooexecute primary side scripts.</span></span> <span data-ttu-id="46e79-206">Deze scripts worden uitgevoerd op de VMM-server Hallo tijdens failover.</span><span class="sxs-lookup"><span data-stu-id="46e79-206">These scripts will run on hello VMM server during failover.</span></span>
<span data-ttu-id="46e79-207">Scripts op de primaire zijn alleen beschikbaar voor vooraf afsluiten en boeken afsluiten fasen.</span><span class="sxs-lookup"><span data-stu-id="46e79-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="46e79-208">Dit is omdat we Hallo primaire site toobe doorgaans niet beschikbaar verwachten wanneer een noodgeval biedt.</span><span class="sxs-lookup"><span data-stu-id="46e79-208">This is because we expect hello primary site toobe typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="46e79-209">Tijdens een niet-geplande failover alleen als u-in voor bewerkingen van de primaire site opt, wordt geprobeerd toorun Hallo primaire kant scripts.</span><span class="sxs-lookup"><span data-stu-id="46e79-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt toorun hello primary side scripts.</span></span> <span data-ttu-id="46e79-210">Als ze zijn niet bereikbaar, of een time-out opgetreden, Hallo failover wordt voortgezet Hallo toorecover virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="46e79-210">If they are not reachable or timeout, hello failover will continue toorecover hello virtual machines.</span></span>
<span data-ttu-id="46e79-211">Scripts op de primaire zijn niet beschikbaar voor VMware/fysiek/Hyper-v-Sites zonder VMM beveiligd tooAzure - terwijl u failover tooAzure.</span><span class="sxs-lookup"><span data-stu-id="46e79-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected tooAzure - while you failover tooAzure.</span></span>
<span data-ttu-id="46e79-212">Echter, wanneer u failback vanuit Azure tooon-premises, scripts (Runbooks) op primaire kan worden gebruikt voor alle doelen behalve VMware.</span><span class="sxs-lookup"><span data-stu-id="46e79-212">However, when you failback from Azure tooon-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-hello-recovery-plan"></a><span data-ttu-id="46e79-213">Testplan Hallo herstel</span><span class="sxs-lookup"><span data-stu-id="46e79-213">Test hello recovery plan</span></span>
<span data-ttu-id="46e79-214">Nadat u hebt toegevoegd Hallo runbook toohello plan kunt u een testfailover initiëren en in actie weergeven.</span><span class="sxs-lookup"><span data-stu-id="46e79-214">Once you have added hello runbook toohello plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="46e79-215">Het is altijd aanbevolen toorun een test failover tootest uw toepassing en Hallo recovery plan tooensure er zijn geen fouten.</span><span class="sxs-lookup"><span data-stu-id="46e79-215">It is always recommended toorun a test failover tootest your application and hello recovery plan tooensure that there are no errors.</span></span>

1. <span data-ttu-id="46e79-216">Selecteer Hallo herstelplan en start een testfailover.</span><span class="sxs-lookup"><span data-stu-id="46e79-216">Select hello recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="46e79-217">Tijdens het uitvoeren van Hallo-abonnement ziet u of Hallo runbook is uitgevoerd of niet via de status ervan.</span><span class="sxs-lookup"><span data-stu-id="46e79-217">During hello plan execution, you can see whether hello runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="46e79-218">U ziet ook Hallo gedetailleerde status van de runbook-uitvoering op Hallo Azure Automation-taken pagina voor het Hallo-runbook.</span><span class="sxs-lookup"><span data-stu-id="46e79-218">You can also see hello detailed runbook execution status on hello Azure Automation jobs page for hello runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="46e79-219">Nadat Hallo failover is voltooid, wordt naast Hallo runbook resultaat van uitvoering, ziet u of het Hallo-uitvoering is voltooid of niet door de virtuele machine van Azure-pagina Hallo bezoeken en bekijkt hello eindpunten.</span><span class="sxs-lookup"><span data-stu-id="46e79-219">After hello failover completes, apart from hello runbook execution result, you can see whether hello execution is successful or not by visiting hello Azure virtual machine page and looking at hello endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="46e79-220">Voorbeeldscripts</span><span class="sxs-lookup"><span data-stu-id="46e79-220">Sample scripts</span></span>
<span data-ttu-id="46e79-221">Terwijl we doorlopen een vaak automatiseren taak van het toevoegen van een eindpunt tooan virtuele machine van Azure in deze zelfstudie gebruikt, kunt u een aantal andere krachtige automatiseringstaken met behulp van Azure automation doen.</span><span class="sxs-lookup"><span data-stu-id="46e79-221">While we walked through automating one commonly used task of adding an endpoint tooan Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="46e79-222">Microsoft en hello Azure Automation-community bieden voorbeeldrunbooks waarmee u kunt aan de slag maken van uw eigen oplossingen en hulpprogramma runbooks, die u kunt gebruiken als bouwstenen voor grotere automatiseringstaken.</span><span class="sxs-lookup"><span data-stu-id="46e79-222">Microsoft and hello Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="46e79-223">Aan de slag met ze uit de galerie Hallo en bouwen van krachtige één muisklik herstelplannen voor uw toepassingen met Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="46e79-223">Start using them from hello gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="46e79-224">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="46e79-224">Additional Resources</span></span>
[<span data-ttu-id="46e79-225">Overzicht van Azure Automation</span><span class="sxs-lookup"><span data-stu-id="46e79-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "overzicht van Azure Automation")

[<span data-ttu-id="46e79-226">Voorbeeld van Azure automatiseringsscripts</span><span class="sxs-lookup"><span data-stu-id="46e79-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "steekproef Azure automatiseringsscripts")
