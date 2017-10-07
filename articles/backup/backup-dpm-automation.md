---
title: back-up - gebruik PowerShell tooback up DPM workloads aaaAzure | Microsoft Docs
description: Meer informatie over hoe toodeploy en beheren van Azure Backup voor Data Protection Manager (DPM) met behulp van PowerShell
services: backup
documentationcenter: 
author: NKolli1
manager: shreeshd
editor: 
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 27d2b4b3127b68c9da564697eb61dc3ccbc34b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="832f4-103">Implementeren en beheren van back-tooAzure voor Data Protection Manager (DPM) servers met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="832f4-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="832f4-104">ARM</span><span class="sxs-lookup"><span data-stu-id="832f4-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="832f4-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="832f4-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="832f4-106">Dit artikel ziet u hoe Azure Backup toouse PowerShell toosetup op een DPM-server en toomanage back-up en herstel.</span><span class="sxs-lookup"><span data-stu-id="832f4-106">This article shows you how toouse PowerShell toosetup Azure Backup on a DPM server, and toomanage backup and recovery.</span></span>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="832f4-107">Hallo PowerShell-omgeving instellen</span><span class="sxs-lookup"><span data-stu-id="832f4-107">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="832f4-108">Voordat u PowerShell toomanage back-ups van Data Protection Manager tooAzure gebruiken kunt, moet u toohave Hallo juiste omgeving in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="832f4-108">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="832f4-109">Bij Hallo begin van de PowerShell-sessie hello, ervoor te zorgen dat u na de opdracht tooimport Hallo rechts modules Hallo uitvoeren en u toocorrectly verwijzing Hallo DPM-cmdlets kunt:</span><span class="sxs-lookup"><span data-stu-id="832f4-109">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="832f4-110">De installatie en registratie</span><span class="sxs-lookup"><span data-stu-id="832f4-110">Setup and Registration</span></span>
<span data-ttu-id="832f4-111">toobegin:</span><span class="sxs-lookup"><span data-stu-id="832f4-111">toobegin:</span></span>

1. <span data-ttu-id="832f4-112">[Download de meest recente PowerShell](https://github.com/Azure/azure-powershell/releases) (minimaal vereiste versie is: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="832f4-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="832f4-113">Hello Azure Backup commandlets inschakelen door het overschakelen te*AzureResourceManager* modus met behulp van Hallo **Switch AzureMode** commandlet:</span><span class="sxs-lookup"><span data-stu-id="832f4-113">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="832f4-114">Hallo kunnen volgende installatie en registratietaken worden geautomatiseerd met PowerShell:</span><span class="sxs-lookup"><span data-stu-id="832f4-114">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="832f4-115">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="832f4-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="832f4-116">Hello Azure backup-agent installeren</span><span class="sxs-lookup"><span data-stu-id="832f4-116">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="832f4-117">Registreren bij hello Azure Backup-service</span><span class="sxs-lookup"><span data-stu-id="832f4-117">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="832f4-118">Netwerkinstellingen</span><span class="sxs-lookup"><span data-stu-id="832f4-118">Networking settings</span></span>
* <span data-ttu-id="832f4-119">Versleutelingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="832f4-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="832f4-120">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="832f4-120">Create a recovery services vault</span></span>
<span data-ttu-id="832f4-121">volgende stappen uit Hallo leiden u bij het maken van een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="832f4-121">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="832f4-122">Een Recovery Services-kluis is anders dan een back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="832f4-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="832f4-123">Als u van Azure Backup voor Hallo eerst gebruikmaakt, moet u Hallo **registreren AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider met uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="832f4-123">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="832f4-124">Hallo Recovery Services-kluis is een ARM-bron, dus u tooplace moet deze binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="832f4-124">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="832f4-125">U kunt een bestaande resourcegroep gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="832f4-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="832f4-126">Bij het maken van een nieuwe resourcegroep Hallo naam en locatie voor resourcegroep Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="832f4-126">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="832f4-127">Gebruik Hallo **nieuw AzureRmRecoveryServicesVault** cmdlet toocreate een nieuwe kluis.</span><span class="sxs-lookup"><span data-stu-id="832f4-127">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate a new vault.</span></span> <span data-ttu-id="832f4-128">Zorg ervoor dat toospecify dezelfde locatie voor de kluis Hallo Hallo werd gebruikt voor de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="832f4-128">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="832f4-129">Geef een Hallo van opslag redundantie toouse; u kunt [lokaal redundante opslag (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) of [geografisch redundante opslag (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="832f4-129">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="832f4-130">Hallo volgende voorbeeld ziet Hallo BackupStorageRedundancy - optie voor testVault tooGeoRedundant is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="832f4-130">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="832f4-131">Veel Azure Backup-cmdlets vereisen Hallo Recovery Services-kluis object als invoer.</span><span class="sxs-lookup"><span data-stu-id="832f4-131">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="832f4-132">Daarom is het handige toostore Hallo back-up Recovery Services-kluis object in een variabele.</span><span class="sxs-lookup"><span data-stu-id="832f4-132">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="832f4-133">Hallo-kluizen in een abonnement weergeven</span><span class="sxs-lookup"><span data-stu-id="832f4-133">View hello vaults in a subscription</span></span>
<span data-ttu-id="832f4-134">Gebruik **Get-AzureRmRecoveryServicesVault** tooview Hallo lijst met alle kluizen in het huidige abonnement Hallo.</span><span class="sxs-lookup"><span data-stu-id="832f4-134">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="832f4-135">U kunt deze opdracht toocheck of een nieuwe kluis is gemaakt of toosee welke kluizen zijn beschikbaar in het Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="832f4-135">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="832f4-136">Hallo-opdracht Get-AzureRmRecoveryServicesVault, uitvoeren en alle kluizen in Hallo abonnement worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="832f4-136">Run hello command, Get-AzureRmRecoveryServicesVault, and all vaults in hello subscription are listed.</span></span>

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


## <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="832f4-137">Hello Azure backup-agent installeren op een DPM-Server</span><span class="sxs-lookup"><span data-stu-id="832f4-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="832f4-138">Voordat u hello Azure backup-agent hebt geïnstalleerd, moet u toohave Hallo installatieprogramma gedownload en aanwezig is op Hallo van Windows Server.</span><span class="sxs-lookup"><span data-stu-id="832f4-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="832f4-139">U kunt de nieuwste versie van de Hallo van Hallo installer krijgen van Hallo [Microsoft Download Center](http://aka.ms/azurebackup_agent) of van de dashboardpagina Hallo Recovery Services-kluis van.</span><span class="sxs-lookup"><span data-stu-id="832f4-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="832f4-140">Hallo-installatieprogramma opslaan tooan toegankelijke locatie zoals * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="832f4-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="832f4-141">tooinstall hello agent, Hallo volgende opdracht in een PowerShell-console met verhoogde bevoegdheden uitvoeren **op de DPM-server Hallo**:</span><span class="sxs-lookup"><span data-stu-id="832f4-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="832f4-142">Dit met alle standaardopties voor Hallo Hallo-agent hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="832f4-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="832f4-143">Hallo installatie duurt een paar minuten op Hallo achtergrond.</span><span class="sxs-lookup"><span data-stu-id="832f4-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="832f4-144">Als u geen Hallo opgeeft */nu* optie Hallo **Windows Update** venster wordt geopend na Hallo Hallo installatie toocheck voor eventuele updates.</span><span class="sxs-lookup"><span data-stu-id="832f4-144">If you do not specify hello */nu* option hello **Windows Update** window opens at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="832f4-145">Hallo-agent wordt weergegeven in het Hallo-lijst met geïnstalleerde programma's.</span><span class="sxs-lookup"><span data-stu-id="832f4-145">hello agent shows up in hello list of installed programs.</span></span> <span data-ttu-id="832f4-146">toosee hello lijst met geïnstalleerde programma's, gaat u te**Configuratiescherm** > **programma's** > **programma's en onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="832f4-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent is geïnstalleerd](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="832f4-148">Opties voor de installatie</span><span class="sxs-lookup"><span data-stu-id="832f4-148">Installation options</span></span>
<span data-ttu-id="832f4-149">toosee alle Hallo opties die beschikbaar zijn via Hallo commandline, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="832f4-149">toosee all hello options available via hello commandline, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="832f4-150">Hallo beschikbare opties zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="832f4-150">hello available options include:</span></span>

| <span data-ttu-id="832f4-151">Optie</span><span class="sxs-lookup"><span data-stu-id="832f4-151">Option</span></span> | <span data-ttu-id="832f4-152">Details</span><span class="sxs-lookup"><span data-stu-id="832f4-152">Details</span></span> | <span data-ttu-id="832f4-153">Standaard</span><span class="sxs-lookup"><span data-stu-id="832f4-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="832f4-154">/q</span><span class="sxs-lookup"><span data-stu-id="832f4-154">/q</span></span> |<span data-ttu-id="832f4-155">Stille installatie</span><span class="sxs-lookup"><span data-stu-id="832f4-155">Quiet installation</span></span> |- |
| <span data-ttu-id="832f4-156">/ p: 'locatie'</span><span class="sxs-lookup"><span data-stu-id="832f4-156">/p:"location"</span></span> |<span data-ttu-id="832f4-157">Pad toohello installatiemap op voor hello Azure backup-agent.</span><span class="sxs-lookup"><span data-stu-id="832f4-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="832f4-158">C:\Program Files\Microsoft Azure Recovery Services-Agent</span><span class="sxs-lookup"><span data-stu-id="832f4-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="832f4-159">/ s: 'locatie'</span><span class="sxs-lookup"><span data-stu-id="832f4-159">/s:"location"</span></span> |<span data-ttu-id="832f4-160">Pad toohello cachemap voor hello Azure backup-agent.</span><span class="sxs-lookup"><span data-stu-id="832f4-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="832f4-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="832f4-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="832f4-162">/m</span><span class="sxs-lookup"><span data-stu-id="832f4-162">/m</span></span> |<span data-ttu-id="832f4-163">Opt-in tooMicrosoft Update</span><span class="sxs-lookup"><span data-stu-id="832f4-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="832f4-164">/nu</span><span class="sxs-lookup"><span data-stu-id="832f4-164">/nu</span></span> |<span data-ttu-id="832f4-165">Niet controleren op updates nadat de installatie is voltooid</span><span class="sxs-lookup"><span data-stu-id="832f4-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="832f4-166">/d</span><span class="sxs-lookup"><span data-stu-id="832f4-166">/d</span></span> |<span data-ttu-id="832f4-167">Hiermee verwijdert u Microsoft Azure Recovery Services-Agent</span><span class="sxs-lookup"><span data-stu-id="832f4-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="832f4-168">/pH</span><span class="sxs-lookup"><span data-stu-id="832f4-168">/ph</span></span> |<span data-ttu-id="832f4-169">Host-proxyadres</span><span class="sxs-lookup"><span data-stu-id="832f4-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="832f4-170">/PO</span><span class="sxs-lookup"><span data-stu-id="832f4-170">/po</span></span> |<span data-ttu-id="832f4-171">Proxy-Host-poortnummer</span><span class="sxs-lookup"><span data-stu-id="832f4-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="832f4-172">/Pu</span><span class="sxs-lookup"><span data-stu-id="832f4-172">/pu</span></span> |<span data-ttu-id="832f4-173">De Proxygebruikersnaam voor de Host</span><span class="sxs-lookup"><span data-stu-id="832f4-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="832f4-174">/PW</span><span class="sxs-lookup"><span data-stu-id="832f4-174">/pw</span></span> |<span data-ttu-id="832f4-175">Proxy-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="832f4-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-tooa-recovery-services-vault"></a><span data-ttu-id="832f4-176">DPM tooa Recovery Services-kluis registreren</span><span class="sxs-lookup"><span data-stu-id="832f4-176">Registering DPM tooa Recovery Services Vault</span></span>
<span data-ttu-id="832f4-177">Nadat u Hallo Recovery Services-kluis hebt gemaakt, de nieuwste agent Hallo en Hallo kluisreferenties downloaden en opslaan in een handige locatie zoals C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="832f4-177">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="832f4-178">Uitvoeren op de DPM-server Hallo Hallo [Start OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister Hallo machine met de Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="832f4-178">On hello DPM server, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="832f4-179">Configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="832f4-179">Initial configuration settings</span></span>
<span data-ttu-id="832f4-180">Nadat Hallo DPM-Server is geregistreerd bij Hallo Recovery Services-kluis, deze begint met de standaardinstellingen van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="832f4-180">Once hello DPM Server is registered with hello Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="832f4-181">Deze abonnementsinstellingen omvatten netwerken, versleuteling en Hallo faseringsgebied.</span><span class="sxs-lookup"><span data-stu-id="832f4-181">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="832f4-182">Abonnementsinstellingen toochange moet u toofirst krijgen een ingang voor Hallo bestaande (standaard)-instellingen met Hallo [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="832f4-182">toochange subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="832f4-183">Alle wijzigingen zijn aangebracht toothis lokale PowerShell-object ```$setting``` en vervolgens volledige Hallo-object is doorgevoerd tooDPM en Azure Backup toosave ze met behulp van Hallo [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="832f4-183">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="832f4-184">U moet toouse hello ```–Commit``` vlag tooensure die Hallo wijzigingen worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="832f4-184">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="832f4-185">Hallo-instellingen worden niet toegepast en door Azure Backup gebruikt tenzij doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="832f4-185">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="832f4-186">Netwerken</span><span class="sxs-lookup"><span data-stu-id="832f4-186">Networking</span></span>
<span data-ttu-id="832f4-187">Als Hallo connectiviteit van Hallo DPM machine toohello Azure Backup-service op Hallo internet via een proxyserver, moeten de proxyserverinstellingen Hallo worden opgegeven voor geslaagde back-ups.</span><span class="sxs-lookup"><span data-stu-id="832f4-187">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="832f4-188">Dit wordt gedaan met behulp van Hallo ```-ProxyServer```en ```-ProxyPort```, ```-ProxyUsername``` en Hallo ```ProxyPassword``` parameters Hello [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="832f4-188">This is done by using hello ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="832f4-189">In dit voorbeeld is het geen proxyserver zodat we alle informatie met betrekking tot de proxy expliciet wordt gewist.</span><span class="sxs-lookup"><span data-stu-id="832f4-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="832f4-190">Bandbreedtegebruik kan ook worden beheerd met opties ```-WorkHourBandwidth``` en ```-NonWorkHourBandwidth``` voor een bepaald aantal dagen van week Hallo.</span><span class="sxs-lookup"><span data-stu-id="832f4-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="832f4-191">In dit voorbeeld stelt we niet beperking.</span><span class="sxs-lookup"><span data-stu-id="832f4-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-hello-staging-area"></a><span data-ttu-id="832f4-192">Hallo faseringsgebied configureren</span><span class="sxs-lookup"><span data-stu-id="832f4-192">Configuring hello staging Area</span></span>
<span data-ttu-id="832f4-193">Hello Azure Backup agent wordt uitgevoerd op Hallo DPM-server moet een tijdelijke opslag voor gegevens die zijn teruggezet vanuit een Hallo cloud (lokaal faseringsgebied).</span><span class="sxs-lookup"><span data-stu-id="832f4-193">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="832f4-194">Hallo faseringsgebied met Hallo configureren [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet en Hallo ```-StagingAreaPath``` parameter.</span><span class="sxs-lookup"><span data-stu-id="832f4-194">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="832f4-195">Hallo bovenstaande voorbeeld Hallo faseringsgebied te worden ingesteld*C:\StagingArea* in PowerShell-object Hallo ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="832f4-195">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="832f4-196">Zorg ervoor dat Hallo opgegeven map bestaat al, anders Hallo laatste doorvoering van de abonnementsinstellingen Hallo zal mislukken.</span><span class="sxs-lookup"><span data-stu-id="832f4-196">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="832f4-197">Versleutelingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="832f4-197">Encryption settings</span></span>
<span data-ttu-id="832f4-198">Hallo back-upgegevens verzonden tooAzure back-up is versleutelde tooprotect Hallo vertrouwelijkheid van Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="832f4-198">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="832f4-199">Hallo-wachtwoordzin voor versleuteling is Hallo 'password' toodecrypt Hallo gegevens op Hallo moment van terugzetten.</span><span class="sxs-lookup"><span data-stu-id="832f4-199">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="832f4-200">Het is belangrijk tookeep deze gegevens veilig en beveiligd als deze eenmaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="832f4-200">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="832f4-201">In volgende Hallo voorbeeld wordt de eerste opdracht Hallo converteert Hallo ```passphrase123456789``` tooa veilige tekenreeks en wijst Hallo veilige tekenreeks toohello variabele met de naam ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="832f4-201">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="832f4-202">de tweede opdracht Hallo Hallo veilige tekenreeks wordt ingesteld in ```$Passphrase``` Hallo wachtwoord voor het versleutelen van back-ups.</span><span class="sxs-lookup"><span data-stu-id="832f4-202">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="832f4-203">Hallo wachtwoordzin gegevens veilig en beveiligd houden als deze eenmaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="832f4-203">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="832f4-204">U zich niet kunnen toorestore gegevens van Azure zonder deze wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="832f4-204">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="832f4-205">Op dit moment moet aangebracht alle Hallo vereist wijzigingen toohello ```$setting``` object.</span><span class="sxs-lookup"><span data-stu-id="832f4-205">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="832f4-206">Houd er rekening mee toocommit Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="832f4-206">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="832f4-207">Gegevens tooAzure back-up beveiligen</span><span class="sxs-lookup"><span data-stu-id="832f4-207">Protect data tooAzure Backup</span></span>
<span data-ttu-id="832f4-208">In deze sectie maakt u een server productie tooDPM toevoegen en Beveilig vervolgens toolocal Hallo-DPM gegevensopslag en vervolgens tooAzure back-up.</span><span class="sxs-lookup"><span data-stu-id="832f4-208">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="832f4-209">In het Hallo-voorbeelden wordt gedemonstreerd hoe tooback van bestanden en mappen.</span><span class="sxs-lookup"><span data-stu-id="832f4-209">In hello examples, we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="832f4-210">Hallo logica kan eenvoudig worden uitgebreide toobackup elke DPM-ondersteunde gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="832f4-210">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="832f4-211">Alle DPM--ups worden geregeld door een Protection Group (PG) met vier onderdelen:</span><span class="sxs-lookup"><span data-stu-id="832f4-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="832f4-212">**Leden** is een lijst van alle beveiligbare objecten voor hello (ook wel bekend als *gegevensbronnen* in DPM) dat u wilt dat tooprotect in Hallo dezelfde beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="832f4-212">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="832f4-213">U kunt bijvoorbeeld tooprotect productie, virtuele machines in een beveiligingsgroep en SQL Server-databases in een andere beveiligingsgroep als ze mogelijk andere back-upvereisten heeft.</span><span class="sxs-lookup"><span data-stu-id="832f4-213">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="832f4-214">Voordat u kunt back-up elke gegevensbron op een productieserver moet u ervoor Hallo toomake DPM-Agent op Hallo-server is geïnstalleerd en wordt beheerd door DPM.</span><span class="sxs-lookup"><span data-stu-id="832f4-214">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="832f4-215">Volg de stappen voor Hallo [DPM-Agent installeren Hallo](https://technet.microsoft.com/library/bb870935.aspx) en het koppelen van toohello DPM-Server nodig.</span><span class="sxs-lookup"><span data-stu-id="832f4-215">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="832f4-216">**Methode voor gegevensbeveiliging** geeft Hallo back-up doellocaties - tape, schijf- en cloud.</span><span class="sxs-lookup"><span data-stu-id="832f4-216">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="832f4-217">In ons voorbeeld beveiligen we gegevens toohello lokale schijf en toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="832f4-217">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="832f4-218">Een **back-upschema** die aangeeft wanneer back-ups moeten toobe genomen en hoe vaak hello gegevens moeten worden gesynchroniseerd tussen Hallo DPM-Server en Hallo productieserver.</span><span class="sxs-lookup"><span data-stu-id="832f4-218">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="832f4-219">Een **bewaarschema** die aangeeft hoe lang tooretain Hallo herstelpunten in Azure.</span><span class="sxs-lookup"><span data-stu-id="832f4-219">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="832f4-220">Een beveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="832f4-220">Creating a protection group</span></span>
<span data-ttu-id="832f4-221">Eerst maakt u een nieuwe beveiligingsgroep met Hallo [nieuw DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="832f4-221">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="832f4-222">Hallo hierboven cmdlet maakt een beveiligingsgroep met de naam *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="832f4-222">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="832f4-223">Een bestaande beveiligingsgroep kan ook later tooadd back-toohello Azure-cloud worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="832f4-223">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="832f4-224">Echter toomake wijzigingen toohello beveiligingsgroep - nieuwe of bestaande - moeten we tooget een koppeling op een *bewerkbaar* -object op met de Hallo [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="832f4-224">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="832f4-225">Groep leden toohello beveiligingsgroep toevoegen</span><span class="sxs-lookup"><span data-stu-id="832f4-225">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="832f4-226">Elke DPM-Agent kent Hallo-lijst van gegevensbronnen op Hallo van server waarop deze is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="832f4-226">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="832f4-227">tooadd een datasource-toohello beveiligingsgroep, Hallo DPM-Agent behoeften toofirst verzend een lijst van Hallo gegevensbronnen back toohello DPM-server.</span><span class="sxs-lookup"><span data-stu-id="832f4-227">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="832f4-228">Een of meer gegevensbronnen zijn geselecteerd en toohello beveiligingsgroep toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="832f4-228">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="832f4-229">Hallo PowerShell stappen nodig tooachieve dit zijn:</span><span class="sxs-lookup"><span data-stu-id="832f4-229">hello PowerShell steps needed tooachieve this are:</span></span>

1. <span data-ttu-id="832f4-230">Haal een lijst met alle servers die door DPM wordt beheerd via Hallo DPM-Agent.</span><span class="sxs-lookup"><span data-stu-id="832f4-230">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="832f4-231">Kies een specifieke server.</span><span class="sxs-lookup"><span data-stu-id="832f4-231">Choose a specific server.</span></span>
3. <span data-ttu-id="832f4-232">Haal een lijst van alle gegevensbronnen op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="832f4-232">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="832f4-233">Kies een of meer gegevensbronnen en toohello beveiligingsgroep toevoegen</span><span class="sxs-lookup"><span data-stu-id="832f4-233">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="832f4-234">Hallo-lijst met servers op welke Hallo DPM-Agent is geïnstalleerd en wordt beheerd door Hallo DPM-Server wordt verkregen door hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="832f4-234">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="832f4-235">In dit voorbeeld wordt filteren en alleen PS configureren met de naam *productionserver01* voor back-up.</span><span class="sxs-lookup"><span data-stu-id="832f4-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="832f4-236">Nu ophalen Hallo-lijst van gegevensbronnen op ```$server``` met Hallo [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="832f4-236">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="832f4-237">In dit voorbeeld zijn er filteren voor Hallo volume * D:\* we tooconfigure willen voor back-up.</span><span class="sxs-lookup"><span data-stu-id="832f4-237">In this example we are filtering for hello volume *D:\* that we want tooconfigure for backup.</span></span> <span data-ttu-id="832f4-238">Deze gegevensbron wordt vervolgens toegevoegd aan toohello beveiligingsgroep met Hallo [toevoegen DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="832f4-238">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="832f4-239">Houd er rekening mee toouse Hallo *bewerkbaar* protection group-object ```$MPG``` toomake Hallo toevoegingen.</span><span class="sxs-lookup"><span data-stu-id="832f4-239">Remember toouse hello *modifiable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="832f4-240">Herhaal deze stap zo vaak als nodig is, totdat u alle Hallo gekozen gegevensbronnen toohello beveiligingsgroep hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="832f4-240">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="832f4-241">U kunt ook starten met slechts één gegevensbron en volledige Hallo-werkstroom voor het maken van Hallo beveiligingsgroep en voeg meer gegevensbronnen toohello beveiligingsgroep op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="832f4-241">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="832f4-242">Hallo-methode voor gegevensbeveiliging selecteren</span><span class="sxs-lookup"><span data-stu-id="832f4-242">Selecting hello data protection method</span></span>
<span data-ttu-id="832f4-243">Zodra het Hallo-gegevensbronnen zijn toegevoegd toohello beveiligingsgroep, de volgende stap Hallo methode voor gegevensbeveiliging van toospecify Hallo Hallo met is [Set DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="832f4-243">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="832f4-244">In dit voorbeeld is Hallo beveiligingsgroep ingesteld voor de lokale schijf en de cloud back-up.</span><span class="sxs-lookup"><span data-stu-id="832f4-244">In this example, hello Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="832f4-245">U moet ook toospecify Hallo gegevensbron die u wilt dat tooprotect toocloud met Hallo [toevoegen DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet uit met - Online vlag.</span><span class="sxs-lookup"><span data-stu-id="832f4-245">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="832f4-246">Hallo bewaartermijn instellen</span><span class="sxs-lookup"><span data-stu-id="832f4-246">Setting hello retention range</span></span>
<span data-ttu-id="832f4-247">Hallo bewaartermijn voor de back-uppunten Hallo Hallo met ingesteld [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="832f4-247">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="832f4-248">Terwijl kan het lijken alsof oneven tooset Hallo bewaren voordat de back-upschema Hallo is gedefinieerd, met behulp van Hallo ```Set-DPMPolicyObjective``` cmdlet stelt automatisch een standaard back-upschema die vervolgens kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="832f4-248">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="832f4-249">Het is altijd mogelijk tooset Hallo back-upschema eerst en Hallo bewaarbeleid na.</span><span class="sxs-lookup"><span data-stu-id="832f4-249">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="832f4-250">In onderstaande Hallo voorbeeld stelt Hallo cmdlet Hallo bewaren parameters voor back-ups van schijf.</span><span class="sxs-lookup"><span data-stu-id="832f4-250">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="832f4-251">Dit, back-ups behouden voor 10 dagen en gegevens synchroniseren om de 6 uur tussen Hallo productieserver en Hallo DPM-server.</span><span class="sxs-lookup"><span data-stu-id="832f4-251">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="832f4-252">Hallo ```SynchronizationFrequencyMinutes``` bevat geen definitie van hoe vaak een back-up is gemaakt, maar hoe vaak gegevens gekopieerde toohello DPM-server is.</span><span class="sxs-lookup"><span data-stu-id="832f4-252">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server.</span></span>  <span data-ttu-id="832f4-253">Deze instelling voorkomt u dat back-ups te groot.</span><span class="sxs-lookup"><span data-stu-id="832f4-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="832f4-254">Hallo bewaartermijnen voor back-ups gaat tooAzure (DPM verwijst toothem als Online back-ups) kunnen worden geconfigureerd voor [langdurig bewaren volgens een schema opa-vader-zoon (algemene)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="832f4-254">For backups going tooAzure (DPM refers toothem as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="832f4-255">Dat wil zeggen, kunt u een gecombineerde bewaarbeleid met betrekking tot dagelijks, wekelijks, maandelijks en jaarlijks bewaarbeleid definiëren.</span><span class="sxs-lookup"><span data-stu-id="832f4-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="832f4-256">In dit voorbeeld wordt een matrix die vertegenwoordigt Hallo complexe bewaarschema die we willen maken en configureer vervolgens bewaartermijn Hallo Hallo met [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="832f4-256">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="832f4-257">Set Hallo back-upschema</span><span class="sxs-lookup"><span data-stu-id="832f4-257">Set hello backup schedule</span></span>
<span data-ttu-id="832f4-258">DPM een back-upschema standaard automatisch ingesteld als u de doelstelling van het Hallo-beveiliging met Hallo opgeeft ```Set-DPMPolicyObjective``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="832f4-258">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="832f4-259">toochange hello standaardplanningen, gebruik Hallo [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet gevolgd door Hallo [Set DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="832f4-259">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="832f4-260">In Hallo hierboven bijvoorbeeld ```$onlineSch``` is een matrix met vier elementen met Hallo bestaande online beveiligingsschema voor Hallo beveiligingsgroep in Hallo algemene schema:</span><span class="sxs-lookup"><span data-stu-id="832f4-260">In hello above example, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="832f4-261">```$onlineSch[0]```Hallo dagelijks schema bevat</span><span class="sxs-lookup"><span data-stu-id="832f4-261">```$onlineSch[0]``` contains hello daily schedule</span></span>
2. <span data-ttu-id="832f4-262">```$onlineSch[1]```Hallo wekelijks schema bevat</span><span class="sxs-lookup"><span data-stu-id="832f4-262">```$onlineSch[1]``` contains hello weekly schedule</span></span>
3. <span data-ttu-id="832f4-263">```$onlineSch[2]```bevat Hallo maandelijks schema</span><span class="sxs-lookup"><span data-stu-id="832f4-263">```$onlineSch[2]``` contains hello monthly schedule</span></span>
4. <span data-ttu-id="832f4-264">```$onlineSch[3]```bevat Hallo jaarlijkse planning</span><span class="sxs-lookup"><span data-stu-id="832f4-264">```$onlineSch[3]``` contains hello yearly schedule</span></span>

<span data-ttu-id="832f4-265">Dus als u toomodify Hallo wekelijkse planning moet, u toorefer toohello moet ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="832f4-265">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="832f4-266">Eerste back-up</span><span class="sxs-lookup"><span data-stu-id="832f4-266">Initial backup</span></span>
<span data-ttu-id="832f4-267">Wanneer een back-up een gegevensbron voor Hallo eerst DPM behoeften maakt eerste replica die, maakt een volledige kopie van Hallo datasource toobe die op de DPM-replicavolume worden beveiligd.</span><span class="sxs-lookup"><span data-stu-id="832f4-267">When backing up a datasource for hello first time, DPM needs creates initial replica that creates a full copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="832f4-268">Deze activiteit kunnen ofwel worden gepland voor een bepaald tijdstip of handmatig kan worden geactiveerd, met behulp van Hallo [Set DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet met de parameter Hallo ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="832f4-268">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="832f4-269">Grootte van de DPM-Replica en herstelpuntvolume van Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="832f4-269">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="832f4-270">U kunt ook wijzigen Hallo grootte van de DPM-replicavolume en het gebruik van de volume Shadow Copy [Set DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet zoals in het volgende voorbeeld Hallo: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-handmatige - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="832f4-270">You can also change hello size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="832f4-271">Beveiligingsgroep de toohello Hallo wijzigingen doorvoeren</span><span class="sxs-lookup"><span data-stu-id="832f4-271">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="832f4-272">Ten slotte moeten Hallo wijzigingen toobe voordat DPM Hallo back-up per Hallo nieuwe beveiligingsgroep configuratie kan worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="832f4-272">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="832f4-273">Dit kan worden bereikt met Hallo [Set DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="832f4-273">This can be achieved using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="832f4-274">Weergave Hallo back-punten</span><span class="sxs-lookup"><span data-stu-id="832f4-274">View hello backup points</span></span>
<span data-ttu-id="832f4-275">U kunt Hallo [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget cmdlet een lijst van alle herstelpunten voor een datasource.</span><span class="sxs-lookup"><span data-stu-id="832f4-275">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="832f4-276">In dit voorbeeld wordt:</span><span class="sxs-lookup"><span data-stu-id="832f4-276">In this example, we will:</span></span>

* <span data-ttu-id="832f4-277">Fetch alle PGs Hallo op Hallo DPM-server en opgeslagen in een matrix```$PG```</span><span class="sxs-lookup"><span data-stu-id="832f4-277">fetch all hello PGs on hello DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="832f4-278">Hallo gegevensbronnen bijbehorende toohello ophalen```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="832f4-278">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="832f4-279">alle Hallo herstelpunten voor een gegevensbron niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="832f4-279">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="832f4-280">Herstellen van gegevens die zijn beveiligd op Azure</span><span class="sxs-lookup"><span data-stu-id="832f4-280">Restore data protected on Azure</span></span>
<span data-ttu-id="832f4-281">Herstellen van gegevens is een combinatie van een ```RecoverableItem``` object en een ```RecoveryOption``` object.</span><span class="sxs-lookup"><span data-stu-id="832f4-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="832f4-282">In de vorige sectie hello wij een lijst met back-uppunten Hallo voor een datasource.</span><span class="sxs-lookup"><span data-stu-id="832f4-282">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="832f4-283">In Hallo onderstaande voorbeeld ziet u hoe toorestore een Hyper-V virtuele machine van Azure Backup door back-uppunten combineren met Hallo als doel voor herstel.</span><span class="sxs-lookup"><span data-stu-id="832f4-283">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="832f4-284">Dit voorbeeld bevat:</span><span class="sxs-lookup"><span data-stu-id="832f4-284">This example includes:</span></span>

* <span data-ttu-id="832f4-285">Maken van een hersteloptie Hallo met [nieuw DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="832f4-285">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="832f4-286">Ophalen Hallo-matrix van back-punten met Hallo ```Get-DPMRecoveryPoint``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="832f4-286">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="832f4-287">Een back-punt toorestore uit te kiezen.</span><span class="sxs-lookup"><span data-stu-id="832f4-287">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="832f4-288">Hallo-opdrachten kunnen gemakkelijk worden uitgebreid voor elk gegevensbrontype.</span><span class="sxs-lookup"><span data-stu-id="832f4-288">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="832f4-289">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="832f4-289">Next steps</span></span>
* <span data-ttu-id="832f4-290">Zie voor meer informatie over DPM tooAzure back-up [inleiding tooDPM back-up](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="832f4-290">For more information about DPM tooAzure Backup see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
