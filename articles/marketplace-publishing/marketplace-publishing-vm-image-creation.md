---
title: De installatiekopie van een virtuele machine maken voor Azure Marketplace | Microsoft Docs
description: Gedetailleerde instructies voor het maken van de installatiekopie van een virtuele machine voor Azure Marketplace voor anderen om aan te schaffen.
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: 046ce7af40301014746c6aef07d08d81ab4adcc2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="guide-to-create-a-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="08516-103">Handleiding voor het maken van de installatiekopie van een virtuele machine voor Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="08516-103">Guide to create a virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="08516-104">In dit artikel **stap 2**, wordt u begeleid bij het voorbereiden van de virtuele harde schijven (VHD's) dat u naar Azure Marketplace implementeren wilt.</span><span class="sxs-lookup"><span data-stu-id="08516-104">This article, **Step 2**, walks you through preparing the virtual hard disks (VHDs) that you will deploy to the Azure Marketplace.</span></span> <span data-ttu-id="08516-105">Uw VHD's vormen de basis van uw SKU.</span><span class="sxs-lookup"><span data-stu-id="08516-105">Your VHDs are the foundation of your SKU.</span></span> <span data-ttu-id="08516-106">Het proces is afhankelijk van of u een SKU op basis van Linux of op basis van Windows biedt.</span><span class="sxs-lookup"><span data-stu-id="08516-106">The process differs depending on whether you are providing a Linux-based or Windows-based SKU.</span></span> <span data-ttu-id="08516-107">In dit artikel komen beide scenario's.</span><span class="sxs-lookup"><span data-stu-id="08516-107">This article covers both scenarios.</span></span> <span data-ttu-id="08516-108">Dit proces kan worden uitgevoerd in combinatie met [accountaanmaking en registratie][link-acct-creation].</span><span class="sxs-lookup"><span data-stu-id="08516-108">This process can be performed in parallel with [Account creation and registration][link-acct-creation].</span></span>

## <a name="1-define-offers-and-skus"></a><span data-ttu-id="08516-109">1. Definieer aanbiedingen en SKU 's</span><span class="sxs-lookup"><span data-stu-id="08516-109">1. Define Offers and SKUs</span></span>
<span data-ttu-id="08516-110">In deze sectie leert u de aanbiedingen en hun bijbehorende SKU's definiëren.</span><span class="sxs-lookup"><span data-stu-id="08516-110">In this section, you learn to define the offers and their associated SKUs.</span></span>

<span data-ttu-id="08516-111">Een aanbieding fungeert als "ouder" voor alle bijbehorende SKU's.</span><span class="sxs-lookup"><span data-stu-id="08516-111">An offer is a "parent" to all of its SKUs.</span></span> <span data-ttu-id="08516-112">U kunt meerdere aanbiedingen hebben.</span><span class="sxs-lookup"><span data-stu-id="08516-112">You can have multiple offers.</span></span> <span data-ttu-id="08516-113">Het is aan u om te besluiten hoe u uw aanbiedingen wilt structureren.</span><span class="sxs-lookup"><span data-stu-id="08516-113">How you decide to structure your offers is up to you.</span></span> <span data-ttu-id="08516-114">Wanneer een aanbieding wordt doorgestuurd voor fasering, wordt deze samen met alle bijbehorende SKU's doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="08516-114">When an offer is pushed to staging, it is pushed along with all of its SKUs.</span></span> <span data-ttu-id="08516-115">Overweeg zorgvuldig de SKU-id's, omdat ze zichtbaar in de URL:</span><span class="sxs-lookup"><span data-stu-id="08516-115">Carefully consider your SKU identifiers, because they will be visible in the URL:</span></span>

* <span data-ttu-id="08516-116">Azure.com: http://azure.microsoft.com/marketplace/partners/ {PartnerNamespace} / {OfferIdentifier}-{SKUidentifier}</span><span class="sxs-lookup"><span data-stu-id="08516-116">Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}</span></span>
* <span data-ttu-id="08516-117">Azure preview-portal: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {SKUIDdentifier}</span><span class="sxs-lookup"><span data-stu-id="08516-117">Azure preview portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}</span></span>  

<span data-ttu-id="08516-118">Een SKU is de naam van de commerciële voor een VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="08516-118">A SKU is the commercial name for a VM image.</span></span> <span data-ttu-id="08516-119">Een VM-installatiekopie bevat de schijf van een besturingssysteem en nul of meer gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="08516-119">A VM image contains one operating system disk and zero or more data disks.</span></span> <span data-ttu-id="08516-120">In essentie is dit het volledige opslagprofiel voor een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="08516-120">It is essentially the complete storage profile for a virtual machine.</span></span> <span data-ttu-id="08516-121">Een VHD is per schijf nodig.</span><span class="sxs-lookup"><span data-stu-id="08516-121">One VHD is needed per disk.</span></span> <span data-ttu-id="08516-122">Zelfs leeg gegevensschijven vereisen een VHD moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08516-122">Even blank data disks require a VHD to be created.</span></span>

<span data-ttu-id="08516-123">Ongeacht het te gebruiken besturingssysteem voegt u alleen het minimum aantal gegevensschijven toe dat voor de SKU is vereist.</span><span class="sxs-lookup"><span data-stu-id="08516-123">Regardless of which operating system you use, add only the minimum number of data disks needed by the SKU.</span></span> <span data-ttu-id="08516-124">Klanten schijven die deel van een afbeelding op het moment van implementatie uitmaken kunnen niet worden verwijderd, maar kunnen altijd schijven toevoegen tijdens of na de implementatie als ze deze nodig.</span><span class="sxs-lookup"><span data-stu-id="08516-124">Customers cannot remove disks that are part of an image at the time of deployment but can always add disks during or after deployment if they need them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08516-125">**Het aantal schijven in een nieuwe Afbeeldingversie niet wijzigen.**</span><span class="sxs-lookup"><span data-stu-id="08516-125">**Do not change disk count in a new image version.**</span></span> <span data-ttu-id="08516-126">Als u gegevensschijven in de afbeelding configureren moet, definieert u een nieuwe SKU.</span><span class="sxs-lookup"><span data-stu-id="08516-126">If you must reconfigure Data disks in the image, define a new SKU.</span></span> <span data-ttu-id="08516-127">Publiceren van een nieuwe Afbeeldingversie met een andere schijf aantallen zal hebben de mogelijkheden van de nieuwe implementatie van recente gebaseerd op de nieuwe afbeeldingsversie in geval van automatisch schalen, automatische implementaties van oplossingen op basis van ARM-sjablonen en andere scenario's.</span><span class="sxs-lookup"><span data-stu-id="08516-127">Publishing a new image version with different disk counts will have the potential of breaking new deployment based on the new image version in cases of auto-scaling, automatic deployments of solutions through ARM templates and other scenarios.</span></span>
>
>

### <a name="11-add-an-offer"></a><span data-ttu-id="08516-128">1.1 een aanbieding toevoegen</span><span class="sxs-lookup"><span data-stu-id="08516-128">1.1 Add an offer</span></span>
1. <span data-ttu-id="08516-129">Aanmelden bij de [Publishing Portal] [ link-pubportal] met behulp van uw verkopersaccount.</span><span class="sxs-lookup"><span data-stu-id="08516-129">Sign in to the [Publishing Portal][link-pubportal] by using your seller account.</span></span>
2. <span data-ttu-id="08516-130">Selecteer de **virtuele Machines** tabblad van de Portal voor publiceren.</span><span class="sxs-lookup"><span data-stu-id="08516-130">Select the **Virtual Machines** tab of the Publishing Portal.</span></span> <span data-ttu-id="08516-131">Voer de aanbiedingsnaam van uw in het veld vraag vermelding.</span><span class="sxs-lookup"><span data-stu-id="08516-131">In the prompted entry field, enter your offer name.</span></span> <span data-ttu-id="08516-132">De aanbiedingsnaam van de is doorgaans de naam van het product of service die u van plan bent om te verkopen in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="08516-132">The offer name is typically the name of the product or service that you plan to sell in the Azure Marketplace.</span></span>
3. <span data-ttu-id="08516-133">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="08516-133">Select **Create**.</span></span>

### <a name="12-define-a-sku"></a><span data-ttu-id="08516-134">1.2 een SKU definiëren</span><span class="sxs-lookup"><span data-stu-id="08516-134">1.2 Define a SKU</span></span>
<span data-ttu-id="08516-135">Nadat u een aanbieding hebt toegevoegd, moet u voor het definiëren en uw SKU's identificeren.</span><span class="sxs-lookup"><span data-stu-id="08516-135">After you have added an offer, you need to define and identify your SKUs.</span></span> <span data-ttu-id="08516-136">U kunt meerdere aanbiedingen hebben kan, en elke aanbieding meerdere SKU's onder deze.</span><span class="sxs-lookup"><span data-stu-id="08516-136">You can have multiple offers, and each offer can have multiple SKUs under it.</span></span> <span data-ttu-id="08516-137">Wanneer een aanbieding wordt doorgestuurd voor fasering, wordt deze samen met alle bijbehorende SKU's doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="08516-137">When an offer is pushed to staging, it is pushed along with all of its SKUs.</span></span>

1. <span data-ttu-id="08516-138">**Voeg een SKU.**</span><span class="sxs-lookup"><span data-stu-id="08516-138">**Add a SKU.**</span></span> <span data-ttu-id="08516-139">De SKU is een id die wordt gebruikt in de URL vereist.</span><span class="sxs-lookup"><span data-stu-id="08516-139">The SKU requires an identifier, which is used in the URL.</span></span> <span data-ttu-id="08516-140">De id moet uniek zijn binnen uw publicatieprofiel, maar er is geen risico bestaat dat ID conflicten met andere uitgevers.</span><span class="sxs-lookup"><span data-stu-id="08516-140">The identifier must be unique within your publishing profile, but there is no risk of identifier collision with other publishers.</span></span>

   > [!NOTE]
   > <span data-ttu-id="08516-141">De aanbieding en SKU-id's worden weergegeven in de URL van de aanbieding in de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="08516-141">The offer and SKU identifiers are displayed in the offer URL in the Marketplace.</span></span>
   >
   >
2. <span data-ttu-id="08516-142">**Voeg een beknopte beschrijving voor de SKU.**</span><span class="sxs-lookup"><span data-stu-id="08516-142">**Add a summary description for your SKU.**</span></span> <span data-ttu-id="08516-143">Samenvatting beschrijvingen zijn zichtbaar voor klanten, dus moet u ze gemakkelijk leesbare.</span><span class="sxs-lookup"><span data-stu-id="08516-143">Summary descriptions are visible to customers, so you should make them easily readable.</span></span> <span data-ttu-id="08516-144">Deze informatie hoeft niet te worden vergrendeld totdat de fase 'Push naar fasering'.</span><span class="sxs-lookup"><span data-stu-id="08516-144">This information does not need to be locked until the "Push to Staging" phase.</span></span> <span data-ttu-id="08516-145">Tot dat moment bent u vrij om de informatie te bewerken.</span><span class="sxs-lookup"><span data-stu-id="08516-145">Until then, you are free to edit it.</span></span>
3. <span data-ttu-id="08516-146">Als u op Windows gebaseerde SKU's gebruikt, volgt u de voorgestelde koppelingen voor het verkrijgen van de goedgekeurde versies van Windows Server.</span><span class="sxs-lookup"><span data-stu-id="08516-146">If you are using Windows-based SKUs, follow the suggested links to acquire the approved versions of Windows Server.</span></span>

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a><span data-ttu-id="08516-147">2. Maken van een Azure-compatibele VHD (op basis van Linux)</span><span class="sxs-lookup"><span data-stu-id="08516-147">2. Create an Azure-compatible VHD (Linux-based)</span></span>
<span data-ttu-id="08516-148">Deze sectie richt zich op de aanbevolen procedures voor het maken van een Linux-gebaseerde VM-installatiekopie voor Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="08516-148">This section focuses on best practices for creating a Linux-based VM image for the Azure Marketplace.</span></span> <span data-ttu-id="08516-149">Raadpleeg de volgende documentatie voor een stapsgewijze: [maakt en uploadt u een virtuele harde schijf met het Linux-besturingssysteem](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="08516-149">For a step-by-step walkthrough, refer to the following documentation: [Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a><span data-ttu-id="08516-150">3. Maken van een Azure-compatibele VHD (gebaseerd op Windows)</span><span class="sxs-lookup"><span data-stu-id="08516-150">3. Create an Azure-compatible VHD (Windows-based)</span></span>
<span data-ttu-id="08516-151">Deze sectie richt zich op de stappen voor het maken van een SKU op basis van Windows Server voor Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="08516-151">This section focuses on the steps to create a SKU based on Windows Server for the Azure Marketplace.</span></span>

### <a name="31-ensure-that-you-are-using-the-correct-base-vhds"></a><span data-ttu-id="08516-152">3.1 Zorg ervoor dat u de juiste base VHD 's</span><span class="sxs-lookup"><span data-stu-id="08516-152">3.1 Ensure that you are using the correct base VHDs</span></span>
<span data-ttu-id="08516-153">Het besturingssysteem VHD voor VM-installatiekopie moet worden gebaseerd op een Azure-goedgekeurde basisinstallatiekopie met Windows Server of SQL Server.</span><span class="sxs-lookup"><span data-stu-id="08516-153">The operating system VHD for your VM image must be based on an Azure-approved base image that contains Windows Server or SQL Server.</span></span>

<span data-ttu-id="08516-154">Een virtuele machine maken van een van de volgende afbeeldingen om te beginnen te vinden op de [Microsoft Azure-portal][link-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="08516-154">To begin, create a VM from one of the following images, located at the [Microsoft Azure portal][link-azure-portal]:</span></span>

* <span data-ttu-id="08516-155">WindowsServer ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])</span><span class="sxs-lookup"><span data-stu-id="08516-155">Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])</span></span>
* <span data-ttu-id="08516-156">SQL Server 2014 ([Enterprise][link-sql-2014-ent], [standaard][link-sql-2014-std], [Web][link-sql-2014-web])</span><span class="sxs-lookup"><span data-stu-id="08516-156">SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web])</span></span>
* <span data-ttu-id="08516-157">SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [standaard][link-sql-2012-std], [Web][link-sql-2012-web])</span><span class="sxs-lookup"><span data-stu-id="08516-157">SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web])</span></span>

<span data-ttu-id="08516-158">Deze koppelingen zijn ook te vinden in de Portal voor Publiceren onder aan de SKU-pagina.</span><span class="sxs-lookup"><span data-stu-id="08516-158">These links can also be found in the Publishing Portal under the SKU page.</span></span>

> [!TIP]
> <span data-ttu-id="08516-159">Als u van de huidige Azure-portal of PowerShell gebruikmaakt, worden Windows Server-installatiekopieën gepubliceerde op 8 September 2014 of hoger goedgekeurd.</span><span class="sxs-lookup"><span data-stu-id="08516-159">If you are using the current Azure portal or PowerShell, Windows Server images published on September 8, 2014 and later are approved.</span></span>
>
>

### <a name="32-create-your-windows-based-vm"></a><span data-ttu-id="08516-160">3.2 maken van de VM op basis van Windows</span><span class="sxs-lookup"><span data-stu-id="08516-160">3.2 Create your Windows-based VM</span></span>
<span data-ttu-id="08516-161">U kunt uw virtuele machine op basis van een goedgekeurde basisinstallatiekopie in een paar eenvoudige stappen maken vanuit de Microsoft Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="08516-161">From the Microsoft Azure portal, you can create your VM based on an approved base image in just a few simple steps.</span></span> <span data-ttu-id="08516-162">Hier volgt een overzicht van het proces:</span><span class="sxs-lookup"><span data-stu-id="08516-162">The following is an overview of the process:</span></span>

1. <span data-ttu-id="08516-163">Selecteer in de pagina basisinstallatiekopie **virtuele Machine maken** om te worden omgeleid naar de nieuwe [Microsoft Azure-portal][link-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="08516-163">From the base image page, select **Create Virtual Machine** to be directed to the new [Microsoft Azure portal][link-azure-portal].</span></span>

    ![tekenen][img-acom-1]
2. <span data-ttu-id="08516-165">Aanmelden bij de portal met de Microsoft-account en wachtwoord voor het Azure-abonnement dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="08516-165">Sign in to the portal with the Microsoft account and password for the Azure subscription you want to use.</span></span>
3. <span data-ttu-id="08516-166">Volg de aanwijzingen voor het maken van een virtuele machine met behulp van de basisinstallatiekopie die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="08516-166">Follow the prompts to create a VM by using the base image you have selected.</span></span> <span data-ttu-id="08516-167">U moet een host (naam van de computer), (geregistreerd als een beheerder) gebruikersnaam en wachtwoord opgeven voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="08516-167">You need to provide a host name (name of the computer), user name (registered as an administrator), and password for the VM.</span></span>

    ![tekenen][img-portal-vm-create]
4. <span data-ttu-id="08516-169">Selecteer de grootte van de virtuele machine te implementeren:</span><span class="sxs-lookup"><span data-stu-id="08516-169">Select the size of the VM to deploy:</span></span>

    <span data-ttu-id="08516-170">a.</span><span class="sxs-lookup"><span data-stu-id="08516-170">a.</span></span>    <span data-ttu-id="08516-171">Als u van plan bent voor het ontwikkelen van de VHD on-premises, wordt de grootte is niet belangrijk.</span><span class="sxs-lookup"><span data-stu-id="08516-171">If you plan to develop the VHD on-premises, the size does not matter.</span></span> <span data-ttu-id="08516-172">Overweeg het gebruikt van een van de kleinere VM's.</span><span class="sxs-lookup"><span data-stu-id="08516-172">Consider using one of the smaller VMs.</span></span>

    <span data-ttu-id="08516-173">b.</span><span class="sxs-lookup"><span data-stu-id="08516-173">b.</span></span>    <span data-ttu-id="08516-174">Als u van plan bent de installatiekopie in Azure te ontwikkelen, kunt u het gebruik van een van de aanbevolen VM-groottes voor de geselecteerde installatiekopie overwegen.</span><span class="sxs-lookup"><span data-stu-id="08516-174">If you plan to develop the image in Azure, consider using one of the recommended VM sizes for the selected image.</span></span>

    <span data-ttu-id="08516-175">c.</span><span class="sxs-lookup"><span data-stu-id="08516-175">c.</span></span>    <span data-ttu-id="08516-176">Raadpleeg voor informatie over prijzen, de **aanbevolen Prijscategorieën** selector op de portal weergegeven.</span><span class="sxs-lookup"><span data-stu-id="08516-176">For pricing information, refer to the **Recommended pricing tiers** selector displayed on the portal.</span></span> <span data-ttu-id="08516-177">Deze biedt de drie aanbevolen groottes die door de uitgever worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="08516-177">It will provide the three recommended sizes provided by the publisher.</span></span> <span data-ttu-id="08516-178">(In dit geval is Microsoft de uitgever.)</span><span class="sxs-lookup"><span data-stu-id="08516-178">(In this case, the publisher is Microsoft.)</span></span>

    ![tekenen][img-portal-vm-size]
5. <span data-ttu-id="08516-180">Eigenschappen instellen:</span><span class="sxs-lookup"><span data-stu-id="08516-180">Set properties:</span></span>

    <span data-ttu-id="08516-181">a.</span><span class="sxs-lookup"><span data-stu-id="08516-181">a.</span></span>    <span data-ttu-id="08516-182">Voor snelle implementatie kunt u de standaardwaarden voor de eigenschappen onder laten **optionele configuratie** en **resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="08516-182">For quick deployment, you can leave the default values for the properties under **Optional Configuration** and **Resource Group**.</span></span>

    <span data-ttu-id="08516-183">b.</span><span class="sxs-lookup"><span data-stu-id="08516-183">b.</span></span>    <span data-ttu-id="08516-184">Onder **Opslagaccount**, kunt u eventueel de storage-account waarin het VHD-besturingssysteem wordt opgeslagen selecteren.</span><span class="sxs-lookup"><span data-stu-id="08516-184">Under **Storage Account**, you can optionally select the storage account in which the operating system VHD will be stored.</span></span>

    <span data-ttu-id="08516-185">c.</span><span class="sxs-lookup"><span data-stu-id="08516-185">c.</span></span>    <span data-ttu-id="08516-186">Onder **resourcegroep**, kunt u eventueel de logische groep voor de virtuele machine te selecteren.</span><span class="sxs-lookup"><span data-stu-id="08516-186">Under **Resource Group**, you can optionally select the logical group in which to place the VM.</span></span>
6. <span data-ttu-id="08516-187">Selecteer de **locatie** voor implementatie:</span><span class="sxs-lookup"><span data-stu-id="08516-187">Select the **Location** for deployment:</span></span>

    <span data-ttu-id="08516-188">a.</span><span class="sxs-lookup"><span data-stu-id="08516-188">a.</span></span>    <span data-ttu-id="08516-189">Als u van plan bent voor het ontwikkelen van de VHD on-premises, wordt de locatie is niet belangrijk omdat u de installatiekopie naar Azure later uploaden zult.</span><span class="sxs-lookup"><span data-stu-id="08516-189">If you plan to develop the VHD on-premises, the location does not matter because you will upload the image to Azure later.</span></span>

    <span data-ttu-id="08516-190">b.</span><span class="sxs-lookup"><span data-stu-id="08516-190">b.</span></span>    <span data-ttu-id="08516-191">Als u van plan bent de installatiekopie in Azure te ontwikkelen, kunt u het gebruik van een van de in de VS gebaseerde Microsoft Azure-regio's vanaf het begin overwegen.</span><span class="sxs-lookup"><span data-stu-id="08516-191">If you plan to develop the image in Azure, consider using one of the US-based Microsoft Azure regions from the beginning.</span></span> <span data-ttu-id="08516-192">Dit versnelt de VHD kopiëren die Microsoft namens jou worden uitgevoerd als u uw afbeelding voor de certificeringsinstantie indienen.</span><span class="sxs-lookup"><span data-stu-id="08516-192">This speeds up the VHD copying process that Microsoft performs on your behalf when you submit your image for certification.</span></span>

    ![tekenen][img-portal-vm-location]
7. <span data-ttu-id="08516-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="08516-194">Click **Create**.</span></span> <span data-ttu-id="08516-195">Voor het implementeren van de VM start.</span><span class="sxs-lookup"><span data-stu-id="08516-195">The VM starts to deploy.</span></span> <span data-ttu-id="08516-196">Binnen enkele minuten beschikt u over een geslaagde implementatie en kunt u beginnen met het maken van de installatiekopie voor uw SKU.</span><span class="sxs-lookup"><span data-stu-id="08516-196">Within minutes, you will have a successful deployment and can begin to create the image for your SKU.</span></span>

### <a name="33-develop-your-vhd-in-the-cloud"></a><span data-ttu-id="08516-197">3.3 ontwikkelen van uw VHD in de cloud</span><span class="sxs-lookup"><span data-stu-id="08516-197">3.3 Develop your VHD in the cloud</span></span>
<span data-ttu-id="08516-198">Wij raden u aan uw VHD in de cloud te ontwikkelen met behulp van Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="08516-198">We strongly recommend that you develop your VHD in the cloud by using Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="08516-199">U verbinding met RDP met de gebruikersnaam en wachtwoord die zijn opgegeven tijdens het inrichten.</span><span class="sxs-lookup"><span data-stu-id="08516-199">You connect to RDP with the user name and password specified during provisioning.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08516-200">Als u uw VHD ontwikkelt op locatie (dit wordt niet aanbevolen), Zie [maken van de installatiekopie van een virtuele machine op de lokale](marketplace-publishing-vm-image-creation-on-premise.md).</span><span class="sxs-lookup"><span data-stu-id="08516-200">If you develop your VHD on-premises (which is not recommended), see [Creating a virtual machine image on-premises](marketplace-publishing-vm-image-creation-on-premise.md).</span></span> <span data-ttu-id="08516-201">Downloaden van de VHD is niet nodig als u in de cloud ontwikkelt.</span><span class="sxs-lookup"><span data-stu-id="08516-201">Downloading your VHD is not necessary if you are developing in the cloud.</span></span>
>
>

<span data-ttu-id="08516-202">**Verbinden via RDP met behulp van de [Microsoft Azure-portal][link-azure-portal]**</span><span class="sxs-lookup"><span data-stu-id="08516-202">**Connect via RDP using the [Microsoft Azure portal][link-azure-portal]**</span></span>

1. <span data-ttu-id="08516-203">Selecteer **Bladeren** > **VMs**.</span><span class="sxs-lookup"><span data-stu-id="08516-203">Select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="08516-204">De virtuele machines-blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="08516-204">The Virtual machines blade opens.</span></span> <span data-ttu-id="08516-205">Zorg dat de virtuele machine die u wilt verbinden met wordt uitgevoerd en selecteer vervolgens in de lijst met geïmplementeerde virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="08516-205">Ensure that the VM that you want to connect with is running, and then select it from the list of deployed VMs.</span></span>
3. <span data-ttu-id="08516-206">Er wordt een blade geopend die worden beschreven van de geselecteerde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="08516-206">A blade opens that describes the selected VM.</span></span> <span data-ttu-id="08516-207">Klik aan de bovenkant **Connect**.</span><span class="sxs-lookup"><span data-stu-id="08516-207">At the top, click **Connect**.</span></span>
4. <span data-ttu-id="08516-208">U wordt gevraagd om in te voeren de gebruikersnaam en wachtwoord die u hebt opgegeven tijdens het inrichten.</span><span class="sxs-lookup"><span data-stu-id="08516-208">You are prompted to enter the user name and password that you specified during provisioning.</span></span>

<span data-ttu-id="08516-209">**Verbinden via RDP met behulp van PowerShell**</span><span class="sxs-lookup"><span data-stu-id="08516-209">**Connect via RDP using PowerShell**</span></span>

<span data-ttu-id="08516-210">Als u wilt downloaden van een extern bureaublad-bestand naar een lokale computer de [cmdlet Get-AzureRemoteDesktopFile][link-technet-2].</span><span class="sxs-lookup"><span data-stu-id="08516-210">To download a remote desktop file to a local machine, use the [Get-AzureRemoteDesktopFile cmdlet][link-technet-2].</span></span> <span data-ttu-id="08516-211">U moet deze cmdlet gebruikt, de naam van de service en de naam van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="08516-211">In order to use this cmdlet, you need to know the name of the service and name of the VM.</span></span> <span data-ttu-id="08516-212">Als u hebt gemaakt van de virtuele machine van de [Microsoft Azure-portal][link-azure-portal], u vindt deze informatie onder VM-eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="08516-212">If you created the VM from the [Microsoft Azure portal][link-azure-portal], you can find this information under VM properties:</span></span>

1. <span data-ttu-id="08516-213">Selecteer in de Microsoft Azure-portal **Bladeren** > **VMs**.</span><span class="sxs-lookup"><span data-stu-id="08516-213">In the Microsoft Azure portal, select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="08516-214">De virtuele machines-blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="08516-214">The Virtual machines blade opens.</span></span> <span data-ttu-id="08516-215">Selecteer de virtuele machine die u hebt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="08516-215">Select the VM that you deployed.</span></span>
3. <span data-ttu-id="08516-216">Er wordt een blade geopend die worden beschreven van de geselecteerde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="08516-216">A blade opens that describes the selected VM.</span></span>
4. <span data-ttu-id="08516-217">Klik op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="08516-217">Click **Properties**.</span></span>
5. <span data-ttu-id="08516-218">Het eerste deel van de domeinnaam is de servicenaam.</span><span class="sxs-lookup"><span data-stu-id="08516-218">The first portion of the domain name is the service name.</span></span> <span data-ttu-id="08516-219">De hostnaam is de naam van de VM.</span><span class="sxs-lookup"><span data-stu-id="08516-219">The host name is the VM name.</span></span>

    ![tekenen][img-portal-vm-rdp]
6. <span data-ttu-id="08516-221">Download het RDP-bestand voor de gemaakte virtuele machine voor de lokale bureaublad van de beheerder van de cmdlet is als volgt.</span><span class="sxs-lookup"><span data-stu-id="08516-221">The cmdlet to download the RDP file for the created VM to the administrator's local desktop is as follows.</span></span>

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

<span data-ttu-id="08516-222">Meer informatie over RDP op MSDN kan worden gevonden in het artikel [verbinding maken met een Azure-VM met RDP of SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).</span><span class="sxs-lookup"><span data-stu-id="08516-222">More information about RDP can be found on MSDN in the article [Connect to an Azure VM with RDP or SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).</span></span>

<span data-ttu-id="08516-223">**Een virtuele machine te configureren en uw SKU maken**</span><span class="sxs-lookup"><span data-stu-id="08516-223">**Configure a VM and create your SKU**</span></span>

<span data-ttu-id="08516-224">Nadat het besturingssysteem dat VHD wordt gedownload, gebruik van Hyper-v en configureren van een virtuele machine om te beginnen met het maken van uw SKU.</span><span class="sxs-lookup"><span data-stu-id="08516-224">After the operating system VHD is downloaded, use Hyper­V and configure a VM to begin creating your SKU.</span></span> <span data-ttu-id="08516-225">Gedetailleerde stappen kunnen worden gevonden op de volgende TechNet-koppeling: [Hyper-v installeren en configureren van een virtuele machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="08516-225">Detailed steps can be found at the following TechNet link: [Install Hyper­V and Configure a VM](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="34-choose-the-correct-vhd-size"></a><span data-ttu-id="08516-226">3.4 Kies de juiste grootte van de VHD</span><span class="sxs-lookup"><span data-stu-id="08516-226">3.4 Choose the correct VHD size</span></span>
<span data-ttu-id="08516-227">De Windows-besturingssysteem VHD in uw VM-installatiekopie moet worden gemaakt als een vaste indeling 128 GB VHD.</span><span class="sxs-lookup"><span data-stu-id="08516-227">The Windows operating system VHD in your VM image should be created as a 128-GB fixed-format VHD.</span></span>  

<span data-ttu-id="08516-228">Als de fysieke grootte minder dan 128 GB is, moet de VHD sparse zijn.</span><span class="sxs-lookup"><span data-stu-id="08516-228">If the physical size is less than 128 GB, the VHD should be sparse.</span></span> <span data-ttu-id="08516-229">De Windows- en SQL Server basisinstallatiekopieën opgegeven al aan deze vereisten voldoet, dus Wijzig de indeling of niet de grootte van de VHD die is verkregen.</span><span class="sxs-lookup"><span data-stu-id="08516-229">The base Windows and SQL Server images provided already meet these requirements, so do not change the format or the size of the VHD obtained.</span></span>  

<span data-ttu-id="08516-230">Gegevensschijven mag even groot zijn als 1 TB.</span><span class="sxs-lookup"><span data-stu-id="08516-230">Data disks can be as large as 1 TB.</span></span> <span data-ttu-id="08516-231">Bij het kiezen van de schijfgrootte, houd er rekening mee dat klanten VHD's binnen een afbeelding kunnen niet op het moment van implementatie aangepast.</span><span class="sxs-lookup"><span data-stu-id="08516-231">When deciding on the disk size, remember that customers cannot resize VHDs within an image at the time of deployment.</span></span> <span data-ttu-id="08516-232">Gegevens schijf VHD's moeten worden gemaakt als een vaste indeling VHD.</span><span class="sxs-lookup"><span data-stu-id="08516-232">Data disk VHDs should be created as a fixed-format VHD.</span></span> <span data-ttu-id="08516-233">Ze moeten ook worden verspreid.</span><span class="sxs-lookup"><span data-stu-id="08516-233">They should also be sparse.</span></span> <span data-ttu-id="08516-234">Gegevensschijven kunnen leeg zijn of gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="08516-234">Data disks can be empty or contain data.</span></span>

### <a name="35-install-the-latest-windows-patches"></a><span data-ttu-id="08516-235">3.5 installeren de nieuwste patches voor Windows</span><span class="sxs-lookup"><span data-stu-id="08516-235">3.5 Install the latest Windows patches</span></span>
<span data-ttu-id="08516-236">De basisinstallatiekopieën bevatten de meest recente patches tot aan de publicatiedatum.</span><span class="sxs-lookup"><span data-stu-id="08516-236">The base images contain the latest patches up to their published date.</span></span> <span data-ttu-id="08516-237">Zorg ervoor dat Windows Update is uitgevoerd en dat alle essentiële en belangrijke beveiligingsupdates zijn geïnstalleerd voordat het publiceren van het besturingssysteem-VHD die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08516-237">Before publishing the operating system VHD you have created, ensure that Windows Update has been run and that all the latest Critical and Important security updates have been installed.</span></span>

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a><span data-ttu-id="08516-238">3.6 uitvoeren van extra taken voor de configuratie en planning indien nodig</span><span class="sxs-lookup"><span data-stu-id="08516-238">3.6 Perform additional configuration and schedule tasks as necessary</span></span>
<span data-ttu-id="08516-239">Wanneer u aanvullende configuratie nodig hebt, overweeg het gebruik van een geplande taak die wordt uitgevoerd bij het opstarten van een definitieve wijzigingen aanbrengen in de virtuele machine nadat deze is geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="08516-239">If additional configuration is needed, consider using a scheduled task that runs at startup to make any final changes to the VM after it has been deployed:</span></span>

* <span data-ttu-id="08516-240">Het wordt aanbevolen om de taak zichzelf na een geslaagde uitvoering te laten verwijderen.</span><span class="sxs-lookup"><span data-stu-id="08516-240">It is a best practice to have the task delete itself upon successful execution.</span></span>
* <span data-ttu-id="08516-241">Er is geen configuratie verstandig stations dan stations C of D, omdat dit de slechts twee stations die gegarandeerd altijd aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="08516-241">No configuration should rely on drives other than drives C or D, because these are the only two drives that are always guaranteed to exist.</span></span> <span data-ttu-id="08516-242">Station C is de besturingssysteemschijf en station D is de tijdelijke lokale schijf.</span><span class="sxs-lookup"><span data-stu-id="08516-242">Drive C is the operating system disk, and drive D is the temporary local disk.</span></span>

### <a name="37-generalize-the-image"></a><span data-ttu-id="08516-243">3.7 generaliseer de installatiekopie</span><span class="sxs-lookup"><span data-stu-id="08516-243">3.7 Generalize the image</span></span>
<span data-ttu-id="08516-244">Alle installatiekopieën in Azure Marketplace moet herbruikbare op algemene wijze.</span><span class="sxs-lookup"><span data-stu-id="08516-244">All images in the Azure Marketplace must be reusable in a generic fashion.</span></span> <span data-ttu-id="08516-245">Met andere woorden, moet de besturingssysteem-VHD worden gegeneraliseerd:</span><span class="sxs-lookup"><span data-stu-id="08516-245">In other words, the operating system VHD must be generalized:</span></span>

* <span data-ttu-id="08516-246">Voor Windows, moet de installatiekopie van het 'Sysprep voorbereide' en geen configuraties worden uitgevoerd die geen ondersteuning voor de **sysprep** opdracht.</span><span class="sxs-lookup"><span data-stu-id="08516-246">For Windows, the image should be "sysprepped," and no configurations should be done that do not support the **sysprep** command.</span></span>
* <span data-ttu-id="08516-247">U kunt de volgende opdracht uitvoeren vanuit de map % windir%\System32\Sysprep.</span><span class="sxs-lookup"><span data-stu-id="08516-247">You can run the following command from the directory %windir%\System32\Sysprep.</span></span>

        sysprep.exe /generalize /oobe /shutdown

  <span data-ttu-id="08516-248">Informatie over hoe het besturingssysteem naar sysprep is opgegeven in stap van de volgende MSDN-artikel: [een Windows Server-VHD naar Azure maken en uploaden](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08516-248">Guidance on how to sysprep the operating system is provided in Step of the following MSDN article: [Create and upload a Windows Server VHD to Azure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="4-deploy-a-vm-from-your-vhds"></a><span data-ttu-id="08516-249">4. Geen VM implementeren vanaf uw VHD 's</span><span class="sxs-lookup"><span data-stu-id="08516-249">4. Deploy a VM from your VHDs</span></span>
<span data-ttu-id="08516-250">Nadat u uw VHD's (de algemene besturingssysteem-VHD en nul of meer gegevens schijf VHD's) naar een Azure storage-account hebt geüpload, kunt u ze kunt registreren als een installatiekopie van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="08516-250">After you have uploaded your VHDs (the generalized operating system VHD and zero or more data disk VHDs) to an Azure storage account, you can register them as a user VM image.</span></span> <span data-ttu-id="08516-251">Vervolgens kunt u die afbeelding testen.</span><span class="sxs-lookup"><span data-stu-id="08516-251">Then you can test that image.</span></span> <span data-ttu-id="08516-252">Houd er rekening mee omdat uw besturingssysteem-VHD is gegeneraliseerd, u de VM rechtstreeks implementeren kunt door de URL van de VHD.</span><span class="sxs-lookup"><span data-stu-id="08516-252">Note that because your operating system VHD is generalized, you cannot directly deploy the VM by providing the VHD URL.</span></span>

<span data-ttu-id="08516-253">Voor meer informatie over de VM-installatiekopieën, controleert u de volgende blogberichten:</span><span class="sxs-lookup"><span data-stu-id="08516-253">To learn more about VM images, review the following blog posts:</span></span>

* [<span data-ttu-id="08516-254">VM-installatiekopie</span><span class="sxs-lookup"><span data-stu-id="08516-254">VM Image</span></span>](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [<span data-ttu-id="08516-255">VM Image PowerShell hoe</span><span class="sxs-lookup"><span data-stu-id="08516-255">VM Image PowerShell How To</span></span>](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [<span data-ttu-id="08516-256">Over de installatiekopieën van de virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="08516-256">About VM images in Azure</span></span>](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-the-necessary-tools-powershell-and-azure-cli"></a><span data-ttu-id="08516-257">De benodigde hulpprogramma's, PowerShell en Azure CLI instellen</span><span class="sxs-lookup"><span data-stu-id="08516-257">Set up the necessary tools, PowerShell and Azure CLI</span></span>
* [<span data-ttu-id="08516-258">Het instellen van PowerShell</span><span class="sxs-lookup"><span data-stu-id="08516-258">How to setup PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="08516-259">Het instellen van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="08516-259">How to setup Azure CLI</span></span>](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a><span data-ttu-id="08516-260">4.1 een installatiekopie van een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="08516-260">4.1 Create a user VM image</span></span>
#### <a name="capture-vm"></a><span data-ttu-id="08516-261">Vastleggen van VM</span><span class="sxs-lookup"><span data-stu-id="08516-261">Capture VM</span></span>
<span data-ttu-id="08516-262">Lees de koppelingen hieronder voor hulp bij het vastleggen van de virtuele machine met behulp van PowerShell-API/Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="08516-262">Please read the links given below for guidance on capturing the VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="08516-263">API</span><span class="sxs-lookup"><span data-stu-id="08516-263">API</span></span>](https://msdn.microsoft.com/library/mt163560.aspx)
* [<span data-ttu-id="08516-264">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08516-264">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="08516-265">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="08516-265">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a><span data-ttu-id="08516-266">Generaliseer installatiekopie</span><span class="sxs-lookup"><span data-stu-id="08516-266">Generalize Image</span></span>
<span data-ttu-id="08516-267">Lees de koppelingen hieronder voor hulp bij het vastleggen van de virtuele machine met behulp van PowerShell-API/Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="08516-267">Please read the links given below for guidance on capturing the VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="08516-268">API</span><span class="sxs-lookup"><span data-stu-id="08516-268">API</span></span>](https://msdn.microsoft.com/library/mt269439.aspx)
* [<span data-ttu-id="08516-269">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08516-269">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="08516-270">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="08516-270">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a><span data-ttu-id="08516-271">4.2 geen VM implementeren vanaf een installatiekopie van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="08516-271">4.2 Deploy a VM from a user VM image</span></span>
<span data-ttu-id="08516-272">Voor het implementeren van een virtuele machine van een installatiekopie van een virtuele machine, kunt u de huidige [Azure-portal](https://manage.windowsazure.com) of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08516-272">To deploy a VM from a user VM image, you can use the current [Azure portal](https://manage.windowsazure.com) or PowerShell.</span></span>

<span data-ttu-id="08516-273">**Geen VM implementeren vanaf de huidige Azure-portal**</span><span class="sxs-lookup"><span data-stu-id="08516-273">**Deploy a VM from the current Azure portal**</span></span>

1. <span data-ttu-id="08516-274">Ga naar **nieuw** > **Compute** > **virtuele machine** > **vanuit galerie**.</span><span class="sxs-lookup"><span data-stu-id="08516-274">Go to **New** > **Compute** > **Virtual machine** > **From gallery**.</span></span>

    ![tekenen][img-manage-vm-new]
2. <span data-ttu-id="08516-276">Ga naar **Mijn afbeeldingen**, en selecteer vervolgens de VM-installatiekopie waaruit een virtuele machine implementeren:</span><span class="sxs-lookup"><span data-stu-id="08516-276">Go to **My images**, and then select the VM image from which to deploy a VM:</span></span>

   1. <span data-ttu-id="08516-277">Aandacht besteedt aan de afbeelding die u selecteert, omdat de **Mijn afbeeldingen** weergave bevat zowel installatiekopieën van besturingssystemen en VM-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="08516-277">Pay close attention to which image you select, because the **My images** view lists both operating system images and VM images.</span></span>
   2. <span data-ttu-id="08516-278">Kijken naar het aantal schijven kunt u bepalen welk type installatiekopie die u implementeert, omdat het merendeel van de VM-installatiekopieën meer dan één schijf.</span><span class="sxs-lookup"><span data-stu-id="08516-278">Looking at the number of disks can help determine what type of image you are deploying, because the majority of VM images have more than one disk.</span></span> <span data-ttu-id="08516-279">Het is echter nog steeds mogelijk om een VM-afbeelding met slechts één besturingssysteemschijf, die vervolgens **aantal schijven** ingesteld op 1.</span><span class="sxs-lookup"><span data-stu-id="08516-279">However, it is still possible to have a VM image with only a single operating system disk, which would then have **Number of disks** set to 1.</span></span>

      ![tekenen][img-manage-vm-select]
3. <span data-ttu-id="08516-281">Volg de wizard virtuele machine maken en de VM naam, VM grootte, locatie, gebruikersnaam en wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="08516-281">Follow the VM creation wizard and specify the VM name, VM size, location, user name, and password.</span></span>

<span data-ttu-id="08516-282">**Een virtuele machine vanuit PowerShell implementeren**</span><span class="sxs-lookup"><span data-stu-id="08516-282">**Deploy a VM from PowerShell**</span></span>

<span data-ttu-id="08516-283">U kunt de volgende cmdlets kunt gebruiken voor het implementeren van een grote virtuele machine van de algemene VM-installatiekopie zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08516-283">To deploy a large VM from the generalized VM image just created, you can use the following cmdlets.</span></span>

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> <span data-ttu-id="08516-284">Zie [probleemoplossing problemen aangetroffen tijdens het maken van de VHD] voor assistentie.</span><span class="sxs-lookup"><span data-stu-id="08516-284">Please refer [Troubleshooting common issues encountered during VHD creation] for additional assistance.</span></span>
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a><span data-ttu-id="08516-285">5. Certificeringsinstantie voor uw VM-installatiekopie verkrijgen</span><span class="sxs-lookup"><span data-stu-id="08516-285">5. Obtain certification for your VM image</span></span>
<span data-ttu-id="08516-286">De volgende stap bij het voorbereiden van uw VM-installatiekopie op Azure Marketplace is dat het gecertificeerd.</span><span class="sxs-lookup"><span data-stu-id="08516-286">The next step in preparing your VM image for the Azure Marketplace is to have it certified.</span></span>

<span data-ttu-id="08516-287">Dit proces omvat het uitvoeren van een certificeringsinstantie speciale hulpprogramma, de verificatieresultaten uploaden naar de Azure-container waarin uw VHD's zich bevinden, toe te voegen een aanbieding, definiëren van uw SKU en verzenden van uw VM-installatiekopie voor certificering.</span><span class="sxs-lookup"><span data-stu-id="08516-287">This process includes running a special certification tool, uploading the verification results to the Azure container where your VHDs reside, adding an offer, defining your SKU, and submitting your VM image for certification.</span></span>

### <a name="51-download-and-run-the-certification-test-tool-for-azure-certified"></a><span data-ttu-id="08516-288">5.1 downloaden en uitvoeren van de certificeringsinstantie Test-hulpprogramma voor Azure gecertificeerd</span><span class="sxs-lookup"><span data-stu-id="08516-288">5.1 Download and run the Certification Test Tool for Azure Certified</span></span>
<span data-ttu-id="08516-289">Het hulpprogramma certificeringsinstantie wordt uitgevoerd op een actieve virtuele machine, ingericht vanuit uw gebruiker VM-installatiekopie, om ervoor te zorgen dat de VM-installatiekopie compatibel met Microsoft Azure is.</span><span class="sxs-lookup"><span data-stu-id="08516-289">The certification tool runs on a running VM, provisioned from your user VM image, to ensure that the VM image is compatible with Microsoft Azure.</span></span> <span data-ttu-id="08516-290">Het hulpprogramma controleert of is voldaan aan de richtlijnen en vereisten voor het voorbereiden van uw VHD.</span><span class="sxs-lookup"><span data-stu-id="08516-290">It will verify that the guidance and requirements about preparing your VHD have been met.</span></span> <span data-ttu-id="08516-291">De uitvoer van het hulpprogramma is een compatibiliteitsrapport die moet worden geüpload in de Publishing Portal tijdens aanvragende certificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="08516-291">The output of the tool is a compatibility report, which should be uploaded on the Publishing Portal while requesting certification.</span></span>

<span data-ttu-id="08516-292">Het hulpprogramma voor de certificeringsinstantie kan worden gebruikt met Windows- en Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="08516-292">The certification tool can be used with both Windows and Linux VMs.</span></span> <span data-ttu-id="08516-293">Deze verbinding maakt met Windows-VM's via PowerShell en verbinding maakt met virtuele machines van Linux via SSH.Net:</span><span class="sxs-lookup"><span data-stu-id="08516-293">It connects to Windows-based VMs via PowerShell and connects to Linux VMs via SSH.Net:</span></span>

1. <span data-ttu-id="08516-294">Downloadt u eerst het hulpprogramma certificeringsinstantie op de [Microsoft-website][link-msft-download].</span><span class="sxs-lookup"><span data-stu-id="08516-294">First, download the certification tool at the [Microsoft download site][link-msft-download].</span></span>
2. <span data-ttu-id="08516-295">Open het hulpprogramma voor certificering en klik vervolgens op de **nieuwe Test Start** knop.</span><span class="sxs-lookup"><span data-stu-id="08516-295">Open the certification tool, and then click the **Start New Test** button.</span></span>
3. <span data-ttu-id="08516-296">Van de **informatie testen** scherm, voer een naam voor de test uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="08516-296">From the **Test Information** screen, enter a name for the test run.</span></span>
4. <span data-ttu-id="08516-297">Bepaal of uw VM op Linux of op Windows draait.</span><span class="sxs-lookup"><span data-stu-id="08516-297">Choose whether your VM is on Linux or Windows.</span></span> <span data-ttu-id="08516-298">Afhankelijk van uw keuze selecteert u de vervolgopties.</span><span class="sxs-lookup"><span data-stu-id="08516-298">Depending on which you choose, select the subsequent options.</span></span>

### <a name="connect-the-certification-tool-to-a-linux-vm-image"></a><span data-ttu-id="08516-299">**Verbinding maken met het hulpprogramma certificeringsinstantie op een installatiekopie van het Linux-VM**</span><span class="sxs-lookup"><span data-stu-id="08516-299">**Connect the certification tool to a Linux VM image**</span></span>
1. <span data-ttu-id="08516-300">Selecteer de SSH-verificatiemodus: wachtwoord of sleutelbestand.</span><span class="sxs-lookup"><span data-stu-id="08516-300">Select the SSH authentication mode: password or key file.</span></span>
2. <span data-ttu-id="08516-301">Als verificatie op basis van wachtwoorden, voer de naam, gebruikersnaam en wachtwoord van Domain Name System (DNS).</span><span class="sxs-lookup"><span data-stu-id="08516-301">If using password-­based authentication, enter the Domain Name System (DNS) name, user name, and password.</span></span>
3. <span data-ttu-id="08516-302">Als u sleutelbestand authenticatie gebruikt, voert u de DNS-naam, de gebruikersnaam en de locatie van de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="08516-302">If using key file authentication, enter the DNS name, user name, and private key location.</span></span>

   ![Wachtwoordverificatie van Linux VM-installatiekopie][img-cert-vm-pswd-lnx]

   ![Sleutelbestand verificatie van Linux VM-installatiekopie][img-cert-vm-key-lnx]

### <a name="connect-the-certification-tool-to-a-windows-based-vm-image"></a><span data-ttu-id="08516-305">**Verbinding maken met het hulpprogramma certificeringsinstantie van een VM op basis van Windows-installatiekopie**</span><span class="sxs-lookup"><span data-stu-id="08516-305">**Connect the certification tool to a Windows-based VM image**</span></span>
1. <span data-ttu-id="08516-306">Geef de volledig gekwalificeerde VM DNS-naam (bijvoorbeeld MyVMName.Cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="08516-306">Enter the fully qualified VM DNS name (for example, MyVMName.Cloudapp.net).</span></span>
2. <span data-ttu-id="08516-307">Geef de gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="08516-307">Enter the user name and password.</span></span>

   ![Wachtwoordverificatie van Windows VM-installatiekopie][img-cert-vm-pswd-win]

<span data-ttu-id="08516-309">Nadat u de juiste opties voor uw Linux- of virtuele machine op basis van Windows-installatiekopie hebt geselecteerd, selecteert u **testverbinding** om ervoor te zorgen dat SSH.Net of PowerShell een geldige verbinding is voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="08516-309">After you have selected the correct options for your Linux or Windows-based VM image, select **Test Connection** to ensure that SSH.Net or PowerShell has a valid connection for testing purposes.</span></span> <span data-ttu-id="08516-310">Nadat een verbinding tot stand is gebracht, selecteert u **volgende** om de test te starten.</span><span class="sxs-lookup"><span data-stu-id="08516-310">After a connection is established, select **Next** to start the test.</span></span>

<span data-ttu-id="08516-311">Wanneer de test is voltooid, ontvangt u de resultaten ('Pass'/'Fail'/'Warning' (Geslaagd/Mislukt/Waarschuwing)) voor elk testelement.</span><span class="sxs-lookup"><span data-stu-id="08516-311">When the test is complete, you will receive the results (Pass/Fail/Warning) for each test element.</span></span>

![Testscenario's voor Linux VM-installatiekopie][img-cert-vm-test-lnx]

![Testscenario's voor VM-installatiekopie voor Windows][img-cert-vm-test-win]

<span data-ttu-id="08516-314">Als een van de tests mislukt, wordt de afbeelding niet gecertificeerd.</span><span class="sxs-lookup"><span data-stu-id="08516-314">If any of the tests fail, your image will not be certified.</span></span> <span data-ttu-id="08516-315">Als dit het geval is, de vereisten doornemen en breng de gewenste wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="08516-315">If this occurs, review the requirements and make any necessary changes.</span></span>

<span data-ttu-id="08516-316">Na de geautomatiseerde test, wordt u gevraagd naar aanvullende gegevens over uw VM-installatiekopie via een scherm vragenlijst opgeven.</span><span class="sxs-lookup"><span data-stu-id="08516-316">After the automated test, you are asked to provide additional input on your VM image via a questionnaire screen.</span></span>  <span data-ttu-id="08516-317">Voltooien van de vragen en selecteer vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="08516-317">Complete the questions, and then select **Next**.</span></span>

![Certificeringsinstantie hulpprogramma vragenlijst][img-cert-vm-questionnaire]

![Certificeringsinstantie hulpprogramma vragenlijst][img-cert-vm-questionnaire-2]

<span data-ttu-id="08516-320">Nadat u de vragenlijst hebt voltooid, kunt u aanvullende informatie zoals SSH toegang tot gegevens van de Linux-VM bieden installatiekopie en een uitleg voor elke mislukte beoordelingen zijn tegengekomen.</span><span class="sxs-lookup"><span data-stu-id="08516-320">After you have completed the questionnaire, you can provide additional information such as SSH access information for the Linux VM image and an explanation for any failed assessments.</span></span> <span data-ttu-id="08516-321">U kunt de testresultaten en de logboekbestanden voor de uitgevoerde testcases naast uw antwoorden op de vragenlijst downloaden.</span><span class="sxs-lookup"><span data-stu-id="08516-321">You can download the test results and log files for the executed test cases in addition to your answers to the questionnaire.</span></span> <span data-ttu-id="08516-322">De resultaten opslaan in dezelfde container als uw virtuele harde schijven.</span><span class="sxs-lookup"><span data-stu-id="08516-322">Save the results in the same container as your VHDs.</span></span>

![Certificeringsinstantie testresultaten opslaan][img-cert-vm-results]

### <a name="52-get-the-shared-access-signature-uri-for-your-vm-images"></a><span data-ttu-id="08516-324">5.2 ophalen van de shared access signature URI voor uw VM-installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="08516-324">5.2 Get the shared access signature URI for your VM images</span></span>
<span data-ttu-id="08516-325">Tijdens het publicatieproces, moet u de uniform resource-id's (URI's) die leiden tot elk van de VHD's die u hebt gemaakt voor de SKU opgeven.</span><span class="sxs-lookup"><span data-stu-id="08516-325">During the publishing process, you specify the uniform resource identifiers (URIs) that lead to each of the VHDs you have created for your SKU.</span></span> <span data-ttu-id="08516-326">Tijdens het certificeringsproces moet Microsoft toegang hebben tot deze VHD's.</span><span class="sxs-lookup"><span data-stu-id="08516-326">Microsoft needs access to these VHDs during the certification process.</span></span> <span data-ttu-id="08516-327">Daarom moet u een shared access signature URI voor elke VHD te maken.</span><span class="sxs-lookup"><span data-stu-id="08516-327">Therefore, you need to create a shared access signature URI for each VHD.</span></span> <span data-ttu-id="08516-328">Dit is de URI die moet worden ingevoerd in de **installatiekopieën** tabblad in de Portal voor publiceren.</span><span class="sxs-lookup"><span data-stu-id="08516-328">This is the URI that should be entered in the **Images** tab in the Publishing Portal.</span></span>

<span data-ttu-id="08516-329">De shared access signature die URI gemaakt moet voldoen aan de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="08516-329">The shared access signature URI created should adhere to the following requirements:</span></span>

* <span data-ttu-id="08516-330">Bij het genereren van shared access signature voor URI's voor uw virtuele harde schijven, zijn machtigingen lijst en lezen voldoende.</span><span class="sxs-lookup"><span data-stu-id="08516-330">When generating shared access signature URIs for your VHDs, List and Read­ permissions are sufficient.</span></span> <span data-ttu-id="08516-331">Verleen geen toegang voor schrijven ('Write') of verwijderen ('Delete').</span><span class="sxs-lookup"><span data-stu-id="08516-331">Do not provide Write or Delete access.</span></span>
* <span data-ttu-id="08516-332">De duur voor toegang moet minimaal drie (3) de weken van wanneer de shared access signature URI wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08516-332">The duration for access should be a minimum of three (3) weeks from when the shared access signature URI is created.</span></span>
* <span data-ttu-id="08516-333">Selecteer om te waarborgen voor UTC-tijd, de dag vóór de huidige datum.</span><span class="sxs-lookup"><span data-stu-id="08516-333">To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="08516-334">Als de huidige datum 6 oktober 2014 valt, selecteert u bijvoorbeeld 5-10-2014.</span><span class="sxs-lookup"><span data-stu-id="08516-334">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

<span data-ttu-id="08516-335">SAS-URL kan worden gegenereerd op meerdere manieren voor het delen van uw VHD voor Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="08516-335">SAS URL can be generated in multiple ways to share your VHD for Azure Marketplace.</span></span>
<span data-ttu-id="08516-336">Hieronder volgen de 3 aanbevolen hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="08516-336">Following are the 3 recommended tools:</span></span>

1.  <span data-ttu-id="08516-337">Azure Opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="08516-337">Azure Storage Explorer</span></span>
2.  <span data-ttu-id="08516-338">Microsoft Opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="08516-338">Microsoft Storage Explorer</span></span>
3.  <span data-ttu-id="08516-339">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="08516-339">Azure CLI</span></span>

<span data-ttu-id="08516-340">**Azure Opslagverkenner (aanbevolen voor Windows-gebruikers)**</span><span class="sxs-lookup"><span data-stu-id="08516-340">**Azure Storage Explorer (Recommended for Windows Users)**</span></span>

<span data-ttu-id="08516-341">Hierna volgen de stappen voor het genereren van SAS-URL met behulp van Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="08516-341">Following are the steps for generating SAS URL by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="08516-342">Download [Azure Storage Explorer 6 Preview 3](https://azurestorageexplorer.codeplex.com/) van CodePlex.</span><span class="sxs-lookup"><span data-stu-id="08516-342">Download [Azure Storage Explorer 6 Preview 3](https://azurestorageexplorer.codeplex.com/) from CodePlex.</span></span> <span data-ttu-id="08516-343">Ga naar [Azure Storage Explorer 6 Preview](https://azurestorageexplorer.codeplex.com/) en klik op **'Downloads'**.</span><span class="sxs-lookup"><span data-stu-id="08516-343">Go to [Azure Storage Explorer 6 Preview](https://azurestorageexplorer.codeplex.com/) and click **"Downloads"**.</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. <span data-ttu-id="08516-345">Download [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) en na deze ritsen installeren.</span><span class="sxs-lookup"><span data-stu-id="08516-345">Download [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) and install after unzipping it.</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. <span data-ttu-id="08516-347">Nadat deze is geïnstalleerd, opent u de toepassing.</span><span class="sxs-lookup"><span data-stu-id="08516-347">After it is installed, open the application.</span></span>
4. <span data-ttu-id="08516-348">Klik op **Account toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="08516-348">Click **Add Account**.</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. <span data-ttu-id="08516-350">Geef de naam van het opslagaccount, opslagaccountsleutel en opslag eindpunten domein.</span><span class="sxs-lookup"><span data-stu-id="08516-350">Specify the storage account name, storage account key, and storage endpoints domain.</span></span> <span data-ttu-id="08516-351">Dit is het opslagaccount in uw Azure-abonnement waar u uw VHD hebt opgeslagen in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="08516-351">This is the storage account in your Azure subscription where you have kept your VHD on Azure portal.</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. <span data-ttu-id="08516-353">Wanneer Azure Opslagverkenner is verbonden met uw specifieke storage-account, start het alle de binnen het opslagaccount bevat.</span><span class="sxs-lookup"><span data-stu-id="08516-353">Once Azure Storage Explorer is connected to your specific storage account, it will start showing all of the contains within the storage account.</span></span> <span data-ttu-id="08516-354">Selecteer de container waarin het besturingssysteem schijf VHD-bestand (ook gegevensschijven als ze van toepassing zijn voor uw scenario).</span><span class="sxs-lookup"><span data-stu-id="08516-354">Select the container where you copied the operating system disk VHD file (also data disks if they are applicable for your scenario).</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. <span data-ttu-id="08516-356">Na het selecteren van de blob-container, Azure Storage Explorer begint met de bestanden in de container.</span><span class="sxs-lookup"><span data-stu-id="08516-356">After selecting the blob container, Azure Storage Explorer starts showing the files within the container.</span></span> <span data-ttu-id="08516-357">Selecteer het installatiekopiebestand (VHD) die moeten worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="08516-357">Select the image file (.vhd) that needs to be submitted.</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  <span data-ttu-id="08516-359">Selecteer het VHD-bestand in de container en klik op de **beveiliging** tabblad.</span><span class="sxs-lookup"><span data-stu-id="08516-359">After selecting the .vhd file in the container, click the **Security** tab.</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  <span data-ttu-id="08516-361">In de **Blob-Container beveiliging** dialoogvenster vak, laat u de standaardinstellingen op de **toegangsniveau** tabblad en klik vervolgens op **Shared Access Signatures** tabblad.</span><span class="sxs-lookup"><span data-stu-id="08516-361">In the **Blob Container Security** dialog box, leave the defaults on the **Access Level** tab, and then click **Shared Access Signatures** tab.</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. <span data-ttu-id="08516-363">Volg onderstaande stappen voor het genereren van een shared access signature URI voor de VHD-installatiekopie:</span><span class="sxs-lookup"><span data-stu-id="08516-363">Follow the steps below to generate a shared access signature URI for the .vhd image:</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    <span data-ttu-id="08516-365">a.</span><span class="sxs-lookup"><span data-stu-id="08516-365">a.</span></span> <span data-ttu-id="08516-366">**Toegang van toegestaan:** om te waarborgen voor UTC-tijd, selecteer de dag vóór de huidige datum.</span><span class="sxs-lookup"><span data-stu-id="08516-366">**Access permitted from:** To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="08516-367">Als de huidige datum 6 oktober 2014 valt, selecteert u bijvoorbeeld 5-10-2014.</span><span class="sxs-lookup"><span data-stu-id="08516-367">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="08516-368">b.</span><span class="sxs-lookup"><span data-stu-id="08516-368">b.</span></span> <span data-ttu-id="08516-369">**Toegang is toegestaan voor:** selecteert u een datum die ten minste drie weken na de **toegang toegestaan van** datum.</span><span class="sxs-lookup"><span data-stu-id="08516-369">**Access permitted to:** Select a date that is at least 3 weeks after the **Access permitted from** date.</span></span>

    <span data-ttu-id="08516-370">c.</span><span class="sxs-lookup"><span data-stu-id="08516-370">c.</span></span> <span data-ttu-id="08516-371">**Acties die zijn toegestaan:** selecteert u de **lijst** en **lezen** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="08516-371">**Actions permitted:** Select the **List** and **Read** permissions.</span></span>

    <span data-ttu-id="08516-372">d.</span><span class="sxs-lookup"><span data-stu-id="08516-372">d.</span></span> <span data-ttu-id="08516-373">Als u uw VHD-bestand juist hebt geselecteerd, wordt het bestand wordt weergegeven in **Blob-naam voor toegang tot** met extensie VHD.</span><span class="sxs-lookup"><span data-stu-id="08516-373">If you have selected your .vhd file correctly, then your file appears in **Blob name to access** with extension .vhd.</span></span>

    <span data-ttu-id="08516-374">e.</span><span class="sxs-lookup"><span data-stu-id="08516-374">e.</span></span> <span data-ttu-id="08516-375">Klik op **Signature genereren**.</span><span class="sxs-lookup"><span data-stu-id="08516-375">Click **Generate Signature**.</span></span>

    <span data-ttu-id="08516-376">f.</span><span class="sxs-lookup"><span data-stu-id="08516-376">f.</span></span> <span data-ttu-id="08516-377">In **gegenereerd Shared Access Signature URI van deze container**, controleren op de volgende stappen uit als gemarkeerde bovenstaande:</span><span class="sxs-lookup"><span data-stu-id="08516-377">In **Generated Shared Access Signature URI of this container**, check for the following as highlighted above:</span></span>

       - <span data-ttu-id="08516-378">Zorg ervoor dat uw installatiekopie bestandsnaam en **".vhd"** zijn in de URI.</span><span class="sxs-lookup"><span data-stu-id="08516-378">Make sure that your image file name and **".vhd"** are in the URI.</span></span>
       - <span data-ttu-id="08516-379">Controleer aan het einde van de handtekening **"rl ="** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="08516-379">At the end of the signature, make sure that **"=rl"** appears.</span></span> <span data-ttu-id="08516-380">Dit toont aan dat toegang voor lezen en de lijst met succes is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="08516-380">This demonstrates that Read and List access was provided successfully.</span></span>
       - <span data-ttu-id="08516-381">Controleer in het midden van de handtekening, **' sr c = "** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="08516-381">In middle of the signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="08516-382">Dit toont aan dat er toegangsniveau van de container</span><span class="sxs-lookup"><span data-stu-id="08516-382">This demonstrates that you have container level access</span></span>

11. <span data-ttu-id="08516-383">Om ervoor te zorgen dat de gegenereerde gedeeld toegang handtekening URI werkt, klikt u op **testen in de Browser**.</span><span class="sxs-lookup"><span data-stu-id="08516-383">To ensure that the generated shared access signature URI works, click **Test in Browser**.</span></span> <span data-ttu-id="08516-384">Deze moet eerst het downloadproces.</span><span class="sxs-lookup"><span data-stu-id="08516-384">It should start the download process.</span></span>

12. <span data-ttu-id="08516-385">Kopieer de shared access signature URI.</span><span class="sxs-lookup"><span data-stu-id="08516-385">Copy the shared access signature URI.</span></span> <span data-ttu-id="08516-386">Dit is de URI die u in de Portal voor Publiceren moet plakken.</span><span class="sxs-lookup"><span data-stu-id="08516-386">This is the URI to paste into the Publishing Portal.</span></span>

13. <span data-ttu-id="08516-387">Herhaal stap 6-10 voor elke VHD in de SKU.</span><span class="sxs-lookup"><span data-stu-id="08516-387">Repeat steps 6-10 for each VHD in the SKU.</span></span>

<span data-ttu-id="08516-388">**Microsoft Azure Opslagverkenner (Windows of MAC/Linux)**</span><span class="sxs-lookup"><span data-stu-id="08516-388">**Microsoft Azure Storage Explorer (Windows/MAC/Linux)**</span></span>

<span data-ttu-id="08516-389">Hierna volgen de stappen voor het genereren van SAS-URL met behulp van Microsoft Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="08516-389">Following are the steps for generating SAS URL by using Microsoft Azure Storage Explorer</span></span>

1.  <span data-ttu-id="08516-390">Downloaden van Microsoft Azure Storage Explorer formulier [http://storageexplorer.com/](http://storageexplorer.com/) website.</span><span class="sxs-lookup"><span data-stu-id="08516-390">Download Microsoft Azure Storage Explorer form [http://storageexplorer.com/](http://storageexplorer.com/) website.</span></span> <span data-ttu-id="08516-391">Ga naar [Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) en klik op **'Downloaden voor Windows'**.</span><span class="sxs-lookup"><span data-stu-id="08516-391">Go to [Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) and click **“Download for Windows”**.</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  <span data-ttu-id="08516-393">Nadat deze is geïnstalleerd, opent u de toepassing.</span><span class="sxs-lookup"><span data-stu-id="08516-393">After it is installed, open the application.</span></span>

3.  <span data-ttu-id="08516-394">Klik op **Account toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="08516-394">Click **Add Account**.</span></span>

4.  <span data-ttu-id="08516-395">Microsoft Azure Storage Explorer configureren voor uw abonnement met aanmelden bij uw account</span><span class="sxs-lookup"><span data-stu-id="08516-395">Configure Microsoft Azure Storage Explorer to your subscription by sign in to your account</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  <span data-ttu-id="08516-397">Ga naar de storage-account en selecteer de Container</span><span class="sxs-lookup"><span data-stu-id="08516-397">Go to storage account and select the Container</span></span>

6.  <span data-ttu-id="08516-398">Selecteer **'Share Access Signature ophalen'...**</span><span class="sxs-lookup"><span data-stu-id="08516-398">Select **“Get Share Access Signature..”**</span></span> <span data-ttu-id="08516-399">met behulp van de rechtermuisknop te klikken op van de **container**</span><span class="sxs-lookup"><span data-stu-id="08516-399">by using Right Click of the **container**</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  <span data-ttu-id="08516-401">Begintijd van de update, verlooptijd en machtigingen volgens de volgende</span><span class="sxs-lookup"><span data-stu-id="08516-401">Update Start time, Expiry time and Permissions as per following</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    <span data-ttu-id="08516-403">a.</span><span class="sxs-lookup"><span data-stu-id="08516-403">a.</span></span>  <span data-ttu-id="08516-404">**Begintijd:** om te waarborgen voor UTC-tijd, selecteer de dag vóór de huidige datum.</span><span class="sxs-lookup"><span data-stu-id="08516-404">**Start Time:** To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="08516-405">Als de huidige datum 6 oktober 2014 valt, selecteert u bijvoorbeeld 5-10-2014.</span><span class="sxs-lookup"><span data-stu-id="08516-405">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="08516-406">b.</span><span class="sxs-lookup"><span data-stu-id="08516-406">b.</span></span>  <span data-ttu-id="08516-407">**Verlooptijd:** selecteert u een datum die ten minste drie weken na de **begintijd** datum.</span><span class="sxs-lookup"><span data-stu-id="08516-407">**Expiry Time:** Select a date that is at least 3 weeks after the **Start Time** date.</span></span>

    <span data-ttu-id="08516-408">c.</span><span class="sxs-lookup"><span data-stu-id="08516-408">c.</span></span>  <span data-ttu-id="08516-409">**Machtigingen:** selecteert u de **lijst** en **lezen** machtigingen</span><span class="sxs-lookup"><span data-stu-id="08516-409">**Permissions:** Select the **List** and **Read** permissions</span></span>

8.  <span data-ttu-id="08516-410">Shared access signature voor containers URI kopiëren</span><span class="sxs-lookup"><span data-stu-id="08516-410">Copy Container shared access signature URI</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    <span data-ttu-id="08516-412">Gegenereerde SAS-URL is voor container niveau en nu moeten de naam van de VHD toevoegen in het.</span><span class="sxs-lookup"><span data-stu-id="08516-412">Generated SAS URL is for container Level and now we need to add VHD name in it.</span></span>

    <span data-ttu-id="08516-413">Indeling van de Container niveau SAS-URL:`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="08516-413">Format of Container Level SAS URL: `https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="08516-414">De naam van de VHD invoegen na de containernaam van de in SAS-URL zoals hieronder`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="08516-414">Insert VHD name after the container name in SAS URL as below `https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="08516-415">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="08516-415">Example:</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    <span data-ttu-id="08516-417">TestRGVM201631920152.vhd is de naam van de VHD en vervolgens de URL van de VHD-SAS`https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="08516-417">TestRGVM201631920152.vhd is the VHD Name then VHD SAS URL will be `https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    - <span data-ttu-id="08516-418">Zorg ervoor dat uw installatiekopie bestandsnaam en **".vhd"** zijn in de URI.</span><span class="sxs-lookup"><span data-stu-id="08516-418">Make sure that your image file name and **".vhd"** are in the URI.</span></span>
    - <span data-ttu-id="08516-419">Controleer in het midden van de handtekening, **"sp rl ="** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="08516-419">In middle of the signature, make sure that **"sp=rl"** appears.</span></span> <span data-ttu-id="08516-420">Dit toont aan dat toegang voor lezen en de lijst met succes is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="08516-420">This demonstrates that Read and List access was provided successfully.</span></span>
    - <span data-ttu-id="08516-421">Controleer in het midden van de handtekening, **' sr c = "** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="08516-421">In middle of the signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="08516-422">Dit toont aan dat er toegangsniveau van de container</span><span class="sxs-lookup"><span data-stu-id="08516-422">This demonstrates that you have container level access</span></span>

9.  <span data-ttu-id="08516-423">Om ervoor te zorgen dat de gegenereerde gedeeld toegang handtekening URI werkt, test u deze in de browser.</span><span class="sxs-lookup"><span data-stu-id="08516-423">To ensure that the generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="08516-424">Het downloadproces moet worden gestart</span><span class="sxs-lookup"><span data-stu-id="08516-424">It should start the download process</span></span>

10. <span data-ttu-id="08516-425">Kopieer de shared access signature URI.</span><span class="sxs-lookup"><span data-stu-id="08516-425">Copy the shared access signature URI.</span></span> <span data-ttu-id="08516-426">Dit is de URI die u in de Portal voor Publiceren moet plakken.</span><span class="sxs-lookup"><span data-stu-id="08516-426">This is the URI to paste into the Publishing Portal.</span></span>

11. <span data-ttu-id="08516-427">Herhaal deze stappen voor elke VHD in de SKU.</span><span class="sxs-lookup"><span data-stu-id="08516-427">Repeat these steps for each VHD in the SKU.</span></span>

<span data-ttu-id="08516-428">**Azure CLI (aanbevolen voor niet-Windows & continue integratie)**</span><span class="sxs-lookup"><span data-stu-id="08516-428">**Azure CLI (Recommended for Non-Windows & Continuous Integration)**</span></span>

<span data-ttu-id="08516-429">Hierna volgen de stappen voor het genereren van SAS-URL met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="08516-429">Following are the steps for generating SAS URL by using Azure CLI</span></span>

1.  <span data-ttu-id="08516-430">Downloaden van Microsoft Azure CLI van [hier](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/).</span><span class="sxs-lookup"><span data-stu-id="08516-430">Download Microsoft Azure CLI from [here](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/).</span></span> <span data-ttu-id="08516-431">Ook vindt u koppelingen naar de andere  **[Windows](http://aka.ms/webpi-azure-cli)**  en  **[MAC OS](http://aka.ms/mac-azure-cli)**.</span><span class="sxs-lookup"><span data-stu-id="08516-431">You can also find different links for **[Windows](http://aka.ms/webpi-azure-cli)** and **[MAC OS](http://aka.ms/mac-azure-cli)**.</span></span>

2.  <span data-ttu-id="08516-432">Zodra deze is gedownload, installeer</span><span class="sxs-lookup"><span data-stu-id="08516-432">Once it is downloaded, please install</span></span>

3.  <span data-ttu-id="08516-433">Een PowerShell-bestand met de volgende code maken en opslaan in de lokale</span><span class="sxs-lookup"><span data-stu-id="08516-433">Create a PowerShell file with following code and save it in local</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    <span data-ttu-id="08516-434">Bijwerken van de volgende parameters in hierboven</span><span class="sxs-lookup"><span data-stu-id="08516-434">Update the following parameters in above</span></span>

    <span data-ttu-id="08516-435">a.</span><span class="sxs-lookup"><span data-stu-id="08516-435">a.</span></span> <span data-ttu-id="08516-436">**`<StorageAccountName>`**: Geef de naam van uw opslagaccount</span><span class="sxs-lookup"><span data-stu-id="08516-436">**`<StorageAccountName>`**: Give your storage account name</span></span>

    <span data-ttu-id="08516-437">b.</span><span class="sxs-lookup"><span data-stu-id="08516-437">b.</span></span> <span data-ttu-id="08516-438">**`<Storage Account Key>`**: Geef de sleutel van uw opslagaccount</span><span class="sxs-lookup"><span data-stu-id="08516-438">**`<Storage Account Key>`**: Give your storage account key</span></span>

    <span data-ttu-id="08516-439">c.</span><span class="sxs-lookup"><span data-stu-id="08516-439">c.</span></span> <span data-ttu-id="08516-440">**`<Permission Start Date>`**: Selecteer om te waarborgen voor UTC-tijd, de dag vóór de huidige datum.</span><span class="sxs-lookup"><span data-stu-id="08516-440">**`<Permission Start Date>`**: To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="08516-441">Bijvoorbeeld, als de huidige datum 26 oktober 2016 is waarde dan 25-10-2016</span><span class="sxs-lookup"><span data-stu-id="08516-441">For example, if the current date is October 26, 2016, then value should be 10/25/2016</span></span>

    <span data-ttu-id="08516-442">d.</span><span class="sxs-lookup"><span data-stu-id="08516-442">d.</span></span> <span data-ttu-id="08516-443">**`<Permission End Date>`**: Selecteer een datum die ten minste drie weken na de **begindatum**.</span><span class="sxs-lookup"><span data-stu-id="08516-443">**`<Permission End Date>`**: Select a date that is at least 3 weeks after the **Start Date**.</span></span> <span data-ttu-id="08516-444">Waarde moet **02-11-2016**.</span><span class="sxs-lookup"><span data-stu-id="08516-444">Then value should be **11/02/2016**.</span></span>

    <span data-ttu-id="08516-445">Hieronder vindt u in de voorbeeldcode na het bijwerken van de juiste parameters</span><span class="sxs-lookup"><span data-stu-id="08516-445">Following is the example code after updating proper parameters</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  <span data-ttu-id="08516-446">Powershell-editor te openen met 'Als Administrator uitvoeren'-modus en open bestand in stap #3.</span><span class="sxs-lookup"><span data-stu-id="08516-446">Open Powershell editor with “Run as Administrator” mode and open file in step #3.</span></span>

5.  <span data-ttu-id="08516-447">Voer het script, vindt u de SAS-URL voor het toegangsniveau van de container</span><span class="sxs-lookup"><span data-stu-id="08516-447">Run the script and it will provide you the SAS URL for container level access</span></span>

    <span data-ttu-id="08516-448">Hieronder wordt de uitvoer van de SAS-handtekening en kopieer het gemarkeerde onderdeel in een Kladblok</span><span class="sxs-lookup"><span data-stu-id="08516-448">Following will be the output of the SAS Signature and copy the highlighted part in a notepad</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  <span data-ttu-id="08516-450">Nu u krijgt container niveau SAS-URL en moet u de naam van de VHD toevoegen in het.</span><span class="sxs-lookup"><span data-stu-id="08516-450">Now you will get container level SAS URL and you need to add VHD name in it.</span></span>

    <span data-ttu-id="08516-451">Container niveau SAS-URL #</span><span class="sxs-lookup"><span data-stu-id="08516-451">Container level SAS URL #</span></span>

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  <span data-ttu-id="08516-452">De naam van de VHD invoegen na de containernaam van de in SAS-URL, zoals hieronder wordt weergegeven`https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span><span class="sxs-lookup"><span data-stu-id="08516-452">Insert VHD name after the container name in SAS URL as shown below `https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span></span>

    <span data-ttu-id="08516-453">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="08516-453">Example:</span></span>

    <span data-ttu-id="08516-454">TestRGVM201631920152.vhd is de naam van de VHD en vervolgens de URL van de VHD-SAS</span><span class="sxs-lookup"><span data-stu-id="08516-454">TestRGVM201631920152.vhd is the VHD Name then VHD SAS URL will be</span></span>

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - <span data-ttu-id="08516-455">Zorg ervoor dat uw afbeeldingsbestandsnaam en ".vhd" in de URI.</span><span class="sxs-lookup"><span data-stu-id="08516-455">Make sure that your image file name and ".vhd" are in the URI.</span></span>
    -   <span data-ttu-id="08516-456">Controleer in het midden van de handtekening 'sp rl =' wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="08516-456">In middle of the signature, make sure that "sp=rl" appears.</span></span> <span data-ttu-id="08516-457">Dit toont aan dat toegang voor lezen en de lijst met succes is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="08516-457">This demonstrates that Read and List access was provided successfully.</span></span>
    -   <span data-ttu-id="08516-458">Controleer in het midden van de handtekening ' sr = c ' wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="08516-458">In middle of the signature, make sure that "sr=c" appears.</span></span> <span data-ttu-id="08516-459">Dit toont aan dat er toegangsniveau van de container</span><span class="sxs-lookup"><span data-stu-id="08516-459">This demonstrates that you have container level access</span></span>

8.  <span data-ttu-id="08516-460">Om ervoor te zorgen dat de gegenereerde gedeeld toegang handtekening URI werkt, test u deze in de browser.</span><span class="sxs-lookup"><span data-stu-id="08516-460">To ensure that the generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="08516-461">Het downloadproces moet worden gestart</span><span class="sxs-lookup"><span data-stu-id="08516-461">It should start the download process</span></span>

9.  <span data-ttu-id="08516-462">Kopieer de shared access signature URI.</span><span class="sxs-lookup"><span data-stu-id="08516-462">Copy the shared access signature URI.</span></span> <span data-ttu-id="08516-463">Dit is de URI die u in de Portal voor Publiceren moet plakken.</span><span class="sxs-lookup"><span data-stu-id="08516-463">This is the URI to paste into the Publishing Portal.</span></span>

10. <span data-ttu-id="08516-464">Herhaal deze stappen voor elke VHD in de SKU.</span><span class="sxs-lookup"><span data-stu-id="08516-464">Repeat these steps for each VHD in the SKU.</span></span>


### <a name="53-provide-information-about-the-vm-image-and-request-certification-in-the-publishing-portal"></a><span data-ttu-id="08516-465">5.3 bieden informatie over de VM-installatiekopie en aanvragen van de certificeringsinstantie in de Portal publiceren</span><span class="sxs-lookup"><span data-stu-id="08516-465">5.3 Provide information about the VM image and request certification in the Publishing Portal</span></span>
<span data-ttu-id="08516-466">Nadat u uw aanbieding en SKU hebt gemaakt, moet u de details van de afbeelding die is gekoppeld aan deze SKU invoeren:</span><span class="sxs-lookup"><span data-stu-id="08516-466">After you have created your offer and SKU, you should enter the image details associated with that SKU:</span></span>

1. <span data-ttu-id="08516-467">Ga naar de [Publishing Portal][link-pubportal], en meld u aan met uw verkopersaccount.</span><span class="sxs-lookup"><span data-stu-id="08516-467">Go to the [Publishing Portal][link-pubportal], and then sign in with your seller account.</span></span>
2. <span data-ttu-id="08516-468">Selecteer de **VM-installatiekopieën** tabblad.</span><span class="sxs-lookup"><span data-stu-id="08516-468">Select the **VM images** tab.</span></span>
3. <span data-ttu-id="08516-469">De id die wordt vermeld op de bovenkant van de pagina is feitelijk de id van de aanbieding en niet de SKU-id.</span><span class="sxs-lookup"><span data-stu-id="08516-469">The identifier listed at the top of the page is actually the offer identifier and not the SKU identifier.</span></span>
4. <span data-ttu-id="08516-470">Vul de eigenschappen onder de **SKU's** sectie.</span><span class="sxs-lookup"><span data-stu-id="08516-470">Fill out the properties under the **SKUs** section.</span></span>
5. <span data-ttu-id="08516-471">Onder **besturingssysteemgroep**, klikt u op het type van het besturingssysteem die is gekoppeld aan de besturingssysteem-VHD.</span><span class="sxs-lookup"><span data-stu-id="08516-471">Under **Operating system family**, click the operating system type associated with the operating system VHD.</span></span>
6. <span data-ttu-id="08516-472">In de **besturingssysteem** vak, beschrijven van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="08516-472">In the **Operating system** box, describe the operating system.</span></span> <span data-ttu-id="08516-473">U kunt een notatie zoals-besturingssystemen, type, versie en updates.</span><span class="sxs-lookup"><span data-stu-id="08516-473">Consider a format such as operating system family, type, version, and updates.</span></span> <span data-ttu-id="08516-474">Een voorbeeld is 'Windows Server Datacenter 2014 R2'.</span><span class="sxs-lookup"><span data-stu-id="08516-474">An example is "Windows Server Datacenter 2014 R2."</span></span>
7. <span data-ttu-id="08516-475">Selecteer de grootte van maximaal zes aanbevolen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="08516-475">Select up to six recommended virtual machine sizes.</span></span> <span data-ttu-id="08516-476">Dit zijn de aanbevelingen die aan de klant in de blade prijzen laag in de Azure Portal worden weergegeven wanneer u ze wilt aanschaffen en implementeren van uw installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="08516-476">These are recommendations that get displayed to the customer in the Pricing tier blade in the Azure Portal when they decide to purchase and deploy your image.</span></span> <span data-ttu-id="08516-477">**Dit zijn alleen aanbevelingen. De klant is kunt selecteren van elke VM-grootte die geschikt is voor de schijven die zijn opgegeven in uw installatiekopie.**</span><span class="sxs-lookup"><span data-stu-id="08516-477">**These are only recommendations. The customer is able to select any VM size that accommodates the disks specified in your image.**</span></span>
8. <span data-ttu-id="08516-478">De versie in te voeren.</span><span class="sxs-lookup"><span data-stu-id="08516-478">Enter the version.</span></span> <span data-ttu-id="08516-479">Het versieveld ingekapseld een semantische versie om het product en de updates te identificeren:</span><span class="sxs-lookup"><span data-stu-id="08516-479">The version field encapsulates a semantic version to identify the product and its updates:</span></span>
   * <span data-ttu-id="08516-480">Versies moet van het formulier X.Y.Z, waarbij X, Y en Z gehele getallen zijn.</span><span class="sxs-lookup"><span data-stu-id="08516-480">Versions should be of the form X.Y.Z, where X, Y, and Z are integers.</span></span>
   * <span data-ttu-id="08516-481">Afbeeldingen in verschillende SKU's kunnen verschillende primaire en secundaire versies hebben.</span><span class="sxs-lookup"><span data-stu-id="08516-481">Images in different SKUs can have different major and minor versions.</span></span>
   * <span data-ttu-id="08516-482">Versies binnen een SKU moet alleen incrementele wijzigingen, die de patch-versie (Z van X.Y.Z) te verhogen.</span><span class="sxs-lookup"><span data-stu-id="08516-482">Versions within a SKU should only be incremental changes, which increase the patch version (Z from X.Y.Z).</span></span>
9. <span data-ttu-id="08516-483">In de **OS VHD URL** Voer de shared access signature URI voor de besturingssysteem-VHD gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08516-483">In the **OS VHD URL** box, enter the shared access signature URI created for the operating system VHD.</span></span>
10. <span data-ttu-id="08516-484">Als er gegevensschijven gekoppeld aan deze SKU, selecteert u de logische eenheid number (LUN) waarnaar u deze gegevensschijf dat wilt aan bij de implementatie worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="08516-484">If there are data disks associated with this SKU, select the logical unit number (LUN) to which you would like this data disk to be mounted upon deployment.</span></span>
11. <span data-ttu-id="08516-485">In de **LUN X VHD URL** Voer de shared access signature URI voor de eerste gegevens VHD gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08516-485">In the **LUN X VHD URL** box, enter the shared access signature URI created for the first data VHD.</span></span>

    ![tekenen](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a><span data-ttu-id="08516-487">Algemene SAS-URL problemen en oplossingen</span><span class="sxs-lookup"><span data-stu-id="08516-487">Common SAS URL issues & fixes</span></span>

|<span data-ttu-id="08516-488">Probleem</span><span class="sxs-lookup"><span data-stu-id="08516-488">Issue</span></span>|<span data-ttu-id="08516-489">Foutbericht</span><span class="sxs-lookup"><span data-stu-id="08516-489">Failure Message</span></span>|<span data-ttu-id="08516-490">Oplossen</span><span class="sxs-lookup"><span data-stu-id="08516-490">Fix</span></span>|<span data-ttu-id="08516-491">Koppeling van documentatie</span><span class="sxs-lookup"><span data-stu-id="08516-491">Documentation Link</span></span>|
|---|---|---|---|
|<span data-ttu-id="08516-492">Fout bij het kopiëren van afbeeldingen - '? ' is niet gevonden in het SAS-url</span><span class="sxs-lookup"><span data-stu-id="08516-492">Failure in copying images - "?" is not found in SAS url</span></span>|<span data-ttu-id="08516-493">Fout: Afbeeldingen kopiëren.</span><span class="sxs-lookup"><span data-stu-id="08516-493">Failure: Copying Images.</span></span> <span data-ttu-id="08516-494">Kan geen downloaden blob met behulp van SAS-Uri.</span><span class="sxs-lookup"><span data-stu-id="08516-494">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="08516-495">Update de SAS-Url met behulp van aanbevolen hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="08516-495">Update the SAS Url using recommended tools</span></span>|[<span data-ttu-id="08516-496">https://Azure.Microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/</span><span class="sxs-lookup"><span data-stu-id="08516-496">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="08516-497">Fout bij het kopiëren van afbeeldingen - parameters voor 'st' en 'se' niet in het SAS-url</span><span class="sxs-lookup"><span data-stu-id="08516-497">Failure in copying images - “st” and “se” parameters not in SAS url</span></span>|<span data-ttu-id="08516-498">Fout: Afbeeldingen kopiëren.</span><span class="sxs-lookup"><span data-stu-id="08516-498">Failure: Copying Images.</span></span> <span data-ttu-id="08516-499">Kan geen downloaden blob met behulp van SAS-Uri.</span><span class="sxs-lookup"><span data-stu-id="08516-499">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="08516-500">De SAS-Url met de begin- en einddatums erop bijwerken</span><span class="sxs-lookup"><span data-stu-id="08516-500">Update the SAS Url with Start and End dates on it</span></span>|[<span data-ttu-id="08516-501">https://Azure.Microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/</span><span class="sxs-lookup"><span data-stu-id="08516-501">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="08516-502">Fout bij het kopiëren van afbeeldingen - 'sp = rl' niet in het SAS-url</span><span class="sxs-lookup"><span data-stu-id="08516-502">Failure in copying images - “sp=rl” not in SAS url</span></span>|<span data-ttu-id="08516-503">Fout: Afbeeldingen kopiëren.</span><span class="sxs-lookup"><span data-stu-id="08516-503">Failure: Copying Images.</span></span> <span data-ttu-id="08516-504">Kan niet worden gedownload van de blob met behulp van SAS-Uri</span><span class="sxs-lookup"><span data-stu-id="08516-504">Not able to download blob using provided SAS Uri</span></span>|<span data-ttu-id="08516-505">Bijwerken van de SAS-Url met machtigingen zijn ingesteld als 'Lezen' en 'lijst</span><span class="sxs-lookup"><span data-stu-id="08516-505">Update the SAS Url with permissions set as “Read” & “List</span></span>|[<span data-ttu-id="08516-506">https://Azure.Microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/</span><span class="sxs-lookup"><span data-stu-id="08516-506">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="08516-507">Fout bij het kopiëren van afbeeldingen - SAS-url spaties hebben in de naam van de vhd</span><span class="sxs-lookup"><span data-stu-id="08516-507">Failure in copying images - SAS url have white spaces in vhd name</span></span>|<span data-ttu-id="08516-508">Fout: Afbeeldingen kopiëren.</span><span class="sxs-lookup"><span data-stu-id="08516-508">Failure: Copying Images.</span></span> <span data-ttu-id="08516-509">Kan geen downloaden blob met behulp van SAS-Uri.</span><span class="sxs-lookup"><span data-stu-id="08516-509">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="08516-510">De SAS-Url zonder spaties bijwerken</span><span class="sxs-lookup"><span data-stu-id="08516-510">Update the SAS Url without white spaces</span></span>|[<span data-ttu-id="08516-511">https://Azure.Microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/</span><span class="sxs-lookup"><span data-stu-id="08516-511">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="08516-512">Fout bij het kopiëren van afbeeldingen – SAS-Url-autorisatie-fout</span><span class="sxs-lookup"><span data-stu-id="08516-512">Failure in copying images – SAS Url Authorization error</span></span>|<span data-ttu-id="08516-513">Fout: Afbeeldingen kopiëren.</span><span class="sxs-lookup"><span data-stu-id="08516-513">Failure: Copying Images.</span></span> <span data-ttu-id="08516-514">Er kan geen blob vanwege Autorisatiefout downloaden</span><span class="sxs-lookup"><span data-stu-id="08516-514">Not able to download blob due to authorization error</span></span>|<span data-ttu-id="08516-515">Opnieuw genereren van SAS-Url</span><span class="sxs-lookup"><span data-stu-id="08516-515">Regenerate the SAS Url</span></span>|[<span data-ttu-id="08516-516">https://Azure.Microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/</span><span class="sxs-lookup"><span data-stu-id="08516-516">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a><span data-ttu-id="08516-517">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="08516-517">Next step</span></span>
<span data-ttu-id="08516-518">Nadat u klaar bent met de SKU-details, kunt u verder gaan naar de [Azure Marketplace marketing inhoud handleiding][link-pushstaging].</span><span class="sxs-lookup"><span data-stu-id="08516-518">After you are done with the SKU details, you can move forward to the [Azure Marketplace marketing content guide][link-pushstaging].</span></span> <span data-ttu-id="08516-519">In deze stap van het publicatieproces, bieden u de marketing inhoud, prijzen en andere informatie die nodig zijn vóór **stap 3: uw virtuele machine testen bieden in fasering**, waarin u verschillende scenario's voor use case testen voordat u de aanbieding voor Azure Marketplace voor openbare zichtbaarheid en inkoop implementeert.</span><span class="sxs-lookup"><span data-stu-id="08516-519">In that step of the publishing process, you provide the marketing content, pricing, and other information necessary prior to **Step 3: Testing your VM offer in staging**, where you test various use-case scenarios before deploying the offer to the Azure Marketplace for public visibility and purchase.</span></span>  

## <a name="see-also"></a><span data-ttu-id="08516-520">Zie ook</span><span class="sxs-lookup"><span data-stu-id="08516-520">See also</span></span>
* [<span data-ttu-id="08516-521">Aan de slag: hoe een aanbieding publiceren in Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="08516-521">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-sql-2014-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014enterprisewindowsserver2012r2/
[link-sql-2014-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014standardwindowsserver2012r2/
[link-sql-2014-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014webwindowsserver2012r2/
[link-sql-2012-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2enterprisewindowsserver2012/
[link-sql-2012-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2standardwindowsserver2012/
[link-sql-2012-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2webwindowsserver2012/
[link-datactr-2012-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012r2datacenter/
[link-datactr-2012]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012datacenter/
[link-datactr-2008-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2008r2sp1/
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/
