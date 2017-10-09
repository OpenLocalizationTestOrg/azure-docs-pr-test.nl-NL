---
title: aaaAzure Bescherm persoonlijke gegevens in rust met versleuteling | Microsoft Docs
description: In dit artikel maakt deel uit van een reeks helpt u Azure tooprotect persoonlijke gegevens gebruiken
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a><span data-ttu-id="c5c73-103">Azure versleutelingstechnologieën: beveiligen van persoonlijke gegevens in rust met versleuteling</span><span class="sxs-lookup"><span data-stu-id="c5c73-103">Azure encryption technologies: Protect personal data at rest with encryption</span></span>

<span data-ttu-id="c5c73-104">In dit artikel helpt u begrijpen en gebruiken van Azure versleuteling technologieën toosecure gegevens in rust.</span><span class="sxs-lookup"><span data-stu-id="c5c73-104">This article helps you understand and use Azure encryption technologies toosecure data at rest.</span></span>

<span data-ttu-id="c5c73-105">Versleuteling van gegevens in rust is essentieel als een best practice tooprotect gevoelige of persoonlijke gegevens en toomeet naleving en gegevens privacy-vereisten.</span><span class="sxs-lookup"><span data-stu-id="c5c73-105">Encryption of data at rest is essential as a best practice tooprotect sensitive or personal data and toomeet compliance and data privacy requirements.</span></span>
<span data-ttu-id="c5c73-106">Codering in rust is ontworpen tooprevent Hallo kwaadwillende persoon toegang krijgen tot gegevens van niet-versleuteld Hallo door ervoor te zorgen Hallo gegevens worden versleuteld op de schijf.</span><span class="sxs-lookup"><span data-stu-id="c5c73-106">Encryption at rest is designed tooprevent hello attacker from accessing hello unencrypted data by ensuring hello data is encrypted when on disk.</span></span>

## <a name="scenario"></a><span data-ttu-id="c5c73-107">Scenario</span><span class="sxs-lookup"><span data-stu-id="c5c73-107">Scenario</span></span> 

<span data-ttu-id="c5c73-108">Een bedrijf grote cruise, gevestigd in de Verenigde Staten Hallo breidt de bewerkingen toooffer routes in Hallo Middellandse, en Baltische veiligheid, evenals Hallo Florida.</span><span class="sxs-lookup"><span data-stu-id="c5c73-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="c5c73-109">toosupport deze inspanningen, heeft deze meerdere kleinere cruise regels op basis van Italië, Duitsland, Denemarken en Hallo VK verkregen</span><span class="sxs-lookup"><span data-stu-id="c5c73-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="c5c73-110">Hallo bedrijf maakt gebruik van Microsoft Azure toostore bedrijfsgegevens Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="c5c73-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="c5c73-111">Dit kan werknemer en/of klantgegevens zoals omvatten:</span><span class="sxs-lookup"><span data-stu-id="c5c73-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="c5c73-112">adressen</span><span class="sxs-lookup"><span data-stu-id="c5c73-112">addresses</span></span>
- <span data-ttu-id="c5c73-113">telefoonnummers</span><span class="sxs-lookup"><span data-stu-id="c5c73-113">phone numbers</span></span>
- <span data-ttu-id="c5c73-114">BTW-id 's</span><span class="sxs-lookup"><span data-stu-id="c5c73-114">tax identification numbers</span></span>
- <span data-ttu-id="c5c73-115">medische informatie</span><span class="sxs-lookup"><span data-stu-id="c5c73-115">medical information</span></span>
- <span data-ttu-id="c5c73-116">creditcardgegevens</span><span class="sxs-lookup"><span data-stu-id="c5c73-116">credit card information</span></span>

<span data-ttu-id="c5c73-117">Hallo bedrijf moet Hallo privacy van werknemers en klanten gegevens beveiligen tijdens het maken van gegevens toegankelijk toothose afdelingen die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="c5c73-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="c5c73-118">(zoals salarissen en -reserveringen afdelingen)</span><span class="sxs-lookup"><span data-stu-id="c5c73-118">(such as payroll and reservations departments)</span></span>

<span data-ttu-id="c5c73-119">Hallo cruise regel onderhoudt ook een grote database van derden en loyaliteit voor leden die persoonlijke gegevens tootrack relaties met de huidige en eerdere klanten bevat.</span><span class="sxs-lookup"><span data-stu-id="c5c73-119">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

### <a name="problem-statement"></a><span data-ttu-id="c5c73-120">Probleemformulering</span><span class="sxs-lookup"><span data-stu-id="c5c73-120">Problem statement</span></span>

<span data-ttu-id="c5c73-121">Hallo bedrijf moet Hallo privacy van klanten en werknemers persoonlijke gegevens beveiligen tijdens het maken van gegevens toegankelijk toothose afdelingen die u nodig hebt (zoals salarissen en -reserveringen afdelingen).</span><span class="sxs-lookup"><span data-stu-id="c5c73-121">hello company must protect hello privacy of employees’ and customers’ personal data while making data accessible toothose departments that need it (such as payroll and reservations departments).</span></span> <span data-ttu-id="c5c73-122">Deze persoonlijke gegevens buiten Hallo zakelijke beheerde Datacenter wordt opgeslagen en wordt niet beheerd van het bedrijf Hallo fysieke.</span><span class="sxs-lookup"><span data-stu-id="c5c73-122">This personal data is stored outside of hello corporate-controlled data center and is not under hello company’s physical control.</span></span>

### <a name="company-goal"></a><span data-ttu-id="c5c73-123">Bedrijf-doel</span><span class="sxs-lookup"><span data-stu-id="c5c73-123">Company goal</span></span>

<span data-ttu-id="c5c73-124">Als onderdeel van een strategie voor een meerlaagse beveiliging van defense-in-depth is een bedrijf doel tooensure dat alle gegevensbronnen die persoonlijke gegevens bevatten zijn versleuteld, met inbegrip van die zich in de cloud-opslag.</span><span class="sxs-lookup"><span data-stu-id="c5c73-124">As part of a multi-layered defense-in-depth security strategy, it is a company goal tooensure that all data sources that contain personal data are encrypted, including those residing in cloud storage.</span></span> <span data-ttu-id="c5c73-125">Als niet-gemachtigde personen voordeel toegang toohello persoonlijke gegevens, moet deze zich in een formulier dat het onleesbaar verschijnt.</span><span class="sxs-lookup"><span data-stu-id="c5c73-125">If unauthorized persons gain access toohello personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="c5c73-126">Versleuteling toepassen, moet eenvoudig of transparante – voor gebruikers en beheerders.</span><span class="sxs-lookup"><span data-stu-id="c5c73-126">Applying encryption should be easy, or transparent – for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="c5c73-127">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="c5c73-127">Solutions</span></span>

<span data-ttu-id="c5c73-128">Azure-services bieden meerdere hulpprogramma's en technologieën toohelp u persoonlijke gegevens in rust beveiligen door deze te coderen.</span><span class="sxs-lookup"><span data-stu-id="c5c73-128">Azure services provide multiple tools and technologies toohelp you protect personal data at rest by encrypting it.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="c5c73-129">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c5c73-129">Azure Key Vault</span></span>

<span data-ttu-id="c5c73-130">[Azure Sleutelkluis](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) biedt een veilige opslag voor Hallo sleutels tooencrypt gegevens in rust in de Azure-services gebruikt en wordt aanbevolen Hallo basisonderdelen opslag en het beheer van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="c5c73-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) provides secure storage for hello keys used tooencrypt data at rest in Azure services and is hello recommended key storage and management solution.</span></span> <span data-ttu-id="c5c73-131">Sleutelbeheer versleuteling is essentieel toosecuring opgeslagen gegevens.</span><span class="sxs-lookup"><span data-stu-id="c5c73-131">Encryption key management is essential toosecuring stored data.</span></span>

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a><span data-ttu-id="c5c73-132">Hoe gebruik ik Azure Key Vault tooprotect sleutels die persoonlijke gegevens te versleutelen?</span><span class="sxs-lookup"><span data-stu-id="c5c73-132">How do I use Azure Key Vault tooprotect keys that encrypt personal data?</span></span>

<span data-ttu-id="c5c73-133">toouse Azure Sleutelkluis, moet u een abonnement tooan Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c5c73-133">toouse Azure Key Vault, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="c5c73-134">U moet ook Azure PowerShell is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c5c73-134">You also need Azure PowerShell installed.</span></span> <span data-ttu-id="c5c73-135">Stappen omvatten het gebruik van PowerShell-cmdlets toodo Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="c5c73-135">Steps include using PowerShell cmdlets toodo hello following:</span></span>

1. <span data-ttu-id="c5c73-136">Verbinding maken met tooyour abonnementen</span><span class="sxs-lookup"><span data-stu-id="c5c73-136">Connect tooyour subscriptions</span></span>

2. <span data-ttu-id="c5c73-137">Een sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="c5c73-137">Create a key vault</span></span>

3. <span data-ttu-id="c5c73-138">Een sleutel of geheim toohello sleutelkluis toevoegen</span><span class="sxs-lookup"><span data-stu-id="c5c73-138">Add a key or secret toohello key vault</span></span>

4. <span data-ttu-id="c5c73-139">Toepassingen die van de sleutelkluis Hallo met Azure Active Directory gebruikmaken registreren</span><span class="sxs-lookup"><span data-stu-id="c5c73-139">Register applications that will use hello key vault with Azure Active Directory</span></span>

5. <span data-ttu-id="c5c73-140">Autoriseren hello toepassingen toouse Hallo sleutel of geheim</span><span class="sxs-lookup"><span data-stu-id="c5c73-140">Authorize hello applications toouse hello key or secret</span></span>

<span data-ttu-id="c5c73-141">een sleutelkluis toocreate Hallo New-AzureRmKeyVault PowerShell-CmDlt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c5c73-141">toocreate a key vault, use hello New-AzureRmKeyVault PowerShell CmDlt.</span></span> <span data-ttu-id="c5c73-142">U kunt een kluisnaam, de naam van een resourcegroep en de geografische locatie wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="c5c73-142">You will assign a vault name, resource group name, and geographic location.</span></span> <span data-ttu-id="c5c73-143">U gebruikt de kluisnaam Hallo bij het beheren van sleutels via andere Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c5c73-143">You’ll use hello vault name when managing keys via other Cmdlets.</span></span> <span data-ttu-id="c5c73-144">Toepassingen die gebruikmaken van de kluis Hallo via Hallo REST-API wordt Hallo vault URI gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c5c73-144">Applications that use hello vault through hello REST API will use hello vault URI.</span></span>

<span data-ttu-id="c5c73-145">Azure Sleutelkluis een softwarematig beveiligde sleutel voor u kunt opgeven of u kunt een bestaande sleutel in importeren een. PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="c5c73-145">Azure Key Vault can provide a software-protected key for you, or you can import an existing key in a .PFX file.</span></span> <span data-ttu-id="c5c73-146">U kunt ook geheimen (wachtwoorden) opslaan in Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="c5c73-146">You can also store secrets (passwords) in hello vault.</span></span>

<span data-ttu-id="c5c73-147">U kunt ook een sleutel in uw lokale HSM genereren en overdragen tooHSMs in Hallo Sleutelkluis-service, zonder Hallo sleutel Hallo HSM-grens verlaat.</span><span class="sxs-lookup"><span data-stu-id="c5c73-147">You can also generate a key in your local HSM and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary.</span></span>

<span data-ttu-id="c5c73-148">Voor gedetailleerde instructies over het gebruik van Azure Sleutelkluis, volg de stappen Hallo in [aan de slag met Azure Sleutelkluis.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span><span class="sxs-lookup"><span data-stu-id="c5c73-148">For detailed instructions on using Azure Key Vault, follow hello steps in [Get Started with Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span></span>

<span data-ttu-id="c5c73-149">Zie voor een lijst van PowerShell-Cmdlets gebruikt met Azure Key Vault [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="c5c73-149">For a list of PowerShell Cmdlets used with Azure Key Vault, see [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

### <a name="azure-disk-encryption-for-windows"></a><span data-ttu-id="c5c73-150">Azure Disk Encryption voor Windows</span><span class="sxs-lookup"><span data-stu-id="c5c73-150">Azure Disk Encryption for Windows</span></span>

<span data-ttu-id="c5c73-151">[Azure Disk Encryption for Windows en Linux IaaS VM's](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) beschermt persoonlijke gegevens in rust op Azure virtuele machines en kan worden geïntegreerd met Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="c5c73-151">[Azure Disk Encryption for Windows and Linux IaaS VMs](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protects personal data at rest on Azure virtual machines and integrates with Azure Key Vault.</span></span> <span data-ttu-id="c5c73-152">Maakt gebruik van Azure Disk Encryption [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows en [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux tooencrypt Hallo beide OS en Hallo gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="c5c73-152">Azure Disk Encryption uses [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows and [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux tooencrypt both hello OS and hello data disks.</span></span> <span data-ttu-id="c5c73-153">Azure Disk Encryption wordt ondersteund op Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 en op Windows 8 en Windows 10-clients.</span><span class="sxs-lookup"><span data-stu-id="c5c73-153">Azure Disk Encryption is supported on Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, and on Windows 8 and Windows 10 clients.</span></span>

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a><span data-ttu-id="c5c73-154">Hoe gebruik ik Azure Disk Encryption tooprotect persoonlijke gegevens?</span><span class="sxs-lookup"><span data-stu-id="c5c73-154">How do I use Azure Disk Encryption tooprotect personal data?</span></span>

<span data-ttu-id="c5c73-155">toouse Azure Disk Encryption, moet u een abonnement tooan Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c5c73-155">toouse Azure Disk Encryption, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="c5c73-156">tooenable Azure Disk Encryption for Windows en Linux-machines Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="c5c73-156">tooenable Azure Disk Encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="c5c73-157">Gebruik hello Azure Disk Encryption Resource Manager-sjabloon, PowerShell of Hallo opdrachtregelinterface (CLI) tooenable schijfversleuteling en geef de configuratie van versleuteling.</span><span class="sxs-lookup"><span data-stu-id="c5c73-157">Use hello Azure Disk Encryption Resource Manager template, PowerShell, or hello command line interface (CLI) tooenable disk encryption and specify the  encryption configuration.</span></span> 

2. <span data-ttu-id="c5c73-158">Verleen toegang toohello Azure-platform tooread Hallo versleuteling materiaal uit de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="c5c73-158">Grant access toohello Azure platform tooread hello encryption material from your key vault.</span></span>

3. <span data-ttu-id="c5c73-159">Geef een Azure Active Directory (AAD) toepassing identiteit toowrite Hallo encryption key wezenlijke tooyour sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="c5c73-159">Provide an Azure Active Directory (AAD) application identity toowrite hello encryption key material tooyour key vault.</span></span>

<span data-ttu-id="c5c73-160">Azure Hallo VM en Hallo sleutelkluis configuratie bijwerken en uw versleutelde virtuele machine instellen.</span><span class="sxs-lookup"><span data-stu-id="c5c73-160">Azure will update hello VM and hello key vault configuration, and set up your encrypted VM.</span></span>

<span data-ttu-id="c5c73-161">Wanneer u uw sleutelkluis toosupport Azure Disk Encryption instelt, kunt u een sleutel versleutelingssleutel (KEK-sleutel) toevoegen voor extra beveiliging en toosupport back-up van versleutelde virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c5c73-161">When you set up your key vault toosupport Azure Disk Encryption, you can add a key encryption key (KEK) for added security and toosupport backup of encrypted virtual machines.</span></span>

![](media/protect-personal-data-at-rest/create-key.png)

<span data-ttu-id="c5c73-162">Gedetailleerde instructies voor het specifieke implementatiescenario's beschreven en gebruikerservaringen zijn opgenomen in [Azure Disk Encryption for Windows en Linux IaaS VM's.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span><span class="sxs-lookup"><span data-stu-id="c5c73-162">Detailed instructions for specific deployment scenarios and user experiences are included in [Azure Disk Encryption for Windows and Linux IaaS VMs.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span></span>

### <a name="azure-storage-service-encryption"></a><span data-ttu-id="c5c73-163">Azure Storage Service-versleuteling</span><span class="sxs-lookup"><span data-stu-id="c5c73-163">Azure Storage Service Encryption</span></span>

<span data-ttu-id="c5c73-164">[Azure Storage Service versleuteling (SSE) voor gegevens in rust](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helpt u bij het beveiligen en uw toomeet gegevens beveiligt uw organisatie beveiliging en naleving verplichtingen.</span><span class="sxs-lookup"><span data-stu-id="c5c73-164">[Azure Storage Service Encryption (SSE) for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helps you protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="c5c73-165">Azure Storage automatisch versleutelt uw gegevens dankzij 256-bits AES-versleuteling voorafgaande toopersisting toostorage en ontsleutelt deze met een eerdere tooretrieval.</span><span class="sxs-lookup"><span data-stu-id="c5c73-165">Azure Storage automatically encrypts your data using 256-bit AES encryption prior toopersisting toostorage, and decrypts it prior tooretrieval.</span></span> <span data-ttu-id="c5c73-166">Deze service is beschikbaar voor Azure Blobs en bestanden.</span><span class="sxs-lookup"><span data-stu-id="c5c73-166">This service is available for Azure Blobs and Files.</span></span>

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a><span data-ttu-id="c5c73-167">Hoe gebruik ik de versleuteling van de opslagruimte tooprotect persoonlijke gegevens?</span><span class="sxs-lookup"><span data-stu-id="c5c73-167">How do I use Storage Service Encryption tooprotect personal data?</span></span>

<span data-ttu-id="c5c73-168">tooenable Storage-Service: versleuteling, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="c5c73-168">tooenable Storage Service Encryption, do hello following:</span></span>

1. <span data-ttu-id="c5c73-169">Meld u aan bij hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c5c73-169">Log into hello Azure portal.</span></span>

2. <span data-ttu-id="c5c73-170">Selecteer een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c5c73-170">Select a storage account.</span></span>

3. <span data-ttu-id="c5c73-171">Selecteer in de instellingen onder sectie van de Blob-Service hello, versleuteling.</span><span class="sxs-lookup"><span data-stu-id="c5c73-171">In Settings, under hello Blob Service section, select Encryption.</span></span>

4. <span data-ttu-id="c5c73-172">Selecteer onder Hallo sectie File-Service, versleuteling.</span><span class="sxs-lookup"><span data-stu-id="c5c73-172">Under hello File Service section, select Encryption.</span></span>

<span data-ttu-id="c5c73-173">Nadat u op de instelling voor wachtwoordversleuteling hello, kunt u in- of uitschakelen van de versleuteling van de opslagruimte.</span><span class="sxs-lookup"><span data-stu-id="c5c73-173">After you click hello Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

<span data-ttu-id="c5c73-174">Nieuwe gegevens worden versleuteld.</span><span class="sxs-lookup"><span data-stu-id="c5c73-174">New data will be encrypted.</span></span> <span data-ttu-id="c5c73-175">Gegevens in de bestaande bestanden in dit opslagaccount wordt onversleuteld blijven.</span><span class="sxs-lookup"><span data-stu-id="c5c73-175">Data in existing files in this storage account will remain unencrypted.</span></span>

<span data-ttu-id="c5c73-176">Kopieer de gegevens toohello storage-account met een van de volgende methoden Hallo na het inschakelen van versleuteling:</span><span class="sxs-lookup"><span data-stu-id="c5c73-176">After enabling encryption, copy data toohello storage account using one of hello following methods:</span></span>

1. <span data-ttu-id="c5c73-177">Kopieer blobs of bestanden met Hallo [AzCopy-opdrachtregelprogramma](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span><span class="sxs-lookup"><span data-stu-id="c5c73-177">Copy blobs or files with hello [AzCopy Command Line utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span></span>

2. <span data-ttu-id="c5c73-178">[Een gebruik van SMB-bestandsshare koppelen](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) zodat u een hulpprogramma zoals Robocopy toocopy bestanden gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="c5c73-178">[Mount a file share using SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) so you can use a utility such as Robocopy toocopy files.</span></span>

3. <span data-ttu-id="c5c73-179">Kopiëren van blob of bestand gegevens tooand van blob-opslag of tussen opslagaccounts met [Opslagclientbibliotheken zoals .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span><span class="sxs-lookup"><span data-stu-id="c5c73-179">Copy blob or file data tooand from blob storage or between storage accounts using [Storage Client Libraries such as .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

4.  <span data-ttu-id="c5c73-180">Gebruik een [Opslagverkenner](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload blobs tooyour storage-account met versleuteling ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c5c73-180">Use a [Storage Explorer](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload blobs tooyour storage account with encryption enabled.</span></span>

### <a name="transparent-data-encryption"></a><span data-ttu-id="c5c73-181">Transparante gegevensversleuteling</span><span class="sxs-lookup"><span data-stu-id="c5c73-181">Transparent Data Encryption</span></span>

<span data-ttu-id="c5c73-182">Transparent Data Encryption (TDE) is een functie in SQL Azure waarmee u gegevens op beide Hallo-database en server niveaus kunt versleutelen.</span><span class="sxs-lookup"><span data-stu-id="c5c73-182">Transparent Data Encryption (TDE) is a feature in SQL Azure by which you can encrypt data at both hello database and server levels.</span></span> <span data-ttu-id="c5c73-183">TDE is nu standaard ingeschakeld op alle nieuwe databases.</span><span class="sxs-lookup"><span data-stu-id="c5c73-183">TDE is now enabled by default on all newly created databases.</span></span> <span data-ttu-id="c5c73-184">TDE voert realtime i/o-versleuteling en ontsleuteling van Hallo gegevens en logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="c5c73-184">TDE performs real-time I/O encryption and decryption of hello data and log files.</span></span>

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a><span data-ttu-id="c5c73-185">Hoe gebruik ik TDE tooprotect persoonlijke gegevens?</span><span class="sxs-lookup"><span data-stu-id="c5c73-185">How do I use TDE tooprotect personal data?</span></span>

<span data-ttu-id="c5c73-186">U kunt TDE via hello Azure-portal configureren met behulp van Hallo REST-API of met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5c73-186">You can configure TDE through hello Azure portal, by using hello REST API, or by using PowerShell.</span></span> <span data-ttu-id="c5c73-187">tooenable TDE op een bestaande database met behulp van hello Azure Portal Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="c5c73-187">tooenable TDE on an existing database using hello Azure Portal, do hello following:</span></span>

1. <span data-ttu-id="c5c73-188">Ga naar hello Azure portal op <https://portal.azure.com> en meld u met uw Azure-beheerder of bijdrager-account.</span><span class="sxs-lookup"><span data-stu-id="c5c73-188">Visit hello Azure portal at <https://portal.azure.com> and sign-in with your Azure Administrator or Contributor account.</span></span>

2. <span data-ttu-id="c5c73-189">Klik op tooBROWSE op Hallo links koptekst, en klik op SQL-databases.</span><span class="sxs-lookup"><span data-stu-id="c5c73-189">On hello left banner, click tooBROWSE, and then click SQL databases.</span></span>

3. <span data-ttu-id="c5c73-190">Met SQL-databases die zijn geselecteerd in het linkerdeelvenster hello, klikt u op de gebruikersdatabase.</span><span class="sxs-lookup"><span data-stu-id="c5c73-190">With SQL databases selected in hello left pane, click your user database.</span></span>

4. <span data-ttu-id="c5c73-191">Klik in de databaseblade hello, alle instellingen.</span><span class="sxs-lookup"><span data-stu-id="c5c73-191">In hello database blade, click All settings.</span></span>

5. <span data-ttu-id="c5c73-192">Klik op de blade instellingen hello, Transparent data encryption onderdeel tooopen Hallo Transparent data versleuteling blade.</span><span class="sxs-lookup"><span data-stu-id="c5c73-192">In hello Settings blade, click Transparent data encryption part tooopen hello Transparent data encryption blade.</span></span>

6. <span data-ttu-id="c5c73-193">Hallo Data encryption blade verplaatsen Hallo Data encryption knop tooOn en klik op opslaan (bovenaan Hallo Hallo pagina) tooapply Hallo-instelling.</span><span class="sxs-lookup"><span data-stu-id="c5c73-193">In hello Data encryption blade, move hello Data encryption button tooOn, and then click Save (at hello top of hello page) tooapply hello setting.</span></span> <span data-ttu-id="c5c73-194">Hallo coderingsstatus wordt bij benadering Hallo voortgang van Hallo transparante gegevensversleuteling.</span><span class="sxs-lookup"><span data-stu-id="c5c73-194">hello Encryption status will approximate hello progress of hello transparent data encryption.</span></span>

![Inschakelen van gegevensversleuteling](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

<span data-ttu-id="c5c73-196">Instructies over hoe tooenable TDE en informatie over het decoderen van databases TDE beveiligd en nog veel meer u in Hallo artikel vindt [Transparent Data Encryption met Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span><span class="sxs-lookup"><span data-stu-id="c5c73-196">Instructions on how tooenable TDE and information on decrypting TDE-protected databases and more can be found in hello article [Transparent Data Encryption with Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span></span>

## <a name="summary"></a><span data-ttu-id="c5c73-197">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="c5c73-197">Summary</span></span>

<span data-ttu-id="c5c73-198">Hallo bedrijf kunt doelstelling van het versleutelen van persoonlijke gegevens die zijn opgeslagen in Azure-cloud Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c5c73-198">hello company can accomplish its goal of encrypting personal data stored in hello Azure cloud.</span></span> <span data-ttu-id="c5c73-199">Ze kunnen dit doen met behulp van Azure Disk Encryption gehele volumes te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="c5c73-199">They can do this by using Azure Disk Encryption too protect entire volumes.</span></span> <span data-ttu-id="c5c73-200">Dit kan omvatten zowel Hallo besturingssysteem en gegevensbestanden die persoonlijk gegevens en andere gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="c5c73-200">This may include both hello operating system files and data files that hold personal identifiable information and other sensitive data.</span></span> <span data-ttu-id="c5c73-201">Versleuteling van Azure Storage-Service kan worden gebruikt tooprotect persoonlijke gegevens die zijn opgeslagen in blobs en bestanden.</span><span class="sxs-lookup"><span data-stu-id="c5c73-201">Azure Storage Service encryption can be used tooprotect personal data that is stored in blobs and files.</span></span> <span data-ttu-id="c5c73-202">Voor gegevens die zijn opgeslagen in Azure SQL-databases, beschermt met transparante gegevensversleuteling van niet-geautoriseerde blootstelling van persoonlijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="c5c73-202">For data that is stored in Azure SQL databases, Transparent Data Encryption provides protection from unauthorized exposure of personal information.</span></span>

<span data-ttu-id="c5c73-203">Hallo bedrijf kunt tooprotect Hallo sleutels die gebruikt tooencrypt gegevens in Azure zijn, Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="c5c73-203">tooprotect hello keys that are used tooencrypt data in Azure, hello company can use Azure Key Vault.</span></span> <span data-ttu-id="c5c73-204">Dit Hallo beheerproces stroomlijnt en schakelt Hallo bedrijf toomaintain beheer van sleutels die toegang tot en persoonlijke gegevens te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="c5c73-204">This streamlines hello key management process and enables hello company toomaintain control of keys that access and encrypt personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5c73-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c5c73-205">Next steps</span></span>

- [<span data-ttu-id="c5c73-206">Handleiding voor probleemoplossing voor Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="c5c73-206">Azure Disk Encryption Troubleshooting Guide</span></span>](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [<span data-ttu-id="c5c73-207">Een virtuele Machine van Azure versleutelen</span><span class="sxs-lookup"><span data-stu-id="c5c73-207">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [<span data-ttu-id="c5c73-208">Versleuteling van gegevens in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c5c73-208">Encryption of data in Azure Data Lake Store</span></span>](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [<span data-ttu-id="c5c73-209">Versleuteling van Azure DB Cosmos-database in rust</span><span class="sxs-lookup"><span data-stu-id="c5c73-209">Azure Cosmos DB database encryption at rest</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
