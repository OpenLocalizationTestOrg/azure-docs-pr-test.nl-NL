---
title: overzicht van aaaAzure Cloud Shell (Preview) | Microsoft Docs
description: Overzicht van hello Azure Cloud-Shell.
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="55787-103">Overzicht van Azure-Cloud-Shell (Preview)</span><span class="sxs-lookup"><span data-stu-id="55787-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="55787-104">Azure Cloud-Shell is een interactieve, browser toegankelijke shell voor het beheren van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="55787-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="55787-105">Functies</span><span class="sxs-lookup"><span data-stu-id="55787-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="55787-106">Browser gebaseerde shell-ervaring</span><span class="sxs-lookup"><span data-stu-id="55787-106">Browser-based shell experience</span></span>
<span data-ttu-id="55787-107">Cloud Shell Hiermee toegang tooa-opdrachtregelprogramma browserervaring gebouwd met Azure beheertaken in gedachten.</span><span class="sxs-lookup"><span data-stu-id="55787-107">Cloud Shell enables access tooa browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="55787-108">Maak gebruik van Cloud-Shell toowork vrije van een lokale computer op een manier die alleen Hallo cloud kan bieden.</span><span class="sxs-lookup"><span data-stu-id="55787-108">Leverage Cloud Shell toowork untethered from a local machine in a way only hello cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="55787-109">Vooraf geconfigureerde Azure werkstation</span><span class="sxs-lookup"><span data-stu-id="55787-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="55787-110">Cloud-Shell is voorgeïnstalleerd met populaire opdrachtregelprogramma's en talen zodat u sneller kunt werken.</span><span class="sxs-lookup"><span data-stu-id="55787-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="55787-111">Hallo volledige tooling lijst weergeven voor Azure Cloud Shell hier.</span><span class="sxs-lookup"><span data-stu-id="55787-111">View hello full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="55787-112">Automatische verificatie</span><span class="sxs-lookup"><span data-stu-id="55787-112">Automatic authentication</span></span>
<span data-ttu-id="55787-113">Cloud-Shell verifieert veilig automatisch op elke sessie voor directe toegang tooyour resources via hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="55787-113">Cloud Shell securely authenticates automatically on each session for instant access tooyour resources through hello Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="55787-114">Verbinding maken met uw Azure File storage</span><span class="sxs-lookup"><span data-stu-id="55787-114">Connect your Azure File storage</span></span>
<span data-ttu-id="55787-115">Cloud-Shell-machines zijn tijdelijk en als gevolg hiervan vereisen een Azure file share toobe gekoppeld als `clouddrive` toopersist uw directory $Home.</span><span class="sxs-lookup"><span data-stu-id="55787-115">Cloud Shell machines are temporary and as a result require an Azure file share toobe mounted as `clouddrive` toopersist your $Home directory.</span></span>
<span data-ttu-id="55787-116">Op de eerste keer opstarten Cloud Shell wordt gevraagd om een resourcegroep, een opslagaccount en een bestand namens jou delen toocreate.</span><span class="sxs-lookup"><span data-stu-id="55787-116">On first launch Cloud Shell prompts toocreate a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="55787-117">Dit is een eenmalige stap en wordt automatisch voor alle sessies worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="55787-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="55787-118">Maken van nieuwe opslag</span><span class="sxs-lookup"><span data-stu-id="55787-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="55787-119">Een lokaal redundant opslagaccount (LRS) kan namens jou worden gemaakt met een Azure-bestandsshare met de installatiekopie van een standaard 5 GB schijf.</span><span class="sxs-lookup"><span data-stu-id="55787-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="55787-120">Hallo-bestandsshare koppelt als `clouddrive` voor bestand delen interactie met Hallo schijfimage gebruikte toosync wordt en uw directory $Home behouden.</span><span class="sxs-lookup"><span data-stu-id="55787-120">hello file share mounts as `clouddrive` for file share interaction with hello disk image being used toosync and persist your $Home directory.</span></span> <span data-ttu-id="55787-121">Reguliere opslagkosten van toepassing.</span><span class="sxs-lookup"><span data-stu-id="55787-121">Regular storage costs apply.</span></span>

<span data-ttu-id="55787-122">Drie bronnen worden namens jou gemaakt:</span><span class="sxs-lookup"><span data-stu-id="55787-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="55787-123">De resourcegroep met de naam:`cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="55787-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="55787-124">Opslagaccount met de naam:`cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="55787-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="55787-125">De bestandsshare met de naam:`cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="55787-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="55787-126">Alle bestanden in uw directory $Home zoals SSH-sleutels worden doorgevoerd in de schijfinstallatiekopie van uw gebruiker opgeslagen in de gekoppelde bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="55787-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="55787-127">Aanbevolen procedures van toepassing bij het opslaan van bestanden in uw directory $Home en gekoppelde bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="55787-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="55787-128">Bestaande bronnen gebruiken</span><span class="sxs-lookup"><span data-stu-id="55787-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="55787-129">Een geavanceerde optie is ook beschikbaar waarmee u tooassociate bestaande resources tooCloud Shell.</span><span class="sxs-lookup"><span data-stu-id="55787-129">An advanced option is also provided allowing you tooassociate existing resources tooCloud Shell.</span></span> <span data-ttu-id="55787-130">Wanneer met Hallo opslag setup prompt weergegeven, klikt u op 'Instellingen voor geavanceerde weergeven' tooselect extra opties.</span><span class="sxs-lookup"><span data-stu-id="55787-130">When presented with hello storage setup prompt, click "Show advanced settings" tooselect additional options.</span></span> <span data-ttu-id="55787-131">Opgegeven waarin DropDowns worden gefilterd voor uw toegewezen Cloud Shell regio en lokaal/globaal-redundant storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="55787-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="55787-132">[Meer informatie over opslag voor Cloud-Shell, gedeelde bestanden bijwerken en het uploaden/downloaden van bestanden.] (het behouden blijven-shell-storage.md)</span><span class="sxs-lookup"><span data-stu-id="55787-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="55787-133">Concepten</span><span class="sxs-lookup"><span data-stu-id="55787-133">Concepts</span></span>
* <span data-ttu-id="55787-134">Cloud-Shell wordt uitgevoerd op een tijdelijke machine die is opgegeven op een per-sessie per gebruiker</span><span class="sxs-lookup"><span data-stu-id="55787-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="55787-135">Time-out opgetreden voor de cloud Shell na 20 minuten zonder interactieve activiteit</span><span class="sxs-lookup"><span data-stu-id="55787-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="55787-136">Cloud-Shell zijn alleen toegankelijk met een bestandsshare die is gekoppeld</span><span class="sxs-lookup"><span data-stu-id="55787-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="55787-137">Cloud-Shell wordt één machine per gebruikersaccount toegewezen</span><span class="sxs-lookup"><span data-stu-id="55787-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="55787-138">Machtigingen zijn ingesteld als een gewone Linux-gebruiker</span><span class="sxs-lookup"><span data-stu-id="55787-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="55787-139">Meer informatie over alle functies van de Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="55787-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="55787-140">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="55787-140">Examples</span></span>
* <span data-ttu-id="55787-141">Maken of bewerken van scripts tooautomate Azure management</span><span class="sxs-lookup"><span data-stu-id="55787-141">Create or edit scripts tooautomate Azure management</span></span>
* <span data-ttu-id="55787-142">Resources via Azure portal en Azure CLI 2.0 tegelijkertijd te beheren</span><span class="sxs-lookup"><span data-stu-id="55787-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="55787-143">Azure CLI 2.0 Test-Drive</span><span class="sxs-lookup"><span data-stu-id="55787-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="55787-144">Probeer deze voorbeelden op Hallo Cloud Shell Quick Start.</span><span class="sxs-lookup"><span data-stu-id="55787-144">Try out all these examples at hello Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="55787-145">Prijzen</span><span class="sxs-lookup"><span data-stu-id="55787-145">Pricing</span></span>
<span data-ttu-id="55787-146">Hallo-machine voor het hosten van Cloud-Shell is gratis, met een vereiste van een gekoppelde Azure-bestand delen toopersist uw directory $Home.</span><span class="sxs-lookup"><span data-stu-id="55787-146">hello machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share toopersist your $Home directory.</span></span> <span data-ttu-id="55787-147">Reguliere opslagkosten van toepassing.</span><span class="sxs-lookup"><span data-stu-id="55787-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="55787-148">Ondersteunde browsers</span><span class="sxs-lookup"><span data-stu-id="55787-148">Supported browsers</span></span>
<span data-ttu-id="55787-149">Cloud-Shell wordt aanbevolen voor Chrome, rand en Safari.</span><span class="sxs-lookup"><span data-stu-id="55787-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="55787-150">Cloud-Shell wordt ondersteund voor Chrome, Firefox Safari, Internet Explorer en Edge, is Cloud Shell onderwerp toospecific browserinstellingen.</span><span class="sxs-lookup"><span data-stu-id="55787-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject toospecific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="55787-151">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="55787-151">Troubleshooting</span></span>
1. <span data-ttu-id="55787-152">Wanneer u een abonnement op Azure Active Directory, ik opslag kan niet maken vanwege tooError: 400 DisallowedOperation.</span><span class="sxs-lookup"><span data-stu-id="55787-152">When using an Azure Active Directory subscription, I cannot create storage due tooError: 400 DisallowedOperation.</span></span> <span data-ttu-id="55787-153">tooresolve, gebruik een Azure-abonnement te maken van de storage-resources.</span><span class="sxs-lookup"><span data-stu-id="55787-153">tooresolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="55787-154">AD-abonnementen zijn niet mogelijk toocreate Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="55787-154">AD subscriptions are not able toocreate Azure resources.</span></span>

<span data-ttu-id="55787-155">Voor specifieke bekende beperkingen, gaat u naar [beperkingen van Cloud-Shell](limitations.md).</span><span class="sxs-lookup"><span data-stu-id="55787-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
