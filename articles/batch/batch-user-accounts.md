---
title: aaaRun taken onder gebruikersaccounts in Azure Batch | Microsoft Docs
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
ms.openlocfilehash: 13d7d76451d89a3cca090c4ef24ed0ed781bbf09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="7ca63-103">Taken onder gebruikersaccounts in Batch uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7ca63-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="7ca63-104">Een taak in Azure Batch wordt altijd uitgevoerd onder een gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="7ca63-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="7ca63-105">Taken worden standaard uitgevoerd onder standaardgebruikersaccounts zonder beheerdersrechten.</span><span class="sxs-lookup"><span data-stu-id="7ca63-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="7ca63-106">Deze standaardinstellingen voor het account van gebruiker zijn meestal voldoende.</span><span class="sxs-lookup"><span data-stu-id="7ca63-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="7ca63-107">Voor bepaalde scenario's is het echter handig toobe kunnen tooconfigure Hallo gebruikersaccount waaronder u een taak toorun.</span><span class="sxs-lookup"><span data-stu-id="7ca63-107">For certain scenarios, however, it's useful toobe able tooconfigure hello user account under which you want a task toorun.</span></span> <span data-ttu-id="7ca63-108">Dit artikel wordt beschreven Hallo typen gebruikersaccounts en hoe u ze kunt configureren voor uw scenario.</span><span class="sxs-lookup"><span data-stu-id="7ca63-108">This article discusses hello types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="7ca63-109">Typen gebruikersaccounts</span><span class="sxs-lookup"><span data-stu-id="7ca63-109">Types of user accounts</span></span>

<span data-ttu-id="7ca63-110">Azure Batch biedt twee soorten gebruikersaccounts voor het uitvoeren van taken:</span><span class="sxs-lookup"><span data-stu-id="7ca63-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="7ca63-111">**Automatische gebruikersaccounts.**</span><span class="sxs-lookup"><span data-stu-id="7ca63-111">**Auto-user accounts.**</span></span> <span data-ttu-id="7ca63-112">Automatische-gebruikersaccounts zijn ingebouwde gebruikersaccounts die automatisch worden gemaakt door Hallo Batch-service.</span><span class="sxs-lookup"><span data-stu-id="7ca63-112">Auto-user accounts are built-in user accounts that are created automatically by hello Batch service.</span></span> <span data-ttu-id="7ca63-113">Taken worden standaard uitgevoerd onder een auto-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="7ca63-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="7ca63-114">Hallo automatisch gebruiker specificatie voor een taak tooindicate onder welke auto-user account een taak moet worden uitgevoerd, kunt u configureren.</span><span class="sxs-lookup"><span data-stu-id="7ca63-114">You can configure hello auto-user specification for a task tooindicate under which auto-user account a task should run.</span></span> <span data-ttu-id="7ca63-115">Hallo automatisch gebruiker specificatie kunt u toospecify Hallo uitbreiding van bevoegdheden niveau en het bereik van Hallo auto-gebruikersaccount dat Hallo-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7ca63-115">hello auto-user specification allows you toospecify hello elevation level and scope of hello auto-user account that will run hello task.</span></span> 

- <span data-ttu-id="7ca63-116">**Een benoemde gebruikersaccount.**</span><span class="sxs-lookup"><span data-stu-id="7ca63-116">**A named user account.**</span></span> <span data-ttu-id="7ca63-117">U kunt een of meer benoemde gebruikersaccounts voor een pool opgeven wanneer u Hallo groep maakt.</span><span class="sxs-lookup"><span data-stu-id="7ca63-117">You can specify one or more named user accounts for a pool when you create hello pool.</span></span> <span data-ttu-id="7ca63-118">Elk gebruikersaccount wordt gemaakt op elk knooppunt van het Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="7ca63-118">Each user account is created on each node of hello pool.</span></span> <span data-ttu-id="7ca63-119">Bovendien toohello accountnaam, u Hallo het wachtwoord voor gebruikersaccount, uitbreiding van bevoegdheden opgeven niveau en, voor Linux-opslaggroepen, persoonlijke Hallo SSH-sleutel.</span><span class="sxs-lookup"><span data-stu-id="7ca63-119">In addition toohello account name, you specify hello user account password, elevation level, and, for Linux pools, hello SSH private key.</span></span> <span data-ttu-id="7ca63-120">Wanneer u een taak toevoegt, kunt u Hallo gebruikersaccount waaronder de taak die moet worden uitgevoerd met de naam opgeven.</span><span class="sxs-lookup"><span data-stu-id="7ca63-120">When you add a task, you can specify hello named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="7ca63-121">Hallo Batch-serviceversie 2017-01-01.4.0 bevat een belangrijke wijziging die is vereist dat u uw code toocall die versie bijwerken.</span><span class="sxs-lookup"><span data-stu-id="7ca63-121">hello Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code toocall that version.</span></span> <span data-ttu-id="7ca63-122">Als u de code migreren van een oudere versie van Batch, houd er rekening mee dat Hallo **runElevated** eigenschap wordt niet meer ondersteund in Hallo REST-API of Batch clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="7ca63-122">If you are migrating code from an older version of Batch, note that hello **runElevated** property is no longer supported in hello REST API or Batch client libraries.</span></span> <span data-ttu-id="7ca63-123">Gebruik Hallo nieuwe **userIdentity** eigenschap van een taak toospecify uitbreiding van bevoegdheden niveau.</span><span class="sxs-lookup"><span data-stu-id="7ca63-123">Use hello new **userIdentity** property of a task toospecify elevation level.</span></span> <span data-ttu-id="7ca63-124">Zie de sectie Hallo [bijwerken van uw code toohello nieuwste Batch-clientbibliotheek](#update-your-code-to-the-latest-batch-client-library) voor snelle richtlijnen voor het bijwerken van uw Batch-code als u van een Hallo clientbibliotheken gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="7ca63-124">See hello section titled [Update your code toohello latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of hello client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="7ca63-125">Hallo-gebruikersaccounts die in dit artikel wordt besproken ondersteunen geen Remote Desktop Protocol (RDP) of Secure Shell (SSH), uit veiligheidsoverwegingen.</span><span class="sxs-lookup"><span data-stu-id="7ca63-125">hello user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="7ca63-126">tooconnect tooa knooppunt actief Hallo Linux Virtuele-machineconfiguratie via SSH, Zie [gebruik extern bureaublad-tooa Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="7ca63-126">tooconnect tooa node running hello Linux virtual machine configuration via SSH, see [Use Remote Desktop tooa Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="7ca63-127">tooconnect toonodes waarop Windows wordt uitgevoerd via RDP, Zie [verbinding maken met Windows Server-VM tooa](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="7ca63-127">tooconnect toonodes running Windows via RDP, see [Connect tooa Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="7ca63-128">tooconnect tooa actieve Hallo cloud service knooppuntconfiguratie via RDP, Zie [extern bureaublad inschakelen voor een rol in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7ca63-128">tooconnect tooa node running hello cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-toofiles-and-directories"></a><span data-ttu-id="7ca63-129">Gebruiker account toegang toofiles en mappen</span><span class="sxs-lookup"><span data-stu-id="7ca63-129">User account access toofiles and directories</span></span>

<span data-ttu-id="7ca63-130">Zowel een auto-gebruikersaccount en een benoemde gebruikersaccount hebben lezen/schrijven toegang toohello van taak-werkmap, gedeelde map en meerdere exemplaren taken directory.</span><span class="sxs-lookup"><span data-stu-id="7ca63-130">Both an auto-user account and a named user account have read/write access toohello task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="7ca63-131">Beide typen accounts hebben leestoegang toohello opstart- en voorbereiding mappen.</span><span class="sxs-lookup"><span data-stu-id="7ca63-131">Both types of accounts have read access toohello startup and job preparation directories.</span></span>

<span data-ttu-id="7ca63-132">Als een taak wordt uitgevoerd onder Hallo hetzelfde account dat is gebruikt voor het uitvoeren van een begintaak, Hallo taak heeft lees-/ schrijftoegang toohello beginmap taak.</span><span class="sxs-lookup"><span data-stu-id="7ca63-132">If a task runs under hello same account that was used for running a start task, hello task has read-write access toohello start task directory.</span></span> <span data-ttu-id="7ca63-133">Op dezelfde manier als een taak wordt uitgevoerd onder Hallo hetzelfde account dat is gebruikt voor het uitvoeren van een jobvoorbereidingstaak, Hallo taak heeft lees-/ schrijftoegang toohello taak voorbereiding taakmap.</span><span class="sxs-lookup"><span data-stu-id="7ca63-133">Similarly, if a task runs under hello same account that was used for running a job preparation task, hello task has read-write access toohello job preparation task directory.</span></span> <span data-ttu-id="7ca63-134">Als een taak wordt uitgevoerd onder een ander account dan Hallo begintaak of jobvoorbereidingstaak, heeft de taak Hallo alleen leestoegang toohello respectieve directory.</span><span class="sxs-lookup"><span data-stu-id="7ca63-134">If a task runs under a different account than hello start task or job preparation task, then hello task has only read access toohello respective directory.</span></span>

<span data-ttu-id="7ca63-135">Zie voor meer informatie over de toegang tot bestanden en mappen uit een taak [ontwikkelen grootschalige parallelle compute-oplossingen met Batch](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="7ca63-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="7ca63-136">Toegang met verhoogde bevoegdheid voor taken</span><span class="sxs-lookup"><span data-stu-id="7ca63-136">Elevated access for tasks</span></span> 

<span data-ttu-id="7ca63-137">Hallo-gebruikersaccount van uitbreiding van bevoegdheden niveau geeft aan of een taak wordt uitgevoerd met verhoogde toegang.</span><span class="sxs-lookup"><span data-stu-id="7ca63-137">hello user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="7ca63-138">Zowel een auto-gebruikersaccount en een benoemde gebruikersaccount kunnen uitvoeren met verhoogde toegang.</span><span class="sxs-lookup"><span data-stu-id="7ca63-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="7ca63-139">Hallo twee opties voor het niveau van de uitbreiding van bevoegdheden zijn:</span><span class="sxs-lookup"><span data-stu-id="7ca63-139">hello two options for elevation level are:</span></span>

- <span data-ttu-id="7ca63-140">**NonAdmin:** Hallo-taak wordt uitgevoerd als standaardgebruiker zonder verhoogde toegang.</span><span class="sxs-lookup"><span data-stu-id="7ca63-140">**NonAdmin:** hello task runs as a standard user without elevated access.</span></span> <span data-ttu-id="7ca63-141">Hallo standaardniveau uitbreiding van bevoegdheden voor een Batch-gebruikersaccount is altijd **NonAdmin**.</span><span class="sxs-lookup"><span data-stu-id="7ca63-141">hello default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="7ca63-142">**Admin:** Hallo-taak wordt uitgevoerd als een gebruiker met toegang met verhoogde bevoegdheid en werkt met volledige Administrator-machtigingen.</span><span class="sxs-lookup"><span data-stu-id="7ca63-142">**Admin:** hello task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="7ca63-143">Automatische gebruikersaccounts</span><span class="sxs-lookup"><span data-stu-id="7ca63-143">Auto-user accounts</span></span>

<span data-ttu-id="7ca63-144">Standaard uitvoeren taken in Batch onder een auto-gebruikersaccount als standaardgebruiker zonder verhoogde toegang tot en met bereik van de taak.</span><span class="sxs-lookup"><span data-stu-id="7ca63-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="7ca63-145">Wanneer Hallo automatisch gebruiker specificatie is geconfigureerd voor het bereik van de taak, maakt Hallo Batch-service een automatische-account voor alleen die taak.</span><span class="sxs-lookup"><span data-stu-id="7ca63-145">When hello auto-user specification is configured for task scope, hello Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="7ca63-146">Hallo alternatieve tootask bereik is bereik van de groep van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7ca63-146">hello alternative tootask scope is pool scope.</span></span> <span data-ttu-id="7ca63-147">Wanneer Hallo automatisch gebruiker specificatie voor een taak voor het bereik van de groep van toepassingen is geconfigureerd, is Hallo-taak wordt uitgevoerd onder een auto-gebruikersaccount op dat beschikbaar tooany taak in de groep Hallo.</span><span class="sxs-lookup"><span data-stu-id="7ca63-147">When hello auto-user specification for a task is configured for pool scope, hello task runs under an auto-user account that is available tooany task in hello pool.</span></span> <span data-ttu-id="7ca63-148">Zie voor meer informatie over het bereik van de groep Hallo gedeelte [een taak uitvoeren zoals auto-gebruiker met een bereik van de groep Hallo](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="7ca63-148">For more information about pool scope, see hello section titled [Run a task as hello auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="7ca63-149">Hallo standaardbereik verschilt op Windows- en Linux-knooppunten:</span><span class="sxs-lookup"><span data-stu-id="7ca63-149">hello default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="7ca63-150">Op Windows-knooppunten taken standaard uitgevoerd onder het bereik van de taak.</span><span class="sxs-lookup"><span data-stu-id="7ca63-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="7ca63-151">Linux-knooppunten kan altijd worden uitgevoerd onder het bereik van de groep van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7ca63-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="7ca63-152">Er zijn vier mogelijke configuraties voor Hallo automatisch gebruiker specificatie die tooa unieke auto-gebruikersaccount overeenkomen:</span><span class="sxs-lookup"><span data-stu-id="7ca63-152">There are four possible configurations for hello auto-user specification, each of which corresponds tooa unique auto-user account:</span></span>

- <span data-ttu-id="7ca63-153">Niet-beheerder toegang met taak-bereik (Hallo standaard automatisch gebruiker specificatie)</span><span class="sxs-lookup"><span data-stu-id="7ca63-153">Non-admin access with task scope (hello default auto-user specification)</span></span>
- <span data-ttu-id="7ca63-154">Beheerderstoegang (verhoogd) met een bereik van de taak</span><span class="sxs-lookup"><span data-stu-id="7ca63-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="7ca63-155">Niet-beheerder toegang met een bereik van de groep van toepassingen</span><span class="sxs-lookup"><span data-stu-id="7ca63-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="7ca63-156">Beheerderstoegang met een bereik van de groep van toepassingen</span><span class="sxs-lookup"><span data-stu-id="7ca63-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="7ca63-157">Taken die worden uitgevoerd onder het bereik van de taak hoeft geen feitelijke toegang tooother taken op een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7ca63-157">Tasks running under task scope do not have de facto access tooother tasks on a node.</span></span> <span data-ttu-id="7ca63-158">Echter, een kwaadwillende gebruiker met toegang toohello account kan deze beperking omzeilen door het indienen van een taak die wordt uitgevoerd met administrator-bevoegdheden en heeft toegang tot andere mappen taak.</span><span class="sxs-lookup"><span data-stu-id="7ca63-158">However, a malicious user with access toohello account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="7ca63-159">Een kwaadwillende gebruiker kan ook gebruiken voor RDP of SSH tooconnect tooa knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7ca63-159">A malicious user could also use RDP or SSH tooconnect tooa node.</span></span> <span data-ttu-id="7ca63-160">Het is belangrijk tooprotect toegang tooyour Batch-account sleutels tooprevent dergelijk scenario.</span><span class="sxs-lookup"><span data-stu-id="7ca63-160">It's important tooprotect access tooyour Batch account keys tooprevent such a scenario.</span></span> <span data-ttu-id="7ca63-161">Als u vermoedt dat uw account is geknoeid, worden tooregenerate ervoor dat uw sleutels.</span><span class="sxs-lookup"><span data-stu-id="7ca63-161">If you suspect your account may have been compromised, be sure tooregenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="7ca63-162">Een taak uitvoeren als een auto-gebruiker met uitgebreide toegang</span><span class="sxs-lookup"><span data-stu-id="7ca63-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="7ca63-163">Hallo automatisch gebruiker specificatie voor de administrator-bevoegdheden kunt u configureren wanneer u een taak met verhoogde toegang toorun nodig.</span><span class="sxs-lookup"><span data-stu-id="7ca63-163">You can configure hello auto-user specification for administrator privileges when you need toorun a task with elevated access.</span></span> <span data-ttu-id="7ca63-164">Een begintaak moet mogelijk toegang met verhoogde bevoegdheid tooinstall software op Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7ca63-164">For example, a start task may need elevated access tooinstall software on hello node.</span></span>

> [!NOTE] 
> <span data-ttu-id="7ca63-165">In het algemeen is het beste toouse met verhoogde bevoegdheden voor toegang alleen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="7ca63-165">In general, it's best toouse elevated access only when necessary.</span></span> <span data-ttu-id="7ca63-166">Aanbevolen Hallo minimale bevoegdheden nodig tooachieve Hallo gewenste resultaat verlenen.</span><span class="sxs-lookup"><span data-stu-id="7ca63-166">Best practices recommend granting hello minimum privilege necessary tooachieve hello desired outcome.</span></span> <span data-ttu-id="7ca63-167">Bijvoorbeeld, als een begintaak software voor de huidige gebruiker hello, in plaats van voor alle gebruikers installeert, hebt u mogelijk kunnen tooavoid tootasks verhoogde toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="7ca63-167">For example, if a start task installs software for hello current user, instead of for all users, you may be able tooavoid granting elevated access tootasks.</span></span> <span data-ttu-id="7ca63-168">U kunt Hallo automatisch gebruiker specificatie voor de scope en niet-beheerders toegang groep voor alle taken die toorun onder dezelfde, inclusief de begintaak Hallo account Hallo moet configureren.</span><span class="sxs-lookup"><span data-stu-id="7ca63-168">You can configure hello auto-user specification for pool scope and non-admin access for all tasks that need toorun under hello same account, including hello start task.</span></span> 
>
>

<span data-ttu-id="7ca63-169">Hallo volgende codefragmenten laten zien hoe tooconfigure automatisch gebruiker specificatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="7ca63-169">hello following code snippets show how tooconfigure hello auto-user specification.</span></span> <span data-ttu-id="7ca63-170">Voorbeelden van Hallo Hallo uitbreiding van bevoegdheden niveau te instellen`Admin` en bereik te Hallo`Task`.</span><span class="sxs-lookup"><span data-stu-id="7ca63-170">hello examples set hello elevation level too`Admin` and hello scope too`Task`.</span></span> <span data-ttu-id="7ca63-171">Bereik van de taak is de standaardinstelling hello, maar dat is opgenomen Hallo verjaardagen van voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7ca63-171">Task scope is hello default setting, but is included here for hello sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="7ca63-172">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="7ca63-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="7ca63-173">Batch Java</span><span class="sxs-lookup"><span data-stu-id="7ca63-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="7ca63-174">Batch Python</span><span class="sxs-lookup"><span data-stu-id="7ca63-174">Batch Python</span></span>

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

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="7ca63-175">Een taak uitvoeren als een auto-gebruiker met een bereik van de groep van toepassingen</span><span class="sxs-lookup"><span data-stu-id="7ca63-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="7ca63-176">Wanneer een knooppunt is ingericht, twee hele groep automatisch-gebruikersaccounts zijn gemaakt op elk knooppunt in de pool hello, één met verhoogde toegang en één zonder verhoogde toegang.</span><span class="sxs-lookup"><span data-stu-id="7ca63-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in hello pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="7ca63-177">Hallo auto-van gebruiker bereik toopool bereik voor een bepaalde taak instellen, voert Hallo taak onder een van deze twee hele pool automatisch-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="7ca63-177">Setting hello auto-user's scope toopool scope for a given task runs hello task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="7ca63-178">Wanneer u een bereik van de groep van toepassingen voor Hallo automatisch-gebruiker opgeeft, alle taken die worden uitgevoerd met beheerdersbevoegdheden worden uitgevoerd onder Hallo dezelfde groep wide auto-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="7ca63-178">When you specify pool scope for hello auto-user, all tasks that run with administrator access run under hello same pool-wide auto-user account.</span></span> <span data-ttu-id="7ca63-179">Taken die worden uitgevoerd zonder beheerdersrechten uitgevoerd op deze manier ook onder één groep wide auto-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="7ca63-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="7ca63-180">Hallo twee hele pool automatisch-gebruikersaccounts zijn afzonderlijke accounts.</span><span class="sxs-lookup"><span data-stu-id="7ca63-180">hello two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="7ca63-181">Taken die worden uitgevoerd onder Hallo hele groep Administrator-account kunnen geen gegevens delen met taken die worden uitgevoerd onder het Hallo-standaardaccount, en vice versa.</span><span class="sxs-lookup"><span data-stu-id="7ca63-181">Tasks running under hello pool-wide administrative account cannot share data with tasks running under hello standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="7ca63-182">Hallo voordeel toorunning onder dezelfde automatisch gebruikersaccount is dat taken kunnen tooshare gegevens met andere taken uitgevoerd op Hallo Hallo hetzelfde knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7ca63-182">hello advantage toorunning under hello same auto-user account is that tasks are able tooshare data with other tasks running on hello same node.</span></span>

<span data-ttu-id="7ca63-183">Delen van geheimen tussen taken is een scenario waarin actieve taken onder een van twee Hallo hele pool automatisch-gebruikersaccounts handig is.</span><span class="sxs-lookup"><span data-stu-id="7ca63-183">Sharing secrets between tasks is one scenario where running tasks under one of hello two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="7ca63-184">Stel bijvoorbeeld dat een begintaak moet tooprovision een geheim op Hallo-knooppunt dat andere taken kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7ca63-184">For example, suppose a start task needs tooprovision a secret onto hello node that other tasks can use.</span></span> <span data-ttu-id="7ca63-185">U kunt Hallo Windows Data Protection API (DPAPI), maar het administrator-bevoegdheden vereist.</span><span class="sxs-lookup"><span data-stu-id="7ca63-185">You could use hello Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="7ca63-186">U kunt in plaats daarvan Hallo geheim op gebruikersniveau Hallo beveiligen.</span><span class="sxs-lookup"><span data-stu-id="7ca63-186">Instead, you can protect hello secret at hello user level.</span></span> <span data-ttu-id="7ca63-187">Taken die worden uitgevoerd onder dezelfde gebruikersaccount toegang heeft tot Hallo Hallo geheim zonder verhoogde toegang.</span><span class="sxs-lookup"><span data-stu-id="7ca63-187">Tasks running under hello same user account can access hello secret without elevated access.</span></span>

<span data-ttu-id="7ca63-188">Een ander scenario waar u mogelijk wilt toorun taken onder een automatische-gebruikersaccount met een bereik van de groep van toepassingen is een Message Passing Interface (MPI)-bestand delen.</span><span class="sxs-lookup"><span data-stu-id="7ca63-188">Another scenario where you may want toorun tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="7ca63-189">Een MPI-bestandsshare is nuttig wanneer Hallo knooppunten in Hallo MPI taak nodig toowork op Hallo dezelfde bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="7ca63-189">An MPI file share is useful when hello nodes in hello MPI task need toowork on hello same file data.</span></span> <span data-ttu-id="7ca63-190">Hallo hoofdknooppunt maakt een bestandsshare die Hallo onderliggende knooppunten toegang hebben tot als ze worden uitgevoerd onder Hallo hetzelfde auto-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="7ca63-190">hello head node creates a file share that hello child nodes can access if they are running under hello same auto-user account.</span></span> 

<span data-ttu-id="7ca63-191">Hallo volgende codefragment stelt Hallo auto-van gebruiker bereik toopool bereik voor een taak in Batch .NET.</span><span class="sxs-lookup"><span data-stu-id="7ca63-191">hello following code snippet sets hello auto-user's scope toopool scope for a task in Batch .NET.</span></span> <span data-ttu-id="7ca63-192">Hallo uitbreiding van bevoegdheden niveau wordt weggelaten, zodat het Hallo-taak wordt uitgevoerd onder Hallo standaard hele pool automatisch-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="7ca63-192">hello elevation level is omitted, so hello task runs under hello standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="7ca63-193">Benoemde gebruikersaccounts</span><span class="sxs-lookup"><span data-stu-id="7ca63-193">Named user accounts</span></span>

<span data-ttu-id="7ca63-194">Wanneer u een groep maakt, kunt u met de naam gebruikersaccounts definiëren.</span><span class="sxs-lookup"><span data-stu-id="7ca63-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="7ca63-195">Een benoemde gebruikersaccount heeft een naam en het wachtwoord dat u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="7ca63-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="7ca63-196">U kunt Hallo uitbreiding van bevoegdheden niveau voor een gebruikersaccount met de naam opgeven.</span><span class="sxs-lookup"><span data-stu-id="7ca63-196">You can specify hello elevation level for a named user account.</span></span> <span data-ttu-id="7ca63-197">U kunt ook een persoonlijke SSH-sleutel voor Linux-knooppunten opgeven.</span><span class="sxs-lookup"><span data-stu-id="7ca63-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="7ca63-198">Een gebruikersaccount met de naam bestaat op alle knooppunten in de groep Hallo en beschikbare tooall taken actief is op die knooppunten.</span><span class="sxs-lookup"><span data-stu-id="7ca63-198">A named user account exists on all nodes in hello pool and is available tooall tasks running on those nodes.</span></span> <span data-ttu-id="7ca63-199">U kunt een willekeurig aantal benoemde gebruikers voor een groep definiëren.</span><span class="sxs-lookup"><span data-stu-id="7ca63-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="7ca63-200">Wanneer u een taak of taak verzameling toevoegt, kunt u opgeven dat Hallo-taak wordt uitgevoerd onder een van de gebruikersaccounts die zijn gedefinieerd op Hallo van toepassingen met de naam Hallo.</span><span class="sxs-lookup"><span data-stu-id="7ca63-200">When you add a task or task collection, you can specify that hello task runs under one of hello named user accounts defined on hello pool.</span></span>

<span data-ttu-id="7ca63-201">Een gebruikersaccount met de naam is handig als u wilt dat toorun alle taken in een job onder Hallo hetzelfde gebruikersaccount, maar ze te isoleren van taken die worden uitgevoerd in andere taken op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="7ca63-201">A named user account is useful when you want toorun all tasks in a job under hello same user account, but isolate them from tasks running in other jobs at hello same time.</span></span> <span data-ttu-id="7ca63-202">U kunt bijvoorbeeld een benoemde gebruiker voor elke taak maken en uitvoeren van taken onder een gebruikersaccount met de naam van elke taak.</span><span class="sxs-lookup"><span data-stu-id="7ca63-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="7ca63-203">Vervolgens kunt elke taak een geheim delen met een eigen taken, maar niet met taken die in andere taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7ca63-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="7ca63-204">U kunt ook een benoemde gebruiker account toorun een taak die op externe bronnen zoals bestandsshares worden machtigingen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7ca63-204">You can also use a named user account toorun a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="7ca63-205">Met een benoemde gebruikersaccount Hallo gebruikersidentiteiten te beheren en kan die gebruiker identiteit tooset machtigingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7ca63-205">With a named user account, you control hello user identity and can use that user identity tooset permissions.</span></span>  

<span data-ttu-id="7ca63-206">Benoemde gebruikersaccounts inschakelen wachtwoordloze SSH tussen Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="7ca63-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="7ca63-207">U kunt een gebruikersaccount met de naam met Linux-knooppunten die taken met meerdere instanties toorun moeten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7ca63-207">You can use a named user account with Linux nodes that need toorun multi-instance tasks.</span></span> <span data-ttu-id="7ca63-208">Elk knooppunt in de pool Hallo kan taken onder een gebruikersaccount dat is gedefinieerd voor de hele groep Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7ca63-208">Each node in hello pool can run tasks under a user account defined on hello whole pool.</span></span> <span data-ttu-id="7ca63-209">Zie voor meer informatie over taken met meerdere instanties [gebruik van meerdere\-exemplaar taken toorun MPI-toepassingen](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="7ca63-209">For more information about multi-instance tasks, see [Use multi\-instance tasks toorun MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="7ca63-210">Benoemde gebruikersaccounts maken</span><span class="sxs-lookup"><span data-stu-id="7ca63-210">Create named user accounts</span></span>

<span data-ttu-id="7ca63-211">toocreate gebruikersaccounts in een Batch met de naam een verzameling van gebruiker accounts toohello groep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7ca63-211">toocreate named user accounts in Batch, add a collection of user accounts toohello pool.</span></span> <span data-ttu-id="7ca63-212">Hallo volgende codefragmenten laten zien hoe toocreate gebruikersaccounts in .NET, Java en Python genoemd.</span><span class="sxs-lookup"><span data-stu-id="7ca63-212">hello following code snippets show how toocreate named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="7ca63-213">Deze fragmenten tonen hoe code toocreate zowel admin en niet-beheerders accounts op een groep met de naam.</span><span class="sxs-lookup"><span data-stu-id="7ca63-213">These code snippets show how toocreate both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="7ca63-214">Hallo voorbeelden van toepassingen met behulp van Hallo cloud service-configuratie maken, maar u gebruiken Hallo dezelfde bij het maken van een Windows of Linux-toepassingen met behulp van de configuratie van de virtuele machine Hallo benaderen.</span><span class="sxs-lookup"><span data-stu-id="7ca63-214">hello examples create pools using hello cloud service configuration, but you use hello same approach when creating a Windows or Linux pool using hello virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="7ca63-215">Batch .NET-voorbeeld (Windows)</span><span class="sxs-lookup"><span data-stu-id="7ca63-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using hello cloud service configuration.
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

// Commit hello pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="7ca63-216">Batch .NET-voorbeeld (Linux)</span><span class="sxs-lookup"><span data-stu-id="7ca63-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello virtual machine configuration toouse toocreate hello pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create hello unbound pool.
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

// Commit hello pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="7ca63-217">Batch Java-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="7ca63-217">Batch Java example</span></span>

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

#### <a name="batch-python-example"></a><span data-ttu-id="7ca63-218">Batch Python-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="7ca63-218">Batch Python example</span></span>

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

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="7ca63-219">Een taak onder een gebruikersaccount met de naam uitvoeren met verhoogde toegang</span><span class="sxs-lookup"><span data-stu-id="7ca63-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="7ca63-220">een taak als verhoogde gebruiker set Hallo taak van toorun **UserIdentity** eigenschap tooa met een gebruikersaccount dat is gemaakt met de naam ervan **ElevationLevel** eigenschappenset te`Admin`.</span><span class="sxs-lookup"><span data-stu-id="7ca63-220">toorun a task as an elevated user, set hello task's **UserIdentity** property tooa named user account that was created with its **ElevationLevel** property set too`Admin`.</span></span>

<span data-ttu-id="7ca63-221">Dit codefragment specificeert dat die Hallo-taak moet worden uitgevoerd onder een gebruikersaccount met de naam.</span><span class="sxs-lookup"><span data-stu-id="7ca63-221">This code snippet specifies that hello task should run under a named user account.</span></span> <span data-ttu-id="7ca63-222">Dit account benoemde gebruiker is gedefinieerd op Hallo van toepassingen wanneer Hallo-groep is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7ca63-222">This named user account was defined on hello pool when hello pool was created.</span></span> <span data-ttu-id="7ca63-223">In dit geval is Hallo gebruikersaccount met de naam gemaakt met de beheerdersmachtigingen:</span><span class="sxs-lookup"><span data-stu-id="7ca63-223">In this case, hello named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a><span data-ttu-id="7ca63-224">Werk uw code toohello nieuwste Batch-clientbibliotheek</span><span class="sxs-lookup"><span data-stu-id="7ca63-224">Update your code toohello latest Batch client library</span></span>

<span data-ttu-id="7ca63-225">Hallo Batch-serviceversie 2017-01-01.4.0 introduceert een belangrijke wijziging, vervangen Hallo **runElevated** eigenschap beschikbaar in eerdere versies Hello **userIdentity** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="7ca63-225">hello Batch service version 2017-01-01.4.0 introduces a breaking change, replacing hello **runElevated** property available in earlier versions with hello **userIdentity** property.</span></span> <span data-ttu-id="7ca63-226">Hallo tabellen na bieden een eenvoudige toewijzing die u kan gebruiken tooupdate uw code uit eerdere versies van Hallo clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="7ca63-226">hello following tables provide a simple mapping that you can use tooupdate your code from earlier versions of hello client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="7ca63-227">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="7ca63-227">Batch .NET</span></span>

| <span data-ttu-id="7ca63-228">Als uw code gebruikt...</span><span class="sxs-lookup"><span data-stu-id="7ca63-228">If your code uses...</span></span>                  | <span data-ttu-id="7ca63-229">Bijwerken naar...</span><span class="sxs-lookup"><span data-stu-id="7ca63-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="7ca63-230">`CloudTask.RunElevated`niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="7ca63-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="7ca63-231">Er is geen update vereist</span><span class="sxs-lookup"><span data-stu-id="7ca63-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="7ca63-232">Batch Java</span><span class="sxs-lookup"><span data-stu-id="7ca63-232">Batch Java</span></span>

| <span data-ttu-id="7ca63-233">Als uw code gebruikt...</span><span class="sxs-lookup"><span data-stu-id="7ca63-233">If your code uses...</span></span>                      | <span data-ttu-id="7ca63-234">Bijwerken naar...</span><span class="sxs-lookup"><span data-stu-id="7ca63-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="7ca63-235">`CloudTask.withRunElevated`niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="7ca63-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="7ca63-236">Er is geen update vereist</span><span class="sxs-lookup"><span data-stu-id="7ca63-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="7ca63-237">Batch Python</span><span class="sxs-lookup"><span data-stu-id="7ca63-237">Batch Python</span></span>

| <span data-ttu-id="7ca63-238">Als uw code gebruikt...</span><span class="sxs-lookup"><span data-stu-id="7ca63-238">If your code uses...</span></span>                      | <span data-ttu-id="7ca63-239">Bijwerken naar...</span><span class="sxs-lookup"><span data-stu-id="7ca63-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="7ca63-240">`user_identity=user`, waarbij</span><span class="sxs-lookup"><span data-stu-id="7ca63-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="7ca63-241">`user_identity=user`, waarbij</span><span class="sxs-lookup"><span data-stu-id="7ca63-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="7ca63-242">`run_elevated`niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="7ca63-242">`run_elevated` not specified</span></span> | <span data-ttu-id="7ca63-243">Er is geen update vereist</span><span class="sxs-lookup"><span data-stu-id="7ca63-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="7ca63-244">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7ca63-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="7ca63-245">Batch-Forum</span><span class="sxs-lookup"><span data-stu-id="7ca63-245">Batch Forum</span></span>

<span data-ttu-id="7ca63-246">Hallo [Azure Batch-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) is uitermate toodiscuss Batch plaats en vragen over Hallo-service op MSDN.</span><span class="sxs-lookup"><span data-stu-id="7ca63-246">hello [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="7ca63-247">Kop op via voor nuttige vastgemaakt berichten, en stel uw vragen wanneer deze zich voordoen tijdens het bouwen van uw Batch-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="7ca63-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>
