---
title: Uitvoeren van taken onder gebruikersaccounts in Azure Batch | Microsoft Docs
description: Gebruikersaccounts voor het uitvoeren van taken in Azure Batch configureren
services: batch
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.openlocfilehash: d408c0565c0ed81fc97cc2b3976a4fc233e31302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="c9fc6-103">Taken onder gebruikersaccounts in Batch uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c9fc6-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="c9fc6-104">Een taak in Azure Batch wordt altijd uitgevoerd onder een gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="c9fc6-105">Taken worden standaard uitgevoerd onder standaardgebruikersaccounts zonder beheerdersrechten.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="c9fc6-106">Deze standaardinstellingen voor het account van gebruiker zijn meestal voldoende.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="c9fc6-107">Voor bepaalde scenario's is het echter handig om te kunnen configureren van het gebruikersaccount waaronder u wilt dat een taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-107">For certain scenarios, however, it's useful to be able to configure the user account under which you want a task to run.</span></span> <span data-ttu-id="c9fc6-108">Dit artikel wordt beschreven welke typen gebruikersaccounts en hoe u ze kunt configureren voor uw scenario.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-108">This article discusses the types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="c9fc6-109">Typen gebruikersaccounts</span><span class="sxs-lookup"><span data-stu-id="c9fc6-109">Types of user accounts</span></span>

<span data-ttu-id="c9fc6-110">Azure Batch biedt twee soorten gebruikersaccounts voor het uitvoeren van taken:</span><span class="sxs-lookup"><span data-stu-id="c9fc6-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="c9fc6-111">**Automatische gebruikersaccounts.**</span><span class="sxs-lookup"><span data-stu-id="c9fc6-111">**Auto-user accounts.**</span></span> <span data-ttu-id="c9fc6-112">Automatische-gebruikersaccounts zijn ingebouwde gebruikersaccounts die automatisch worden gemaakt door de Batch-service.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-112">Auto-user accounts are built-in user accounts that are created automatically by the Batch service.</span></span> <span data-ttu-id="c9fc6-113">Taken worden standaard uitgevoerd onder een auto-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="c9fc6-114">U kunt de specificatie automatisch gebruiker voor een taak om aan te geven onder welke automatisch gebruikersaccount een taak moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-114">You can configure the auto-user specification for a task to indicate under which auto-user account a task should run.</span></span> <span data-ttu-id="c9fc6-115">De specificatie auto-gebruiker kunt u opgeven van het niveau van de uitbreiding van bevoegdheden en het bereik van de automatische-gebruikersaccount op dat de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-115">The auto-user specification allows you to specify the elevation level and scope of the auto-user account that will run the task.</span></span> 

- <span data-ttu-id="c9fc6-116">**Een benoemde gebruikersaccount.**</span><span class="sxs-lookup"><span data-stu-id="c9fc6-116">**A named user account.**</span></span> <span data-ttu-id="c9fc6-117">U kunt een of meer benoemde gebruikersaccounts voor een pool opgeven wanneer u de groep maakt.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-117">You can specify one or more named user accounts for a pool when you create the pool.</span></span> <span data-ttu-id="c9fc6-118">Elk gebruikersaccount wordt gemaakt op elk knooppunt van de groep.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-118">Each user account is created on each node of the pool.</span></span> <span data-ttu-id="c9fc6-119">Naast de accountnaam Geef wachtwoord voor het gebruikersaccount, uitbreiding van bevoegdheden niveau en, voor Linux-toepassingen, de persoonlijke SSH-sleutel.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-119">In addition to the account name, you specify the user account password, elevation level, and, for Linux pools, the SSH private key.</span></span> <span data-ttu-id="c9fc6-120">Wanneer u een taak toevoegt, kunt u de benoemde gebruikersaccount waaronder de taak die moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-120">When you add a task, you can specify the named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="c9fc6-121">Versie van de Batch-service 2017-01-01.4.0 introduceert een belangrijke wijziging die is vereist dat u uw code om aan te roepen die versie bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-121">The Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code to call that version.</span></span> <span data-ttu-id="c9fc6-122">Als u de code migreren van een oudere versie van Batch, houd er rekening mee dat de **runElevated** eigenschap wordt niet meer ondersteund in de REST-API of Batch-clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-122">If you are migrating code from an older version of Batch, note that the **runElevated** property is no longer supported in the REST API or Batch client libraries.</span></span> <span data-ttu-id="c9fc6-123">Gebruik het nieuwe **userIdentity** eigenschap van een taak om uitbreiding van bevoegdheden op te geven.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-123">Use the new **userIdentity** property of a task to specify elevation level.</span></span> <span data-ttu-id="c9fc6-124">Zie de sectie [werk uw code naar de meest recente Batch-clientbibliotheek](#update-your-code-to-the-latest-batch-client-library) voor snelle richtlijnen voor het bijwerken van uw Batch-code als u een van de clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-124">See the section titled [Update your code to the latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of the client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="c9fc6-125">De gebruikersaccounts die in dit artikel wordt besproken ondersteunen geen Remote Desktop Protocol (RDP) of Secure Shell (SSH), uit veiligheidsoverwegingen.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-125">The user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="c9fc6-126">Zie voor verbinding met een knooppunt met de configuratie van de Linux-virtuele machine via SSH, [extern bureaublad gebruiken voor een Linux-VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="c9fc6-126">To connect to a node running the Linux virtual machine configuration via SSH, see [Use Remote Desktop to a Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="c9fc6-127">Zie voor verbinding met knooppunten waarop Windows wordt uitgevoerd via RDP, [verbinding maken met een Windows Server VM](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="c9fc6-127">To connect to nodes running Windows via RDP, see [Connect to a Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="c9fc6-128">Zie voor verbinding met een knooppunt met de configuratie van de cloud-service via RDP, [extern bureaublad inschakelen voor een rol in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c9fc6-128">To connect to a node running the cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-to-files-and-directories"></a><span data-ttu-id="c9fc6-129">Gebruikersaccount toegang tot bestanden en mappen</span><span class="sxs-lookup"><span data-stu-id="c9fc6-129">User account access to files and directories</span></span>

<span data-ttu-id="c9fc6-130">Zowel een auto-gebruikersaccount en een benoemde gebruikersaccount hebben lezen/schrijven toegang tot de werkmap, gedeelde map en meerdere exemplaren taken directory van de taak.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-130">Both an auto-user account and a named user account have read/write access to the task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="c9fc6-131">Beide typen accounts beschikken over leestoegang tot de opstart- en voorbereiding-mappen.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-131">Both types of accounts have read access to the startup and job preparation directories.</span></span>

<span data-ttu-id="c9fc6-132">Als een taak wordt uitgevoerd onder hetzelfde account dat is gebruikt voor het uitvoeren van een taak gestart, heeft de taak lees-/ schrijftoegang tot de map van de taak is gestart.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-132">If a task runs under the same account that was used for running a start task, the task has read-write access to the start task directory.</span></span> <span data-ttu-id="c9fc6-133">Op dezelfde manier als een taak wordt uitgevoerd onder hetzelfde account dat is gebruikt voor het uitvoeren van een jobvoorbereidingstaak, de taak lezen-schrijven toegang heeft tot de taakmap taak voorbereiding.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-133">Similarly, if a task runs under the same account that was used for running a job preparation task, the task has read-write access to the job preparation task directory.</span></span> <span data-ttu-id="c9fc6-134">Als een taak wordt uitgevoerd onder een ander account dan de begintaak of jobvoorbereidingstaak, heeft de taak alleen leestoegang tot de betreffende map.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-134">If a task runs under a different account than the start task or job preparation task, then the task has only read access to the respective directory.</span></span>

<span data-ttu-id="c9fc6-135">Zie voor meer informatie over de toegang tot bestanden en mappen uit een taak [ontwikkelen grootschalige parallelle compute-oplossingen met Batch](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="c9fc6-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="c9fc6-136">Toegang met verhoogde bevoegdheid voor taken</span><span class="sxs-lookup"><span data-stu-id="c9fc6-136">Elevated access for tasks</span></span> 

<span data-ttu-id="c9fc6-137">Het gebruikersaccount uitbreiding van bevoegdheden niveau geeft aan of een taak wordt uitgevoerd met verhoogde toegang.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-137">The user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="c9fc6-138">Zowel een auto-gebruikersaccount en een benoemde gebruikersaccount kunnen uitvoeren met verhoogde toegang.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="c9fc6-139">De twee opties voor uitbreiding van bevoegdheden niveau zijn:</span><span class="sxs-lookup"><span data-stu-id="c9fc6-139">The two options for elevation level are:</span></span>

- <span data-ttu-id="c9fc6-140">**NonAdmin:** de taak wordt uitgevoerd als standaardgebruiker zonder verhoogde toegang.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-140">**NonAdmin:** The task runs as a standard user without elevated access.</span></span> <span data-ttu-id="c9fc6-141">Het standaardniveau voor uitbreiding van bevoegdheden voor een Batch-gebruikersaccount is altijd **NonAdmin**.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-141">The default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="c9fc6-142">**Admin:** de taak wordt uitgevoerd als een gebruiker met toegang met verhoogde bevoegdheid en werkt met volledige Administrator-machtigingen.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-142">**Admin:** The task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="c9fc6-143">Automatische gebruikersaccounts</span><span class="sxs-lookup"><span data-stu-id="c9fc6-143">Auto-user accounts</span></span>

<span data-ttu-id="c9fc6-144">Standaard uitvoeren taken in Batch onder een auto-gebruikersaccount als standaardgebruiker zonder verhoogde toegang tot en met bereik van de taak.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="c9fc6-145">Wanneer de gebruiker automatisch-specificatie voor taak scope is geconfigureerd, maakt de Batch-service een automatische-account voor alleen die taak.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-145">When the auto-user specification is configured for task scope, the Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="c9fc6-146">Het alternatief voor het bereik van de taak is bereik van de groep.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-146">The alternative to task scope is pool scope.</span></span> <span data-ttu-id="c9fc6-147">Wanneer de gebruiker automatisch-specificatie voor een taak voor het bereik van de groep van toepassingen is geconfigureerd, wordt de taak wordt uitgevoerd onder een auto-gebruikersaccount op dat beschikbaar is voor elke taak in de groep.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-147">When the auto-user specification for a task is configured for pool scope, the task runs under an auto-user account that is available to any task in the pool.</span></span> <span data-ttu-id="c9fc6-148">Zie het gedeelte voor meer informatie over toepassingen bereik [een taak uitvoeren als de automatische-gebruiker met een bereik van de groep](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="c9fc6-148">For more information about pool scope, see the section titled [Run a task as the auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="c9fc6-149">Het standaardbereik verschilt op Windows- en Linux-knooppunten:</span><span class="sxs-lookup"><span data-stu-id="c9fc6-149">The default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="c9fc6-150">Op Windows-knooppunten taken standaard uitgevoerd onder het bereik van de taak.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="c9fc6-151">Linux-knooppunten kan altijd worden uitgevoerd onder het bereik van de groep van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="c9fc6-152">Er zijn vier mogelijke configuraties voor de gebruiker automatisch-specificatie die met een gebruikersaccount van de unieke automatisch overeenkomen:</span><span class="sxs-lookup"><span data-stu-id="c9fc6-152">There are four possible configurations for the auto-user specification, each of which corresponds to a unique auto-user account:</span></span>

- <span data-ttu-id="c9fc6-153">Niet-beheerder toegang met taak-bereik (standaard automatisch gebruiker specificatie)</span><span class="sxs-lookup"><span data-stu-id="c9fc6-153">Non-admin access with task scope (the default auto-user specification)</span></span>
- <span data-ttu-id="c9fc6-154">Beheerderstoegang (verhoogd) met een bereik van de taak</span><span class="sxs-lookup"><span data-stu-id="c9fc6-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="c9fc6-155">Niet-beheerder toegang met een bereik van de groep van toepassingen</span><span class="sxs-lookup"><span data-stu-id="c9fc6-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="c9fc6-156">Beheerderstoegang met een bereik van de groep van toepassingen</span><span class="sxs-lookup"><span data-stu-id="c9fc6-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="c9fc6-157">Taken die worden uitgevoerd onder het bereik van de taak bent niet gemachtigd feitelijke aan andere taken op een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-157">Tasks running under task scope do not have de facto access to other tasks on a node.</span></span> <span data-ttu-id="c9fc6-158">Echter, een kwaadwillende gebruiker met toegang tot het account kan deze beperking omzeilen door het indienen van een taak die wordt uitgevoerd met administrator-bevoegdheden en heeft toegang tot andere mappen taak.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-158">However, a malicious user with access to the account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="c9fc6-159">Een kwaadwillende gebruiker kan verbinding maken met een knooppunt ook RDP of SSH kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-159">A malicious user could also use RDP or SSH to connect to a node.</span></span> <span data-ttu-id="c9fc6-160">Het is belangrijk om te beveiligen van toegang tot de sleutels van uw Batch-account om te voorkomen dat dergelijke scenario.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-160">It's important to protect access to your Batch account keys to prevent such a scenario.</span></span> <span data-ttu-id="c9fc6-161">Als u vermoedt dat uw account is geknoeid, zorg er dan voor dat uw sleutels genereren.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-161">If you suspect your account may have been compromised, be sure to regenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="c9fc6-162">Een taak uitvoeren als een auto-gebruiker met uitgebreide toegang</span><span class="sxs-lookup"><span data-stu-id="c9fc6-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="c9fc6-163">Als u een taak uitvoeren met verhoogde toegang nodig hebt, kunt u de gebruiker automatisch-specificatie voor de administrator-bevoegdheden configureren.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-163">You can configure the auto-user specification for administrator privileges when you need to run a task with elevated access.</span></span> <span data-ttu-id="c9fc6-164">Een begintaak moet mogelijk de toegang met verhoogde bevoegdheid om software te installeren op het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-164">For example, a start task may need elevated access to install software on the node.</span></span>

> [!NOTE] 
> <span data-ttu-id="c9fc6-165">In het algemeen is het beste verhoogde toegang alleen indien nodig gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-165">In general, it's best to use elevated access only when necessary.</span></span> <span data-ttu-id="c9fc6-166">Aanbevolen de minimale bevoegdheden die nodig zijn voor het bereiken van het gewenste resultaat verlenen.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-166">Best practices recommend granting the minimum privilege necessary to achieve the desired outcome.</span></span> <span data-ttu-id="c9fc6-167">Bijvoorbeeld, als een begintaak software voor de huidige gebruiker, in plaats van voor alle gebruikers installeert wellicht kunt u voorkomen met verhoogde bevoegdheden geen toegang verlenen tot taken.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-167">For example, if a start task installs software for the current user, instead of for all users, you may be able to avoid granting elevated access to tasks.</span></span> <span data-ttu-id="c9fc6-168">U kunt de specificatie automatisch gebruiker voor de scope en niet-beheerders toegang groep voor alle taken die moeten worden uitgevoerd onder hetzelfde account, met inbegrip van de begintaak configureren.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-168">You can configure the auto-user specification for pool scope and non-admin access for all tasks that need to run under the same account, including the start task.</span></span> 
>
>

<span data-ttu-id="c9fc6-169">De volgende codefragmenten laten zien hoe de specificatie van de gebruiker automatisch configureren.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-169">The following code snippets show how to configure the auto-user specification.</span></span> <span data-ttu-id="c9fc6-170">De voorbeelden ingesteld de uitbreiding van bevoegdheden op `Admin` en de scope `Task`.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-170">The examples set the elevation level to `Admin` and the scope to `Task`.</span></span> <span data-ttu-id="c9fc6-171">Bereik van de taak is de standaardinstelling, maar is hier opgenomen om het voorbeeld te houden.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-171">Task scope is the default setting, but is included here for the sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="c9fc6-172">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="c9fc6-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="c9fc6-173">Batch Java</span><span class="sxs-lookup"><span data-stu-id="c9fc6-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="c9fc6-174">Batch Python</span><span class="sxs-lookup"><span data-stu-id="c9fc6-174">Batch Python</span></span>

```python
user = batchmodels.UserIdentity(
    auto_user=batchmodels.AutoUserSpecification(
        elevation_level=batchmodels.ElevationLevel.admin,
        scope=batchmodels.AutoUserScope.task))
task = batchmodels.TaskAddParameter(
    id='task_1',
    command_line='cmd /c "echo hello world"',
    user_identity=user)
batch_client.task.add(job_id=jobid, task=task)
```

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="c9fc6-175">Een taak uitvoeren als een auto-gebruiker met een bereik van de groep van toepassingen</span><span class="sxs-lookup"><span data-stu-id="c9fc6-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="c9fc6-176">Wanneer een knooppunt is ingericht, twee hele groep automatisch-gebruikersaccounts zijn gemaakt op elk knooppunt in de groep, één met verhoogde toegang en één zonder verhoogde toegang.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in the pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="c9fc6-177">Het bereik van de automatische-gebruiker aan groep-bereik voor een bepaalde taak instellen, voert de taak onder een van deze twee hele pool automatisch-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-177">Setting the auto-user's scope to pool scope for a given task runs the task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="c9fc6-178">Wanneer u toepassingen bereik voor de automatische-gebruiker, alle taken die worden uitgevoerd met beheerdersbevoegdheden uitgevoerd onder dezelfde groep wide auto-gebruikersaccount opgeven.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-178">When you specify pool scope for the auto-user, all tasks that run with administrator access run under the same pool-wide auto-user account.</span></span> <span data-ttu-id="c9fc6-179">Taken die worden uitgevoerd zonder beheerdersrechten uitgevoerd op deze manier ook onder één groep wide auto-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="c9fc6-180">De twee toepassingen wide auto-gebruikersaccounts zijn afzonderlijke accounts.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-180">The two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="c9fc6-181">Taken die worden uitgevoerd onder de hele groep Administrator-account kunnen geen gegevens delen met taken die worden uitgevoerd onder de standaard-account en vice versa.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-181">Tasks running under the pool-wide administrative account cannot share data with tasks running under the standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="c9fc6-182">Het voordeel in wordt uitgevoerd onder dezelfde auto-gebruikersaccount is dat taken kunnen geen gegevens delen met andere taken op hetzelfde knooppunt uitvoert.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-182">The advantage to running under the same auto-user account is that tasks are able to share data with other tasks running on the same node.</span></span>

<span data-ttu-id="c9fc6-183">Delen van geheimen tussen taken is een scenario waarin actieve taken onder een van de twee toepassingen wide auto-gebruikersaccounts handig is.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-183">Sharing secrets between tasks is one scenario where running tasks under one of the two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="c9fc6-184">Stel bijvoorbeeld dat een begintaak moet voor het inrichten van een geheim naar het knooppunt dat andere taken kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-184">For example, suppose a start task needs to provision a secret onto the node that other tasks can use.</span></span> <span data-ttu-id="c9fc6-185">U kunt Windows Data Protection API (DPAPI), maar het administrator-bevoegdheden vereist.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-185">You could use the Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="c9fc6-186">In plaats daarvan kunt u het geheim op gebruikersniveau beveiligen.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-186">Instead, you can protect the secret at the user level.</span></span> <span data-ttu-id="c9fc6-187">Taken die worden uitgevoerd onder dezelfde gebruikersaccount hebben toegang tot het geheim zonder verhoogde toegang.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-187">Tasks running under the same user account can access the secret without elevated access.</span></span>

<span data-ttu-id="c9fc6-188">Een ander scenario waar u mogelijk wilt uitvoeren van taken onder een gebruikersaccount op de automatische met bereik van de groep van toepassingen is een bestandsshare Message Passing Interface (MPI).</span><span class="sxs-lookup"><span data-stu-id="c9fc6-188">Another scenario where you may want to run tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="c9fc6-189">Een MPI-bestandsshare is handig wanneer de knooppunten in de MPI-taak moeten werken op dezelfde bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-189">An MPI file share is useful when the nodes in the MPI task need to work on the same file data.</span></span> <span data-ttu-id="c9fc6-190">Het hoofdknooppunt maakt een bestandsshare die de onderliggende knooppunten toegang hebben tot als ze worden uitgevoerd onder dezelfde auto-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-190">The head node creates a file share that the child nodes can access if they are running under the same auto-user account.</span></span> 

<span data-ttu-id="c9fc6-191">Het volgende codefragment stelt de automatische-gebruiker scope aan groep-bereik voor een taak in Batch .NET.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-191">The following code snippet sets the auto-user's scope to pool scope for a task in Batch .NET.</span></span> <span data-ttu-id="c9fc6-192">Het niveau van de uitbreiding van bevoegdheden wordt weggelaten, zodat de taak wordt uitgevoerd onder de hele groep automatisch-standaardgebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-192">The elevation level is omitted, so the task runs under the standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="c9fc6-193">Benoemde gebruikersaccounts</span><span class="sxs-lookup"><span data-stu-id="c9fc6-193">Named user accounts</span></span>

<span data-ttu-id="c9fc6-194">Wanneer u een groep maakt, kunt u met de naam gebruikersaccounts definiëren.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="c9fc6-195">Een benoemde gebruikersaccount heeft een naam en het wachtwoord dat u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="c9fc6-196">U kunt het niveau van de uitbreiding van bevoegdheden voor een benoemde gebruikersaccount opgeven.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-196">You can specify the elevation level for a named user account.</span></span> <span data-ttu-id="c9fc6-197">U kunt ook een persoonlijke SSH-sleutel voor Linux-knooppunten opgeven.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="c9fc6-198">Een gebruikersaccount met de naam bestaat op alle knooppunten in de groep en is beschikbaar voor alle taken die worden uitgevoerd op die knooppunten.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-198">A named user account exists on all nodes in the pool and is available to all tasks running on those nodes.</span></span> <span data-ttu-id="c9fc6-199">U kunt een willekeurig aantal benoemde gebruikers voor een groep definiëren.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="c9fc6-200">Wanneer u een taak of taak verzameling toevoegt, kunt u opgeven dat de taak wordt uitgevoerd onder een van de benoemde gebruikersaccounts die zijn gedefinieerd in de groep.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-200">When you add a task or task collection, you can specify that the task runs under one of the named user accounts defined on the pool.</span></span>

<span data-ttu-id="c9fc6-201">Een gebruikersaccount met de naam is handig als u wilt alle taken uitvoeren in een taak onder hetzelfde gebruikersaccount, maar ze van taken die in andere taken worden uitgevoerd op hetzelfde moment te isoleren.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-201">A named user account is useful when you want to run all tasks in a job under the same user account, but isolate them from tasks running in other jobs at the same time.</span></span> <span data-ttu-id="c9fc6-202">U kunt bijvoorbeeld een benoemde gebruiker voor elke taak maken en uitvoeren van taken onder een gebruikersaccount met de naam van elke taak.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="c9fc6-203">Vervolgens kunt elke taak een geheim delen met een eigen taken, maar niet met taken die in andere taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="c9fc6-204">U kunt ook een gebruikersaccount met de naam voor het uitvoeren van een taak die op externe bronnen zoals bestandsshares worden machtigingen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-204">You can also use a named user account to run a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="c9fc6-205">Met een benoemde gebruikersaccount bepalen van de gebruikers-id en de identiteit van die gebruiker machtigingen instellen kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-205">With a named user account, you control the user identity and can use that user identity to set permissions.</span></span>  

<span data-ttu-id="c9fc6-206">Benoemde gebruikersaccounts inschakelen wachtwoordloze SSH tussen Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="c9fc6-207">U kunt een benoemde gebruikersaccount gebruiken met Linux-knooppunten die moeten worden uitgevoerd van taken met meerdere instanties.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-207">You can use a named user account with Linux nodes that need to run multi-instance tasks.</span></span> <span data-ttu-id="c9fc6-208">Elk knooppunt in de pool kan taken onder een gebruikersaccount dat is gedefinieerd voor de hele groep uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-208">Each node in the pool can run tasks under a user account defined on the whole pool.</span></span> <span data-ttu-id="c9fc6-209">Zie voor meer informatie over taken met meerdere instanties [gebruik van meerdere\-taken MPI-toepassingen uit te voeren van exemplaar van](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="c9fc6-209">For more information about multi-instance tasks, see [Use multi\-instance tasks to run MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="c9fc6-210">Benoemde gebruikersaccounts maken</span><span class="sxs-lookup"><span data-stu-id="c9fc6-210">Create named user accounts</span></span>

<span data-ttu-id="c9fc6-211">Voor benoemde gebruikersaccounts in Batch maakt, moet u een verzameling van gebruikersaccounts toevoegen aan de groep.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-211">To create named user accounts in Batch, add a collection of user accounts to the pool.</span></span> <span data-ttu-id="c9fc6-212">De volgende codefragmenten laten zien hoe gebruikersaccounts te maken met de naam in .NET, Java en Python.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-212">The following code snippets show how to create named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="c9fc6-213">Deze codefragmenten laten zien hoe admin en niet-beheerders accounts op een groep met de naam maken.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-213">These code snippets show how to create both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="c9fc6-214">De voorbeelden van toepassingen met behulp van de configuratie van de cloud-service maken, maar u dezelfde manier gebruiken bij het maken van een Windows- of Linux-toepassingen met behulp van de configuratie van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-214">The examples create pools using the cloud service configuration, but you use the same approach when creating a Windows or Linux pool using the virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="c9fc6-215">Batch .NET-voorbeeld (Windows)</span><span class="sxs-lookup"><span data-stu-id="c9fc6-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using the cloud service configuration.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                                         
    virtualMachineSize: "small",                                                
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));   

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount("adminUser", "xyz123", ElevationLevel.Admin),
    new UserAccount("nonAdminUser", "123xyz", ElevationLevel.NonAdmin),
};

// Commit the pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="c9fc6-216">Batch .NET-voorbeeld (Linux)</span><span class="sxs-lookup"><span data-stu-id="c9fc6-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of the VM image to use.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain the first node agent SKU in the collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create the virtual machine configuration to use to create the pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create the unbound pool.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                             
    virtualMachineSize: "Standard_A1",                                      
    virtualMachineConfiguration: virtualMachineConfiguration);                  

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount(
        name: "adminUser",
        password: "xyz123",
        elevationLevel: ElevationLevel.Admin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 12345,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
    new UserAccount(
        name: "nonAdminUser",
        password: "123xyz",
        elevationLevel: ElevationLevel.NonAdmin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 45678,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
};

// Commit the pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="c9fc6-217">Batch Java-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c9fc6-217">Batch Java example</span></span>

```java
List<UserAccount> userList = new ArrayList<>();
userList.add(new UserAccount().withName(adminUserAccountName).withPassword(adminPassword).withElevationLevel(ElevationLevel.ADMIN));
userList.add(new UserAccount().withName(nonAdminUserAccountName).withPassword(nonAdminPassword).withElevationLevel(ElevationLevel.NONADMIN));
PoolAddParameter addParameter = new PoolAddParameter()
        .withId(poolId)
        .withTargetDedicatedNodes(POOL_VM_COUNT)
        .withVmSize(POOL_VM_SIZE)
        .withCloudServiceConfiguration(configuration)
        .withUserAccounts(userList);
batchClient.poolOperations().createPool(addParameter);
```

#### <a name="batch-python-example"></a><span data-ttu-id="c9fc6-218">Batch Python-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c9fc6-218">Batch Python example</span></span>

```python
users = [
    batchmodels.UserAccount(
        name='pool-admin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.admin)
    batchmodels.UserAccount(
        name='pool-nonadmin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.nonadmin)
]
pool = batchmodels.PoolAddParameter(
    id=pool_id,
    user_accounts=users,
    virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
        image_reference=image_ref_to_use,
        node_agent_sku_id=sku_to_use),
    vm_size=vm_size,
    target_dedicated=vm_count)
batch_client.pool.add(pool)
```

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="c9fc6-219">Een taak onder een gebruikersaccount met de naam uitvoeren met verhoogde toegang</span><span class="sxs-lookup"><span data-stu-id="c9fc6-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="c9fc6-220">Als een taak wordt uitgevoerd als een gebruiker met verhoogde bevoegdheid, instellen van de taak **UserIdentity** eigenschap aan een benoemde gebruikersaccount dat is gemaakt met de **ElevationLevel** eigenschap ingesteld op `Admin`.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-220">To run a task as an elevated user, set the task's **UserIdentity** property to a named user account that was created with its **ElevationLevel** property set to `Admin`.</span></span>

<span data-ttu-id="c9fc6-221">Dit codefragment geeft aan dat de taak wordt uitgevoerd onder een gebruikersaccount met de naam.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-221">This code snippet specifies that the task should run under a named user account.</span></span> <span data-ttu-id="c9fc6-222">Dit account benoemde gebruiker is gedefinieerd in de groep wanneer de groep is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-222">This named user account was defined on the pool when the pool was created.</span></span> <span data-ttu-id="c9fc6-223">In dit geval is de benoemde gebruiker-account gemaakt met de beheerdersmachtigingen:</span><span class="sxs-lookup"><span data-stu-id="c9fc6-223">In this case, the named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-to-the-latest-batch-client-library"></a><span data-ttu-id="c9fc6-224">Werk uw code naar de meest recente Batch-clientbibliotheek</span><span class="sxs-lookup"><span data-stu-id="c9fc6-224">Update your code to the latest Batch client library</span></span>

<span data-ttu-id="c9fc6-225">Versie van de Batch-service 2017-01-01.4.0 introduceert een belangrijke wijziging, vervangt de **runElevated** eigenschap beschikbaar in eerdere versies met de **userIdentity** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-225">The Batch service version 2017-01-01.4.0 introduces a breaking change, replacing the **runElevated** property available in earlier versions with the **userIdentity** property.</span></span> <span data-ttu-id="c9fc6-226">De volgende tabellen bevatten een eenvoudige toewijzing die u gebruiken kunt om bij te werken van uw code uit eerdere versies van de clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-226">The following tables provide a simple mapping that you can use to update your code from earlier versions of the client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="c9fc6-227">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="c9fc6-227">Batch .NET</span></span>

| <span data-ttu-id="c9fc6-228">Als uw code gebruikt...</span><span class="sxs-lookup"><span data-stu-id="c9fc6-228">If your code uses...</span></span>                  | <span data-ttu-id="c9fc6-229">Bijwerken naar...</span><span class="sxs-lookup"><span data-stu-id="c9fc6-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="c9fc6-230">`CloudTask.RunElevated`niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="c9fc6-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="c9fc6-231">Er is geen update vereist</span><span class="sxs-lookup"><span data-stu-id="c9fc6-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="c9fc6-232">Batch Java</span><span class="sxs-lookup"><span data-stu-id="c9fc6-232">Batch Java</span></span>

| <span data-ttu-id="c9fc6-233">Als uw code gebruikt...</span><span class="sxs-lookup"><span data-stu-id="c9fc6-233">If your code uses...</span></span>                      | <span data-ttu-id="c9fc6-234">Bijwerken naar...</span><span class="sxs-lookup"><span data-stu-id="c9fc6-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="c9fc6-235">`CloudTask.withRunElevated`niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="c9fc6-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="c9fc6-236">Er is geen update vereist</span><span class="sxs-lookup"><span data-stu-id="c9fc6-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="c9fc6-237">Batch Python</span><span class="sxs-lookup"><span data-stu-id="c9fc6-237">Batch Python</span></span>

| <span data-ttu-id="c9fc6-238">Als uw code gebruikt...</span><span class="sxs-lookup"><span data-stu-id="c9fc6-238">If your code uses...</span></span>                      | <span data-ttu-id="c9fc6-239">Bijwerken naar...</span><span class="sxs-lookup"><span data-stu-id="c9fc6-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="c9fc6-240">`user_identity=user`, waarbij</span><span class="sxs-lookup"><span data-stu-id="c9fc6-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="c9fc6-241">`user_identity=user`, waarbij</span><span class="sxs-lookup"><span data-stu-id="c9fc6-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="c9fc6-242">`run_elevated`niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="c9fc6-242">`run_elevated` not specified</span></span> | <span data-ttu-id="c9fc6-243">Er is geen update vereist</span><span class="sxs-lookup"><span data-stu-id="c9fc6-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="c9fc6-244">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c9fc6-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="c9fc6-245">Batch-Forum</span><span class="sxs-lookup"><span data-stu-id="c9fc6-245">Batch Forum</span></span>

<span data-ttu-id="c9fc6-246">De [Azure Batch-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) is een goede plaats om te bespreken Batch en vragen over de service op MSDN.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-246">The [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="c9fc6-247">Kop op via voor nuttige vastgemaakt berichten, en stel uw vragen wanneer deze zich voordoen tijdens het bouwen van uw Batch-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="c9fc6-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>