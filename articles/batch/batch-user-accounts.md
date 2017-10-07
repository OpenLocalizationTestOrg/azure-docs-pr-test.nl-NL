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
# <a name="run-tasks-under-user-accounts-in-batch"></a>Taken onder gebruikersaccounts in Batch uitvoeren

Een taak in Azure Batch wordt altijd uitgevoerd onder een gebruikersaccount. Taken worden standaard uitgevoerd onder standaardgebruikersaccounts zonder beheerdersrechten. Deze standaardinstellingen voor het account van gebruiker zijn meestal voldoende. Voor bepaalde scenario's is het echter handig toobe kunnen tooconfigure Hallo gebruikersaccount waaronder u een taak toorun. Dit artikel wordt beschreven Hallo typen gebruikersaccounts en hoe u ze kunt configureren voor uw scenario.

## <a name="types-of-user-accounts"></a>Typen gebruikersaccounts

Azure Batch biedt twee soorten gebruikersaccounts voor het uitvoeren van taken:

- **Automatische gebruikersaccounts.** Automatische-gebruikersaccounts zijn ingebouwde gebruikersaccounts die automatisch worden gemaakt door Hallo Batch-service. Taken worden standaard uitgevoerd onder een auto-gebruikersaccount. Hallo automatisch gebruiker specificatie voor een taak tooindicate onder welke auto-user account een taak moet worden uitgevoerd, kunt u configureren. Hallo automatisch gebruiker specificatie kunt u toospecify Hallo uitbreiding van bevoegdheden niveau en het bereik van Hallo auto-gebruikersaccount dat Hallo-taak wordt uitgevoerd. 

- **Een benoemde gebruikersaccount.** U kunt een of meer benoemde gebruikersaccounts voor een pool opgeven wanneer u Hallo groep maakt. Elk gebruikersaccount wordt gemaakt op elk knooppunt van het Hallo-groep. Bovendien toohello accountnaam, u Hallo het wachtwoord voor gebruikersaccount, uitbreiding van bevoegdheden opgeven niveau en, voor Linux-opslaggroepen, persoonlijke Hallo SSH-sleutel. Wanneer u een taak toevoegt, kunt u Hallo gebruikersaccount waaronder de taak die moet worden uitgevoerd met de naam opgeven.

> [!IMPORTANT] 
> Hallo Batch-serviceversie 2017-01-01.4.0 bevat een belangrijke wijziging die is vereist dat u uw code toocall die versie bijwerken. Als u de code migreren van een oudere versie van Batch, houd er rekening mee dat Hallo **runElevated** eigenschap wordt niet meer ondersteund in Hallo REST-API of Batch clientbibliotheken. Gebruik Hallo nieuwe **userIdentity** eigenschap van een taak toospecify uitbreiding van bevoegdheden niveau. Zie de sectie Hallo [bijwerken van uw code toohello nieuwste Batch-clientbibliotheek](#update-your-code-to-the-latest-batch-client-library) voor snelle richtlijnen voor het bijwerken van uw Batch-code als u van een Hallo clientbibliotheken gebruikmaakt.
>
>

> [!NOTE] 
> Hallo-gebruikersaccounts die in dit artikel wordt besproken ondersteunen geen Remote Desktop Protocol (RDP) of Secure Shell (SSH), uit veiligheidsoverwegingen. 
>
> tooconnect tooa knooppunt actief Hallo Linux Virtuele-machineconfiguratie via SSH, Zie [gebruik extern bureaublad-tooa Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md). tooconnect toonodes waarop Windows wordt uitgevoerd via RDP, Zie [verbinding maken met Windows Server-VM tooa](../virtual-machines/windows/connect-logon.md).<br /><br />
> tooconnect tooa actieve Hallo cloud service knooppuntconfiguratie via RDP, Zie [extern bureaublad inschakelen voor een rol in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).
>
>

## <a name="user-account-access-toofiles-and-directories"></a>Gebruiker account toegang toofiles en mappen

Zowel een auto-gebruikersaccount en een benoemde gebruikersaccount hebben lezen/schrijven toegang toohello van taak-werkmap, gedeelde map en meerdere exemplaren taken directory. Beide typen accounts hebben leestoegang toohello opstart- en voorbereiding mappen.

Als een taak wordt uitgevoerd onder Hallo hetzelfde account dat is gebruikt voor het uitvoeren van een begintaak, Hallo taak heeft lees-/ schrijftoegang toohello beginmap taak. Op dezelfde manier als een taak wordt uitgevoerd onder Hallo hetzelfde account dat is gebruikt voor het uitvoeren van een jobvoorbereidingstaak, Hallo taak heeft lees-/ schrijftoegang toohello taak voorbereiding taakmap. Als een taak wordt uitgevoerd onder een ander account dan Hallo begintaak of jobvoorbereidingstaak, heeft de taak Hallo alleen leestoegang toohello respectieve directory.

Zie voor meer informatie over de toegang tot bestanden en mappen uit een taak [ontwikkelen grootschalige parallelle compute-oplossingen met Batch](batch-api-basics.md#files-and-directories).

## <a name="elevated-access-for-tasks"></a>Toegang met verhoogde bevoegdheid voor taken 

Hallo-gebruikersaccount van uitbreiding van bevoegdheden niveau geeft aan of een taak wordt uitgevoerd met verhoogde toegang. Zowel een auto-gebruikersaccount en een benoemde gebruikersaccount kunnen uitvoeren met verhoogde toegang. Hallo twee opties voor het niveau van de uitbreiding van bevoegdheden zijn:

- **NonAdmin:** Hallo-taak wordt uitgevoerd als standaardgebruiker zonder verhoogde toegang. Hallo standaardniveau uitbreiding van bevoegdheden voor een Batch-gebruikersaccount is altijd **NonAdmin**.
- **Admin:** Hallo-taak wordt uitgevoerd als een gebruiker met toegang met verhoogde bevoegdheid en werkt met volledige Administrator-machtigingen. 

## <a name="auto-user-accounts"></a>Automatische gebruikersaccounts

Standaard uitvoeren taken in Batch onder een auto-gebruikersaccount als standaardgebruiker zonder verhoogde toegang tot en met bereik van de taak. Wanneer Hallo automatisch gebruiker specificatie is geconfigureerd voor het bereik van de taak, maakt Hallo Batch-service een automatische-account voor alleen die taak.

Hallo alternatieve tootask bereik is bereik van de groep van toepassingen. Wanneer Hallo automatisch gebruiker specificatie voor een taak voor het bereik van de groep van toepassingen is geconfigureerd, is Hallo-taak wordt uitgevoerd onder een auto-gebruikersaccount op dat beschikbaar tooany taak in de groep Hallo. Zie voor meer informatie over het bereik van de groep Hallo gedeelte [een taak uitvoeren zoals auto-gebruiker met een bereik van de groep Hallo](#run-a-task-as-the-autouser-with-pool-scope).   

Hallo standaardbereik verschilt op Windows- en Linux-knooppunten:

- Op Windows-knooppunten taken standaard uitgevoerd onder het bereik van de taak.
- Linux-knooppunten kan altijd worden uitgevoerd onder het bereik van de groep van toepassingen.

Er zijn vier mogelijke configuraties voor Hallo automatisch gebruiker specificatie die tooa unieke auto-gebruikersaccount overeenkomen:

- Niet-beheerder toegang met taak-bereik (Hallo standaard automatisch gebruiker specificatie)
- Beheerderstoegang (verhoogd) met een bereik van de taak
- Niet-beheerder toegang met een bereik van de groep van toepassingen
- Beheerderstoegang met een bereik van de groep van toepassingen

> [!IMPORTANT] 
> Taken die worden uitgevoerd onder het bereik van de taak hoeft geen feitelijke toegang tooother taken op een knooppunt. Echter, een kwaadwillende gebruiker met toegang toohello account kan deze beperking omzeilen door het indienen van een taak die wordt uitgevoerd met administrator-bevoegdheden en heeft toegang tot andere mappen taak. Een kwaadwillende gebruiker kan ook gebruiken voor RDP of SSH tooconnect tooa knooppunt. Het is belangrijk tooprotect toegang tooyour Batch-account sleutels tooprevent dergelijk scenario. Als u vermoedt dat uw account is geknoeid, worden tooregenerate ervoor dat uw sleutels.
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a>Een taak uitvoeren als een auto-gebruiker met uitgebreide toegang

Hallo automatisch gebruiker specificatie voor de administrator-bevoegdheden kunt u configureren wanneer u een taak met verhoogde toegang toorun nodig. Een begintaak moet mogelijk toegang met verhoogde bevoegdheid tooinstall software op Hallo-knooppunt.

> [!NOTE] 
> In het algemeen is het beste toouse met verhoogde bevoegdheden voor toegang alleen indien nodig. Aanbevolen Hallo minimale bevoegdheden nodig tooachieve Hallo gewenste resultaat verlenen. Bijvoorbeeld, als een begintaak software voor de huidige gebruiker hello, in plaats van voor alle gebruikers installeert, hebt u mogelijk kunnen tooavoid tootasks verhoogde toegang verlenen. U kunt Hallo automatisch gebruiker specificatie voor de scope en niet-beheerders toegang groep voor alle taken die toorun onder dezelfde, inclusief de begintaak Hallo account Hallo moet configureren. 
>
>

Hallo volgende codefragmenten laten zien hoe tooconfigure automatisch gebruiker specificatie Hallo. Voorbeelden van Hallo Hallo uitbreiding van bevoegdheden niveau te instellen`Admin` en bereik te Hallo`Task`. Bereik van de taak is de standaardinstelling hello, maar dat is opgenomen Hallo verjaardagen van voorbeeld.

#### <a name="batch-net"></a>Batch .NET

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a>Batch Java

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a>Batch Python

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

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a>Een taak uitvoeren als een auto-gebruiker met een bereik van de groep van toepassingen

Wanneer een knooppunt is ingericht, twee hele groep automatisch-gebruikersaccounts zijn gemaakt op elk knooppunt in de pool hello, één met verhoogde toegang en één zonder verhoogde toegang. Hallo auto-van gebruiker bereik toopool bereik voor een bepaalde taak instellen, voert Hallo taak onder een van deze twee hele pool automatisch-gebruikersaccounts. 

Wanneer u een bereik van de groep van toepassingen voor Hallo automatisch-gebruiker opgeeft, alle taken die worden uitgevoerd met beheerdersbevoegdheden worden uitgevoerd onder Hallo dezelfde groep wide auto-gebruikersaccount. Taken die worden uitgevoerd zonder beheerdersrechten uitgevoerd op deze manier ook onder één groep wide auto-gebruikersaccount. 

> [!NOTE] 
> Hallo twee hele pool automatisch-gebruikersaccounts zijn afzonderlijke accounts. Taken die worden uitgevoerd onder Hallo hele groep Administrator-account kunnen geen gegevens delen met taken die worden uitgevoerd onder het Hallo-standaardaccount, en vice versa. 
>
>

Hallo voordeel toorunning onder dezelfde automatisch gebruikersaccount is dat taken kunnen tooshare gegevens met andere taken uitgevoerd op Hallo Hallo hetzelfde knooppunt.

Delen van geheimen tussen taken is een scenario waarin actieve taken onder een van twee Hallo hele pool automatisch-gebruikersaccounts handig is. Stel bijvoorbeeld dat een begintaak moet tooprovision een geheim op Hallo-knooppunt dat andere taken kunnen gebruiken. U kunt Hallo Windows Data Protection API (DPAPI), maar het administrator-bevoegdheden vereist. U kunt in plaats daarvan Hallo geheim op gebruikersniveau Hallo beveiligen. Taken die worden uitgevoerd onder dezelfde gebruikersaccount toegang heeft tot Hallo Hallo geheim zonder verhoogde toegang.

Een ander scenario waar u mogelijk wilt toorun taken onder een automatische-gebruikersaccount met een bereik van de groep van toepassingen is een Message Passing Interface (MPI)-bestand delen. Een MPI-bestandsshare is nuttig wanneer Hallo knooppunten in Hallo MPI taak nodig toowork op Hallo dezelfde bestandsgegevens. Hallo hoofdknooppunt maakt een bestandsshare die Hallo onderliggende knooppunten toegang hebben tot als ze worden uitgevoerd onder Hallo hetzelfde auto-gebruikersaccount. 

Hallo volgende codefragment stelt Hallo auto-van gebruiker bereik toopool bereik voor een taak in Batch .NET. Hallo uitbreiding van bevoegdheden niveau wordt weggelaten, zodat het Hallo-taak wordt uitgevoerd onder Hallo standaard hele pool automatisch-gebruikersaccount.

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a>Benoemde gebruikersaccounts

Wanneer u een groep maakt, kunt u met de naam gebruikersaccounts definiëren. Een benoemde gebruikersaccount heeft een naam en het wachtwoord dat u opgeeft. U kunt Hallo uitbreiding van bevoegdheden niveau voor een gebruikersaccount met de naam opgeven. U kunt ook een persoonlijke SSH-sleutel voor Linux-knooppunten opgeven.

Een gebruikersaccount met de naam bestaat op alle knooppunten in de groep Hallo en beschikbare tooall taken actief is op die knooppunten. U kunt een willekeurig aantal benoemde gebruikers voor een groep definiëren. Wanneer u een taak of taak verzameling toevoegt, kunt u opgeven dat Hallo-taak wordt uitgevoerd onder een van de gebruikersaccounts die zijn gedefinieerd op Hallo van toepassingen met de naam Hallo.

Een gebruikersaccount met de naam is handig als u wilt dat toorun alle taken in een job onder Hallo hetzelfde gebruikersaccount, maar ze te isoleren van taken die worden uitgevoerd in andere taken op Hallo hetzelfde moment. U kunt bijvoorbeeld een benoemde gebruiker voor elke taak maken en uitvoeren van taken onder een gebruikersaccount met de naam van elke taak. Vervolgens kunt elke taak een geheim delen met een eigen taken, maar niet met taken die in andere taken worden uitgevoerd.

U kunt ook een benoemde gebruiker account toorun een taak die op externe bronnen zoals bestandsshares worden machtigingen ingesteld. Met een benoemde gebruikersaccount Hallo gebruikersidentiteiten te beheren en kan die gebruiker identiteit tooset machtigingen gebruiken.  

Benoemde gebruikersaccounts inschakelen wachtwoordloze SSH tussen Linux-knooppunten. U kunt een gebruikersaccount met de naam met Linux-knooppunten die taken met meerdere instanties toorun moeten gebruiken. Elk knooppunt in de pool Hallo kan taken onder een gebruikersaccount dat is gedefinieerd voor de hele groep Hallo uitvoeren. Zie voor meer informatie over taken met meerdere instanties [gebruik van meerdere\-exemplaar taken toorun MPI-toepassingen](batch-mpi.md).

### <a name="create-named-user-accounts"></a>Benoemde gebruikersaccounts maken

toocreate gebruikersaccounts in een Batch met de naam een verzameling van gebruiker accounts toohello groep toevoegen. Hallo volgende codefragmenten laten zien hoe toocreate gebruikersaccounts in .NET, Java en Python genoemd. Deze fragmenten tonen hoe code toocreate zowel admin en niet-beheerders accounts op een groep met de naam. Hallo voorbeelden van toepassingen met behulp van Hallo cloud service-configuratie maken, maar u gebruiken Hallo dezelfde bij het maken van een Windows of Linux-toepassingen met behulp van de configuratie van de virtuele machine Hallo benaderen.

#### <a name="batch-net-example-windows"></a>Batch .NET-voorbeeld (Windows)

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

#### <a name="batch-net-example-linux"></a>Batch .NET-voorbeeld (Linux)

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


#### <a name="batch-java-example"></a>Batch Java-voorbeeld

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

#### <a name="batch-python-example"></a>Batch Python-voorbeeld

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

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a>Een taak onder een gebruikersaccount met de naam uitvoeren met verhoogde toegang

een taak als verhoogde gebruiker set Hallo taak van toorun **UserIdentity** eigenschap tooa met een gebruikersaccount dat is gemaakt met de naam ervan **ElevationLevel** eigenschappenset te`Admin`.

Dit codefragment specificeert dat die Hallo-taak moet worden uitgevoerd onder een gebruikersaccount met de naam. Dit account benoemde gebruiker is gedefinieerd op Hallo van toepassingen wanneer Hallo-groep is gemaakt. In dit geval is Hallo gebruikersaccount met de naam gemaakt met de beheerdersmachtigingen:

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a>Werk uw code toohello nieuwste Batch-clientbibliotheek

Hallo Batch-serviceversie 2017-01-01.4.0 introduceert een belangrijke wijziging, vervangen Hallo **runElevated** eigenschap beschikbaar in eerdere versies Hello **userIdentity** eigenschap. Hallo tabellen na bieden een eenvoudige toewijzing die u kan gebruiken tooupdate uw code uit eerdere versies van Hallo clientbibliotheken.

### <a name="batch-net"></a>Batch .NET

| Als uw code gebruikt...                  | Bijwerken naar...                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| `CloudTask.RunElevated`niet opgegeven | Er is geen update vereist                                                                                               |

### <a name="batch-java"></a>Batch Java

| Als uw code gebruikt...                      | Bijwerken naar...                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| `CloudTask.withRunElevated`niet opgegeven | Er is geen update vereist                                                                                                                     |

### <a name="batch-python"></a>Batch Python

| Als uw code gebruikt...                      | Bijwerken naar...                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | `user_identity=user`, waarbij <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | `user_identity=user`, waarbij <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| `run_elevated`niet opgegeven | Er is geen update vereist                                                                                                                                  |


## <a name="next-steps"></a>Volgende stappen

### <a name="batch-forum"></a>Batch-Forum

Hallo [Azure Batch-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) is uitermate toodiscuss Batch plaats en vragen over Hallo-service op MSDN. Kop op via voor nuttige vastgemaakt berichten, en stel uw vragen wanneer deze zich voordoen tijdens het bouwen van uw Batch-oplossingen.
