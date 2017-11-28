---
title: aaaUse PowerShell tooback van Windows Server tooAzure | Microsoft Docs
description: Meer informatie over hoe toodeploy en Azure back-up met behulp van PowerShell beheren
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: f13224f53abd6fbd132fee4347b0b99e8f5e2678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="7bc53-103">Implementeren en beheren van back-tooAzure voor Windows Server/Windows-clients met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="7bc53-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7bc53-104">ARM</span><span class="sxs-lookup"><span data-stu-id="7bc53-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="7bc53-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="7bc53-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="7bc53-106">Dit artikel ziet u hoe toouse PowerShell voor het instellen van Azure Backup op Windows Server of een Windows-client en het beheren van back-up en herstel.</span><span class="sxs-lookup"><span data-stu-id="7bc53-106">This article shows you how toouse PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="7bc53-107">Azure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="7bc53-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="7bc53-108">Dit artikel is gericht op Hallo Azure Resource Manager (ARM) en Hallo MS Online back-up PowerShell-cmdlets waarmee u een Recovery Services-kluis in een resourcegroep toouse.</span><span class="sxs-lookup"><span data-stu-id="7bc53-108">This article focuses on hello Azure Resource Manager (ARM) and hello MS Online Backup PowerShell cmdlets that enable you toouse a Recovery Services vault in a resource group.</span></span>

<span data-ttu-id="7bc53-109">In oktober 2015 is Azure PowerShell 1.0 uitgebracht.</span><span class="sxs-lookup"><span data-stu-id="7bc53-109">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="7bc53-110">Deze release Hallo 0.9.8 release is voltooid en over een aantal belangrijke wijzigingen, met name in Hallo naamgevingspatroon Hallo-cmdlets worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="7bc53-110">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="7bc53-111">1.0 cmdlets volgen Hallo naamgevingspatroon {werkwoord}-AzureRm {zelfstandig naamwoord}; terwijl Hallo 0.9.8 namen geen bevatten **Rm** (bijvoorbeeld New-AzureRmResourceGroup in plaats van New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="7bc53-111">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="7bc53-112">Wanneer u Azure PowerShell 0.9.8 gebruikt, moet u eerst Hallo Resource Manager-modus inschakelen door het uitvoeren van Hallo **Switch Azure AzureResourceManager** opdracht.</span><span class="sxs-lookup"><span data-stu-id="7bc53-112">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="7bc53-113">Met deze opdracht hoeft niet in 1.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="7bc53-113">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="7bc53-114">Als u uw scripts die zijn geschreven voor Hallo 0.9.8-omgeving in Hallo 1.0 of hoger omgeving toouse wilt u moet zorgvuldig bijwerken en Hallo scripts te testen in een testomgeving voordat u ze in productie tooavoid onverwachte impact.</span><span class="sxs-lookup"><span data-stu-id="7bc53-114">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully update and test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="7bc53-115">[Download de meest recente PowerShell-versie Hallo](https://github.com/Azure/azure-powershell/releases) (minimaal vereiste versie is: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="7bc53-115">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="7bc53-116">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="7bc53-116">Create a recovery services vault</span></span>
<span data-ttu-id="7bc53-117">volgende stappen uit Hallo leiden u bij het maken van een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="7bc53-117">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="7bc53-118">Een Recovery Services-kluis is anders dan een back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="7bc53-118">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="7bc53-119">Als u van Azure Backup voor Hallo eerst gebruikmaakt, moet u Hallo **registreren AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider met uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="7bc53-119">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="7bc53-120">Hallo Recovery Services-kluis is een ARM-bron, dus u tooplace moet deze binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="7bc53-120">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="7bc53-121">U kunt een bestaande resourcegroep gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="7bc53-121">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="7bc53-122">Bij het maken van een nieuwe resourcegroep Hallo naam en locatie voor resourcegroep Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="7bc53-122">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. <span data-ttu-id="7bc53-123">Gebruik Hallo **nieuw AzureRmRecoveryServicesVault** cmdlet toocreate Hallo nieuwe kluis.</span><span class="sxs-lookup"><span data-stu-id="7bc53-123">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate hello new vault.</span></span> <span data-ttu-id="7bc53-124">Zorg ervoor dat toospecify dezelfde locatie voor de kluis Hallo Hallo werd gebruikt voor de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bc53-124">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. <span data-ttu-id="7bc53-125">Geef een Hallo van opslag redundantie toouse; u kunt [lokaal redundante opslag (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) of [geografisch redundante opslag (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="7bc53-125">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="7bc53-126">Hallo volgende voorbeeld ziet Hallo BackupStorageRedundancy - optie voor testVault tooGeoRedundant is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7bc53-126">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="7bc53-127">Veel Azure Backup-cmdlets vereisen Hallo Recovery Services-kluis object als invoer.</span><span class="sxs-lookup"><span data-stu-id="7bc53-127">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="7bc53-128">Daarom is het handige toostore Hallo back-up Recovery Services-kluis object in een variabele.</span><span class="sxs-lookup"><span data-stu-id="7bc53-128">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="7bc53-129">Hallo-kluizen in een abonnement weergeven</span><span class="sxs-lookup"><span data-stu-id="7bc53-129">View hello vaults in a subscription</span></span>
<span data-ttu-id="7bc53-130">Gebruik **Get-AzureRmRecoveryServicesVault** tooview Hallo lijst met alle kluizen in het huidige abonnement Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bc53-130">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="7bc53-131">U kunt deze opdracht toocheck of een nieuwe kluis is gemaakt of toosee welke kluizen zijn beschikbaar in het Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7bc53-131">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="7bc53-132">Hallo-opdracht uitvoeren **Get-AzureRmRecoveryServicesVault**, en alle kluizen in Hallo abonnement worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7bc53-132">Run hello command, **Get-AzureRmRecoveryServicesVault**, and all vaults in hello subscription are listed.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="7bc53-133">Hello Azure backup-agent installeren</span><span class="sxs-lookup"><span data-stu-id="7bc53-133">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="7bc53-134">Voordat u hello Azure backup-agent hebt geïnstalleerd, moet u toohave Hallo installatieprogramma gedownload en aanwezig is op Hallo van Windows Server.</span><span class="sxs-lookup"><span data-stu-id="7bc53-134">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="7bc53-135">U kunt de nieuwste versie van de Hallo van Hallo installer krijgen van Hallo [Microsoft Download Center](http://aka.ms/azurebackup_agent) of van de dashboardpagina Hallo Recovery Services-kluis van.</span><span class="sxs-lookup"><span data-stu-id="7bc53-135">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="7bc53-136">Hallo-installatieprogramma opslaan tooan toegankelijke locatie zoals * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="7bc53-136">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="7bc53-137">U kunt ook gebruik PowerShell tooget Hallo downloader:</span><span class="sxs-lookup"><span data-stu-id="7bc53-137">Alternatively, use PowerShell tooget hello downloader:</span></span>
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

<span data-ttu-id="7bc53-138">tooinstall Hallo agent uitvoeren Hallo volgende opdracht in een PowerShell-console met verhoogde bevoegdheid:</span><span class="sxs-lookup"><span data-stu-id="7bc53-138">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="7bc53-139">Dit met alle standaardopties voor Hallo Hallo-agent hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7bc53-139">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="7bc53-140">Hallo installatie duurt een paar minuten op Hallo achtergrond.</span><span class="sxs-lookup"><span data-stu-id="7bc53-140">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="7bc53-141">Als u geen Hallo opgeeft */nu* optie vervolgens Hallo **Windows Update** venster wordt geopend na Hallo Hallo installatie toocheck voor eventuele updates.</span><span class="sxs-lookup"><span data-stu-id="7bc53-141">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="7bc53-142">Wanneer is geïnstalleerd, weergegeven Hallo agent in Hallo lijst met geïnstalleerde programma's.</span><span class="sxs-lookup"><span data-stu-id="7bc53-142">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="7bc53-143">toosee hello lijst met geïnstalleerde programma's, gaat u te**Configuratiescherm** > **programma's** > **programma's en onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="7bc53-143">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent is geïnstalleerd](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="7bc53-145">Opties voor de installatie</span><span class="sxs-lookup"><span data-stu-id="7bc53-145">Installation options</span></span>
<span data-ttu-id="7bc53-146">alle opties die beschikbaar zijn via Hallo toosee Hallo opdrachtregelprogramma, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7bc53-146">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="7bc53-147">Hallo beschikbare opties zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="7bc53-147">hello available options include:</span></span>

| <span data-ttu-id="7bc53-148">Optie</span><span class="sxs-lookup"><span data-stu-id="7bc53-148">Option</span></span> | <span data-ttu-id="7bc53-149">Details</span><span class="sxs-lookup"><span data-stu-id="7bc53-149">Details</span></span> | <span data-ttu-id="7bc53-150">Standaard</span><span class="sxs-lookup"><span data-stu-id="7bc53-150">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7bc53-151">/q</span><span class="sxs-lookup"><span data-stu-id="7bc53-151">/q</span></span> |<span data-ttu-id="7bc53-152">Stille installatie</span><span class="sxs-lookup"><span data-stu-id="7bc53-152">Quiet installation</span></span> |- |
| <span data-ttu-id="7bc53-153">/ p: 'locatie'</span><span class="sxs-lookup"><span data-stu-id="7bc53-153">/p:"location"</span></span> |<span data-ttu-id="7bc53-154">Pad toohello installatiemap op voor hello Azure backup-agent.</span><span class="sxs-lookup"><span data-stu-id="7bc53-154">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="7bc53-155">C:\Program Files\Microsoft Azure Recovery Services-Agent</span><span class="sxs-lookup"><span data-stu-id="7bc53-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="7bc53-156">/ s: 'locatie'</span><span class="sxs-lookup"><span data-stu-id="7bc53-156">/s:"location"</span></span> |<span data-ttu-id="7bc53-157">Pad toohello cachemap voor hello Azure backup-agent.</span><span class="sxs-lookup"><span data-stu-id="7bc53-157">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="7bc53-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="7bc53-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="7bc53-159">/m</span><span class="sxs-lookup"><span data-stu-id="7bc53-159">/m</span></span> |<span data-ttu-id="7bc53-160">Opt-in tooMicrosoft Update</span><span class="sxs-lookup"><span data-stu-id="7bc53-160">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="7bc53-161">/nu</span><span class="sxs-lookup"><span data-stu-id="7bc53-161">/nu</span></span> |<span data-ttu-id="7bc53-162">Niet controleren op updates nadat de installatie is voltooid</span><span class="sxs-lookup"><span data-stu-id="7bc53-162">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="7bc53-163">/d</span><span class="sxs-lookup"><span data-stu-id="7bc53-163">/d</span></span> |<span data-ttu-id="7bc53-164">Hiermee verwijdert u Microsoft Azure Recovery Services-Agent</span><span class="sxs-lookup"><span data-stu-id="7bc53-164">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="7bc53-165">/pH</span><span class="sxs-lookup"><span data-stu-id="7bc53-165">/ph</span></span> |<span data-ttu-id="7bc53-166">Host-proxyadres</span><span class="sxs-lookup"><span data-stu-id="7bc53-166">Proxy Host Address</span></span> |- |
| <span data-ttu-id="7bc53-167">/PO</span><span class="sxs-lookup"><span data-stu-id="7bc53-167">/po</span></span> |<span data-ttu-id="7bc53-168">Proxy-Host-poortnummer</span><span class="sxs-lookup"><span data-stu-id="7bc53-168">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="7bc53-169">/Pu</span><span class="sxs-lookup"><span data-stu-id="7bc53-169">/pu</span></span> |<span data-ttu-id="7bc53-170">De Proxygebruikersnaam voor de Host</span><span class="sxs-lookup"><span data-stu-id="7bc53-170">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="7bc53-171">/PW</span><span class="sxs-lookup"><span data-stu-id="7bc53-171">/pw</span></span> |<span data-ttu-id="7bc53-172">Proxy-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="7bc53-172">Proxy Password</span></span> |- |

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a><span data-ttu-id="7bc53-173">Registreren van Windows Server of Windows client machine tooa Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="7bc53-173">Registering Windows Server or Windows client machine tooa Recovery Services Vault</span></span>
<span data-ttu-id="7bc53-174">Nadat u Hallo Recovery Services-kluis hebt gemaakt, de nieuwste agent Hallo en Hallo kluisreferenties downloaden en opslaan in een handige locatie zoals C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="7bc53-174">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

<span data-ttu-id="7bc53-175">Voer Hallo op Hallo Windows Server of Windows-clientcomputer [Start OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister Hallo machine met de Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="7bc53-175">On hello Windows Server or Windows client machine, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>
<span data-ttu-id="7bc53-176">Deze en andere cmdlets gebruikt voor back-up, zijn afkomstig van Hallo MSONLINE module welke Mars AgentInstaller toegevoegd als onderdeel van het installatieproces Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bc53-176">This, and other cmdlets used for backup, are from hello MSONLINE module which hello Mars AgentInstaller added as part of hello installation process.</span></span> 

<span data-ttu-id="7bc53-177">het installatieprogramma van Agent Hallo Hallo $Env niet bijgewerkt: PSModulePath variabele.</span><span class="sxs-lookup"><span data-stu-id="7bc53-177">hello Agent installer does not update hello $Env:PSModulePath variable.</span></span> <span data-ttu-id="7bc53-178">Dit betekent dat module automatisch laden is mislukt.</span><span class="sxs-lookup"><span data-stu-id="7bc53-178">This means module auto-load fails.</span></span> <span data-ttu-id="7bc53-179">tooresolve dit kunt u doen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="7bc53-179">tooresolve this you can do hello following:</span></span>

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

<span data-ttu-id="7bc53-180">U kunt ook kunt u handmatig laden Hallo module in uw script als volgt:</span><span class="sxs-lookup"><span data-stu-id="7bc53-180">Alternatively, you can manually load hello module in your script as follows:</span></span>

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

<span data-ttu-id="7bc53-181">Zodra u Hallo Online Backup-cmdlets geladen, kunt u referenties voor de kluis Hallo registreren:</span><span class="sxs-lookup"><span data-stu-id="7bc53-181">Once you load hello Online Backup cmdlets, you register hello vault credentials:</span></span>


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="7bc53-182">Gebruik geen relatieve paden toospecify hello kluisreferentiebestand.</span><span class="sxs-lookup"><span data-stu-id="7bc53-182">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="7bc53-183">U moet een absoluut pad opgeven als een cmdlet invoer toohello.</span><span class="sxs-lookup"><span data-stu-id="7bc53-183">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="7bc53-184">Netwerkinstellingen</span><span class="sxs-lookup"><span data-stu-id="7bc53-184">Networking settings</span></span>
<span data-ttu-id="7bc53-185">Wanneer de connectiviteit Hallo Hallo Windows machine toohello die Internet via een proxyserver is, kunnen Hallo proxy-instellingen ook worden opgegeven toohello agent.</span><span class="sxs-lookup"><span data-stu-id="7bc53-185">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="7bc53-186">In dit voorbeeld is het geen proxyserver zodat we alle informatie met betrekking tot de proxy expliciet wordt gewist.</span><span class="sxs-lookup"><span data-stu-id="7bc53-186">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="7bc53-187">Bandbreedtegebruik kan ook worden beheerd met Hallo opties ```work hour bandwidth``` en ```non-work hour bandwidth``` voor een bepaald aantal dagen van week Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bc53-187">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="7bc53-188">Hallo-proxy en bandbreedte details van de instelling wordt gedaan met behulp van Hallo [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7bc53-188">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="7bc53-189">Versleutelingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="7bc53-189">Encryption settings</span></span>
<span data-ttu-id="7bc53-190">Hallo back-upgegevens verzonden tooAzure back-up is versleutelde tooprotect Hallo vertrouwelijkheid van Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="7bc53-190">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="7bc53-191">Hallo-wachtwoordzin voor versleuteling is Hallo 'password' toodecrypt Hallo gegevens op Hallo moment van terugzetten.</span><span class="sxs-lookup"><span data-stu-id="7bc53-191">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="7bc53-192">Hallo wachtwoordzin gegevens veilig en beveiligd houden als deze eenmaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7bc53-192">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="7bc53-193">U kunt toorestore gegevens van Azure zonder deze wachtwoordzin niet zijn.</span><span class="sxs-lookup"><span data-stu-id="7bc53-193">You are not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="7bc53-194">Back-up maken van bestanden en mappen</span><span class="sxs-lookup"><span data-stu-id="7bc53-194">Back up files and folders</span></span>
<span data-ttu-id="7bc53-195">Alle back-ups van Windows-Servers en clients tooAzure back-up worden geregeld door een beleid.</span><span class="sxs-lookup"><span data-stu-id="7bc53-195">All backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="7bc53-196">Hallo-beleid bestaat uit drie delen:</span><span class="sxs-lookup"><span data-stu-id="7bc53-196">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="7bc53-197">Een **back-upschema** die aangeeft wanneer back-ups moeten toobe gemaakt en gesynchroniseerd met Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="7bc53-197">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="7bc53-198">Een **bewaarschema** die aangeeft hoe lang tooretain Hallo herstelpunten in Azure.</span><span class="sxs-lookup"><span data-stu-id="7bc53-198">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="7bc53-199">Een **opnemen of uitsluiten opgeven van een bestand** die bepaalt wat moet een back-up.</span><span class="sxs-lookup"><span data-stu-id="7bc53-199">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="7bc53-200">In dit document, omdat er bij het automatiseren van back-up, gebruiken we dat er niets is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="7bc53-200">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="7bc53-201">We beginnen met het maken van een nieuwe back-upbeleid Hallo met [nieuw OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bc53-201">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="7bc53-202">Op dit moment Hallo beleid leeg is en andere cmdlets zijn benodigde toodefine welke items worden opgenomen of uitgesloten, wanneer back-ups wordt uitgevoerd en waarbij Hallo back-ups worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7bc53-202">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="7bc53-203">Back-upschema Hallo configureren</span><span class="sxs-lookup"><span data-stu-id="7bc53-203">Configuring hello backup schedule</span></span>
<span data-ttu-id="7bc53-204">eerst Hallo Hallo 3 delen van een beleid is de back-upschema hello, die is gemaakt met een Hallo [nieuw OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bc53-204">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="7bc53-205">back-upschema Hallo definieert wanneer back-ups moeten toobe genomen.</span><span class="sxs-lookup"><span data-stu-id="7bc53-205">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="7bc53-206">Bij het maken van een schema moet u de invoerparameters toospecify 2:</span><span class="sxs-lookup"><span data-stu-id="7bc53-206">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="7bc53-207">**Dagen van week Hallo** Hallo back-up moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7bc53-207">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="7bc53-208">U kunt back-uptaak Hallo op slechts één dag, of elke dag van week hello of een combinatie van daartussen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7bc53-208">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="7bc53-209">**Hallo tijdstippen** wanneer Hallo back-up moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7bc53-209">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="7bc53-210">U kunt definiëren up too3 verschillende tijdstippen Hallo wanneer Hallo back-up wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="7bc53-210">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="7bc53-211">U kunt bijvoorbeeld een back-upbeleid dat wordt uitgevoerd op 4 uur elke zaterdag en zondag configureren.</span><span class="sxs-lookup"><span data-stu-id="7bc53-211">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="7bc53-212">Hallo back-upschema moet toobe die zijn gekoppeld aan een beleid en dit kan worden gerealiseerd met behulp van Hallo [Set OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bc53-212">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="7bc53-213">Een bewaarbeleid configureren</span><span class="sxs-lookup"><span data-stu-id="7bc53-213">Configuring a retention policy</span></span>
<span data-ttu-id="7bc53-214">Hallo bewaarbeleid definieert hoe lang herstel die zijn gemaakt vanuit een back-uptaken worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="7bc53-214">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="7bc53-215">Bij het maken van een nieuw bewaarbeleid Hallo met [nieuw OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, kunt u opgeven aantal dagen dat de back-up herstelpunten Hallo Hallo moet toobe behouden met Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="7bc53-215">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="7bc53-216">Hallo in het volgende voorbeeld wordt een bewaarbeleid van 7 dagen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7bc53-216">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="7bc53-217">Hallo bewaarbeleid moet worden gekoppeld met de belangrijkste Hallo-beleid met de cmdlet Hallo [Set OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="7bc53-217">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="7bc53-218">Opnemen en uitsluiten van bestanden toobe back-up</span><span class="sxs-lookup"><span data-stu-id="7bc53-218">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="7bc53-219">Een ```OBFileSpec``` object definieert Hallo bestanden toobe opgenomen en uitgesloten van een back-up.</span><span class="sxs-lookup"><span data-stu-id="7bc53-219">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="7bc53-220">Dit is een reeks regels dat bereik uit Hallo bestanden en mappen op een computer beveiligde.</span><span class="sxs-lookup"><span data-stu-id="7bc53-220">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="7bc53-221">U kunt als veel bestand opgenomen of uitgesloten regels zoals vereist en deze koppelen aan een beleid hebben.</span><span class="sxs-lookup"><span data-stu-id="7bc53-221">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="7bc53-222">Wanneer u een nieuw OBFileSpec-object maakt, kunt u:</span><span class="sxs-lookup"><span data-stu-id="7bc53-222">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="7bc53-223">Hallo-bestanden en mappen toobe opgenomen opgeven</span><span class="sxs-lookup"><span data-stu-id="7bc53-223">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="7bc53-224">Hallo-bestanden en mappen toobe uitgesloten opgeven</span><span class="sxs-lookup"><span data-stu-id="7bc53-224">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="7bc53-225">Geef recursieve back-up van gegevens in een map (of) of op het hoogste niveau bestanden alleen Hallo in de opgegeven map Hallo een back-.</span><span class="sxs-lookup"><span data-stu-id="7bc53-225">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="7bc53-226">Hallo laatstgenoemde wordt bereikt door middel van Hallo - niet-recursieve vlag in Hallo nieuw OBFileSpec-opdracht.</span><span class="sxs-lookup"><span data-stu-id="7bc53-226">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="7bc53-227">In onderstaande Hallo voorbeeld, we back-up volume C: en D: en Hallo OS binaire bestanden in de map Windows hello en tijdelijke mappen uitsluiten.</span><span class="sxs-lookup"><span data-stu-id="7bc53-227">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="7bc53-228">toodo zodat maken we twee bestandsspecificaties Hallo met [nieuw OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - één voor insluiting en één voor uitsluiting.</span><span class="sxs-lookup"><span data-stu-id="7bc53-228">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="7bc53-229">Zodra het Hallo-bestandsspecificaties zijn gemaakt, deze zijn gekoppeld aan Hallo beleid met behulp van Hallo [toevoegen OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bc53-229">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-hello-policy"></a><span data-ttu-id="7bc53-230">Hallo-beleid wordt toegepast</span><span class="sxs-lookup"><span data-stu-id="7bc53-230">Applying hello policy</span></span>
<span data-ttu-id="7bc53-231">Nu Hallo group policy object is voltooid en heeft een bijbehorende back-upschema, bewaarbeleid en een lijst opnemen of uitsluiten van bestanden.</span><span class="sxs-lookup"><span data-stu-id="7bc53-231">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="7bc53-232">Dit beleid kan nu worden toegezegd voor Azure Backup toouse.</span><span class="sxs-lookup"><span data-stu-id="7bc53-232">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="7bc53-233">Voordat u nieuwe Hallo toepassen beleid Zorg ervoor dat er geen bestaande back-upbeleid gekoppeld aan Hallo-server met behulp van Hallo [verwijderen OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bc53-233">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="7bc53-234">Verwijderen van het Hallo-beleid wordt om bevestiging gevraagd.</span><span class="sxs-lookup"><span data-stu-id="7bc53-234">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="7bc53-235">bevestiging van tooskip hello gebruiken Hallo ```-Confirm:$false``` vlag met Hallo-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bc53-235">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="7bc53-236">Hallo group policy object doorvoeren wordt gedaan met behulp van Hallo [Set OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bc53-236">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="7bc53-237">Dit wordt ook gevraagd om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="7bc53-237">This will also ask for confirmation.</span></span> <span data-ttu-id="7bc53-238">bevestiging van tooskip hello gebruiken Hallo ```-Confirm:$false``` vlag met Hallo-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bc53-238">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

<span data-ttu-id="7bc53-239">U kunt details Hallo Hallo bestaande back-upbeleid met Hallo weergeven [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bc53-239">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="7bc53-240">U kunt inzoomen verder met Hallo [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet voor back-upschema Hallo en Hallo [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet voor het bewaarbeleid Hallo</span><span class="sxs-lookup"><span data-stu-id="7bc53-240">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="7bc53-241">Een ad-hoc back-up maken</span><span class="sxs-lookup"><span data-stu-id="7bc53-241">Performing an ad-hoc backup</span></span>
<span data-ttu-id="7bc53-242">Wanneer een back-upbeleid is ingesteld Hallo back-ups per Hallo schema uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7bc53-242">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="7bc53-243">Activering van een ad-hoc back-up is ook mogelijk met behulp van Hallo [Start OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7bc53-243">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing hello metadata VHD...
Data transfer is in progress. It might take longer since it is hello first backup and all data needs toobe transferred...
Data transfer completed and all backed up data is in hello cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="7bc53-244">Gegevens terugzetten vanuit Azure Backup</span><span class="sxs-lookup"><span data-stu-id="7bc53-244">Restore data from Azure Backup</span></span>
<span data-ttu-id="7bc53-245">Deze sectie leidt u door Hallo stappen voor het automatiseren van herstel van gegevens vanuit Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="7bc53-245">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="7bc53-246">Dit omvat dus Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7bc53-246">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="7bc53-247">Kies het bronvolume Hallo</span><span class="sxs-lookup"><span data-stu-id="7bc53-247">Pick hello source volume</span></span>
2. <span data-ttu-id="7bc53-248">Kies een back-punt toorestore</span><span class="sxs-lookup"><span data-stu-id="7bc53-248">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="7bc53-249">Kies een item toorestore</span><span class="sxs-lookup"><span data-stu-id="7bc53-249">Choose an item toorestore</span></span>
4. <span data-ttu-id="7bc53-250">Trigger Hallo herstelproces</span><span class="sxs-lookup"><span data-stu-id="7bc53-250">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="7bc53-251">Hallo bronvolume verzamelen</span><span class="sxs-lookup"><span data-stu-id="7bc53-251">Picking hello source volume</span></span>
<span data-ttu-id="7bc53-252">In de volgorde toorestore een item uit Azure Backup moet u eerst tooidentify Hallo bron van Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="7bc53-252">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="7bc53-253">Aangezien we Hallo opdrachten in de context van een Windows-Server of een Windows-client hello uitvoeren je, is al Hallo machine geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="7bc53-253">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="7bc53-254">volgende stap bij het identificeren van bron Hallo Hallo is tooidentify Hallo volume met het.</span><span class="sxs-lookup"><span data-stu-id="7bc53-254">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="7bc53-255">Een lijst van volumes of bronnen wordt een back-up van deze computer kan worden opgehaald door het uitvoeren van Hallo [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bc53-255">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="7bc53-256">Met deze opdracht retourneert een matrix van alle Hallo bronnen back-up van deze server /-client.</span><span class="sxs-lookup"><span data-stu-id="7bc53-256">This command returns an array of all hello sources backed up from this server/client.</span></span>

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-from-which-toorestore"></a><span data-ttu-id="7bc53-257">Een back-uppunt kiezen in welke toorestore</span><span class="sxs-lookup"><span data-stu-id="7bc53-257">Choosing a backup point from which toorestore</span></span>
<span data-ttu-id="7bc53-258">U een lijst met back-uppunten door het uitvoeren van Hallo ophalen [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet met de juiste parameters.</span><span class="sxs-lookup"><span data-stu-id="7bc53-258">You retreive a list of backup points by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="7bc53-259">In ons voorbeeld kiest Hallo meest recente back-punt voor het bronvolume Hallo *D:* en gebruik deze toorecover een specifiek bestand.</span><span class="sxs-lookup"><span data-stu-id="7bc53-259">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
<span data-ttu-id="7bc53-260">Hallo-object ```$rps``` is een matrix met back-uppunten.</span><span class="sxs-lookup"><span data-stu-id="7bc53-260">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="7bc53-261">Hallo eerste element is het laatste herstelpunt Hallo en ne Hallo-element is Hallo oudste punt.</span><span class="sxs-lookup"><span data-stu-id="7bc53-261">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="7bc53-262">toochoose hello laatste herstelpunt, gebruiken we ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="7bc53-262">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="7bc53-263">Een item toorestore kiezen</span><span class="sxs-lookup"><span data-stu-id="7bc53-263">Choosing an item toorestore</span></span>
<span data-ttu-id="7bc53-264">tooidentify hello exacte bestand of map toorestore, recursief hello gebruiken [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bc53-264">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="7bc53-265">Die hiërarchie manier Hallo map kan worden gebladerd uitsluitend met Hallo ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="7bc53-265">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="7bc53-266">In dit voorbeeld als we toorestore Hallo bestand wilt *finances.xls* we kan verwijzen naar dat als u met Hallo object ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="7bc53-266">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

<span data-ttu-id="7bc53-267">U kunt ook zoeken naar items toorestore met Hallo ```Get-OBRecoverableItem``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bc53-267">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="7bc53-268">In ons voorbeeld toosearch voor *finances.xls* we kan een ingang krijgen op Hallo-bestand door deze opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="7bc53-268">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="7bc53-269">Activerende Hallo herstelproces</span><span class="sxs-lookup"><span data-stu-id="7bc53-269">Triggering hello restore process</span></span>
<span data-ttu-id="7bc53-270">tootrigger hello herstelproces, moeten we eerst toospecify Hallo herstelopties.</span><span class="sxs-lookup"><span data-stu-id="7bc53-270">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="7bc53-271">Dit kan worden gedaan met behulp van Hallo [nieuw OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bc53-271">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="7bc53-272">In dit voorbeeld gaan we ervan uit dat we toorestore Hallo bestanden te willen*C:\temp*. Laten we ook uitgaan dat we willen tooskip bestanden die al aanwezig op de doelmap Hallo *C:\temp*. toocreate dergelijke een hersteloptie Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7bc53-272">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="7bc53-273">Hallo herstelproces nu te activeren met behulp van Hallo [Start OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) opdracht op Hallo geselecteerd ```$item``` van uitvoer Hallo Hallo ```Get-OBRecoverableItem``` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7bc53-273">Now trigger hello restore process by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="7bc53-274">Hello Azure backup-agent verwijderen</span><span class="sxs-lookup"><span data-stu-id="7bc53-274">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="7bc53-275">Verwijderen hello Azure backup-agent kan worden gedaan met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="7bc53-275">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="7bc53-276">Hallo agent binaire bestanden verwijderen van de machine Hallo heeft enkele tooconsider gevolgen:</span><span class="sxs-lookup"><span data-stu-id="7bc53-276">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="7bc53-277">Hallo-bestandsfilter uit Hallo machine wordt verwijderd en bijhouden van wijzigingen is gestopt.</span><span class="sxs-lookup"><span data-stu-id="7bc53-277">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="7bc53-278">Alle beleidsgegevens van Hallo machine wordt verwijderd, maar Hallo beleidsgegevens blijft toobe opgeslagen in het Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="7bc53-278">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="7bc53-279">Alle back-upschema's worden verwijderd en er is geen verdere back-ups worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7bc53-279">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="7bc53-280">Echter gegevens die zijn opgeslagen in Azure blijft Hallo en door u aan de hand van Hallo bewaren beleid setup wordt bewaard.</span><span class="sxs-lookup"><span data-stu-id="7bc53-280">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="7bc53-281">Oudere punten worden automatisch verouderde.</span><span class="sxs-lookup"><span data-stu-id="7bc53-281">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="7bc53-282">Extern beheer</span><span class="sxs-lookup"><span data-stu-id="7bc53-282">Remote management</span></span>
<span data-ttu-id="7bc53-283">Alle Hallo management rond hello Azure backup-agent, beleid en gegevensbronnen kan op afstand worden uitgevoerd via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7bc53-283">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="7bc53-284">Hallo-machine die op afstand worden beheerd moet toobe correct voorbereid.</span><span class="sxs-lookup"><span data-stu-id="7bc53-284">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="7bc53-285">Hallo WinRM-service is standaard geconfigureerd voor handmatig opstarten.</span><span class="sxs-lookup"><span data-stu-id="7bc53-285">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="7bc53-286">Opstarttype Hello te moet worden ingesteld*automatische* en Hallo-service moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="7bc53-286">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="7bc53-287">tooverify die Hallo WinRM-service wordt uitgevoerd, Hallo-waarde van de eigenschap Status Hallo moet *met*.</span><span class="sxs-lookup"><span data-stu-id="7bc53-287">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="7bc53-288">PowerShell moet worden geconfigureerd voor externe toegang.</span><span class="sxs-lookup"><span data-stu-id="7bc53-288">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="7bc53-289">Hallo-machine kan nu worden beheerd op afstand - van Hallo Hallo agent-installatie wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="7bc53-289">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="7bc53-290">Bijvoorbeeld, Hallo script volgen Hallo agent toohello externe computer worden gekopieerd en installeert deze.</span><span class="sxs-lookup"><span data-stu-id="7bc53-290">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="7bc53-291">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7bc53-291">Next steps</span></span>
<span data-ttu-id="7bc53-292">Voor meer informatie over Azure Backup voor Windows Server /-Client, Zie</span><span class="sxs-lookup"><span data-stu-id="7bc53-292">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="7bc53-293">Inleiding tooAzure back-up</span><span class="sxs-lookup"><span data-stu-id="7bc53-293">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="7bc53-294">Back-up van Windows-Servers</span><span class="sxs-lookup"><span data-stu-id="7bc53-294">Back up Windows Servers</span></span>](backup-configure-vault.md)
