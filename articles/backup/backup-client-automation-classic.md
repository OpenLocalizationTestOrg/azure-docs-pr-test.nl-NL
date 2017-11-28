---
title: aaaUse PowerShell toomanage Windows Server back-ups in Azure | Microsoft Docs
description: Implementeren en beheren van Windows Server back-ups met behulp van PowerShell.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: e7e269e2-1f11-41a9-957b-a2155de6a1e0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: saurse;markgal;nkolli;trinadhk
ms.openlocfilehash: 72292e510b0f059102440bd49a195be4ef700a6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="1ac65-103">Implementeren en beheren van back-tooAzure voor Windows Server/Windows-clients met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ac65-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ac65-104">ARM</span><span class="sxs-lookup"><span data-stu-id="1ac65-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="1ac65-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="1ac65-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="1ac65-106">Dit artikel wordt uitgelegd hoe toouse PowerShell tooback van Windows Server of Windows workstation gegevens tooa back-up kluis.</span><span class="sxs-lookup"><span data-stu-id="1ac65-106">This article explains how toouse PowerShell tooback up Windows Server or Windows workstation data tooa backup vault.</span></span> <span data-ttu-id="1ac65-107">Microsoft raadt u aan met behulp van de Recovery Services-kluizen voor alle nieuwe implementaties.</span><span class="sxs-lookup"><span data-stu-id="1ac65-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="1ac65-108">Als u een nieuwe gebruiker in de Azure Backup en niet een back-upkluis in uw abonnement hebt gemaakt, gebruikt u Hallo artikel [implementeren en beheren van Data Protection Manager gegevens tooAzure met behulp van PowerShell](backup-client-automation.md) zodat u uw gegevens in een Recovery Services-kluis opslaat.</span><span class="sxs-lookup"><span data-stu-id="1ac65-108">If you are a new Azure Backup user and have not created a backup vault in your subscription, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-client-automation.md) so you store your data in a Recovery Services vault.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1ac65-109">U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden.</span><span class="sxs-lookup"><span data-stu-id="1ac65-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="1ac65-110">Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="1ac65-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="1ac65-111">Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="1ac65-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="1ac65-112">U kunt PowerShell toocreate Backup-kluizen niet gebruiken na 15 oktober 2017.</span><span class="sxs-lookup"><span data-stu-id="1ac65-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="1ac65-113">**Per 1 november 2017**:</span><span class="sxs-lookup"><span data-stu-id="1ac65-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="1ac65-114">Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="1ac65-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="1ac65-115">U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="1ac65-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="1ac65-116">In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="1ac65-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="install-azure-powershell"></a><span data-ttu-id="1ac65-117">Azure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="1ac65-117">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="1ac65-118">In oktober 2015 is Azure PowerShell 1.0 uitgebracht.</span><span class="sxs-lookup"><span data-stu-id="1ac65-118">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="1ac65-119">Deze release Hallo 0.9.8 release is voltooid en over een aantal belangrijke wijzigingen, met name in Hallo naamgevingspatroon Hallo-cmdlets worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="1ac65-119">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="1ac65-120">1.0 cmdlets volgen Hallo naamgevingspatroon {werkwoord}-AzureRm {zelfstandig naamwoord}; terwijl Hallo 0.9.8 namen geen bevatten **Rm** (bijvoorbeeld New-AzureRmResourceGroup in plaats van New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="1ac65-120">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="1ac65-121">Wanneer u Azure PowerShell 0.9.8 gebruikt, moet u eerst Hallo Resource Manager-modus inschakelen door het uitvoeren van Hallo **Switch Azure AzureResourceManager** opdracht.</span><span class="sxs-lookup"><span data-stu-id="1ac65-121">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="1ac65-122">Met deze opdracht hoeft niet in 1.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="1ac65-122">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="1ac65-123">Als u wilt dat toouse uw scripts die zijn geschreven voor Hallo 0.9.8-omgeving in Hallo 1.0 of hoger omgeving, moet u zorgvuldig testen Hallo scripts in een testomgeving voordat u ze in productie tooavoid onverwachte impact.</span><span class="sxs-lookup"><span data-stu-id="1ac65-123">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="1ac65-124">[Download de meest recente PowerShell-versie Hallo](https://github.com/Azure/azure-powershell/releases) (minimaal vereiste versie is: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="1ac65-124">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="1ac65-125">Een back-upkluis maken</span><span class="sxs-lookup"><span data-stu-id="1ac65-125">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="1ac65-126">Voor klanten die gebruikmaken van Azure Backup voor Hallo eerst, moet u tooregister hello Azure Backup-provider toobe gebruikt met uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="1ac65-126">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="1ac65-127">Dit kan worden gedaan door het uitvoeren van de volgende opdracht Hallo: Register AzureProvider - ProviderNamespace 'Microsoft.Backup'</span><span class="sxs-lookup"><span data-stu-id="1ac65-127">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="1ac65-128">U kunt een nieuwe back-upkluis met Hallo maken **nieuw AzureRMBackupVault** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ac65-128">You can create a new backup vault using hello **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="1ac65-129">Hallo back-upkluis is een ARM-bron, dus u tooplace moet deze binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="1ac65-129">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="1ac65-130">Voer Hallo volgende opdrachten in een verhoogde Azure PowerShell-console:</span><span class="sxs-lookup"><span data-stu-id="1ac65-130">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="1ac65-131">Gebruik Hallo **Get-AzureRMBackupVault** cmdlet toolist Hallo backup-kluizen in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="1ac65-131">Use hello **Get-AzureRMBackupVault** cmdlet toolist hello backup vaults in a subscription.</span></span>

## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="1ac65-132">Hello Azure backup-agent installeren</span><span class="sxs-lookup"><span data-stu-id="1ac65-132">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="1ac65-133">Voordat u hello Azure backup-agent hebt geïnstalleerd, moet u toohave Hallo installatieprogramma gedownload en aanwezig is op Hallo van Windows Server.</span><span class="sxs-lookup"><span data-stu-id="1ac65-133">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="1ac65-134">U kunt de nieuwste versie van de Hallo van Hallo installer krijgen van Hallo [Microsoft Download Center](http://aka.ms/azurebackup_agent) of van de dashboardpagina Hallo back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="1ac65-134">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="1ac65-135">Hallo-installatieprogramma opslaan tooan toegankelijke locatie zoals * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="1ac65-135">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="1ac65-136">tooinstall Hallo agent uitvoeren Hallo volgende opdracht in een PowerShell-console met verhoogde bevoegdheid:</span><span class="sxs-lookup"><span data-stu-id="1ac65-136">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="1ac65-137">Dit met alle standaardopties voor Hallo Hallo-agent hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1ac65-137">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="1ac65-138">Hallo installatie duurt een paar minuten op Hallo achtergrond.</span><span class="sxs-lookup"><span data-stu-id="1ac65-138">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="1ac65-139">Als u geen Hallo opgeeft */nu* optie vervolgens Hallo **Windows Update** venster wordt geopend na Hallo Hallo installatie toocheck voor eventuele updates.</span><span class="sxs-lookup"><span data-stu-id="1ac65-139">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="1ac65-140">Wanneer is geïnstalleerd, weergegeven Hallo agent in Hallo lijst met geïnstalleerde programma's.</span><span class="sxs-lookup"><span data-stu-id="1ac65-140">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="1ac65-141">toosee hello lijst met geïnstalleerde programma's, gaat u te**Configuratiescherm** > **programma's** > **programma's en onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="1ac65-141">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent is geïnstalleerd](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="1ac65-143">Opties voor de installatie</span><span class="sxs-lookup"><span data-stu-id="1ac65-143">Installation options</span></span>
<span data-ttu-id="1ac65-144">alle opties die beschikbaar zijn via Hallo toosee Hallo opdrachtregelprogramma, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="1ac65-144">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="1ac65-145">Hallo beschikbare opties zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="1ac65-145">hello available options include:</span></span>

| <span data-ttu-id="1ac65-146">Optie</span><span class="sxs-lookup"><span data-stu-id="1ac65-146">Option</span></span> | <span data-ttu-id="1ac65-147">Details</span><span class="sxs-lookup"><span data-stu-id="1ac65-147">Details</span></span> | <span data-ttu-id="1ac65-148">Standaard</span><span class="sxs-lookup"><span data-stu-id="1ac65-148">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1ac65-149">/q</span><span class="sxs-lookup"><span data-stu-id="1ac65-149">/q</span></span> |<span data-ttu-id="1ac65-150">Stille installatie</span><span class="sxs-lookup"><span data-stu-id="1ac65-150">Quiet installation</span></span> |- |
| <span data-ttu-id="1ac65-151">/ p: 'locatie'</span><span class="sxs-lookup"><span data-stu-id="1ac65-151">/p:"location"</span></span> |<span data-ttu-id="1ac65-152">Pad toohello installatiemap op voor hello Azure backup-agent.</span><span class="sxs-lookup"><span data-stu-id="1ac65-152">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="1ac65-153">C:\Program Files\Microsoft Azure Recovery Services-Agent</span><span class="sxs-lookup"><span data-stu-id="1ac65-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="1ac65-154">/ s: 'locatie'</span><span class="sxs-lookup"><span data-stu-id="1ac65-154">/s:"location"</span></span> |<span data-ttu-id="1ac65-155">Pad toohello cachemap voor hello Azure backup-agent.</span><span class="sxs-lookup"><span data-stu-id="1ac65-155">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="1ac65-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="1ac65-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="1ac65-157">/m</span><span class="sxs-lookup"><span data-stu-id="1ac65-157">/m</span></span> |<span data-ttu-id="1ac65-158">Opt-in tooMicrosoft Update</span><span class="sxs-lookup"><span data-stu-id="1ac65-158">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="1ac65-159">/nu</span><span class="sxs-lookup"><span data-stu-id="1ac65-159">/nu</span></span> |<span data-ttu-id="1ac65-160">Niet controleren op updates nadat de installatie is voltooid</span><span class="sxs-lookup"><span data-stu-id="1ac65-160">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="1ac65-161">/d</span><span class="sxs-lookup"><span data-stu-id="1ac65-161">/d</span></span> |<span data-ttu-id="1ac65-162">Hiermee verwijdert u Microsoft Azure Recovery Services-Agent</span><span class="sxs-lookup"><span data-stu-id="1ac65-162">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="1ac65-163">/pH</span><span class="sxs-lookup"><span data-stu-id="1ac65-163">/ph</span></span> |<span data-ttu-id="1ac65-164">Host-proxyadres</span><span class="sxs-lookup"><span data-stu-id="1ac65-164">Proxy Host Address</span></span> |- |
| <span data-ttu-id="1ac65-165">/PO</span><span class="sxs-lookup"><span data-stu-id="1ac65-165">/po</span></span> |<span data-ttu-id="1ac65-166">Proxy-Host-poortnummer</span><span class="sxs-lookup"><span data-stu-id="1ac65-166">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="1ac65-167">/Pu</span><span class="sxs-lookup"><span data-stu-id="1ac65-167">/pu</span></span> |<span data-ttu-id="1ac65-168">De Proxygebruikersnaam voor de Host</span><span class="sxs-lookup"><span data-stu-id="1ac65-168">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="1ac65-169">/PW</span><span class="sxs-lookup"><span data-stu-id="1ac65-169">/pw</span></span> |<span data-ttu-id="1ac65-170">Proxy-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="1ac65-170">Proxy Password</span></span> |- |

## <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="1ac65-171">Registreren bij hello Azure Backup-service</span><span class="sxs-lookup"><span data-stu-id="1ac65-171">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="1ac65-172">Voordat u met hello Azure Backup-service registreren kunt, moet u tooensure die Hallo [vereisten](backup-configure-vault.md) wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="1ac65-172">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="1ac65-173">U moet doen:</span><span class="sxs-lookup"><span data-stu-id="1ac65-173">You must:</span></span>

* <span data-ttu-id="1ac65-174">Een geldige Azure-abonnement hebt</span><span class="sxs-lookup"><span data-stu-id="1ac65-174">Have a valid Azure subscription</span></span>
* <span data-ttu-id="1ac65-175">Hebt u een back-upkluis</span><span class="sxs-lookup"><span data-stu-id="1ac65-175">Have a backup vault</span></span>

<span data-ttu-id="1ac65-176">toodownload hello kluisreferenties, Voer Hallo **Get-AzureRMBackupVaultCredentials** cmdlet in een Azure PowerShell-console en opslaan in een handige locatie, zoals * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="1ac65-176">toodownload hello vault credentials, run hello **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="1ac65-177">Registreren Hallo-machine met de Hallo kluis wordt gedaan met behulp van Hallo [Start OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1ac65-177">Registering hello machine with hello vault is done using hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration -VaultCredentials $cred -Confirm:$false

CertThumbprint      : 7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName : test-vault
Region              : West US

Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="1ac65-178">Gebruik geen relatieve paden toospecify hello kluisreferentiebestand.</span><span class="sxs-lookup"><span data-stu-id="1ac65-178">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="1ac65-179">U moet een absoluut pad opgeven als een cmdlet invoer toohello.</span><span class="sxs-lookup"><span data-stu-id="1ac65-179">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="1ac65-180">Netwerkinstellingen</span><span class="sxs-lookup"><span data-stu-id="1ac65-180">Networking settings</span></span>
<span data-ttu-id="1ac65-181">Wanneer de connectiviteit Hallo Hallo Windows machine toohello die Internet via een proxyserver is, kunnen Hallo proxy-instellingen ook worden opgegeven toohello agent.</span><span class="sxs-lookup"><span data-stu-id="1ac65-181">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="1ac65-182">In dit voorbeeld is het geen proxyserver zodat we alle informatie met betrekking tot de proxy expliciet wordt gewist.</span><span class="sxs-lookup"><span data-stu-id="1ac65-182">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="1ac65-183">Bandbreedtegebruik kan ook worden beheerd met Hallo opties ```work hour bandwidth``` en ```non-work hour bandwidth``` voor een bepaald aantal dagen van week Hallo.</span><span class="sxs-lookup"><span data-stu-id="1ac65-183">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="1ac65-184">Hallo-proxy en bandbreedte details van de instelling wordt gedaan met behulp van Hallo [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1ac65-184">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="1ac65-185">Versleutelingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="1ac65-185">Encryption settings</span></span>
<span data-ttu-id="1ac65-186">Hallo back-upgegevens verzonden tooAzure back-up is versleutelde tooprotect Hallo vertrouwelijkheid van Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="1ac65-186">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="1ac65-187">Hallo-wachtwoordzin voor versleuteling is Hallo 'password' toodecrypt Hallo gegevens op Hallo moment van terugzetten.</span><span class="sxs-lookup"><span data-stu-id="1ac65-187">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="1ac65-188">Hallo wachtwoordzin gegevens veilig en beveiligd houden als deze eenmaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1ac65-188">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="1ac65-189">U zich niet kunnen toorestore gegevens van Azure zonder deze wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="1ac65-189">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="1ac65-190">Back-up maken van bestanden en mappen</span><span class="sxs-lookup"><span data-stu-id="1ac65-190">Back up files and folders</span></span>
<span data-ttu-id="1ac65-191">Alle uw back-ups van Windows-Servers en clients tooAzure back-up worden geregeld door een beleid.</span><span class="sxs-lookup"><span data-stu-id="1ac65-191">All your backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="1ac65-192">Hallo-beleid bestaat uit drie delen:</span><span class="sxs-lookup"><span data-stu-id="1ac65-192">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="1ac65-193">Een **back-upschema** die aangeeft wanneer back-ups moeten toobe gemaakt en gesynchroniseerd met Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="1ac65-193">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="1ac65-194">Een **bewaarschema** die aangeeft hoe lang tooretain Hallo herstelpunten in Azure.</span><span class="sxs-lookup"><span data-stu-id="1ac65-194">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="1ac65-195">Een **opnemen of uitsluiten opgeven van een bestand** die bepaalt wat moet een back-up.</span><span class="sxs-lookup"><span data-stu-id="1ac65-195">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="1ac65-196">In dit document, omdat er bij het automatiseren van back-up, gebruiken we dat er niets is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1ac65-196">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="1ac65-197">We beginnen met het maken van een nieuwe back-upbeleid Hallo met [nieuw OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet en het gebruik van maken.</span><span class="sxs-lookup"><span data-stu-id="1ac65-197">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="1ac65-198">Op dit moment Hallo beleid leeg is en andere cmdlets zijn benodigde toodefine welke items worden opgenomen of uitgesloten, wanneer back-ups wordt uitgevoerd en waarbij Hallo back-ups worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1ac65-198">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="1ac65-199">Back-upschema Hallo configureren</span><span class="sxs-lookup"><span data-stu-id="1ac65-199">Configuring hello backup schedule</span></span>
<span data-ttu-id="1ac65-200">eerst Hallo Hallo 3 delen van een beleid is de back-upschema hello, die is gemaakt met een Hallo [nieuw OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ac65-200">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="1ac65-201">back-upschema Hallo definieert wanneer back-ups moeten toobe genomen.</span><span class="sxs-lookup"><span data-stu-id="1ac65-201">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="1ac65-202">Bij het maken van een schema moet u de invoerparameters toospecify 2:</span><span class="sxs-lookup"><span data-stu-id="1ac65-202">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="1ac65-203">**Dagen van week Hallo** Hallo back-up moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1ac65-203">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="1ac65-204">U kunt back-uptaak Hallo op slechts één dag, of elke dag van week hello of een combinatie van daartussen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1ac65-204">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="1ac65-205">**Hallo tijdstippen** wanneer Hallo back-up moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1ac65-205">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="1ac65-206">U kunt definiëren up too3 verschillende tijdstippen Hallo wanneer Hallo back-up wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="1ac65-206">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="1ac65-207">U kunt bijvoorbeeld een back-upbeleid dat wordt uitgevoerd op 4 uur elke zaterdag en zondag configureren.</span><span class="sxs-lookup"><span data-stu-id="1ac65-207">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="1ac65-208">Hallo back-upschema moet toobe die zijn gekoppeld aan een beleid en dit kan worden gerealiseerd met behulp van Hallo [Set OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ac65-208">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="1ac65-209">Een bewaarbeleid configureren</span><span class="sxs-lookup"><span data-stu-id="1ac65-209">Configuring a retention policy</span></span>
<span data-ttu-id="1ac65-210">Hallo bewaarbeleid definieert hoe lang herstel die zijn gemaakt vanuit een back-uptaken worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="1ac65-210">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="1ac65-211">Bij het maken van een nieuw bewaarbeleid Hallo met [nieuw OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, kunt u opgeven aantal dagen dat de back-up herstelpunten Hallo Hallo moet toobe behouden met Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="1ac65-211">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="1ac65-212">Hallo in het volgende voorbeeld wordt een bewaarbeleid van 7 dagen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1ac65-212">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="1ac65-213">Hallo bewaarbeleid moet worden gekoppeld met de belangrijkste Hallo-beleid met de cmdlet Hallo [Set OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="1ac65-213">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="1ac65-214">Opnemen en uitsluiten van bestanden toobe back-up</span><span class="sxs-lookup"><span data-stu-id="1ac65-214">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="1ac65-215">Een ```OBFileSpec``` object definieert Hallo bestanden toobe opgenomen en uitgesloten van een back-up.</span><span class="sxs-lookup"><span data-stu-id="1ac65-215">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="1ac65-216">Dit is een reeks regels dat bereik uit Hallo bestanden en mappen op een computer beveiligde.</span><span class="sxs-lookup"><span data-stu-id="1ac65-216">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="1ac65-217">U kunt als veel bestand opgenomen of uitgesloten regels zoals vereist en deze koppelen aan een beleid hebben.</span><span class="sxs-lookup"><span data-stu-id="1ac65-217">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="1ac65-218">Wanneer u een nieuw OBFileSpec-object maakt, kunt u:</span><span class="sxs-lookup"><span data-stu-id="1ac65-218">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="1ac65-219">Hallo-bestanden en mappen toobe opgenomen opgeven</span><span class="sxs-lookup"><span data-stu-id="1ac65-219">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="1ac65-220">Hallo-bestanden en mappen toobe uitgesloten opgeven</span><span class="sxs-lookup"><span data-stu-id="1ac65-220">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="1ac65-221">Geef recursieve back-up van gegevens in een map (of) of op het hoogste niveau bestanden alleen Hallo in de opgegeven map Hallo een back-.</span><span class="sxs-lookup"><span data-stu-id="1ac65-221">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="1ac65-222">Hallo laatstgenoemde wordt bereikt door middel van Hallo - niet-recursieve vlag in Hallo nieuw OBFileSpec-opdracht.</span><span class="sxs-lookup"><span data-stu-id="1ac65-222">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="1ac65-223">In onderstaande Hallo voorbeeld, we back-up volume C: en D: en Hallo OS binaire bestanden in de map Windows hello en tijdelijke mappen uitsluiten.</span><span class="sxs-lookup"><span data-stu-id="1ac65-223">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="1ac65-224">toodo zodat maken we twee bestandsspecificaties Hallo met [nieuw OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - één voor insluiting en één voor uitsluiting.</span><span class="sxs-lookup"><span data-stu-id="1ac65-224">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="1ac65-225">Zodra het Hallo-bestandsspecificaties zijn gemaakt, deze zijn gekoppeld aan Hallo beleid met behulp van Hallo [toevoegen OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ac65-225">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-hello-policy"></a><span data-ttu-id="1ac65-226">Hallo-beleid wordt toegepast</span><span class="sxs-lookup"><span data-stu-id="1ac65-226">Applying hello policy</span></span>
<span data-ttu-id="1ac65-227">Nu Hallo group policy object is voltooid en heeft een bijbehorende back-upschema, bewaarbeleid en een lijst opnemen of uitsluiten van bestanden.</span><span class="sxs-lookup"><span data-stu-id="1ac65-227">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="1ac65-228">Dit beleid kan nu worden toegezegd voor Azure Backup toouse.</span><span class="sxs-lookup"><span data-stu-id="1ac65-228">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="1ac65-229">Voordat u nieuwe Hallo toepassen beleid Zorg ervoor dat er geen bestaande back-upbeleid gekoppeld aan Hallo-server met behulp van Hallo [verwijderen OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ac65-229">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="1ac65-230">Verwijderen van het Hallo-beleid wordt om bevestiging gevraagd.</span><span class="sxs-lookup"><span data-stu-id="1ac65-230">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="1ac65-231">bevestiging van tooskip hello gebruiken Hallo ```-Confirm:$false``` vlag met Hallo-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ac65-231">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="1ac65-232">Hallo group policy object doorvoeren wordt gedaan met behulp van Hallo [Set OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ac65-232">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="1ac65-233">Dit wordt ook gevraagd om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="1ac65-233">This will also ask for confirmation.</span></span> <span data-ttu-id="1ac65-234">bevestiging van tooskip hello gebruiken Hallo ```-Confirm:$false``` vlag met Hallo-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ac65-234">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

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

<span data-ttu-id="1ac65-235">U kunt details Hallo Hallo bestaande back-upbeleid met Hallo weergeven [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ac65-235">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="1ac65-236">U kunt inzoomen verder met Hallo [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet voor back-upschema Hallo en Hallo [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet voor het bewaarbeleid Hallo</span><span class="sxs-lookup"><span data-stu-id="1ac65-236">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="1ac65-237">Een ad-hoc back-up maken</span><span class="sxs-lookup"><span data-stu-id="1ac65-237">Performing an ad-hoc backup</span></span>
<span data-ttu-id="1ac65-238">Wanneer een back-upbeleid is ingesteld Hallo back-ups per Hallo schema uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1ac65-238">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="1ac65-239">Activering van een ad-hoc back-up is ook mogelijk met behulp van Hallo [Start OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1ac65-239">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="1ac65-240">Gegevens terugzetten vanuit Azure Backup</span><span class="sxs-lookup"><span data-stu-id="1ac65-240">Restore data from Azure Backup</span></span>
<span data-ttu-id="1ac65-241">Deze sectie leidt u door Hallo stappen voor het automatiseren van herstel van gegevens vanuit Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="1ac65-241">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="1ac65-242">Dit omvat dus Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1ac65-242">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="1ac65-243">Kies het bronvolume Hallo</span><span class="sxs-lookup"><span data-stu-id="1ac65-243">Pick hello source volume</span></span>
2. <span data-ttu-id="1ac65-244">Kies een back-punt toorestore</span><span class="sxs-lookup"><span data-stu-id="1ac65-244">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="1ac65-245">Kies een item toorestore</span><span class="sxs-lookup"><span data-stu-id="1ac65-245">Choose an item toorestore</span></span>
4. <span data-ttu-id="1ac65-246">Trigger Hallo herstelproces</span><span class="sxs-lookup"><span data-stu-id="1ac65-246">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="1ac65-247">Hallo bronvolume verzamelen</span><span class="sxs-lookup"><span data-stu-id="1ac65-247">Picking hello source volume</span></span>
<span data-ttu-id="1ac65-248">In de volgorde toorestore een item uit Azure Backup moet u eerst tooidentify Hallo bron van Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="1ac65-248">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="1ac65-249">Aangezien we Hallo opdrachten in de context van een Windows-Server of een Windows-client hello uitvoeren je, is al Hallo machine geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="1ac65-249">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="1ac65-250">volgende stap bij het identificeren van bron Hallo Hallo is tooidentify Hallo volume met het.</span><span class="sxs-lookup"><span data-stu-id="1ac65-250">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="1ac65-251">Een lijst van volumes of bronnen wordt een back-up van deze computer kan worden opgehaald door het uitvoeren van Hallo [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ac65-251">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="1ac65-252">Met deze opdracht retourneert een matrix van alle Hallo bronnen back-up van deze server /-client.</span><span class="sxs-lookup"><span data-stu-id="1ac65-252">This command returns an array of all hello sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-toorestore"></a><span data-ttu-id="1ac65-253">Een back-punt toorestore kiezen</span><span class="sxs-lookup"><span data-stu-id="1ac65-253">Choosing a backup point toorestore</span></span>
<span data-ttu-id="1ac65-254">Hallo lijst van back-punten kan worden opgehaald door het uitvoeren van Hallo [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet met de juiste parameters.</span><span class="sxs-lookup"><span data-stu-id="1ac65-254">hello list of backup points can be retrieved by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="1ac65-255">In ons voorbeeld kiest Hallo meest recente back-punt voor het bronvolume Hallo *D:* en gebruik deze toorecover een specifiek bestand.</span><span class="sxs-lookup"><span data-stu-id="1ac65-255">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

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
<span data-ttu-id="1ac65-256">Hallo-object ```$rps``` is een matrix met back-uppunten.</span><span class="sxs-lookup"><span data-stu-id="1ac65-256">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="1ac65-257">Hallo eerste element is het laatste herstelpunt Hallo en ne Hallo-element is Hallo oudste punt.</span><span class="sxs-lookup"><span data-stu-id="1ac65-257">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="1ac65-258">toochoose hello laatste herstelpunt, gebruiken we ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="1ac65-258">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="1ac65-259">Een item toorestore kiezen</span><span class="sxs-lookup"><span data-stu-id="1ac65-259">Choosing an item toorestore</span></span>
<span data-ttu-id="1ac65-260">tooidentify hello exacte bestand of map toorestore, recursief hello gebruiken [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ac65-260">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="1ac65-261">Die hiërarchie manier Hallo map kan worden gebladerd uitsluitend met Hallo ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="1ac65-261">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="1ac65-262">In dit voorbeeld als we toorestore Hallo bestand wilt *finances.xls* we kan verwijzen naar dat als u met Hallo object ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="1ac65-262">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="1ac65-263">U kunt ook zoeken naar items toorestore met Hallo ```Get-OBRecoverableItem``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ac65-263">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="1ac65-264">In ons voorbeeld toosearch voor *finances.xls* we kan een ingang krijgen op Hallo-bestand door deze opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="1ac65-264">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="1ac65-265">Activerende Hallo herstelproces</span><span class="sxs-lookup"><span data-stu-id="1ac65-265">Triggering hello restore process</span></span>
<span data-ttu-id="1ac65-266">tootrigger hello herstelproces, moeten we eerst toospecify Hallo herstelopties.</span><span class="sxs-lookup"><span data-stu-id="1ac65-266">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="1ac65-267">Dit kan worden gedaan met behulp van Hallo [nieuw OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ac65-267">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="1ac65-268">In dit voorbeeld gaan we ervan uit dat we toorestore Hallo bestanden te willen*C:\temp*. Laten we ook uitgaan dat we willen tooskip bestanden die al aanwezig op de doelmap Hallo *C:\temp*. toocreate dergelijke een hersteloptie Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="1ac65-268">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="1ac65-269">Nu activeren herstellen met behulp van Hallo [Start OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) opdracht op Hallo geselecteerd ```$item``` van uitvoer Hallo Hallo ```Get-OBRecoverableItem``` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1ac65-269">Now trigger restore by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="1ac65-270">Hello Azure backup-agent verwijderen</span><span class="sxs-lookup"><span data-stu-id="1ac65-270">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="1ac65-271">Verwijderen hello Azure backup-agent kan worden gedaan met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="1ac65-271">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="1ac65-272">Hallo agent binaire bestanden verwijderen van de machine Hallo heeft enkele tooconsider gevolgen:</span><span class="sxs-lookup"><span data-stu-id="1ac65-272">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="1ac65-273">Hallo-bestandsfilter uit Hallo machine wordt verwijderd en bijhouden van wijzigingen is gestopt.</span><span class="sxs-lookup"><span data-stu-id="1ac65-273">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="1ac65-274">Alle beleidsgegevens van Hallo machine wordt verwijderd, maar Hallo beleidsgegevens blijft toobe opgeslagen in het Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="1ac65-274">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="1ac65-275">Alle back-upschema's worden verwijderd en er is geen verdere back-ups worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1ac65-275">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="1ac65-276">Echter gegevens die zijn opgeslagen in Azure blijft Hallo en door u aan de hand van Hallo bewaren beleid setup wordt bewaard.</span><span class="sxs-lookup"><span data-stu-id="1ac65-276">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="1ac65-277">Oudere punten worden automatisch verouderde.</span><span class="sxs-lookup"><span data-stu-id="1ac65-277">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="1ac65-278">Extern beheer</span><span class="sxs-lookup"><span data-stu-id="1ac65-278">Remote management</span></span>
<span data-ttu-id="1ac65-279">Alle Hallo management rond hello Azure backup-agent, beleid en gegevensbronnen kan op afstand worden uitgevoerd via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ac65-279">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="1ac65-280">Hallo-machine die op afstand worden beheerd moet toobe correct voorbereid.</span><span class="sxs-lookup"><span data-stu-id="1ac65-280">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="1ac65-281">Hallo WinRM-service is standaard geconfigureerd voor handmatig opstarten.</span><span class="sxs-lookup"><span data-stu-id="1ac65-281">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="1ac65-282">Opstarttype Hello te moet worden ingesteld*automatische* en Hallo-service moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="1ac65-282">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="1ac65-283">tooverify die Hallo WinRM-service wordt uitgevoerd, Hallo-waarde van de eigenschap Status Hallo moet *met*.</span><span class="sxs-lookup"><span data-stu-id="1ac65-283">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="1ac65-284">PowerShell moet worden geconfigureerd voor externe toegang.</span><span class="sxs-lookup"><span data-stu-id="1ac65-284">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="1ac65-285">Hallo-machine kan nu worden beheerd op afstand - van Hallo Hallo agent-installatie wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="1ac65-285">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="1ac65-286">Bijvoorbeeld, Hallo script volgen Hallo agent toohello externe computer worden gekopieerd en installeert deze.</span><span class="sxs-lookup"><span data-stu-id="1ac65-286">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="1ac65-287">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1ac65-287">Next steps</span></span>
<span data-ttu-id="1ac65-288">Voor meer informatie over Azure Backup voor Windows Server /-Client, Zie</span><span class="sxs-lookup"><span data-stu-id="1ac65-288">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="1ac65-289">Inleiding tooAzure back-up</span><span class="sxs-lookup"><span data-stu-id="1ac65-289">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="1ac65-290">Back-up van Windows-Servers</span><span class="sxs-lookup"><span data-stu-id="1ac65-290">Back up Windows Servers</span></span>](backup-configure-vault.md)
