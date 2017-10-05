---
title: Overzicht van Azure Cloud-Shell (Preview) | Microsoft Docs
description: Overzicht van de Azure-Cloud-Shell.
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
ms.openlocfilehash: 7165633cd354eeea2e3619f839338e6af1524e56
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="d8016-103">Overzicht van Azure-Cloud-Shell (Preview)</span><span class="sxs-lookup"><span data-stu-id="d8016-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="d8016-104">Azure Cloud-Shell is een interactieve, browser toegankelijke shell voor het beheren van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="d8016-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="d8016-105">Functies</span><span class="sxs-lookup"><span data-stu-id="d8016-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="d8016-106">Browser gebaseerde shell-ervaring</span><span class="sxs-lookup"><span data-stu-id="d8016-106">Browser-based shell experience</span></span>
<span data-ttu-id="d8016-107">Cloud-Shell kan toegang tot een browser gebaseerde opdrachtregelprogramma ervaring gebouwd met Azure beheertaken in gedachten.</span><span class="sxs-lookup"><span data-stu-id="d8016-107">Cloud Shell enables access to a browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="d8016-108">Hefboomwerking Cloud Shell voelt van een lokale computer werkt op een manier alleen de cloud kunnen bieden.</span><span class="sxs-lookup"><span data-stu-id="d8016-108">Leverage Cloud Shell to work untethered from a local machine in a way only the cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="d8016-109">Vooraf geconfigureerde Azure werkstation</span><span class="sxs-lookup"><span data-stu-id="d8016-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="d8016-110">Cloud-Shell is voorgeïnstalleerd met populaire opdrachtregelprogramma's en talen zodat u sneller kunt werken.</span><span class="sxs-lookup"><span data-stu-id="d8016-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="d8016-111">De lijst volledige tooling voor Azure Cloud Shell hier weergeven.</span><span class="sxs-lookup"><span data-stu-id="d8016-111">View the full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="d8016-112">Automatische verificatie</span><span class="sxs-lookup"><span data-stu-id="d8016-112">Automatic authentication</span></span>
<span data-ttu-id="d8016-113">Cloud-Shell verifieert veilig automatisch op elke sessie voor directe toegang tot uw resources via de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="d8016-113">Cloud Shell securely authenticates automatically on each session for instant access to your resources through the Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="d8016-114">Verbinding maken met uw Azure File storage</span><span class="sxs-lookup"><span data-stu-id="d8016-114">Connect your Azure File storage</span></span>
<span data-ttu-id="d8016-115">Cloud-Shell-machines zijn tijdelijk en als gevolg hiervan vereisen een Azure-bestandsshare te koppelen als `clouddrive` voor het persistent maken van uw directory $Home.</span><span class="sxs-lookup"><span data-stu-id="d8016-115">Cloud Shell machines are temporary and as a result require an Azure file share to be mounted as `clouddrive` to persist your $Home directory.</span></span>
<span data-ttu-id="d8016-116">Op de eerste keer opstarten die cloud Shell wordt gevraagd om een resource te maken delen groep, storage-account en -bestand namens jou.</span><span class="sxs-lookup"><span data-stu-id="d8016-116">On first launch Cloud Shell prompts to create a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="d8016-117">Dit is een eenmalige stap en wordt automatisch voor alle sessies worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="d8016-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="d8016-118">Maken van nieuwe opslag</span><span class="sxs-lookup"><span data-stu-id="d8016-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="d8016-119">Een lokaal redundant opslagaccount (LRS) kan namens jou worden gemaakt met een Azure-bestandsshare met de installatiekopie van een standaard 5 GB schijf.</span><span class="sxs-lookup"><span data-stu-id="d8016-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="d8016-120">De bestandsshare koppelt als `clouddrive` delen interactie met de installatiekopie van de schijf die wordt gebruikt om te synchroniseren en uw directory $Home behouden voor het bestand.</span><span class="sxs-lookup"><span data-stu-id="d8016-120">The file share mounts as `clouddrive` for file share interaction with the disk image being used to sync and persist your $Home directory.</span></span> <span data-ttu-id="d8016-121">Reguliere opslagkosten van toepassing.</span><span class="sxs-lookup"><span data-stu-id="d8016-121">Regular storage costs apply.</span></span>

<span data-ttu-id="d8016-122">Drie bronnen worden namens jou gemaakt:</span><span class="sxs-lookup"><span data-stu-id="d8016-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="d8016-123">De resourcegroep met de naam:`cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="d8016-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="d8016-124">Opslagaccount met de naam:`cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="d8016-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="d8016-125">De bestandsshare met de naam:`cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="d8016-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="d8016-126">Alle bestanden in uw directory $Home zoals SSH-sleutels worden doorgevoerd in de schijfinstallatiekopie van uw gebruiker opgeslagen in de gekoppelde bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="d8016-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="d8016-127">Aanbevolen procedures van toepassing bij het opslaan van bestanden in uw directory $Home en gekoppelde bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="d8016-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="d8016-128">Bestaande bronnen gebruiken</span><span class="sxs-lookup"><span data-stu-id="d8016-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="d8016-129">Een geavanceerde optie is ook beschikbaar waarmee u kunt het koppelen van bestaande resources voor Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="d8016-129">An advanced option is also provided allowing you to associate existing resources to Cloud Shell.</span></span> <span data-ttu-id="d8016-130">Wanneer de opslag setup prompt krijgt, klikt u op 'Weergeven geavanceerde instellingen' om extra opties te selecteren.</span><span class="sxs-lookup"><span data-stu-id="d8016-130">When presented with the storage setup prompt, click "Show advanced settings" to select additional options.</span></span> <span data-ttu-id="d8016-131">Opgegeven waarin DropDowns worden gefilterd voor uw toegewezen Cloud Shell regio en lokaal/globaal-redundant storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="d8016-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="d8016-132">[Meer informatie over opslag voor Cloud-Shell, gedeelde bestanden bijwerken en het uploaden/downloaden van bestanden.] (het behouden blijven-shell-storage.md)</span><span class="sxs-lookup"><span data-stu-id="d8016-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="d8016-133">Concepten</span><span class="sxs-lookup"><span data-stu-id="d8016-133">Concepts</span></span>
* <span data-ttu-id="d8016-134">Cloud-Shell wordt uitgevoerd op een tijdelijke machine die is opgegeven op een per-sessie per gebruiker</span><span class="sxs-lookup"><span data-stu-id="d8016-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="d8016-135">Time-out opgetreden voor de cloud Shell na 20 minuten zonder interactieve activiteit</span><span class="sxs-lookup"><span data-stu-id="d8016-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="d8016-136">Cloud-Shell zijn alleen toegankelijk met een bestandsshare die is gekoppeld</span><span class="sxs-lookup"><span data-stu-id="d8016-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="d8016-137">Cloud-Shell wordt één machine per gebruikersaccount toegewezen</span><span class="sxs-lookup"><span data-stu-id="d8016-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="d8016-138">Machtigingen zijn ingesteld als een gewone Linux-gebruiker</span><span class="sxs-lookup"><span data-stu-id="d8016-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="d8016-139">Meer informatie over alle functies van de Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="d8016-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="d8016-140">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="d8016-140">Examples</span></span>
* <span data-ttu-id="d8016-141">Maken of bewerken van scripts voor het automatiseren van Azure management</span><span class="sxs-lookup"><span data-stu-id="d8016-141">Create or edit scripts to automate Azure management</span></span>
* <span data-ttu-id="d8016-142">Resources via Azure portal en Azure CLI 2.0 tegelijkertijd te beheren</span><span class="sxs-lookup"><span data-stu-id="d8016-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="d8016-143">Azure CLI 2.0 Test-Drive</span><span class="sxs-lookup"><span data-stu-id="d8016-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="d8016-144">Probeer deze voorbeelden op de Cloud Shell Quick Start.</span><span class="sxs-lookup"><span data-stu-id="d8016-144">Try out all these examples at the Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="d8016-145">Prijzen</span><span class="sxs-lookup"><span data-stu-id="d8016-145">Pricing</span></span>
<span data-ttu-id="d8016-146">De computer die als host fungeert voor Cloud-Shell is gratis, met een vereiste van een gekoppelde Azure-bestandsshare voor het persistent maken van uw directory $Home.</span><span class="sxs-lookup"><span data-stu-id="d8016-146">The machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share to persist your $Home directory.</span></span> <span data-ttu-id="d8016-147">Reguliere opslagkosten van toepassing.</span><span class="sxs-lookup"><span data-stu-id="d8016-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="d8016-148">Ondersteunde browsers</span><span class="sxs-lookup"><span data-stu-id="d8016-148">Supported browsers</span></span>
<span data-ttu-id="d8016-149">Cloud-Shell wordt aanbevolen voor Chrome, rand en Safari.</span><span class="sxs-lookup"><span data-stu-id="d8016-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="d8016-150">Cloud-Shell wordt ondersteund voor Chrome, Firefox Safari, Internet Explorer en Edge, is Cloud Shell onderworpen aan specifieke browserinstellingen.</span><span class="sxs-lookup"><span data-stu-id="d8016-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject to specific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d8016-151">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="d8016-151">Troubleshooting</span></span>
1. <span data-ttu-id="d8016-152">Wanneer u een abonnement op Azure Active Directory gebruikt, kan ik niet maken opslag vanwege fout: 400 DisallowedOperation.</span><span class="sxs-lookup"><span data-stu-id="d8016-152">When using an Azure Active Directory subscription, I cannot create storage due to Error: 400 DisallowedOperation.</span></span> <span data-ttu-id="d8016-153">Gebruik een Azure-abonnement te maken van de storage-resources op te lossen dit.</span><span class="sxs-lookup"><span data-stu-id="d8016-153">To resolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="d8016-154">Er zijn geen AD-abonnementen kunnen maken van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="d8016-154">AD subscriptions are not able to create Azure resources.</span></span>

<span data-ttu-id="d8016-155">Voor specifieke bekende beperkingen, gaat u naar [beperkingen van Cloud-Shell](limitations.md).</span><span class="sxs-lookup"><span data-stu-id="d8016-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
