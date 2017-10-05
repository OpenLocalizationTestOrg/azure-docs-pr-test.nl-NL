---
title: Genereren en overdragen van met HSM beveiligde sleutels voor Azure Sleutelkluis | Microsoft Docs
description: Gebruik dit artikel voor hulp bij het plannen en brengt u uw eigen HSM beveiligde sleutels voor gebruik met Azure Sleutelkluis genereren. Ook wel BYOK of breng uw eigen sleutel.
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 5dbee1221f64045c64fecb344de1e03b2183dfb1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-generate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="65dbb-104">Genereren en overdragen HSM beveiligde sleutels voor Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="65dbb-104">How to generate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="65dbb-105">Inleiding</span><span class="sxs-lookup"><span data-stu-id="65dbb-105">Introduction</span></span>
<span data-ttu-id="65dbb-106">Voor de zekerheid wanneer u Azure Sleutelkluis, gebruikt kunt u importeren of genereren van sleutels in hardware security modules (HSM's) die de HSM-grens nooit verlaten.</span><span class="sxs-lookup"><span data-stu-id="65dbb-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="65dbb-107">Dit scenario wordt vaak aangeduid als *Breng uw eigen sleutel*, of BYOK.</span><span class="sxs-lookup"><span data-stu-id="65dbb-107">This scenario is often referred to as *bring your own key*, or BYOK.</span></span> <span data-ttu-id="65dbb-108">De HSM's zijn FIPS 140-2 Level 2-gevalideerde modules.</span><span class="sxs-lookup"><span data-stu-id="65dbb-108">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="65dbb-109">Azure Sleutelkluis gebruikt Thales nShield-familie van HSM's voor het beveiligen van uw sleutels.</span><span class="sxs-lookup"><span data-stu-id="65dbb-109">Azure Key Vault uses Thales nShield family of HSMs to protect your keys.</span></span>

<span data-ttu-id="65dbb-110">Gebruik de informatie in dit onderwerp voor hulp bij het plannen en brengt u uw eigen HSM beveiligde sleutels voor gebruik met Azure Sleutelkluis genereren.</span><span class="sxs-lookup"><span data-stu-id="65dbb-110">Use the information in this topic to help you plan for, generate, and then transfer your own HSM-protected keys to use with Azure Key Vault.</span></span>

<span data-ttu-id="65dbb-111">Deze functionaliteit is niet beschikbaar voor Azure China.</span><span class="sxs-lookup"><span data-stu-id="65dbb-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="65dbb-112">Zie voor meer informatie over Azure Sleutelkluis [wat is Azure Sleutelkluis?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="65dbb-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="65dbb-113">Zie voor een zelfstudie aan de slag, waaronder het maken van een sleutelkluis voor met HSM beveiligde sleutels, [aan de slag met Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="65dbb-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="65dbb-114">Meer informatie over het genereren en overdragen van een HSM beveiligde sleutel via Internet:</span><span class="sxs-lookup"><span data-stu-id="65dbb-114">More information about generating and transferring an HSM-protected key over the Internet:</span></span>

* <span data-ttu-id="65dbb-115">U kunt de sleutel genereren van een offline werkstation, wat minder gevoelig voor aanvallen.</span><span class="sxs-lookup"><span data-stu-id="65dbb-115">You generate the key from an offline workstation, which reduces the attack surface.</span></span>
* <span data-ttu-id="65dbb-116">De sleutel is gecodeerd met een KEK Key Exchange Key (), die versleuteld blijft totdat deze worden overgedragen naar de Azure Key Vault HSM's.</span><span class="sxs-lookup"><span data-stu-id="65dbb-116">The key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred to the Azure Key Vault HSMs.</span></span> <span data-ttu-id="65dbb-117">Alleen de versleutelde versie van uw sleutel verlaat het oorspronkelijke werkstation.</span><span class="sxs-lookup"><span data-stu-id="65dbb-117">Only the encrypted version of your key leaves the original workstation.</span></span>
* <span data-ttu-id="65dbb-118">De toolset stelt de eigenschappen van uw tenantsleutel die wordt uw sleutel aan de beveiligingswereld van Azure Sleutelkluis gebonden.</span><span class="sxs-lookup"><span data-stu-id="65dbb-118">The toolset sets properties on your tenant key that binds your key to the Azure Key Vault security world.</span></span> <span data-ttu-id="65dbb-119">Dus nadat de Azure Key Vault HSM's ontvangen en uw sleutel ontsleuteld, kunnen deze HSM's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="65dbb-119">So after the Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="65dbb-120">Uw sleutel kan niet worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="65dbb-120">Your key cannot be exported.</span></span> <span data-ttu-id="65dbb-121">Deze binding wordt afgedwongen door de Thales HSM's.</span><span class="sxs-lookup"><span data-stu-id="65dbb-121">This binding is enforced by the Thales HSMs.</span></span>
* <span data-ttu-id="65dbb-122">De KEK Key Exchange Key () die wordt gebruikt voor het versleutelen van uw sleutel wordt gegenereerd binnen de Azure Key Vault HSM's en kan niet worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="65dbb-122">The Key Exchange Key (KEK) that is used to encrypt your key is generated inside the Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="65dbb-123">De HSM's dwingen af dat er geen versie van de KEK buiten de HSM's kunnen worden.</span><span class="sxs-lookup"><span data-stu-id="65dbb-123">The HSMs enforce that there can be no clear version of the KEK outside the HSMs.</span></span> <span data-ttu-id="65dbb-124">Daarnaast bevat de toolset attest van Thales dat de KEK kan niet worden geëxporteerd en is gegenereerd binnen een legitieme door Thales vervaardigde HSM.</span><span class="sxs-lookup"><span data-stu-id="65dbb-124">In addition, the toolset includes attestation from Thales that the KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="65dbb-125">De toolset bevat een attest van Thales dat de Azure Sleutelkluis-beveiligingswereld ook is gegeneerd met een legitieme HSM, door Thales vervaardigde.</span><span class="sxs-lookup"><span data-stu-id="65dbb-125">The toolset includes attestation from Thales that the Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="65dbb-126">Deze verklaring is uw bewijs dat Microsoft legitieme hardware wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="65dbb-126">This attestation proves to you that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="65dbb-127">Microsoft gebruikt afzonderlijke kek's en afzonderlijke Beveiligingswerelden in elke geografische regio.</span><span class="sxs-lookup"><span data-stu-id="65dbb-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="65dbb-128">Deze scheiding zorgt ervoor dat uw sleutel kan alleen worden gebruikt in datacenters in de regio waarin u het versleuteld.</span><span class="sxs-lookup"><span data-stu-id="65dbb-128">This separation ensures that your key can be used only in data centers in the region in which you encrypted it.</span></span> <span data-ttu-id="65dbb-129">Bijvoorbeeld, kan niet een sleutel van een Europese klant worden gebruikt in datacenters in Noord-Amerika of Azië.</span><span class="sxs-lookup"><span data-stu-id="65dbb-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="65dbb-130">Meer informatie over Thales HSM's en Microsoft-services</span><span class="sxs-lookup"><span data-stu-id="65dbb-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="65dbb-131">Thales e-Security is een toonaangevende, wereldwijde leverancier van gegevensversleuteling en cyberbeveiliging beveiligingsoplossingen voor de financiële, hightech productie, overheid en technologiesector.</span><span class="sxs-lookup"><span data-stu-id="65dbb-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions to the financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="65dbb-132">Met een 40 jaar bogen van het beveiligen van bedrijfs- en overheidsgegevens worden oplossingen van Thales gebruikt door vier van de vijf grootste energie en ruimtevaart bedrijven.</span><span class="sxs-lookup"><span data-stu-id="65dbb-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of the five largest energy and aerospace companies.</span></span> <span data-ttu-id="65dbb-133">Hun oplossingen worden ook gebruikt door 22 NAVO-landen en meer dan 80 procent van de betalingstransacties wereldwijd beveiligen.</span><span class="sxs-lookup"><span data-stu-id="65dbb-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="65dbb-134">Microsoft heeft samengewerkt met Thales voor het verbeteren van de status van de illustraties HSM's.</span><span class="sxs-lookup"><span data-stu-id="65dbb-134">Microsoft has collaborated with Thales to enhance the state of art for HSMs.</span></span> <span data-ttu-id="65dbb-135">Deze verbeteringen kunnen u profiteren van de gebruikelijke voordelen van gehoste services, zonder verliest controle over uw sleutels.</span><span class="sxs-lookup"><span data-stu-id="65dbb-135">These enhancements enable you to get the typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="65dbb-136">In het bijzonder kan deze uitbreidingen Microsoft de HSM's zodat u niet te hoeft beheren.</span><span class="sxs-lookup"><span data-stu-id="65dbb-136">Specifically, these enhancements let Microsoft manage the HSMs so that you do not have to.</span></span> <span data-ttu-id="65dbb-137">Als een cloudservice schaalt Azure Key Vault op korte termijn om te voldoen aan de gebruikspieken binnen uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="65dbb-137">As a cloud service, Azure Key Vault scales up at short notice to meet your organization’s usage spikes.</span></span> <span data-ttu-id="65dbb-138">Op hetzelfde moment uw sleutel beschermd binnen de HSM's van Microsoft: U behoudt controle over de levenscyclus van de sleutel omdat u de sleutel te genereren en naar HSM's van Microsoft overdragen.</span><span class="sxs-lookup"><span data-stu-id="65dbb-138">At the same time, your key is protected inside Microsoft’s HSMs: You retain control over the key lifecycle because you generate the key and transfer it to Microsoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="65dbb-139">Implementatie van uw eigen BYOK (bring key) voor Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="65dbb-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="65dbb-140">Gebruik de volgende informatie en procedures als u uw eigen met HSM beschermde sleutel genereren en vervolgens naar Azure Sleutelkluis overbrengen, het bring uw eigen scenario key (BYOK).</span><span class="sxs-lookup"><span data-stu-id="65dbb-140">Use the following information and procedures if you will generate your own HSM-protected key and then transfer it to Azure Key Vault—the bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="65dbb-141">Vereisten voor BYOK</span><span class="sxs-lookup"><span data-stu-id="65dbb-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="65dbb-142">Zie de volgende tabel voor een lijst met vereisten voor uw eigen BYOK (bring key) voor Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="65dbb-142">See the following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="65dbb-143">Vereiste</span><span class="sxs-lookup"><span data-stu-id="65dbb-143">Requirement</span></span> | <span data-ttu-id="65dbb-144">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="65dbb-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="65dbb-145">Een abonnement op Azure</span><span class="sxs-lookup"><span data-stu-id="65dbb-145">A subscription to Azure</span></span> |<span data-ttu-id="65dbb-146">Voor het maken van een Azure Sleutelkluis, moet u een Azure-abonnement: [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="65dbb-146">To create an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="65dbb-147">De Azure Key Vault Premium servicecategorie ter ondersteuning van met HSM beveiligde sleutels</span><span class="sxs-lookup"><span data-stu-id="65dbb-147">The Azure Key Vault Premium service tier to support HSM-protected keys</span></span> |<span data-ttu-id="65dbb-148">Zie voor meer informatie over de servicecategorieën en mogelijkheden voor Azure Sleutelkluis de [prijzen van Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/) website.</span><span class="sxs-lookup"><span data-stu-id="65dbb-148">For more information about the service tiers and capabilities for Azure Key Vault, see the [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="65dbb-149">Thales HSM, smartcards en ondersteunende software</span><span class="sxs-lookup"><span data-stu-id="65dbb-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="65dbb-150">U moet toegang hebben tot een Thales Hardware Security Module en operationele basiskennis hebben van Thales HSM's.</span><span class="sxs-lookup"><span data-stu-id="65dbb-150">You must have access to a Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="65dbb-151">Zie [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) voor de lijst met compatibele modellen of om aan te schaffen van een HSM, als u nog geen abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="65dbb-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for the list of compatible models, or to purchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="65dbb-152">De volgende hardware en software:</span><span class="sxs-lookup"><span data-stu-id="65dbb-152">The following hardware and software:</span></span><ol><li><span data-ttu-id="65dbb-153">Een offline x64 werkstation met een besturingssysteem minimaal Windows 7 en Thales nShield-software die ten minste versie 11.50.</span><span class="sxs-lookup"><span data-stu-id="65dbb-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="65dbb-154">Als dit werkstation Windows 7 wordt uitgevoerd, moet u [Installeer Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span><span class="sxs-lookup"><span data-stu-id="65dbb-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="65dbb-155">Een werkstation dat is verbonden met Internet en een Windows-besturingssysteem minimaal Windows 7 en [Azure PowerShell](/powershell/azure/overview) **minimaal versie 1.1.0** geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="65dbb-155">A workstation that is connected to the Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="65dbb-156">Een USB-station of ander draagbaar opslagapparaat met ten minste 16 MB vrije ruimte heeft.</span><span class="sxs-lookup"><span data-stu-id="65dbb-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="65dbb-157">Uit veiligheidsoverwegingen is het raadzaam dat de eerste werkstation niet is verbonden met een netwerk.</span><span class="sxs-lookup"><span data-stu-id="65dbb-157">For security reasons, we recommend that the first workstation is not connected to a network.</span></span> <span data-ttu-id="65dbb-158">Deze aanbeveling is echter niet via een programma afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="65dbb-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="65dbb-159">Houd er rekening mee dat in de volgende instructies wordt dit werkstation aangeduid als niet-verbonden werkstation.</span><span class="sxs-lookup"><span data-stu-id="65dbb-159">Note that in the instructions that follow, this workstation is referred to as the disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="65dbb-160">Bovendien, als uw tenantsleutel bedoeld voor een productienetwerk is, raden wij aan dat u een tweede, afzonderlijk werkstation gebruiken om te downloaden van de toolset en de tenantsleutel te uploaden.</span><span class="sxs-lookup"><span data-stu-id="65dbb-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation to download the toolset and upload the tenant key.</span></span> <span data-ttu-id="65dbb-161">Maar voor testdoeleinden kunt u hetzelfde werkstation gebruiken als het eerste.</span><span class="sxs-lookup"><span data-stu-id="65dbb-161">But for testing purposes, you can use the same workstation as the first one.</span></span><br/><br/><span data-ttu-id="65dbb-162">Houd er rekening mee dat in de volgende instructies wordt dit tweede werkstation aangeduid als het met Internet verbonden werkstation.</span><span class="sxs-lookup"><span data-stu-id="65dbb-162">Note that in the instructions that follow, this second workstation is referred to as the Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-to-azure-key-vault-hsm"></a><span data-ttu-id="65dbb-163">Genereren en overdragen van uw sleutel naar Azure Key Vault HSM</span><span class="sxs-lookup"><span data-stu-id="65dbb-163">Generate and transfer your key to Azure Key Vault HSM</span></span>
<span data-ttu-id="65dbb-164">Gebruik de volgende vijf stappen voor het genereren en uw sleutel overdraagt naar een Azure Key Vault HSM:</span><span class="sxs-lookup"><span data-stu-id="65dbb-164">You will use the following five steps to generate and transfer your key to an Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="65dbb-165">Stap 1: Uw met Internet verbonden werkstation voorbereiden</span><span class="sxs-lookup"><span data-stu-id="65dbb-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="65dbb-166">Stap 2: Uw niet-verbonden werkstation voorbereiden</span><span class="sxs-lookup"><span data-stu-id="65dbb-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="65dbb-167">Stap 3: Uw sleutel genereren</span><span class="sxs-lookup"><span data-stu-id="65dbb-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="65dbb-168">Stap 4: De sleutel voor de overdracht voorbereiden</span><span class="sxs-lookup"><span data-stu-id="65dbb-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="65dbb-169">Stap 5: Uw sleutel overdraagt naar Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="65dbb-169">Step 5: Transfer your key to Azure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="65dbb-170">Stap 1: Uw met Internet verbonden werkstation voorbereiden</span><span class="sxs-lookup"><span data-stu-id="65dbb-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="65dbb-171">Deze eerste stap komen de volgende procedures op uw werkstation dat is verbonden met Internet.</span><span class="sxs-lookup"><span data-stu-id="65dbb-171">For this first step, do the following procedures on your workstation that is connected to the Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="65dbb-172">Stap 1.1: Azure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="65dbb-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="65dbb-173">Vanaf het Internet verbonden werkstation, download en installeer de Azure PowerShell-module met de cmdlets voor het beheren van Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="65dbb-173">From the Internet-connected workstation, download and install the Azure PowerShell module that includes the cmdlets to manage Azure Key Vault.</span></span> <span data-ttu-id="65dbb-174">Hiervoor moet een minimumversie van 0.8.13.</span><span class="sxs-lookup"><span data-stu-id="65dbb-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="65dbb-175">Zie voor installatie-instructies [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65dbb-175">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="65dbb-176">Stap 1.2: Uw Azure-abonnement-ID ophalen</span><span class="sxs-lookup"><span data-stu-id="65dbb-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="65dbb-177">Start een Azure PowerShell-sessie en meld u aan bij uw Azure-account met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="65dbb-177">Start an Azure PowerShell session and sign in to your Azure account by using the following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="65dbb-178">Voer in het pop-upvenster in de browser uw gebruikersnaam en wachtwoord voor uw Azure-account in.</span><span class="sxs-lookup"><span data-stu-id="65dbb-178">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="65dbb-179">Gebruik vervolgens de [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) opdracht:</span><span class="sxs-lookup"><span data-stu-id="65dbb-179">Then, use the [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="65dbb-180">Zoek de ID voor het abonnement dat u voor Azure Sleutelkluis gebruiken wilt van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="65dbb-180">From the output, locate the ID for the subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="65dbb-181">U kunt deze abonnement-ID wordt later nodig.</span><span class="sxs-lookup"><span data-stu-id="65dbb-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="65dbb-182">De Azure PowerShell-venster niet sluiten.</span><span class="sxs-lookup"><span data-stu-id="65dbb-182">Do not close the Azure PowerShell window.</span></span>

### <a name="step-13-download-the-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="65dbb-183">Stap 1.3: Download de BYOK-toolset voor Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="65dbb-183">Step 1.3: Download the BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="65dbb-184">Ga naar het Microsoft Download Center en [download de Azure Key Vault BYOK-hulpmiddelenset](http://www.microsoft.com/download/details.aspx?id=45345) voor uw geografische regio of het exemplaar van Azure.</span><span class="sxs-lookup"><span data-stu-id="65dbb-184">Go to the Microsoft Download Center and [download the Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="65dbb-185">Gebruik de volgende informatie om te identificeren, de naam van het pakket downloaden en de bijbehorende SHA-256-pakket-hash:</span><span class="sxs-lookup"><span data-stu-id="65dbb-185">Use the following information to identify the package name to download and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="65dbb-186">**Verenigde Staten:**</span><span class="sxs-lookup"><span data-stu-id="65dbb-186">**United States:**</span></span>

<span data-ttu-id="65dbb-187">KeyVault-BYOK-hulpprogramma's-Verenigd States.zip</span><span class="sxs-lookup"><span data-stu-id="65dbb-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="65dbb-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="65dbb-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="65dbb-189">**Europa:**</span><span class="sxs-lookup"><span data-stu-id="65dbb-189">**Europe:**</span></span>

<span data-ttu-id="65dbb-190">KeyVault-BYOK-hulpprogramma's-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="65dbb-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="65dbb-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="65dbb-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="65dbb-192">**Azië:**</span><span class="sxs-lookup"><span data-stu-id="65dbb-192">**Asia:**</span></span>

<span data-ttu-id="65dbb-193">KeyVault-BYOK-hulpprogramma's-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="65dbb-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="65dbb-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="65dbb-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="65dbb-195">**Latijns-Amerika:**</span><span class="sxs-lookup"><span data-stu-id="65dbb-195">**Latin America:**</span></span>

<span data-ttu-id="65dbb-196">KeyVault-BYOK-hulpprogramma's-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="65dbb-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="65dbb-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="65dbb-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="65dbb-198">**Japan:**</span><span class="sxs-lookup"><span data-stu-id="65dbb-198">**Japan:**</span></span>

<span data-ttu-id="65dbb-199">KeyVault-BYOK-hulpprogramma's-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="65dbb-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="65dbb-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="65dbb-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="65dbb-201">**Korea:**</span><span class="sxs-lookup"><span data-stu-id="65dbb-201">**Korea:**</span></span>

<span data-ttu-id="65dbb-202">KeyVault-BYOK-hulpprogramma's-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="65dbb-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="65dbb-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="65dbb-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="65dbb-204">**Australië:**</span><span class="sxs-lookup"><span data-stu-id="65dbb-204">**Australia:**</span></span>

<span data-ttu-id="65dbb-205">KeyVault-BYOK-hulpprogramma's-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="65dbb-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="65dbb-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="65dbb-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="65dbb-207">**Azure Government:**</span><span class="sxs-lookup"><span data-stu-id="65dbb-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="65dbb-208">KeyVault-BYOK-hulpprogramma's-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="65dbb-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="65dbb-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="65dbb-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="65dbb-210">**Amerikaanse overheid DOD:**</span><span class="sxs-lookup"><span data-stu-id="65dbb-210">**US Government DOD:**</span></span>

<span data-ttu-id="65dbb-211">KeyVault-BYOK-hulpprogramma's-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="65dbb-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="65dbb-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="65dbb-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="65dbb-213">**Canada:**</span><span class="sxs-lookup"><span data-stu-id="65dbb-213">**Canada:**</span></span>

<span data-ttu-id="65dbb-214">KeyVault-BYOK-hulpprogramma's-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="65dbb-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="65dbb-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="65dbb-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="65dbb-216">**Duitsland:**</span><span class="sxs-lookup"><span data-stu-id="65dbb-216">**Germany:**</span></span>

<span data-ttu-id="65dbb-217">KeyVault-BYOK-hulpprogramma's-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="65dbb-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="65dbb-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="65dbb-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="65dbb-219">**India:**</span><span class="sxs-lookup"><span data-stu-id="65dbb-219">**India:**</span></span>

<span data-ttu-id="65dbb-220">KeyVault-BYOK-hulpprogramma's-India.zip</span><span class="sxs-lookup"><span data-stu-id="65dbb-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="65dbb-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="65dbb-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="65dbb-222">**Verenigd Koninkrijk:**</span><span class="sxs-lookup"><span data-stu-id="65dbb-222">**United Kingdom:**</span></span>

<span data-ttu-id="65dbb-223">KeyVault-BYOK-hulpprogramma's-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="65dbb-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="65dbb-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="65dbb-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="65dbb-225">U kunt controleren de integriteit van de gedownloade BYOK-toolset van uw Azure PowerShell-sessie gebruiken de [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="65dbb-225">To validate the integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use the [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="65dbb-226">De toolset bevat het volgende:</span><span class="sxs-lookup"><span data-stu-id="65dbb-226">The toolset includes the following:</span></span>

* <span data-ttu-id="65dbb-227">Een KEK Key Exchange Key ()-pakket met een naam die begint met **BYOK-KEK - pkg-.**</span><span class="sxs-lookup"><span data-stu-id="65dbb-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="65dbb-228">Een beveiligingswereldpakket met een naam die begint met **BYOK-SecurityWorld - pkg-.**</span><span class="sxs-lookup"><span data-stu-id="65dbb-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="65dbb-229">Een pythonscript met de naam **verifykeypackage.py.**</span><span class="sxs-lookup"><span data-stu-id="65dbb-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="65dbb-230">Een uitvoerbaar opdrachtregelbestand met de naam **KeyTransferRemote.exe** en bijbehorende DLL-bestanden.</span><span class="sxs-lookup"><span data-stu-id="65dbb-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="65dbb-231">Een herdistrueerbare pakket Visual C++, met de naam **vcredist_x64.exe.**</span><span class="sxs-lookup"><span data-stu-id="65dbb-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="65dbb-232">Kopieer het pakket naar een USB-station of ander draagbaar opslagmedium.</span><span class="sxs-lookup"><span data-stu-id="65dbb-232">Copy the package to a USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="65dbb-233">Stap 2: Uw niet-verbonden werkstation voorbereiden</span><span class="sxs-lookup"><span data-stu-id="65dbb-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="65dbb-234">Voer de volgende procedures op het werkstation dat niet is verbonden met een netwerk (Internet of het interne netwerk) voor deze tweede stap.</span><span class="sxs-lookup"><span data-stu-id="65dbb-234">For this second step, do the following procedures on the workstation that is not connected to a network (either the Internet or your internal network).</span></span>

### <a name="step-21-prepare-the-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="65dbb-235">Stap 2.1: De niet-verbonden werkstation met Thales HSM voorbereiden</span><span class="sxs-lookup"><span data-stu-id="65dbb-235">Step 2.1: Prepare the disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="65dbb-236">De (Thales) nCipher-ondersteuningssoftware installeren op een Windows-computer en vervolgens een Thales HSM aan die computer te koppelen.</span><span class="sxs-lookup"><span data-stu-id="65dbb-236">Install the nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM to that computer.</span></span>

<span data-ttu-id="65dbb-237">Zorg ervoor dat de Thales-hulpprogramma's in het pad (**%nfast_home%\bin**).</span><span class="sxs-lookup"><span data-stu-id="65dbb-237">Ensure that the Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="65dbb-238">Typ bijvoorbeeld het volgende:</span><span class="sxs-lookup"><span data-stu-id="65dbb-238">For example, type the following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="65dbb-239">Zie voor meer informatie de handleiding inbegrepen bij de Thales HSM.</span><span class="sxs-lookup"><span data-stu-id="65dbb-239">For more information, see the user guide included with the Thales HSM.</span></span>

### <a name="step-22-install-the-byok-toolset-on-the-disconnected-workstation"></a><span data-ttu-id="65dbb-240">Step 2.2: Installeer de BYOK-toolset op niet-verbonden werkstation</span><span class="sxs-lookup"><span data-stu-id="65dbb-240">Step 2.2: Install the BYOK toolset on the disconnected workstation</span></span>
<span data-ttu-id="65dbb-241">Kopieer het BYOK-toolset pakket van het USB-station of ander draagbaar opslagmedium en doe het volgende:</span><span class="sxs-lookup"><span data-stu-id="65dbb-241">Copy the BYOK toolset package from the USB drive or other portable storage, and then do the following:</span></span>

1. <span data-ttu-id="65dbb-242">Pak de bestanden uit het gedownloade pakket naar een map.</span><span class="sxs-lookup"><span data-stu-id="65dbb-242">Extract the files from the downloaded package into any folder.</span></span>
2. <span data-ttu-id="65dbb-243">Voer vcredist_x64.exe uit in die map.</span><span class="sxs-lookup"><span data-stu-id="65dbb-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="65dbb-244">Volg de instructies voor de installatie het Visual C++ runtime-onderdelen voor Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="65dbb-244">Follow the instructions to the install the Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="65dbb-245">Stap 3: Uw sleutel genereren</span><span class="sxs-lookup"><span data-stu-id="65dbb-245">Step 3: Generate your key</span></span>
<span data-ttu-id="65dbb-246">Voer de volgende procedures op de niet-verbonden werkstation voor deze derde stap.</span><span class="sxs-lookup"><span data-stu-id="65dbb-246">For this third step, do the following procedures on the disconnected workstation.</span></span> <span data-ttu-id="65dbb-247">Voltooi deze stap moet uw HSM initialisatie-modus.</span><span class="sxs-lookup"><span data-stu-id="65dbb-247">To complete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-the-hsm-mode-to-i"></a><span data-ttu-id="65dbb-248">Stap 3.1: De HSM-modus wijzigen in 'I'</span><span class="sxs-lookup"><span data-stu-id="65dbb-248">Step 3.1: Change the HSM mode to 'I'</span></span>
<span data-ttu-id="65dbb-249">Als u Thales nShield Microsoft Edge wordt gebruikt om de modus te wijzigen: 1.</span><span class="sxs-lookup"><span data-stu-id="65dbb-249">If you are using Thales nShield Edge, to change the mode: 1.</span></span> <span data-ttu-id="65dbb-250">Gebruik de knop modus om de vereiste modus te markeren.</span><span class="sxs-lookup"><span data-stu-id="65dbb-250">Use the Mode button to highlight the required mode.</span></span> <span data-ttu-id="65dbb-251">2.</span><span class="sxs-lookup"><span data-stu-id="65dbb-251">2.</span></span> <span data-ttu-id="65dbb-252">Binnen een paar seconden en houdt u de knop wissen van een paar seconden.</span><span class="sxs-lookup"><span data-stu-id="65dbb-252">Within a few seconds, press and hold the Clear button for a couple of seconds.</span></span> <span data-ttu-id="65dbb-253">Als de modus wordt gewijzigd, wordt de nieuwe modus LED niet meer knippert en blijft branden.</span><span class="sxs-lookup"><span data-stu-id="65dbb-253">If the mode changes, the new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="65dbb-254">De Status LED onregelmatig mogelijk flash een paar seconden en vervolgens knippert regelmatig wanneer het apparaat gereed is.</span><span class="sxs-lookup"><span data-stu-id="65dbb-254">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span></span> <span data-ttu-id="65dbb-255">Anders wordt het apparaat blijft in de huidige modus, met de juiste modus LED branden.</span><span class="sxs-lookup"><span data-stu-id="65dbb-255">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="65dbb-256">Stap 3.2: Maak een beveiligingswereld</span><span class="sxs-lookup"><span data-stu-id="65dbb-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="65dbb-257">Start een opdrachtprompt en voer het nieuwe-wereld-programma van Thales.</span><span class="sxs-lookup"><span data-stu-id="65dbb-257">Start a command prompt and run the Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="65dbb-258">Dit programma maakt een **Beveiligingswereld** bestand op % NFAST_KMDATA%\local\world, wat overeenkomt met de map C:\ProgramData\nCipher\Key Management Settings\User.</span><span class="sxs-lookup"><span data-stu-id="65dbb-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds to the C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="65dbb-259">U kunt andere waarden gebruiken voor het quorum, maar in ons voorbeeld wordt u gevraagd drie lege kaarten en pincodes voor elk adres invoeren.</span><span class="sxs-lookup"><span data-stu-id="65dbb-259">You can use different values for the quorum but in our example, you’re prompted to enter three blank cards and pins for each one.</span></span> <span data-ttu-id="65dbb-260">Vervolgens wordt door elke twee kaarten volledige toegang geven tot de beveiligingswereld.</span><span class="sxs-lookup"><span data-stu-id="65dbb-260">Then, any two cards give full access to the security world.</span></span> <span data-ttu-id="65dbb-261">Deze kaarten worden de **Beheerderskaartenset** voor de nieuwe beveiligingswereld.</span><span class="sxs-lookup"><span data-stu-id="65dbb-261">These cards become the **Administrator Card Set** for the new security world.</span></span>

<span data-ttu-id="65dbb-262">Ga daarna als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="65dbb-262">Then do the following:</span></span>

* <span data-ttu-id="65dbb-263">Back-up van het wereldbestand.</span><span class="sxs-lookup"><span data-stu-id="65dbb-263">Back up the world file.</span></span> <span data-ttu-id="65dbb-264">Secure en beveiligen van het wereldbestand, de Beheerderskaarten en de bijbehorende pincodes en zorg ervoor dat niemand toegang tot meer dan één kaart heeft.</span><span class="sxs-lookup"><span data-stu-id="65dbb-264">Secure and protect the world file, the Administrator Cards, and their pins, and make sure that no single person has access to more than one card.</span></span>

### <a name="step-33-change-the-hsm-mode-to-o"></a><span data-ttu-id="65dbb-265">Stap 3.3: Wijzig de HSM-modus ' o '</span><span class="sxs-lookup"><span data-stu-id="65dbb-265">Step 3.3: Change the HSM mode to 'O'</span></span>
<span data-ttu-id="65dbb-266">Als u Thales nShield Microsoft Edge wordt gebruikt om de modus te wijzigen: 1.</span><span class="sxs-lookup"><span data-stu-id="65dbb-266">If you are using Thales nShield Edge, to change the mode: 1.</span></span> <span data-ttu-id="65dbb-267">Gebruik de knop modus om de vereiste modus te markeren.</span><span class="sxs-lookup"><span data-stu-id="65dbb-267">Use the Mode button to highlight the required mode.</span></span> <span data-ttu-id="65dbb-268">2.</span><span class="sxs-lookup"><span data-stu-id="65dbb-268">2.</span></span> <span data-ttu-id="65dbb-269">Binnen een paar seconden en houdt u de knop wissen van een paar seconden.</span><span class="sxs-lookup"><span data-stu-id="65dbb-269">Within a few seconds, press and hold the Clear button for a couple of seconds.</span></span> <span data-ttu-id="65dbb-270">Als de modus wordt gewijzigd, wordt de nieuwe modus LED niet meer knippert en blijft branden.</span><span class="sxs-lookup"><span data-stu-id="65dbb-270">If the mode changes, the new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="65dbb-271">De Status LED onregelmatig mogelijk flash een paar seconden en vervolgens knippert regelmatig wanneer het apparaat gereed is.</span><span class="sxs-lookup"><span data-stu-id="65dbb-271">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span></span> <span data-ttu-id="65dbb-272">Anders wordt het apparaat blijft in de huidige modus, met de juiste modus LED branden.</span><span class="sxs-lookup"><span data-stu-id="65dbb-272">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span></span>


### <a name="step-34-validate-the-downloaded-package"></a><span data-ttu-id="65dbb-273">Stap 3.4: Het gedownloade pakket valideren</span><span class="sxs-lookup"><span data-stu-id="65dbb-273">Step 3.4: Validate the downloaded package</span></span>
<span data-ttu-id="65dbb-274">Deze stap is optioneel maar aanbevolen zodat u het volgende kunt valideren:</span><span class="sxs-lookup"><span data-stu-id="65dbb-274">This step is optional but recommended so that you can validate the following:</span></span>

* <span data-ttu-id="65dbb-275">De uitwisselingssleutel van de sleutel die is opgenomen in de hulpmiddelenset, is gegenereerd met een legitieme Thales HSM.</span><span class="sxs-lookup"><span data-stu-id="65dbb-275">The Key Exchange Key that is included in the toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="65dbb-276">De hash van de Beveiligingswereld die is opgenomen in de hulpmiddelenset, is gegenereerd met een legitieme Thales HSM.</span><span class="sxs-lookup"><span data-stu-id="65dbb-276">The hash of the Security World that is included in the toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="65dbb-277">De Key Exchange is niet exporteerbaar.</span><span class="sxs-lookup"><span data-stu-id="65dbb-277">The Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="65dbb-278">Als u wilt het gedownloade pakket valideren, moet de HSM moet worden verbonden, zijn ingeschakeld, en een beveiligingswereld (zoals de groep die u zojuist hebt gemaakt).</span><span class="sxs-lookup"><span data-stu-id="65dbb-278">To validate the downloaded package, the HSM must be connected, powered on, and must have a security world on it (such as the one you’ve just created).</span></span>
>
>

<span data-ttu-id="65dbb-279">Het gedownloade pakket valideren:</span><span class="sxs-lookup"><span data-stu-id="65dbb-279">To validate the downloaded package:</span></span>

1. <span data-ttu-id="65dbb-280">Voer het script door één van de volgende, afhankelijk van uw geografische regio of het exemplaar van Azure te typen:</span><span class="sxs-lookup"><span data-stu-id="65dbb-280">Run the verifykeypackage.py script by typing one of the following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="65dbb-281">Voor Noord-Amerika:</span><span class="sxs-lookup"><span data-stu-id="65dbb-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="65dbb-282">Voor Europa:</span><span class="sxs-lookup"><span data-stu-id="65dbb-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="65dbb-283">Voor Azië:</span><span class="sxs-lookup"><span data-stu-id="65dbb-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="65dbb-284">Voor Latijns-Amerika:</span><span class="sxs-lookup"><span data-stu-id="65dbb-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="65dbb-285">Voor Japan:</span><span class="sxs-lookup"><span data-stu-id="65dbb-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="65dbb-286">Voor Korea:</span><span class="sxs-lookup"><span data-stu-id="65dbb-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="65dbb-287">Voor Australië:</span><span class="sxs-lookup"><span data-stu-id="65dbb-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="65dbb-288">Voor [Azure Government](https://azure.microsoft.com/features/gov/), waarbij het US government-exemplaar van Azure wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="65dbb-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="65dbb-289">Voor de overheid van de VS DOD:</span><span class="sxs-lookup"><span data-stu-id="65dbb-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="65dbb-290">Voor Canada:</span><span class="sxs-lookup"><span data-stu-id="65dbb-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="65dbb-291">Voor Duitsland:</span><span class="sxs-lookup"><span data-stu-id="65dbb-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="65dbb-292">Voor India:</span><span class="sxs-lookup"><span data-stu-id="65dbb-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="65dbb-293">De Thales-software bevat python in %NFAST_HOME%\python\bin</span><span class="sxs-lookup"><span data-stu-id="65dbb-293">The Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="65dbb-294">Controleer of u het volgende, waarmee wordt aangegeven validatie is geslaagd: **resultaat: geslaagd**</span><span class="sxs-lookup"><span data-stu-id="65dbb-294">Confirm that you see the following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="65dbb-295">Dit script valideert de ondertekenaarsketen tot de Thales-hoofdsleutel.</span><span class="sxs-lookup"><span data-stu-id="65dbb-295">This script validates the signer chain up to the Thales root key.</span></span> <span data-ttu-id="65dbb-296">De hash van deze hoofdsleutel is ingesloten in het script en de waarde moet **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span><span class="sxs-lookup"><span data-stu-id="65dbb-296">The hash of this root key is embedded in the script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="65dbb-297">U kunt deze waarde ook afzonderlijk controleren in via de [Thales-website](http://www.thalesesec.com/).</span><span class="sxs-lookup"><span data-stu-id="65dbb-297">You can also confirm this value separately by visiting the [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="65dbb-298">U kunt nu een nieuwe sleutel te maken.</span><span class="sxs-lookup"><span data-stu-id="65dbb-298">You’re now ready to create a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="65dbb-299">Stap 3.5: Maak een nieuwe sleutel</span><span class="sxs-lookup"><span data-stu-id="65dbb-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="65dbb-300">Een sleutel genereren met behulp van de Thales **generatekey** programma.</span><span class="sxs-lookup"><span data-stu-id="65dbb-300">Generate a key by using the Thales **generatekey** program.</span></span>

<span data-ttu-id="65dbb-301">Voer de volgende opdracht om de sleutel te genereren:</span><span class="sxs-lookup"><span data-stu-id="65dbb-301">Run the following command to generate the key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="65dbb-302">Wanneer u deze opdracht uitvoert, gebruikt u deze instructies:</span><span class="sxs-lookup"><span data-stu-id="65dbb-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="65dbb-303">De parameter *beveiligen* moet worden ingesteld op de waarde **module**, zoals wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="65dbb-303">The parameter *protect* must be set to the value **module**, as shown.</span></span> <span data-ttu-id="65dbb-304">Hiermee maakt u een modulair beveiligde sleutel.</span><span class="sxs-lookup"><span data-stu-id="65dbb-304">This creates a module-protected key.</span></span> <span data-ttu-id="65dbb-305">De BYOK-toolset biedt geen ondersteuning voor OCS beveiligde sleutels.</span><span class="sxs-lookup"><span data-stu-id="65dbb-305">The BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="65dbb-306">Vervang de waarde van *contosokey* voor de **ident** en **plainname** met een tekenreekswaarde.</span><span class="sxs-lookup"><span data-stu-id="65dbb-306">Replace the value of *contosokey* for the **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="65dbb-307">Om administratieve overhead te minimaliseren en verlaagt de kans op fouten, is het raadzaam dat u dezelfde waarde voor beide gebruiken.</span><span class="sxs-lookup"><span data-stu-id="65dbb-307">To minimize administrative overheads and reduce the risk of errors, we recommend that you use the same value for both.</span></span> <span data-ttu-id="65dbb-308">De **ident** waarde mag alleen cijfers, streepjes en kleine letters bestaan.</span><span class="sxs-lookup"><span data-stu-id="65dbb-308">The **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="65dbb-309">De pubexp is leeg (standaard) in dit voorbeeld, maar u kunt specifieke waarden opgeven.</span><span class="sxs-lookup"><span data-stu-id="65dbb-309">The pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="65dbb-310">Zie de Thales-documentatie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="65dbb-310">For more information, see the Thales documentation.</span></span>

<span data-ttu-id="65dbb-311">Deze opdracht maakt u een Tokenized sleutelbestand in uw map %NFAST_KMDATA%\local met een naam die begint met **key_simple_**, gevolgd door de **ident** dat is opgegeven in de opdracht.</span><span class="sxs-lookup"><span data-stu-id="65dbb-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by the **ident** that was specified in the command.</span></span> <span data-ttu-id="65dbb-312">Bijvoorbeeld: **key_simple_contosokey**.</span><span class="sxs-lookup"><span data-stu-id="65dbb-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="65dbb-313">Dit bestand bevat een versleutelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="65dbb-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="65dbb-314">Back-up van deze Tokenized sleutelbestand op een veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="65dbb-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65dbb-315">Wanneer u uw sleutel later naar Azure Sleutelkluis overdraagt, Microsoft kan sleutel niet exporteren dit voor u dus is het erg belangrijk back-up van uw sleutel en beveiligingswereld veilig.</span><span class="sxs-lookup"><span data-stu-id="65dbb-315">When you later transfer your key to Azure Key Vault, Microsoft cannot export this key back to you so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="65dbb-316">Neem contact op met Thales voor richtlijnen en aanbevolen procedures voor back-ups van uw sleutel.</span><span class="sxs-lookup"><span data-stu-id="65dbb-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="65dbb-317">U bent nu klaar om over te dragen van uw sleutel naar Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="65dbb-317">You are now ready to transfer your key to Azure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="65dbb-318">Stap 4: De sleutel voor de overdracht voorbereiden</span><span class="sxs-lookup"><span data-stu-id="65dbb-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="65dbb-319">Voer de volgende procedures op de niet-verbonden werkstation voor deze vierde stap.</span><span class="sxs-lookup"><span data-stu-id="65dbb-319">For this fourth step, do the following procedures on the disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="65dbb-320">Stap 4.1: Maak een kopie van uw sleutel met beperkte machtigingen</span><span class="sxs-lookup"><span data-stu-id="65dbb-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="65dbb-321">Open een nieuw opdrachtpromptvenster en wijzig de huidige map naar de locatie waar u de BYOK-zip-bestand hebt uitgepakt.</span><span class="sxs-lookup"><span data-stu-id="65dbb-321">Open a new command prompt and change the current directory to the location where you unzipped the BYOK zip file.</span></span> <span data-ttu-id="65dbb-322">Als u de machtigingen voor uw sleutel vanaf een opdrachtprompt, voert u een van de volgende, afhankelijk van uw geografische regio of het exemplaar van Azure:</span><span class="sxs-lookup"><span data-stu-id="65dbb-322">To reduce the permissions on your key, from a command prompt, run one of the following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="65dbb-323">Voor Noord-Amerika:</span><span class="sxs-lookup"><span data-stu-id="65dbb-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="65dbb-324">Voor Europa:</span><span class="sxs-lookup"><span data-stu-id="65dbb-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="65dbb-325">Voor Azië:</span><span class="sxs-lookup"><span data-stu-id="65dbb-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="65dbb-326">Voor Latijns-Amerika:</span><span class="sxs-lookup"><span data-stu-id="65dbb-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="65dbb-327">Voor Japan:</span><span class="sxs-lookup"><span data-stu-id="65dbb-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="65dbb-328">Voor Korea:</span><span class="sxs-lookup"><span data-stu-id="65dbb-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="65dbb-329">Voor Australië:</span><span class="sxs-lookup"><span data-stu-id="65dbb-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="65dbb-330">Voor [Azure Government](https://azure.microsoft.com/features/gov/), waarbij het US government-exemplaar van Azure wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="65dbb-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="65dbb-331">Voor de overheid van de VS DOD:</span><span class="sxs-lookup"><span data-stu-id="65dbb-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="65dbb-332">Voor Canada:</span><span class="sxs-lookup"><span data-stu-id="65dbb-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="65dbb-333">Voor Duitsland:</span><span class="sxs-lookup"><span data-stu-id="65dbb-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="65dbb-334">Voor India:</span><span class="sxs-lookup"><span data-stu-id="65dbb-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="65dbb-335">Wanneer u deze opdracht uitvoert, vervangt *contosokey* door dezelfde waarde als u hebt opgegeven in **stap 3.5: Maak een nieuwe sleutel** van de [uw sleutel genereren](#step-3-generate-your-key) stap.</span><span class="sxs-lookup"><span data-stu-id="65dbb-335">When you run this command, replace *contosokey* with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="65dbb-336">U wordt gevraagd om uw security world admin-kaarten.</span><span class="sxs-lookup"><span data-stu-id="65dbb-336">You are asked to plug in your security world admin cards.</span></span>

<span data-ttu-id="65dbb-337">Wanneer de opdracht is voltooid, ziet u **resultaat: SUCCES** en de kopie van uw sleutel met beperkte machtigingen zich in het bestand met de naam key_xferacId_<contosokey>.</span><span class="sxs-lookup"><span data-stu-id="65dbb-337">When the command completes, you see **Result: SUCCESS** and the copy of your key with reduced permissions are in the file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="65dbb-338">U kunt inspecteert de ACL's met behulp van volgende opdrachten met de Thales-hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="65dbb-338">You may inspects the ACLS using following commands using the Thales utilities:</span></span>

* <span data-ttu-id="65dbb-339">aclprint.PY:</span><span class="sxs-lookup"><span data-stu-id="65dbb-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="65dbb-340">kmfile-dump.exe:</span><span class="sxs-lookup"><span data-stu-id="65dbb-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="65dbb-341">Wanneer u deze opdrachten uitvoert, vervangt u contosokey met dezelfde waarde die u hebt opgegeven in **stap 3.5: Maak een nieuwe sleutel** van de [uw sleutel genereren](#step-3-generate-your-key) stap.</span><span class="sxs-lookup"><span data-stu-id="65dbb-341">When you run these commands, replace contosokey with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="65dbb-342">Stap 4.2: Versleutel de sleutel met behulp van Microsoft sleutel voor sleuteluitwisseling</span><span class="sxs-lookup"><span data-stu-id="65dbb-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="65dbb-343">Voer een van de volgende opdrachten uit, afhankelijk van uw geografische regio of het exemplaar van Azure:</span><span class="sxs-lookup"><span data-stu-id="65dbb-343">Run one of the following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="65dbb-344">Voor Noord-Amerika:</span><span class="sxs-lookup"><span data-stu-id="65dbb-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65dbb-345">Voor Europa:</span><span class="sxs-lookup"><span data-stu-id="65dbb-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65dbb-346">Voor Azië:</span><span class="sxs-lookup"><span data-stu-id="65dbb-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65dbb-347">Voor Latijns-Amerika:</span><span class="sxs-lookup"><span data-stu-id="65dbb-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65dbb-348">Voor Japan:</span><span class="sxs-lookup"><span data-stu-id="65dbb-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65dbb-349">Voor Korea:</span><span class="sxs-lookup"><span data-stu-id="65dbb-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65dbb-350">Voor Australië:</span><span class="sxs-lookup"><span data-stu-id="65dbb-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65dbb-351">Voor [Azure Government](https://azure.microsoft.com/features/gov/), waarbij het US government-exemplaar van Azure wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="65dbb-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65dbb-352">Voor de overheid van de VS DOD:</span><span class="sxs-lookup"><span data-stu-id="65dbb-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65dbb-353">Voor Canada:</span><span class="sxs-lookup"><span data-stu-id="65dbb-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65dbb-354">Voor Duitsland:</span><span class="sxs-lookup"><span data-stu-id="65dbb-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="65dbb-355">Voor India:</span><span class="sxs-lookup"><span data-stu-id="65dbb-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="65dbb-356">Wanneer u deze opdracht uitvoert, gebruikt u deze instructies:</span><span class="sxs-lookup"><span data-stu-id="65dbb-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="65dbb-357">Vervang *contosokey* met de id die u gebruikt voor het genereren van de sleutel in **stap 3.5: Maak een nieuwe sleutel** van de [uw sleutel genereren](#step-3-generate-your-key) stap.</span><span class="sxs-lookup"><span data-stu-id="65dbb-357">Replace *contosokey* with the identifier that you used to generate the key in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="65dbb-358">Vervang *SubscriptionID* met de ID van de Azure-abonnement dat de sleutelkluis bevat.</span><span class="sxs-lookup"><span data-stu-id="65dbb-358">Replace *SubscriptionID* with the ID of the Azure subscription that contains your key vault.</span></span> <span data-ttu-id="65dbb-359">U hebt deze waarde opgehaald in **stap 1.2: uw Azure-abonnement-ID ophalen** van de [uw met Internet verbonden werkstation voorbereiden](#step-1-prepare-your-internet-connected-workstation) stap.</span><span class="sxs-lookup"><span data-stu-id="65dbb-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from the [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="65dbb-360">Vervang *ContosoFirstHSMKey* met een label dat wordt gebruikt voor naam van uw uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="65dbb-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="65dbb-361">Wanneer dit succesvol is voltooid, wordt weergegeven **resultaat: SUCCES** en er is een nieuw bestand in de huidige map met de volgende naam: KeyTransferPackage -*ContosoFirstHSMkey*.byok</span><span class="sxs-lookup"><span data-stu-id="65dbb-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in the current folder that has the following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-to-the-internet-connected-workstation"></a><span data-ttu-id="65dbb-362">Stap 4.3: Kopieer uw pakket voor sleuteloverdracht naar het Internet verbonden werkstation</span><span class="sxs-lookup"><span data-stu-id="65dbb-362">Step 4.3: Copy your key transfer package to the Internet-connected workstation</span></span>
<span data-ttu-id="65dbb-363">Gebruik een USB-station of ander draagbaar opslagmedium kopiëren van het bestand voor uitvoer van de vorige stap (KeyTransferPackage-ContosoFirstHSMkey.byok) naar uw met Internet verbonden werkstation.</span><span class="sxs-lookup"><span data-stu-id="65dbb-363">Use a USB drive or other portable storage to copy the output file from the previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) to your Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-to-azure-key-vault"></a><span data-ttu-id="65dbb-364">Stap 5: Uw sleutel overdraagt naar Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="65dbb-364">Step 5: Transfer your key to Azure Key Vault</span></span>
<span data-ttu-id="65dbb-365">Voor deze laatste stap op het Internet verbonden werkstation maakt gebruik van de [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet voor het uploaden van het sleuteloverdrachtpakket die u hebt gekopieerd uit de niet-verbonden werkstation naar Azure Key Vault HSM:</span><span class="sxs-lookup"><span data-stu-id="65dbb-365">For this final step, on the Internet-connected workstation, use the [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet to upload the key transfer package that you copied from the disconnected workstation to the Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="65dbb-366">Als het uploaden voltooid is, ziet u de eigenschappen van de sleutel die u zojuist hebt toegevoegd wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="65dbb-366">If the upload is successful, you see displayed the properties of the key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65dbb-367">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="65dbb-367">Next steps</span></span>
<span data-ttu-id="65dbb-368">U kunt deze met HSM beschermde sleutel nu gebruiken in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="65dbb-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="65dbb-369">Zie voor meer informatie de **als u wilt gebruiken een hardware security module (HSM)** sectie het [aan de slag met Azure Key Vault](key-vault-get-started.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="65dbb-369">For more information, see the **If you want to use a hardware security module (HSM)** section in the [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
