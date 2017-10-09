---
title: aaaHow toogenerate en de overdracht met HSM beveiligde sleutels voor Azure Sleutelkluis | Microsoft Docs
description: Gebruik dit artikel toohelp plannen, te genereren en brengt u uw eigen toouse HSM beveiligde sleutels met Azure Sleutelkluis. Ook wel BYOK of breng uw eigen sleutel.
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
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="a84f2-104">Hoe toogenerate en de overdracht met HSM beveiligde sleutels voor Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="a84f2-104">How toogenerate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="a84f2-105">Inleiding</span><span class="sxs-lookup"><span data-stu-id="a84f2-105">Introduction</span></span>
<span data-ttu-id="a84f2-106">Voor de zekerheid wanneer u Azure Sleutelkluis, gebruikt kunt u importeren of genereren van sleutels in hardware security modules (HSM's) die Hallo HSM-grens nooit verlaten.</span><span class="sxs-lookup"><span data-stu-id="a84f2-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="a84f2-107">Dit scenario is het vaak waarnaar wordt verwezen tooas *Breng uw eigen sleutel*, of BYOK.</span><span class="sxs-lookup"><span data-stu-id="a84f2-107">This scenario is often referred tooas *bring your own key*, or BYOK.</span></span> <span data-ttu-id="a84f2-108">Hallo HSM's zijn FIPS 140-2 Level 2-gevalideerde modules.</span><span class="sxs-lookup"><span data-stu-id="a84f2-108">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="a84f2-109">Azure Sleutelkluis gebruikt Thales nShield-familie van HSM's tooprotect uw sleutels.</span><span class="sxs-lookup"><span data-stu-id="a84f2-109">Azure Key Vault uses Thales nShield family of HSMs tooprotect your keys.</span></span>

<span data-ttu-id="a84f2-110">Gebruik Hallo informatie in dit onderwerp toohelp plannen, te genereren en brengt u uw eigen toouse HSM beveiligde sleutels met Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="a84f2-110">Use hello information in this topic toohelp you plan for, generate, and then transfer your own HSM-protected keys toouse with Azure Key Vault.</span></span>

<span data-ttu-id="a84f2-111">Deze functionaliteit is niet beschikbaar voor Azure China.</span><span class="sxs-lookup"><span data-stu-id="a84f2-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="a84f2-112">Zie voor meer informatie over Azure Sleutelkluis [wat is Azure Sleutelkluis?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="a84f2-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="a84f2-113">Zie voor een zelfstudie aan de slag, waaronder het maken van een sleutelkluis voor met HSM beveiligde sleutels, [aan de slag met Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a84f2-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="a84f2-114">Meer informatie over het genereren en overdragen van een HSM beveiligde sleutel via Internet Hallo:</span><span class="sxs-lookup"><span data-stu-id="a84f2-114">More information about generating and transferring an HSM-protected key over hello Internet:</span></span>

* <span data-ttu-id="a84f2-115">U Hallo sleutel genereren van een offline werkstation, waardoor de kwetsbaarheid Hallo.</span><span class="sxs-lookup"><span data-stu-id="a84f2-115">You generate hello key from an offline workstation, which reduces hello attack surface.</span></span>
* <span data-ttu-id="a84f2-116">Hallo-sleutel is versleuteld met een KEK Key Exchange Key (), die versleuteld blijft totdat deze overgedragen toohello Azure Key Vault HSM's is.</span><span class="sxs-lookup"><span data-stu-id="a84f2-116">hello key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred toohello Azure Key Vault HSMs.</span></span> <span data-ttu-id="a84f2-117">Alleen Hallo versleutelde versie van uw sleutel verlaat Hallo oorspronkelijke werkstation.</span><span class="sxs-lookup"><span data-stu-id="a84f2-117">Only hello encrypted version of your key leaves hello original workstation.</span></span>
* <span data-ttu-id="a84f2-118">Hallo toolset stelt de eigenschappen van uw tenantsleutel waaraan uw belangrijkste toohello beveiligingswereld van Azure Sleutelkluis is gebonden.</span><span class="sxs-lookup"><span data-stu-id="a84f2-118">hello toolset sets properties on your tenant key that binds your key toohello Azure Key Vault security world.</span></span> <span data-ttu-id="a84f2-119">Dus nadat hello Azure Key Vault HSM's ontvangen en uw sleutel ontsleuteld, kunnen deze HSM's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a84f2-119">So after hello Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="a84f2-120">Uw sleutel kan niet worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="a84f2-120">Your key cannot be exported.</span></span> <span data-ttu-id="a84f2-121">Deze binding wordt afgedwongen door Hallo Thales HSM's.</span><span class="sxs-lookup"><span data-stu-id="a84f2-121">This binding is enforced by hello Thales HSMs.</span></span>
* <span data-ttu-id="a84f2-122">Hello KEK Key Exchange Key () die is gebruikt tooencrypt uw sleutel wordt gegenereerd binnen hello Azure Key Vault HSM's en kan niet worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="a84f2-122">hello Key Exchange Key (KEK) that is used tooencrypt your key is generated inside hello Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="a84f2-123">Hallo HSM's dwingen af dat er geen versie van Hallo KEK buiten Hallo HSM's kunnen worden.</span><span class="sxs-lookup"><span data-stu-id="a84f2-123">hello HSMs enforce that there can be no clear version of hello KEK outside hello HSMs.</span></span> <span data-ttu-id="a84f2-124">Daarnaast bevat de toolset Hallo attest van Thales dat Hallo KEK-sleutel kan niet worden geëxporteerd en is gegenereerd binnen een legitieme door Thales vervaardigde HSM.</span><span class="sxs-lookup"><span data-stu-id="a84f2-124">In addition, hello toolset includes attestation from Thales that hello KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="a84f2-125">Hallo toolset bevat een attest van Thales dat hello Azure Key Vault beveiligingswereld ook is gegeneerd met een legitieme HSM, door Thales vervaardigde.</span><span class="sxs-lookup"><span data-stu-id="a84f2-125">hello toolset includes attestation from Thales that hello Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="a84f2-126">Deze verklaring bewijst tooyou dat Microsoft legitieme hardware wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a84f2-126">This attestation proves tooyou that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="a84f2-127">Microsoft gebruikt afzonderlijke kek's en afzonderlijke Beveiligingswerelden in elke geografische regio.</span><span class="sxs-lookup"><span data-stu-id="a84f2-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="a84f2-128">Deze scheiding zorgt ervoor dat uw sleutel kan alleen worden gebruikt in datacenters in Hallo regio waarin u het versleuteld.</span><span class="sxs-lookup"><span data-stu-id="a84f2-128">This separation ensures that your key can be used only in data centers in hello region in which you encrypted it.</span></span> <span data-ttu-id="a84f2-129">Bijvoorbeeld, kan niet een sleutel van een Europese klant worden gebruikt in datacenters in Noord-Amerika of Azië.</span><span class="sxs-lookup"><span data-stu-id="a84f2-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="a84f2-130">Meer informatie over Thales HSM's en Microsoft-services</span><span class="sxs-lookup"><span data-stu-id="a84f2-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="a84f2-131">Thales e-Security is een toonaangevende, wereldwijde leverancier van gegevensversleuteling en cyberbeveiliging beveiliging oplossingen toohello financiële diensten, high tech productie, overheid en technologiesector.</span><span class="sxs-lookup"><span data-stu-id="a84f2-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions toohello financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="a84f2-132">Met een 40 jaar bogen van het beveiligen van bedrijfs- en overheidsgegevens worden oplossingen van Thales gebruikt door vier Hallo vijf grootste energie en ruimtevaart bedrijven.</span><span class="sxs-lookup"><span data-stu-id="a84f2-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of hello five largest energy and aerospace companies.</span></span> <span data-ttu-id="a84f2-133">Hun oplossingen worden ook gebruikt door 22 NAVO-landen en meer dan 80 procent van de betalingstransacties wereldwijd beveiligen.</span><span class="sxs-lookup"><span data-stu-id="a84f2-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="a84f2-134">Microsoft heeft samengewerkt met Thales tooenhance Hallo status van de illustraties HSM's.</span><span class="sxs-lookup"><span data-stu-id="a84f2-134">Microsoft has collaborated with Thales tooenhance hello state of art for HSMs.</span></span> <span data-ttu-id="a84f2-135">Dankzij deze verbeteringen kunt u tooget Hallo gebruikelijke voordelen van gehoste services, zonder verliest controle over uw sleutels.</span><span class="sxs-lookup"><span data-stu-id="a84f2-135">These enhancements enable you tooget hello typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="a84f2-136">In het bijzonder kan deze uitbreidingen Microsoft hello HSM's beheren, zodat u niet te hoeft.</span><span class="sxs-lookup"><span data-stu-id="a84f2-136">Specifically, these enhancements let Microsoft manage hello HSMs so that you do not have to.</span></span> <span data-ttu-id="a84f2-137">Als een cloud die service, Azure Key Vault op korte termijn toomeet schaalt bereikt gebruik van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="a84f2-137">As a cloud service, Azure Key Vault scales up at short notice toomeet your organization’s usage spikes.</span></span> <span data-ttu-id="a84f2-138">AT Hallo dezelfde tijd, uw sleutel beschermd binnen de HSM's van Microsoft: U controle over de levenscyclus van Hallo behouden omdat u Hallo sleutel genereren en tooMicrosoft van HSM's overdragen.</span><span class="sxs-lookup"><span data-stu-id="a84f2-138">At hello same time, your key is protected inside Microsoft’s HSMs: You retain control over hello key lifecycle because you generate hello key and transfer it tooMicrosoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="a84f2-139">Implementatie van uw eigen BYOK (bring key) voor Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="a84f2-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="a84f2-140">Gebruik Hallo informatie en procedures te volgen als u uw eigen met HSM beschermde sleutel genereren en vervolgens tooAzure Sleutelkluis overdragen: Hallo brengt uw eigen scenario key (BYOK).</span><span class="sxs-lookup"><span data-stu-id="a84f2-140">Use hello following information and procedures if you will generate your own HSM-protected key and then transfer it tooAzure Key Vault—hello bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="a84f2-141">Vereisten voor BYOK</span><span class="sxs-lookup"><span data-stu-id="a84f2-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="a84f2-142">Zie Hallo volgende tabel voor een lijst met vereisten voor uw eigen BYOK (bring key) voor Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="a84f2-142">See hello following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="a84f2-143">Vereiste</span><span class="sxs-lookup"><span data-stu-id="a84f2-143">Requirement</span></span> | <span data-ttu-id="a84f2-144">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="a84f2-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="a84f2-145">Een abonnement tooAzure</span><span class="sxs-lookup"><span data-stu-id="a84f2-145">A subscription tooAzure</span></span> |<span data-ttu-id="a84f2-146">een Azure Sleutelkluis toocreate, moet u een Azure-abonnement: [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="a84f2-146">toocreate an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="a84f2-147">Hello Azure Key Vault Premium service tier toosupport HSM beveiligde sleutels</span><span class="sxs-lookup"><span data-stu-id="a84f2-147">hello Azure Key Vault Premium service tier toosupport HSM-protected keys</span></span> |<span data-ttu-id="a84f2-148">Zie voor meer informatie over Hallo Servicelagen en mogelijkheden voor Azure Sleutelkluis hello [prijzen van Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/) website.</span><span class="sxs-lookup"><span data-stu-id="a84f2-148">For more information about hello service tiers and capabilities for Azure Key Vault, see hello [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="a84f2-149">Thales HSM, smartcards en ondersteunende software</span><span class="sxs-lookup"><span data-stu-id="a84f2-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="a84f2-150">U moet hebben toegang tot tooa Thales Hardware Security Module en operationele basiskennis hebben van Thales HSM's.</span><span class="sxs-lookup"><span data-stu-id="a84f2-150">You must have access tooa Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="a84f2-151">Zie [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) voor Hallo-lijst met compatibele modellen of toopurchase een HSM als u nog geen abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="a84f2-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for hello list of compatible models, or toopurchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="a84f2-152">Hallo volgende hardware en software:</span><span class="sxs-lookup"><span data-stu-id="a84f2-152">hello following hardware and software:</span></span><ol><li><span data-ttu-id="a84f2-153">Een offline x64 werkstation met een besturingssysteem minimaal Windows 7 en Thales nShield-software die ten minste versie 11.50.</span><span class="sxs-lookup"><span data-stu-id="a84f2-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="a84f2-154">Als dit werkstation Windows 7 wordt uitgevoerd, moet u [Installeer Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span><span class="sxs-lookup"><span data-stu-id="a84f2-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="a84f2-155">Een werkstation dat is verbonden toohello Internet en een Windows-besturingssysteem minimaal Windows 7 en [Azure PowerShell](/powershell/azure/overview) **minimaal versie 1.1.0** geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a84f2-155">A workstation that is connected toohello Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="a84f2-156">Een USB-station of ander draagbaar opslagapparaat met ten minste 16 MB vrije ruimte heeft.</span><span class="sxs-lookup"><span data-stu-id="a84f2-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="a84f2-157">Uit veiligheidsoverwegingen is het raadzaam dat Hallo eerste werkstation is niet verbonden tooa netwerk.</span><span class="sxs-lookup"><span data-stu-id="a84f2-157">For security reasons, we recommend that hello first workstation is not connected tooa network.</span></span> <span data-ttu-id="a84f2-158">Deze aanbeveling is echter niet via een programma afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="a84f2-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="a84f2-159">Houd er rekening mee dat in Hallo instructies wordt dit werkstation waarnaar wordt verwezen tooas Hallo niet verbonden werkstation.</span><span class="sxs-lookup"><span data-stu-id="a84f2-159">Note that in hello instructions that follow, this workstation is referred tooas hello disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="a84f2-160">Bovendien, als uw tenantsleutel bedoeld voor een productienetwerk is, raden wij aan dat u een tweede, afzonderlijk werkstation toodownload Hallo toolset en uploaden Hallo tenantsleutel.</span><span class="sxs-lookup"><span data-stu-id="a84f2-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation toodownload hello toolset and upload hello tenant key.</span></span> <span data-ttu-id="a84f2-161">Maar voor testdoeleinden kunt u hetzelfde werkstation Hallo als eerste Hallo.</span><span class="sxs-lookup"><span data-stu-id="a84f2-161">But for testing purposes, you can use hello same workstation as hello first one.</span></span><br/><br/><span data-ttu-id="a84f2-162">Houd er rekening mee dat in Hallo instructies wordt dit tweede werkstation waarnaar wordt verwezen tooas Hallo met Internet verbonden werkstation.</span><span class="sxs-lookup"><span data-stu-id="a84f2-162">Note that in hello instructions that follow, this second workstation is referred tooas hello Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a><span data-ttu-id="a84f2-163">Genereren en overdragen van uw belangrijkste tooAzure Sleutelkluis HSM</span><span class="sxs-lookup"><span data-stu-id="a84f2-163">Generate and transfer your key tooAzure Key Vault HSM</span></span>
<span data-ttu-id="a84f2-164">U wilt gebruiken Hallo toogenerate van vijf stappen te volgen en dragen uw sleutel tooan Azure Key Vault HSM:</span><span class="sxs-lookup"><span data-stu-id="a84f2-164">You will use hello following five steps toogenerate and transfer your key tooan Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="a84f2-165">Stap 1: Uw met Internet verbonden werkstation voorbereiden</span><span class="sxs-lookup"><span data-stu-id="a84f2-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="a84f2-166">Stap 2: Uw niet-verbonden werkstation voorbereiden</span><span class="sxs-lookup"><span data-stu-id="a84f2-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="a84f2-167">Stap 3: Uw sleutel genereren</span><span class="sxs-lookup"><span data-stu-id="a84f2-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="a84f2-168">Stap 4: De sleutel voor de overdracht voorbereiden</span><span class="sxs-lookup"><span data-stu-id="a84f2-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="a84f2-169">Stap 5: Draag uw belangrijkste tooAzure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="a84f2-169">Step 5: Transfer your key tooAzure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="a84f2-170">Stap 1: Uw met Internet verbonden werkstation voorbereiden</span><span class="sxs-lookup"><span data-stu-id="a84f2-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="a84f2-171">Deze eerste stap Hallo procedures te volgen op uw werkstation dat is verbonden toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="a84f2-171">For this first step, do hello following procedures on your workstation that is connected toohello Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="a84f2-172">Stap 1.1: Azure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="a84f2-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="a84f2-173">Van Hallo met Internet verbonden werkstation, download en installeer hello Azure PowerShell-module met Hallo cmdlets toomanage Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="a84f2-173">From hello Internet-connected workstation, download and install hello Azure PowerShell module that includes hello cmdlets toomanage Azure Key Vault.</span></span> <span data-ttu-id="a84f2-174">Hiervoor moet een minimumversie van 0.8.13.</span><span class="sxs-lookup"><span data-stu-id="a84f2-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="a84f2-175">Zie voor installatie-instructies [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a84f2-175">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="a84f2-176">Stap 1.2: Uw Azure-abonnement-ID ophalen</span><span class="sxs-lookup"><span data-stu-id="a84f2-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="a84f2-177">Start een Azure PowerShell-sessie en meld u aan tooyour Azure-account met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a84f2-177">Start an Azure PowerShell session and sign in tooyour Azure account by using hello following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="a84f2-178">In het pop-browservenster hello, Voer uw Azure-account, gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a84f2-178">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="a84f2-179">Gebruik vervolgens Hallo [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) opdracht:</span><span class="sxs-lookup"><span data-stu-id="a84f2-179">Then, use hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="a84f2-180">Zoek van uitvoer Hallo Hallo-ID voor Hallo abonnement die u voor Azure Sleutelkluis gebruiken wilt.</span><span class="sxs-lookup"><span data-stu-id="a84f2-180">From hello output, locate hello ID for hello subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="a84f2-181">U kunt deze abonnement-ID wordt later nodig.</span><span class="sxs-lookup"><span data-stu-id="a84f2-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="a84f2-182">Hello Azure PowerShell-venster niet sluiten.</span><span class="sxs-lookup"><span data-stu-id="a84f2-182">Do not close hello Azure PowerShell window.</span></span>

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="a84f2-183">Stap 1.3: Download de BYOK-hulpmiddelenset Hallo voor Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="a84f2-183">Step 1.3: Download hello BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="a84f2-184">Ga toohello Microsoft Download Center en [download hello Azure Key Vault BYOK-hulpmiddelenset](http://www.microsoft.com/download/details.aspx?id=45345) voor uw geografische regio of het exemplaar van Azure.</span><span class="sxs-lookup"><span data-stu-id="a84f2-184">Go toohello Microsoft Download Center and [download hello Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="a84f2-185">Gebruik de volgende Hallo informatie tooidentify Hallo pakket naam toodownload en de bijbehorende SHA-256 hash van het pakket:</span><span class="sxs-lookup"><span data-stu-id="a84f2-185">Use hello following information tooidentify hello package name toodownload and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="a84f2-186">**Verenigde Staten:**</span><span class="sxs-lookup"><span data-stu-id="a84f2-186">**United States:**</span></span>

<span data-ttu-id="a84f2-187">KeyVault-BYOK-hulpprogramma's-Verenigd States.zip</span><span class="sxs-lookup"><span data-stu-id="a84f2-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="a84f2-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="a84f2-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="a84f2-189">**Europa:**</span><span class="sxs-lookup"><span data-stu-id="a84f2-189">**Europe:**</span></span>

<span data-ttu-id="a84f2-190">KeyVault-BYOK-hulpprogramma's-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="a84f2-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="a84f2-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="a84f2-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="a84f2-192">**Azië:**</span><span class="sxs-lookup"><span data-stu-id="a84f2-192">**Asia:**</span></span>

<span data-ttu-id="a84f2-193">KeyVault-BYOK-hulpprogramma's-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="a84f2-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="a84f2-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="a84f2-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="a84f2-195">**Latijns-Amerika:**</span><span class="sxs-lookup"><span data-stu-id="a84f2-195">**Latin America:**</span></span>

<span data-ttu-id="a84f2-196">KeyVault-BYOK-hulpprogramma's-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="a84f2-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="a84f2-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="a84f2-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="a84f2-198">**Japan:**</span><span class="sxs-lookup"><span data-stu-id="a84f2-198">**Japan:**</span></span>

<span data-ttu-id="a84f2-199">KeyVault-BYOK-hulpprogramma's-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="a84f2-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="a84f2-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="a84f2-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="a84f2-201">**Korea:**</span><span class="sxs-lookup"><span data-stu-id="a84f2-201">**Korea:**</span></span>

<span data-ttu-id="a84f2-202">KeyVault-BYOK-hulpprogramma's-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="a84f2-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="a84f2-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="a84f2-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="a84f2-204">**Australië:**</span><span class="sxs-lookup"><span data-stu-id="a84f2-204">**Australia:**</span></span>

<span data-ttu-id="a84f2-205">KeyVault-BYOK-hulpprogramma's-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="a84f2-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="a84f2-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="a84f2-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="a84f2-207">**Azure Government:**</span><span class="sxs-lookup"><span data-stu-id="a84f2-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="a84f2-208">KeyVault-BYOK-hulpprogramma's-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="a84f2-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="a84f2-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="a84f2-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="a84f2-210">**Amerikaanse overheid DOD:**</span><span class="sxs-lookup"><span data-stu-id="a84f2-210">**US Government DOD:**</span></span>

<span data-ttu-id="a84f2-211">KeyVault-BYOK-hulpprogramma's-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="a84f2-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="a84f2-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="a84f2-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="a84f2-213">**Canada:**</span><span class="sxs-lookup"><span data-stu-id="a84f2-213">**Canada:**</span></span>

<span data-ttu-id="a84f2-214">KeyVault-BYOK-hulpprogramma's-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="a84f2-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="a84f2-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="a84f2-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="a84f2-216">**Duitsland:**</span><span class="sxs-lookup"><span data-stu-id="a84f2-216">**Germany:**</span></span>

<span data-ttu-id="a84f2-217">KeyVault-BYOK-hulpprogramma's-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="a84f2-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="a84f2-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="a84f2-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="a84f2-219">**India:**</span><span class="sxs-lookup"><span data-stu-id="a84f2-219">**India:**</span></span>

<span data-ttu-id="a84f2-220">KeyVault-BYOK-hulpprogramma's-India.zip</span><span class="sxs-lookup"><span data-stu-id="a84f2-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="a84f2-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="a84f2-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="a84f2-222">**Verenigd Koninkrijk:**</span><span class="sxs-lookup"><span data-stu-id="a84f2-222">**United Kingdom:**</span></span>

<span data-ttu-id="a84f2-223">KeyVault-BYOK-hulpprogramma's-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="a84f2-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="a84f2-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="a84f2-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="a84f2-225">toovalidate hello integriteit van de gedownloade BYOK-toolset van uw Azure PowerShell-sessie gebruik Hallo [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a84f2-225">toovalidate hello integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="a84f2-226">Hallo toolset bevat Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="a84f2-226">hello toolset includes hello following:</span></span>

* <span data-ttu-id="a84f2-227">Een KEK Key Exchange Key ()-pakket met een naam die begint met **BYOK-KEK - pkg-.**</span><span class="sxs-lookup"><span data-stu-id="a84f2-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="a84f2-228">Een beveiligingswereldpakket met een naam die begint met **BYOK-SecurityWorld - pkg-.**</span><span class="sxs-lookup"><span data-stu-id="a84f2-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="a84f2-229">Een pythonscript met de naam **verifykeypackage.py.**</span><span class="sxs-lookup"><span data-stu-id="a84f2-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="a84f2-230">Een uitvoerbaar opdrachtregelbestand met de naam **KeyTransferRemote.exe** en bijbehorende DLL-bestanden.</span><span class="sxs-lookup"><span data-stu-id="a84f2-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="a84f2-231">Een herdistrueerbare pakket Visual C++, met de naam **vcredist_x64.exe.**</span><span class="sxs-lookup"><span data-stu-id="a84f2-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="a84f2-232">Kopieer Hallo pakket tooa USB-station of ander draagbaar opslagmedium.</span><span class="sxs-lookup"><span data-stu-id="a84f2-232">Copy hello package tooa USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="a84f2-233">Stap 2: Uw niet-verbonden werkstation voorbereiden</span><span class="sxs-lookup"><span data-stu-id="a84f2-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="a84f2-234">Deze tweede stap Hallo procedures te volgen op Hallo werkstation dat geen netwerk verbonden tooa (Hallo Internet of het interne netwerk).</span><span class="sxs-lookup"><span data-stu-id="a84f2-234">For this second step, do hello following procedures on hello workstation that is not connected tooa network (either hello Internet or your internal network).</span></span>

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="a84f2-235">Stap 2.1: Bereid Hallo verbroken werkstation met Thales HSM</span><span class="sxs-lookup"><span data-stu-id="a84f2-235">Step 2.1: Prepare hello disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="a84f2-236">Hallo (Thales) nCipher-ondersteuningssoftware installeren op een Windows-computer, en voeg vervolgens een Thales HSM toothat-computer.</span><span class="sxs-lookup"><span data-stu-id="a84f2-236">Install hello nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM toothat computer.</span></span>

<span data-ttu-id="a84f2-237">Zorg ervoor dat Hallo Thales-hulpprogramma's zijn in het pad (**%nfast_home%\bin**).</span><span class="sxs-lookup"><span data-stu-id="a84f2-237">Ensure that hello Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="a84f2-238">Typ bijvoorbeeld de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="a84f2-238">For example, type hello following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="a84f2-239">Zie voor meer informatie Hallo handleiding inbegrepen bij Hallo Thales HSM.</span><span class="sxs-lookup"><span data-stu-id="a84f2-239">For more information, see hello user guide included with hello Thales HSM.</span></span>

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a><span data-ttu-id="a84f2-240">Step 2.2: Installatie Hallo BYOK-toolset op Hallo niet verbonden werkstation</span><span class="sxs-lookup"><span data-stu-id="a84f2-240">Step 2.2: Install hello BYOK toolset on hello disconnected workstation</span></span>
<span data-ttu-id="a84f2-241">Hallo BYOK-toolset pakket van Hallo USB-station of ander draagbaar opslagmedium kopiëren en vervolgens Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="a84f2-241">Copy hello BYOK toolset package from hello USB drive or other portable storage, and then do hello following:</span></span>

1. <span data-ttu-id="a84f2-242">Hallo-bestanden extraheren uit pakket Hallo gedownload naar een map.</span><span class="sxs-lookup"><span data-stu-id="a84f2-242">Extract hello files from hello downloaded package into any folder.</span></span>
2. <span data-ttu-id="a84f2-243">Voer vcredist_x64.exe uit in die map.</span><span class="sxs-lookup"><span data-stu-id="a84f2-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="a84f2-244">Hallo instructies toohello Hallo Visual C++ runtime-onderdelen voor Visual Studio 2013 installeren.</span><span class="sxs-lookup"><span data-stu-id="a84f2-244">Follow hello instructions toohello install hello Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="a84f2-245">Stap 3: Uw sleutel genereren</span><span class="sxs-lookup"><span data-stu-id="a84f2-245">Step 3: Generate your key</span></span>
<span data-ttu-id="a84f2-246">Deze derde stap Hallo procedures te volgen op Hallo niet verbonden werkstation.</span><span class="sxs-lookup"><span data-stu-id="a84f2-246">For this third step, do hello following procedures on hello disconnected workstation.</span></span> <span data-ttu-id="a84f2-247">toocomplete deze stap uw HSM moet in de modus van de initialisatie.</span><span class="sxs-lookup"><span data-stu-id="a84f2-247">toocomplete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-hello-hsm-mode-tooi"></a><span data-ttu-id="a84f2-248">Stap 3.1: Wijzig Hallo HSM modus too'I'</span><span class="sxs-lookup"><span data-stu-id="a84f2-248">Step 3.1: Change hello HSM mode too'I'</span></span>
<span data-ttu-id="a84f2-249">Als u van Thales nShield Edge, toochange Hallo modus gebruikmaakt: 1.</span><span class="sxs-lookup"><span data-stu-id="a84f2-249">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="a84f2-250">Hallo modus knop toohighlight Hallo vereist modus gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a84f2-250">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="a84f2-251">2.</span><span class="sxs-lookup"><span data-stu-id="a84f2-251">2.</span></span> <span data-ttu-id="a84f2-252">Binnen een paar seconden en houdt u knop Hallo-wissen van een paar seconden.</span><span class="sxs-lookup"><span data-stu-id="a84f2-252">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="a84f2-253">Hallo-modus wordt gewijzigd, hello nieuwe modus LED niet meer knippert als blijft branden.</span><span class="sxs-lookup"><span data-stu-id="a84f2-253">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="a84f2-254">Hallo Status LED onregelmatig mogelijk flash een paar seconden en vervolgens knippert regelmatig wanneer Hallo apparaat gereed is.</span><span class="sxs-lookup"><span data-stu-id="a84f2-254">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="a84f2-255">Anders Hallo apparaat blijft in de huidige modus Hallo met relevante Hallo-modus LED branden.</span><span class="sxs-lookup"><span data-stu-id="a84f2-255">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="a84f2-256">Stap 3.2: Maak een beveiligingswereld</span><span class="sxs-lookup"><span data-stu-id="a84f2-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="a84f2-257">Start een opdrachtprompt en Voer Hallo nieuwe-wereld-programma van Thales uit.</span><span class="sxs-lookup"><span data-stu-id="a84f2-257">Start a command prompt and run hello Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="a84f2-258">Dit programma maakt een **Beveiligingswereld** bestand op % NFAST_KMDATA%\local\world, wat overeenkomt met toohello C:\ProgramData\nCipher\Key Management Settings\User map.</span><span class="sxs-lookup"><span data-stu-id="a84f2-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds toohello C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="a84f2-259">U kunt andere waarden gebruiken voor Hallo quorum maar in ons voorbeeld u na vragen aan gebruiker tooenter drie lege kaarten en pincodes voor elk criterium.</span><span class="sxs-lookup"><span data-stu-id="a84f2-259">You can use different values for hello quorum but in our example, you’re prompted tooenter three blank cards and pins for each one.</span></span> <span data-ttu-id="a84f2-260">Vervolgens geeft twee kaarten volledige toegang toohello beveiligingswereld.</span><span class="sxs-lookup"><span data-stu-id="a84f2-260">Then, any two cards give full access toohello security world.</span></span> <span data-ttu-id="a84f2-261">Deze kaarten worden Hallo **Beheerderskaartenset** voor Hallo nieuwe beveiligingswereld.</span><span class="sxs-lookup"><span data-stu-id="a84f2-261">These cards become hello **Administrator Card Set** for hello new security world.</span></span>

<span data-ttu-id="a84f2-262">Vervolgens Hallo na:</span><span class="sxs-lookup"><span data-stu-id="a84f2-262">Then do hello following:</span></span>

* <span data-ttu-id="a84f2-263">Back-up Hallo wereld-bestand.</span><span class="sxs-lookup"><span data-stu-id="a84f2-263">Back up hello world file.</span></span> <span data-ttu-id="a84f2-264">Secure beveiligen Hallo wereld-bestand, Hallo Beheerderskaarten en de bijbehorende pincodes en zorg ervoor dat iemand toegang toomore dan één kaart heeft.</span><span class="sxs-lookup"><span data-stu-id="a84f2-264">Secure and protect hello world file, hello Administrator Cards, and their pins, and make sure that no single person has access toomore than one card.</span></span>

### <a name="step-33-change-hello-hsm-mode-tooo"></a><span data-ttu-id="a84f2-265">Stap 3.3: Wijzig Hallo HSM modus too'O'</span><span class="sxs-lookup"><span data-stu-id="a84f2-265">Step 3.3: Change hello HSM mode too'O'</span></span>
<span data-ttu-id="a84f2-266">Als u van Thales nShield Edge, toochange Hallo modus gebruikmaakt: 1.</span><span class="sxs-lookup"><span data-stu-id="a84f2-266">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="a84f2-267">Hallo modus knop toohighlight Hallo vereist modus gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a84f2-267">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="a84f2-268">2.</span><span class="sxs-lookup"><span data-stu-id="a84f2-268">2.</span></span> <span data-ttu-id="a84f2-269">Binnen een paar seconden en houdt u knop Hallo-wissen van een paar seconden.</span><span class="sxs-lookup"><span data-stu-id="a84f2-269">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="a84f2-270">Hallo-modus wordt gewijzigd, hello nieuwe modus LED niet meer knippert als blijft branden.</span><span class="sxs-lookup"><span data-stu-id="a84f2-270">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="a84f2-271">Hallo Status LED onregelmatig mogelijk flash een paar seconden en vervolgens knippert regelmatig wanneer Hallo apparaat gereed is.</span><span class="sxs-lookup"><span data-stu-id="a84f2-271">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="a84f2-272">Anders Hallo apparaat blijft in de huidige modus Hallo met relevante Hallo-modus LED branden.</span><span class="sxs-lookup"><span data-stu-id="a84f2-272">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>


### <a name="step-34-validate-hello-downloaded-package"></a><span data-ttu-id="a84f2-273">Stap 3.4: Hallo gedownloade pakket valideren</span><span class="sxs-lookup"><span data-stu-id="a84f2-273">Step 3.4: Validate hello downloaded package</span></span>
<span data-ttu-id="a84f2-274">Deze stap is optioneel maar aanbevolen zodat u kunt de volgende Hallo valideren:</span><span class="sxs-lookup"><span data-stu-id="a84f2-274">This step is optional but recommended so that you can validate hello following:</span></span>

* <span data-ttu-id="a84f2-275">Hallo-sleutel voor sleuteluitwisseling die is opgenomen in de hulpmiddelenset Hallo is gegenereerd met een legitieme Thales HSM.</span><span class="sxs-lookup"><span data-stu-id="a84f2-275">hello Key Exchange Key that is included in hello toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="a84f2-276">Hallo-hash van het Hallo-Beveiligingswereld die is opgenomen in de hulpmiddelenset Hallo is gegenereerd met een legitieme Thales HSM.</span><span class="sxs-lookup"><span data-stu-id="a84f2-276">hello hash of hello Security World that is included in hello toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="a84f2-277">Hallo-sleutel voor sleuteluitwisseling is niet exporteerbaar.</span><span class="sxs-lookup"><span data-stu-id="a84f2-277">hello Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="a84f2-278">Hallo toovalidate pakket hebt gedownload, hello HSM moet worden verbonden, wordt ingeschakeld, en moet een beveiligingswereld (zoals Hallo dat die u zojuist hebt gemaakt).</span><span class="sxs-lookup"><span data-stu-id="a84f2-278">toovalidate hello downloaded package, hello HSM must be connected, powered on, and must have a security world on it (such as hello one you’ve just created).</span></span>
>
>

<span data-ttu-id="a84f2-279">toovalidate hello gedownload pakket:</span><span class="sxs-lookup"><span data-stu-id="a84f2-279">toovalidate hello downloaded package:</span></span>

1. <span data-ttu-id="a84f2-280">Hallo verifykeypackage.py script uitvoeren door een van de volgende hello, afhankelijk van uw geografische regio of het exemplaar van Azure te typen:</span><span class="sxs-lookup"><span data-stu-id="a84f2-280">Run hello verifykeypackage.py script by typing one of hello following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="a84f2-281">Voor Noord-Amerika:</span><span class="sxs-lookup"><span data-stu-id="a84f2-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="a84f2-282">Voor Europa:</span><span class="sxs-lookup"><span data-stu-id="a84f2-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="a84f2-283">Voor Azië:</span><span class="sxs-lookup"><span data-stu-id="a84f2-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="a84f2-284">Voor Latijns-Amerika:</span><span class="sxs-lookup"><span data-stu-id="a84f2-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="a84f2-285">Voor Japan:</span><span class="sxs-lookup"><span data-stu-id="a84f2-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="a84f2-286">Voor Korea:</span><span class="sxs-lookup"><span data-stu-id="a84f2-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="a84f2-287">Voor Australië:</span><span class="sxs-lookup"><span data-stu-id="a84f2-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="a84f2-288">Voor [Azure Government](https://azure.microsoft.com/features/gov/), waarbij Hallo US government-exemplaar van Azure wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="a84f2-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="a84f2-289">Voor de overheid van de VS DOD:</span><span class="sxs-lookup"><span data-stu-id="a84f2-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="a84f2-290">Voor Canada:</span><span class="sxs-lookup"><span data-stu-id="a84f2-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="a84f2-291">Voor Duitsland:</span><span class="sxs-lookup"><span data-stu-id="a84f2-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="a84f2-292">Voor India:</span><span class="sxs-lookup"><span data-stu-id="a84f2-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="a84f2-293">Hallo Thales-software bevat python in %NFAST_HOME%\python\bin</span><span class="sxs-lookup"><span data-stu-id="a84f2-293">hello Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="a84f2-294">Controleer of u de volgende hello, waarmee wordt aangegeven validatie is geslaagd: **resultaat: geslaagd**</span><span class="sxs-lookup"><span data-stu-id="a84f2-294">Confirm that you see hello following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="a84f2-295">Dit script valideert Hallo ondertekenaarsketen up toohello Thales-hoofdsleutel.</span><span class="sxs-lookup"><span data-stu-id="a84f2-295">This script validates hello signer chain up toohello Thales root key.</span></span> <span data-ttu-id="a84f2-296">Hallo-hash van deze hoofdsleutel is ingesloten in het Hallo-script en de waarde moet **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span><span class="sxs-lookup"><span data-stu-id="a84f2-296">hello hash of this root key is embedded in hello script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="a84f2-297">U kunt deze waarde ook afzonderlijk controleren door te bezoeken Hallo [Thales-website](http://www.thalesesec.com/).</span><span class="sxs-lookup"><span data-stu-id="a84f2-297">You can also confirm this value separately by visiting hello [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="a84f2-298">U bent nu klaar toocreate een nieuwe sleutel.</span><span class="sxs-lookup"><span data-stu-id="a84f2-298">You’re now ready toocreate a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="a84f2-299">Stap 3.5: Maak een nieuwe sleutel</span><span class="sxs-lookup"><span data-stu-id="a84f2-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="a84f2-300">Een sleutel genereren met behulp van Hallo Thales **generatekey** programma.</span><span class="sxs-lookup"><span data-stu-id="a84f2-300">Generate a key by using hello Thales **generatekey** program.</span></span>

<span data-ttu-id="a84f2-301">Voer Hallo opdracht toogenerate Hallo sleutel te volgen:</span><span class="sxs-lookup"><span data-stu-id="a84f2-301">Run hello following command toogenerate hello key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="a84f2-302">Wanneer u deze opdracht uitvoert, gebruikt u deze instructies:</span><span class="sxs-lookup"><span data-stu-id="a84f2-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="a84f2-303">parameter Hallo *beveiligen* toohello-waarde moet worden ingesteld **module**, zoals wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a84f2-303">hello parameter *protect* must be set toohello value **module**, as shown.</span></span> <span data-ttu-id="a84f2-304">Hiermee maakt u een modulair beveiligde sleutel.</span><span class="sxs-lookup"><span data-stu-id="a84f2-304">This creates a module-protected key.</span></span> <span data-ttu-id="a84f2-305">Hallo BYOK-toolset biedt geen ondersteuning voor OCS beveiligde sleutels.</span><span class="sxs-lookup"><span data-stu-id="a84f2-305">hello BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="a84f2-306">Vervang de waarde Hallo van *contosokey* voor Hallo **ident** en **plainname** met een tekenreekswaarde.</span><span class="sxs-lookup"><span data-stu-id="a84f2-306">Replace hello value of *contosokey* for hello **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="a84f2-307">toominimize administratieve overhead en Hallo risico's te beperken van fouten, wordt aangeraden dezelfde voor beide waarde hello te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a84f2-307">toominimize administrative overheads and reduce hello risk of errors, we recommend that you use hello same value for both.</span></span> <span data-ttu-id="a84f2-308">Hallo **ident** waarde mag alleen cijfers, streepjes en kleine letters bestaan.</span><span class="sxs-lookup"><span data-stu-id="a84f2-308">hello **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="a84f2-309">Hallo pubexp is leeg (standaard) in dit voorbeeld, maar u kunt specifieke waarden opgeven.</span><span class="sxs-lookup"><span data-stu-id="a84f2-309">hello pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="a84f2-310">Zie voor meer informatie Hallo Thales-documentatie.</span><span class="sxs-lookup"><span data-stu-id="a84f2-310">For more information, see hello Thales documentation.</span></span>

<span data-ttu-id="a84f2-311">Deze opdracht maakt u een Tokenized sleutelbestand in uw map %NFAST_KMDATA%\local met een naam die begint met **key_simple_**, gevolgd door Hallo **ident** dat is opgegeven in het Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="a84f2-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by hello **ident** that was specified in hello command.</span></span> <span data-ttu-id="a84f2-312">Bijvoorbeeld: **key_simple_contosokey**.</span><span class="sxs-lookup"><span data-stu-id="a84f2-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="a84f2-313">Dit bestand bevat een versleutelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="a84f2-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="a84f2-314">Back-up van deze Tokenized sleutelbestand op een veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="a84f2-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a84f2-315">Wanneer u later uw sleutel tooAzure Sleutelkluis overdraagt, kan Microsoft deze sleutel back tooyou niet exporteren dus is het erg belangrijk back-up van uw sleutel en beveiligingswereld veilig.</span><span class="sxs-lookup"><span data-stu-id="a84f2-315">When you later transfer your key tooAzure Key Vault, Microsoft cannot export this key back tooyou so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="a84f2-316">Neem contact op met Thales voor richtlijnen en aanbevolen procedures voor back-ups van uw sleutel.</span><span class="sxs-lookup"><span data-stu-id="a84f2-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="a84f2-317">U zijn nu gereed tootransfer uw belangrijkste tooAzure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="a84f2-317">You are now ready tootransfer your key tooAzure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="a84f2-318">Stap 4: De sleutel voor de overdracht voorbereiden</span><span class="sxs-lookup"><span data-stu-id="a84f2-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="a84f2-319">Deze vierde stap Hallo procedures te volgen op Hallo niet verbonden werkstation.</span><span class="sxs-lookup"><span data-stu-id="a84f2-319">For this fourth step, do hello following procedures on hello disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="a84f2-320">Stap 4.1: Maak een kopie van uw sleutel met beperkte machtigingen</span><span class="sxs-lookup"><span data-stu-id="a84f2-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="a84f2-321">Open een nieuw opdrachtpromptvenster en wijzig Hallo huidige directory toohello locatie waar u Hallo BYOK zip-bestand hebt uitgepakt.</span><span class="sxs-lookup"><span data-stu-id="a84f2-321">Open a new command prompt and change hello current directory toohello location where you unzipped hello BYOK zip file.</span></span> <span data-ttu-id="a84f2-322">tooreduce hello machtigingen voor de sleutel, vanaf een opdrachtprompt, voer een van de volgende hello, afhankelijk van uw geografische regio of het exemplaar van Azure:</span><span class="sxs-lookup"><span data-stu-id="a84f2-322">tooreduce hello permissions on your key, from a command prompt, run one of hello following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="a84f2-323">Voor Noord-Amerika:</span><span class="sxs-lookup"><span data-stu-id="a84f2-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="a84f2-324">Voor Europa:</span><span class="sxs-lookup"><span data-stu-id="a84f2-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="a84f2-325">Voor Azië:</span><span class="sxs-lookup"><span data-stu-id="a84f2-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="a84f2-326">Voor Latijns-Amerika:</span><span class="sxs-lookup"><span data-stu-id="a84f2-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="a84f2-327">Voor Japan:</span><span class="sxs-lookup"><span data-stu-id="a84f2-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="a84f2-328">Voor Korea:</span><span class="sxs-lookup"><span data-stu-id="a84f2-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="a84f2-329">Voor Australië:</span><span class="sxs-lookup"><span data-stu-id="a84f2-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="a84f2-330">Voor [Azure Government](https://azure.microsoft.com/features/gov/), waarbij Hallo US government-exemplaar van Azure wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="a84f2-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="a84f2-331">Voor de overheid van de VS DOD:</span><span class="sxs-lookup"><span data-stu-id="a84f2-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="a84f2-332">Voor Canada:</span><span class="sxs-lookup"><span data-stu-id="a84f2-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="a84f2-333">Voor Duitsland:</span><span class="sxs-lookup"><span data-stu-id="a84f2-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="a84f2-334">Voor India:</span><span class="sxs-lookup"><span data-stu-id="a84f2-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="a84f2-335">Wanneer u deze opdracht uitvoert, vervangt *contosokey* Hello dezelfde waarde als u hebt opgegeven in **stap 3.5: Maak een nieuwe sleutel** van Hallo [uw sleutel genereren](#step-3-generate-your-key) stap.</span><span class="sxs-lookup"><span data-stu-id="a84f2-335">When you run this command, replace *contosokey* with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="a84f2-336">Wordt u gevraagd tooplug in uw security world admin-kaarten.</span><span class="sxs-lookup"><span data-stu-id="a84f2-336">You are asked tooplug in your security world admin cards.</span></span>

<span data-ttu-id="a84f2-337">Wanneer Hallo-opdracht is voltooid, ziet u **resultaat: SUCCES** en Hallo kopie van uw sleutel met beperkte machtigingen zich in Hallo-bestand met de naam key_xferacId_<contosokey>.</span><span class="sxs-lookup"><span data-stu-id="a84f2-337">When hello command completes, you see **Result: SUCCESS** and hello copy of your key with reduced permissions are in hello file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="a84f2-338">U mag inspecteert Hallo ACL's met behulp van volgende opdrachten met Thales-hulpprogramma Hallo:</span><span class="sxs-lookup"><span data-stu-id="a84f2-338">You may inspects hello ACLS using following commands using hello Thales utilities:</span></span>

* <span data-ttu-id="a84f2-339">aclprint.PY:</span><span class="sxs-lookup"><span data-stu-id="a84f2-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="a84f2-340">kmfile-dump.exe:</span><span class="sxs-lookup"><span data-stu-id="a84f2-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="a84f2-341">Wanneer u deze opdrachten uitvoert, vervangt u contosokey Hello dezelfde waarde als u hebt opgegeven in **stap 3.5: Maak een nieuwe sleutel** van Hallo [uw sleutel genereren](#step-3-generate-your-key) stap.</span><span class="sxs-lookup"><span data-stu-id="a84f2-341">When you run these commands, replace contosokey with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="a84f2-342">Stap 4.2: Versleutel de sleutel met behulp van Microsoft sleutel voor sleuteluitwisseling</span><span class="sxs-lookup"><span data-stu-id="a84f2-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="a84f2-343">Voer een van de volgende opdrachten uit, afhankelijk van uw geografische regio of het exemplaar van Azure Hallo:</span><span class="sxs-lookup"><span data-stu-id="a84f2-343">Run one of hello following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="a84f2-344">Voor Noord-Amerika:</span><span class="sxs-lookup"><span data-stu-id="a84f2-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a84f2-345">Voor Europa:</span><span class="sxs-lookup"><span data-stu-id="a84f2-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a84f2-346">Voor Azië:</span><span class="sxs-lookup"><span data-stu-id="a84f2-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a84f2-347">Voor Latijns-Amerika:</span><span class="sxs-lookup"><span data-stu-id="a84f2-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a84f2-348">Voor Japan:</span><span class="sxs-lookup"><span data-stu-id="a84f2-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a84f2-349">Voor Korea:</span><span class="sxs-lookup"><span data-stu-id="a84f2-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a84f2-350">Voor Australië:</span><span class="sxs-lookup"><span data-stu-id="a84f2-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a84f2-351">Voor [Azure Government](https://azure.microsoft.com/features/gov/), waarbij Hallo US government-exemplaar van Azure wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="a84f2-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a84f2-352">Voor de overheid van de VS DOD:</span><span class="sxs-lookup"><span data-stu-id="a84f2-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a84f2-353">Voor Canada:</span><span class="sxs-lookup"><span data-stu-id="a84f2-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a84f2-354">Voor Duitsland:</span><span class="sxs-lookup"><span data-stu-id="a84f2-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a84f2-355">Voor India:</span><span class="sxs-lookup"><span data-stu-id="a84f2-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="a84f2-356">Wanneer u deze opdracht uitvoert, gebruikt u deze instructies:</span><span class="sxs-lookup"><span data-stu-id="a84f2-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="a84f2-357">Vervang *contosokey* door Hallo-id die u gebruikt toogenerate Hallo sleutel in **stap 3.5: Maak een nieuwe sleutel** van Hallo [uw sleutel genereren](#step-3-generate-your-key) stap.</span><span class="sxs-lookup"><span data-stu-id="a84f2-357">Replace *contosokey* with hello identifier that you used toogenerate hello key in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="a84f2-358">Vervang *SubscriptionID* met de Hallo ID hello Azure-abonnement dat u de sleutelkluis bevat.</span><span class="sxs-lookup"><span data-stu-id="a84f2-358">Replace *SubscriptionID* with hello ID of hello Azure subscription that contains your key vault.</span></span> <span data-ttu-id="a84f2-359">U hebt deze waarde opgehaald in **stap 1.2: uw Azure-abonnement-ID ophalen** van Hallo [uw met Internet verbonden werkstation voorbereiden](#step-1-prepare-your-internet-connected-workstation) stap.</span><span class="sxs-lookup"><span data-stu-id="a84f2-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from hello [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="a84f2-360">Vervang *ContosoFirstHSMKey* met een label dat wordt gebruikt voor naam van uw uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="a84f2-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="a84f2-361">Wanneer dit succesvol is voltooid, wordt weergegeven **resultaat: SUCCES** en er is een nieuw bestand in de huidige Hallo-map met Hallo achter naam: KeyTransferPackage -*ContosoFirstHSMkey*.byok</span><span class="sxs-lookup"><span data-stu-id="a84f2-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in hello current folder that has hello following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a><span data-ttu-id="a84f2-362">Stap 4.3: Kopieer uw sleuteloverdracht pakket toohello met Internet verbonden werkstation</span><span class="sxs-lookup"><span data-stu-id="a84f2-362">Step 4.3: Copy your key transfer package toohello Internet-connected workstation</span></span>
<span data-ttu-id="a84f2-363">Gebruik een USB-station of ander draagbaar opslagmedium toocopy Hallo-bestand voor uitvoer van Hallo vorige stap (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour met Internet verbonden werkstation.</span><span class="sxs-lookup"><span data-stu-id="a84f2-363">Use a USB drive or other portable storage toocopy hello output file from hello previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a><span data-ttu-id="a84f2-364">Stap 5: Draag uw belangrijkste tooAzure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="a84f2-364">Step 5: Transfer your key tooAzure Key Vault</span></span>
<span data-ttu-id="a84f2-365">Gebruik voor deze laatste stap op Hallo met Internet verbonden werkstation, Hallo [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello sleuteloverdrachtpakket die u hebt gekopieerd uit Hallo verbroken werkstation toohello Azure Key Vault HSM:</span><span class="sxs-lookup"><span data-stu-id="a84f2-365">For this final step, on hello Internet-connected workstation, use hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello key transfer package that you copied from hello disconnected workstation toohello Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="a84f2-366">Als Hallo uploaden voltooid is, ziet u de eigenschappen weergegeven Hallo van Hallo-sleutel die u zojuist hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a84f2-366">If hello upload is successful, you see displayed hello properties of hello key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a84f2-367">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a84f2-367">Next steps</span></span>
<span data-ttu-id="a84f2-368">U kunt deze met HSM beschermde sleutel nu gebruiken in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="a84f2-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="a84f2-369">Zie voor meer informatie, Hallo **als u wilt dat er een hardware security module (HSM) toouse** sectie in Hallo [aan de slag met Azure Key Vault](key-vault-get-started.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a84f2-369">For more information, see hello **If you want toouse a hardware security module (HSM)** section in hello [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
