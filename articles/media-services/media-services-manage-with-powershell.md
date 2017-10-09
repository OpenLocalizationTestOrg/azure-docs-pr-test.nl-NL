---
title: aaaManage Azure Media Services-Accounts met PowerShell
description: Meer informatie over hoe Azure Media Services toomanage van accounts met PowerShell-cmdlets.
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="dd9f5-103">Azure Media Services-Accounts met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="dd9f5-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd9f5-104">Portal</span><span class="sxs-lookup"><span data-stu-id="dd9f5-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="dd9f5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd9f5-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="dd9f5-106">REST</span><span class="sxs-lookup"><span data-stu-id="dd9f5-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="dd9f5-107">toobe kunnen toocreate een Azure Media Services-account, moet u een Azure-account hebben.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-107">toobe able toocreate an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="dd9f5-108">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="dd9f5-109">Zie <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Gratis proefversie van Azure</a> voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="dd9f5-110">Overzicht</span><span class="sxs-lookup"><span data-stu-id="dd9f5-110">Overview</span></span>
<span data-ttu-id="dd9f5-111">In dit artikel bevat hello Azure PowerShell-cmdlets voor Azure Media Services (AMS) in hello Azure Resource Manager-framework.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-111">This article lists hello Azure PowerShell cmdlets for Azure Media Services (AMS) in hello Azure Resource Manager framework.</span></span> <span data-ttu-id="dd9f5-112">Hallo-cmdlets bestaan in Hallo **Microsoft.Azure.Commands.Media** naamruimte.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-112">hello cmdlets exist in hello **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="dd9f5-113">Versies</span><span class="sxs-lookup"><span data-stu-id="dd9f5-113">Versions</span></span>
<span data-ttu-id="dd9f5-114">**ApiVersion**: '2015-10-01'</span><span class="sxs-lookup"><span data-stu-id="dd9f5-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="dd9f5-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="dd9f5-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="dd9f5-116">Hiermee maakt u een mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="dd9f5-117">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="dd9f5-117">Syntax</span></span>
<span data-ttu-id="dd9f5-118">Parameterset: StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="dd9f5-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="dd9f5-119">Parameterset: StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="dd9f5-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="dd9f5-120">Parameters</span><span class="sxs-lookup"><span data-stu-id="dd9f5-120">Parameters</span></span>
<span data-ttu-id="dd9f5-121">**-ResourceGroupName &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-122">Geeft de naam Hallo van Hallo resource groep toowhich die deze mediaservice behoort.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-122">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="dd9f5-123">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-123">Aliases</span></span> | <span data-ttu-id="dd9f5-124">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-125">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-125">Required?</span></span> |<span data-ttu-id="dd9f5-126">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-126">true</span></span> |
| <span data-ttu-id="dd9f5-127">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-127">Position?</span></span> |<span data-ttu-id="dd9f5-128">0</span><span class="sxs-lookup"><span data-stu-id="dd9f5-128">0</span></span> |
| <span data-ttu-id="dd9f5-129">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-129">Default value</span></span> |<span data-ttu-id="dd9f5-130">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-130">none</span></span> |
| <span data-ttu-id="dd9f5-131">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-131">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-132">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-133">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-133">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-134">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-134">false</span></span> |

<span data-ttu-id="dd9f5-135">**-AccountName &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-136">Geeft de naam Hallo van Hallo mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-136">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="dd9f5-137">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-137">Aliases</span></span> | <span data-ttu-id="dd9f5-138">Naam</span><span class="sxs-lookup"><span data-stu-id="dd9f5-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-139">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-139">Required?</span></span> |<span data-ttu-id="dd9f5-140">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-140">true</span></span> |
| <span data-ttu-id="dd9f5-141">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-141">Position?</span></span> |<span data-ttu-id="dd9f5-142">1</span><span class="sxs-lookup"><span data-stu-id="dd9f5-142">1</span></span> |
| <span data-ttu-id="dd9f5-143">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-143">Default value</span></span> |<span data-ttu-id="dd9f5-144">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-144">none</span></span> |
| <span data-ttu-id="dd9f5-145">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-145">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-146">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-146">false</span></span> |
| <span data-ttu-id="dd9f5-147">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-147">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-148">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-148">false</span></span> |

<span data-ttu-id="dd9f5-149">**-Locatie &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-150">Hiermee geeft u Resourcelocatie Hallo van Hallo mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-150">Specifies hello resource location of hello media service.</span></span>

| <span data-ttu-id="dd9f5-151">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-151">Aliases</span></span> | <span data-ttu-id="dd9f5-152">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-153">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-153">Required?</span></span> |<span data-ttu-id="dd9f5-154">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-154">true</span></span> |
| <span data-ttu-id="dd9f5-155">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-155">Position?</span></span> |<span data-ttu-id="dd9f5-156">2</span><span class="sxs-lookup"><span data-stu-id="dd9f5-156">2</span></span> |
| <span data-ttu-id="dd9f5-157">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-157">Default value</span></span> |<span data-ttu-id="dd9f5-158">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-158">none</span></span> |
| <span data-ttu-id="dd9f5-159">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-159">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-160">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-161">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-161">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-162">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-162">false</span></span> |

<span data-ttu-id="dd9f5-163">**-StorageAccountId &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-164">Hiermee geeft u een primaire opslagaccount die zijn gekoppeld aan Hallo mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-164">Specifies a primary storage account that associated with hello media service.</span></span>

* <span data-ttu-id="dd9f5-165">Nieuwe storage-account (gemaakt met de Hallo Resource Manager-API) alleen wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-165">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="dd9f5-166">Hallo storage-account moet aanwezig zijn en heeft dezelfde locatie met mediaservice Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-166">hello storage account must exist and has hello same location with hello media service.</span></span>

| <span data-ttu-id="dd9f5-167">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-167">Aliases</span></span> | <span data-ttu-id="dd9f5-168">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-169">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-169">Required?</span></span> |<span data-ttu-id="dd9f5-170">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-170">true</span></span> |
| <span data-ttu-id="dd9f5-171">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-171">Position?</span></span> |<span data-ttu-id="dd9f5-172">3</span><span class="sxs-lookup"><span data-stu-id="dd9f5-172">3</span></span> |
| <span data-ttu-id="dd9f5-173">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-173">Default value</span></span> |<span data-ttu-id="dd9f5-174">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-174">none</span></span> |
| <span data-ttu-id="dd9f5-175">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-175">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-176">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-177">Naam van de parameter</span><span class="sxs-lookup"><span data-stu-id="dd9f5-177">Parameter set name</span></span> |<span data-ttu-id="dd9f5-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="dd9f5-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="dd9f5-179">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-179">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-180">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-180">false</span></span> |

<span data-ttu-id="dd9f5-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="dd9f5-182">Hiermee geeft u opslagaccounts die zijn gekoppeld aan Hallo mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-182">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="dd9f5-183">Nieuwe storage-account (gemaakt met de Hallo Resource Manager-API) alleen wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-183">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="dd9f5-184">Hallo storage-account moet aanwezig zijn en heeft dezelfde locatie met mediaservice Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-184">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="dd9f5-185">Slechts één opslagaccount kan worden opgegeven als primaire.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="dd9f5-186">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-186">Aliases</span></span> | <span data-ttu-id="dd9f5-187">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-188">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-188">Required?</span></span> |<span data-ttu-id="dd9f5-189">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-189">true</span></span> |
| <span data-ttu-id="dd9f5-190">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-190">Position?</span></span> |<span data-ttu-id="dd9f5-191">3</span><span class="sxs-lookup"><span data-stu-id="dd9f5-191">3</span></span> |
| <span data-ttu-id="dd9f5-192">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-192">Default value</span></span> |<span data-ttu-id="dd9f5-193">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-193">none</span></span> |
| <span data-ttu-id="dd9f5-194">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-194">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-195">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-196">Naam van de parameter</span><span class="sxs-lookup"><span data-stu-id="dd9f5-196">Parameter set name</span></span> |<span data-ttu-id="dd9f5-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="dd9f5-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="dd9f5-198">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-198">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-199">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-199">false</span></span> |

<span data-ttu-id="dd9f5-200">**-Tags &lt;hashtabel&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="dd9f5-201">Hiermee geeft u een hash-tabel van Hallo-labels die gekoppeld aan Hallo mediaservice zijn.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-201">Specifies a hash table of hello tags that are associated with hello media service.</span></span>

* <span data-ttu-id="dd9f5-202">Voorbeeld: @{"tag1 isgelijkteken (=) value1";" tag2 ' =: value2 "}</span><span class="sxs-lookup"><span data-stu-id="dd9f5-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="dd9f5-203">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-203">Aliases</span></span> | <span data-ttu-id="dd9f5-204">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-205">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-205">Required?</span></span> |<span data-ttu-id="dd9f5-206">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-206">false</span></span> |
| <span data-ttu-id="dd9f5-207">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-207">Position?</span></span> |<span data-ttu-id="dd9f5-208">Met de naam</span><span class="sxs-lookup"><span data-stu-id="dd9f5-208">named</span></span> |
| <span data-ttu-id="dd9f5-209">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-209">Default value</span></span> |<span data-ttu-id="dd9f5-210">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-210">none</span></span> |
| <span data-ttu-id="dd9f5-211">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-211">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-212">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-212">false</span></span> |
| <span data-ttu-id="dd9f5-213">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-213">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-214">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-214">false</span></span> |

<span data-ttu-id="dd9f5-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="dd9f5-216">Deze cmdlet ondersteunt Hallo algemene parameters:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, -InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction en -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-216">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="dd9f5-217">Invoer</span><span class="sxs-lookup"><span data-stu-id="dd9f5-217">Inputs</span></span>
<span data-ttu-id="dd9f5-218">Hallo-invoertype is Hallo Hallo type objecten dat u toohello cmdlet kunt overbrengen.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-218">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="dd9f5-219">uitvoer</span><span class="sxs-lookup"><span data-stu-id="dd9f5-219">Outputs</span></span>
<span data-ttu-id="dd9f5-220">Hallo-uitvoertype is Hallo type Hallo-objecten dat Hallo cmdlet verzendt.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-220">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="dd9f5-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="dd9f5-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="dd9f5-222">Een mediaservice-updates.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="dd9f5-223">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="dd9f5-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="dd9f5-224">Parameters</span><span class="sxs-lookup"><span data-stu-id="dd9f5-224">Parameters</span></span>
<span data-ttu-id="dd9f5-225">**-ResourceGroupName &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-226">Geeft de naam Hallo van Hallo resource groep toowhich die deze mediaservice behoort.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-226">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="dd9f5-227">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-227">Aliases</span></span> | <span data-ttu-id="dd9f5-228">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-229">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-229">Required?</span></span> |<span data-ttu-id="dd9f5-230">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-230">true</span></span> |
| <span data-ttu-id="dd9f5-231">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-231">Position?</span></span> |<span data-ttu-id="dd9f5-232">0</span><span class="sxs-lookup"><span data-stu-id="dd9f5-232">0</span></span> |
| <span data-ttu-id="dd9f5-233">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-233">Default Value</span></span> |<span data-ttu-id="dd9f5-234">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-234">none</span></span> |
| <span data-ttu-id="dd9f5-235">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="dd9f5-236">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-237">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-237">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-238">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-238">false</span></span> |

<span data-ttu-id="dd9f5-239">**-AccountName &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-240">Geeft de naam Hallo van Hallo mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-240">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="dd9f5-241">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-241">Aliases</span></span> | <span data-ttu-id="dd9f5-242">Naam</span><span class="sxs-lookup"><span data-stu-id="dd9f5-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-243">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-243">Required?</span></span> |<span data-ttu-id="dd9f5-244">True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-244">True</span></span> |
| <span data-ttu-id="dd9f5-245">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-245">Position?</span></span> |<span data-ttu-id="dd9f5-246">1</span><span class="sxs-lookup"><span data-stu-id="dd9f5-246">1</span></span> |
| <span data-ttu-id="dd9f5-247">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-247">Default value</span></span> |<span data-ttu-id="dd9f5-248">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-248">None</span></span> |
| <span data-ttu-id="dd9f5-249">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-249">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-250">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-251">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-251">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-252">False</span><span class="sxs-lookup"><span data-stu-id="dd9f5-252">False</span></span> |

<span data-ttu-id="dd9f5-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="dd9f5-254">Hiermee geeft u opslagaccounts die zijn gekoppeld aan Hallo mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-254">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="dd9f5-255">Nieuwe storage-account (gemaakt met de Hallo Resource Manager-API) alleen wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-255">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="dd9f5-256">Hallo storage-account moet aanwezig zijn en heeft dezelfde locatie met mediaservice Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-256">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="dd9f5-257">Slechts één opslagaccount kan worden opgegeven als primaire.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="dd9f5-258">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-258">Aliases</span></span> | <span data-ttu-id="dd9f5-259">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-260">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-260">Required?</span></span> |<span data-ttu-id="dd9f5-261">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-261">false</span></span> |
| <span data-ttu-id="dd9f5-262">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-262">Position?</span></span> |<span data-ttu-id="dd9f5-263">Met de naam</span><span class="sxs-lookup"><span data-stu-id="dd9f5-263">Named</span></span> |
| <span data-ttu-id="dd9f5-264">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-264">Default value</span></span> |<span data-ttu-id="dd9f5-265">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-265">none</span></span> |
| <span data-ttu-id="dd9f5-266">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-266">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-267">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-268">Naam van de parameter</span><span class="sxs-lookup"><span data-stu-id="dd9f5-268">Parameter set name</span></span> |<span data-ttu-id="dd9f5-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="dd9f5-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="dd9f5-270">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-270">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-271">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-271">false</span></span> |

<span data-ttu-id="dd9f5-272">**-Tags &lt;hashtabel&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="dd9f5-273">Hiermee geeft u een hash-tabel van Hallo-labels die gekoppeld aan deze mediaservice zijn.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-273">Specifies a hash table of hello tags that are associated with this media service.</span></span>

* <span data-ttu-id="dd9f5-274">Hallo-labels die gekoppeld aan Hallo mediaservice zijn worden vervangen door de waarde die is opgegeven door de klant Hallo.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-274">hello tags that are associated with hello media service are replaced with value specified by hello customer.</span></span>

| <span data-ttu-id="dd9f5-275">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-275">Aliases</span></span> | <span data-ttu-id="dd9f5-276">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-277">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-277">Required?</span></span> |<span data-ttu-id="dd9f5-278">False</span><span class="sxs-lookup"><span data-stu-id="dd9f5-278">False</span></span> |
| <span data-ttu-id="dd9f5-279">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-279">Position?</span></span> |<span data-ttu-id="dd9f5-280">Met de naam</span><span class="sxs-lookup"><span data-stu-id="dd9f5-280">Named</span></span> |
| <span data-ttu-id="dd9f5-281">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-281">Default value</span></span> |<span data-ttu-id="dd9f5-282">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-282">None</span></span> |
| <span data-ttu-id="dd9f5-283">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-283">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-284">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-285">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-285">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-286">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-286">false</span></span> |

<span data-ttu-id="dd9f5-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="dd9f5-288">Deze cmdlet ondersteunt Hallo algemene parameters:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, -InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction en -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-288">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="dd9f5-289">Invoer</span><span class="sxs-lookup"><span data-stu-id="dd9f5-289">Inputs</span></span>
<span data-ttu-id="dd9f5-290">Hallo-invoertype is Hallo Hallo type objecten dat u toohello cmdlet kunt overbrengen.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-290">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="dd9f5-291">uitvoer</span><span class="sxs-lookup"><span data-stu-id="dd9f5-291">Outputs</span></span>
<span data-ttu-id="dd9f5-292">Hallo-uitvoertype is Hallo type Hallo-objecten dat Hallo cmdlet verzendt.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-292">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="dd9f5-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="dd9f5-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="dd9f5-294">Hiermee verwijdert u een mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="dd9f5-295">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="dd9f5-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="dd9f5-296">Parameters</span><span class="sxs-lookup"><span data-stu-id="dd9f5-296">Parameters</span></span>
<span data-ttu-id="dd9f5-297">**-ResourceGroupName &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-298">Geeft de naam Hallo van Hallo resource groep toowhich die deze mediaservice behoort.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-298">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="dd9f5-299">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-299">Aliases</span></span> | <span data-ttu-id="dd9f5-300">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-301">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-301">Required?</span></span> |<span data-ttu-id="dd9f5-302">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-302">true</span></span> |
| <span data-ttu-id="dd9f5-303">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-303">Position?</span></span> |<span data-ttu-id="dd9f5-304">0</span><span class="sxs-lookup"><span data-stu-id="dd9f5-304">0</span></span> |
| <span data-ttu-id="dd9f5-305">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-305">Default value</span></span> |<span data-ttu-id="dd9f5-306">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-306">none</span></span> |
| <span data-ttu-id="dd9f5-307">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-307">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-308">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-309">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-309">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-310">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-310">false</span></span> |

<span data-ttu-id="dd9f5-311">**-AccountName &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-312">Geeft de naam Hallo van Hallo mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-312">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="dd9f5-313">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-313">Aliases</span></span> | <span data-ttu-id="dd9f5-314">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-315">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-315">Required?</span></span> |<span data-ttu-id="dd9f5-316">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-316">true</span></span> |
| <span data-ttu-id="dd9f5-317">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-317">Position?</span></span> |<span data-ttu-id="dd9f5-318">2</span><span class="sxs-lookup"><span data-stu-id="dd9f5-318">2</span></span> |
| <span data-ttu-id="dd9f5-319">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-319">Default value</span></span> |<span data-ttu-id="dd9f5-320">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-320">None</span></span> |
| <span data-ttu-id="dd9f5-321">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-321">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-322">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-323">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-323">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-324">False</span><span class="sxs-lookup"><span data-stu-id="dd9f5-324">False</span></span> |

<span data-ttu-id="dd9f5-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="dd9f5-326">Deze cmdlet ondersteunt Hallo algemene parameters:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, -InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction en -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-326">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="dd9f5-327">Invoer</span><span class="sxs-lookup"><span data-stu-id="dd9f5-327">Inputs</span></span>
<span data-ttu-id="dd9f5-328">Hallo-invoertype is Hallo Hallo type objecten dat u toohello cmdlet kunt overbrengen.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-328">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="dd9f5-329">uitvoer</span><span class="sxs-lookup"><span data-stu-id="dd9f5-329">Outputs</span></span>
<span data-ttu-id="dd9f5-330">Hallo-uitvoertype is Hallo type Hallo-objecten dat Hallo cmdlet verzendt.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-330">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="dd9f5-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="dd9f5-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="dd9f5-332">Hiermee haalt u alle mediaservices in een resourcegroep of een mediaservice met een bepaalde naam.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="dd9f5-333">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="dd9f5-333">Syntax</span></span>
<span data-ttu-id="dd9f5-334">ParameterSet: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="dd9f5-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="dd9f5-335">ParameterSet: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="dd9f5-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="dd9f5-336">Parameters</span><span class="sxs-lookup"><span data-stu-id="dd9f5-336">Parameters</span></span>
<span data-ttu-id="dd9f5-337">**-ResourceGroupName &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-338">Geeft de naam Hallo van Hallo resource groep toowhich die deze mediaservice behoort.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-338">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="dd9f5-339">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-339">Aliases</span></span> | <span data-ttu-id="dd9f5-340">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-341">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-341">Required?</span></span> |<span data-ttu-id="dd9f5-342">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-342">true</span></span> |
| <span data-ttu-id="dd9f5-343">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-343">Position?</span></span> |<span data-ttu-id="dd9f5-344">0</span><span class="sxs-lookup"><span data-stu-id="dd9f5-344">0</span></span> |
| <span data-ttu-id="dd9f5-345">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-345">Default value</span></span> |<span data-ttu-id="dd9f5-346">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-346">none</span></span> |
| <span data-ttu-id="dd9f5-347">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-347">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-348">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-349">Naam van de parameter</span><span class="sxs-lookup"><span data-stu-id="dd9f5-349">Parameter set name</span></span> |<span data-ttu-id="dd9f5-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="dd9f5-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="dd9f5-351">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-351">Accept wildcard characters?</span></span>   <span data-ttu-id="dd9f5-352">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-352">false</span></span>

<span data-ttu-id="dd9f5-353">**-AccountName &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-354">Geeft de naam Hallo van Hallo mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-354">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="dd9f5-355">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-355">Aliases</span></span> | <span data-ttu-id="dd9f5-356">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-357">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-357">Required?</span></span> |<span data-ttu-id="dd9f5-358">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-358">true</span></span> |
| <span data-ttu-id="dd9f5-359">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-359">Position?</span></span> |<span data-ttu-id="dd9f5-360">1</span><span class="sxs-lookup"><span data-stu-id="dd9f5-360">1</span></span> |
| <span data-ttu-id="dd9f5-361">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-361">Default value</span></span> |<span data-ttu-id="dd9f5-362">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-362">none</span></span> |
| <span data-ttu-id="dd9f5-363">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-363">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-364">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-365">Naam van de parameter</span><span class="sxs-lookup"><span data-stu-id="dd9f5-365">Parameter set name</span></span> |<span data-ttu-id="dd9f5-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="dd9f5-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="dd9f5-367">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-367">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-368">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-368">false</span></span> |

<span data-ttu-id="dd9f5-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="dd9f5-370">Deze cmdlet ondersteunt Hallo algemene parameters:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, -InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction en -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-370">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="dd9f5-371">Invoer</span><span class="sxs-lookup"><span data-stu-id="dd9f5-371">Inputs</span></span>
<span data-ttu-id="dd9f5-372">Hallo-invoertype is Hallo Hallo type objecten dat u toohello cmdlet kunt overbrengen.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-372">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="dd9f5-373">uitvoer</span><span class="sxs-lookup"><span data-stu-id="dd9f5-373">Outputs</span></span>
<span data-ttu-id="dd9f5-374">Hallo-uitvoertype is Hallo type Hallo-objecten dat Hallo cmdlet verzendt.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-374">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="dd9f5-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="dd9f5-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="dd9f5-376">Sleutels van een mediaservice opgehaald.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="dd9f5-377">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="dd9f5-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="dd9f5-378">Parameters</span><span class="sxs-lookup"><span data-stu-id="dd9f5-378">Parameters</span></span>
<span data-ttu-id="dd9f5-379">**-ResourceGroupName &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-380">Geeft de naam Hallo van Hallo resource groep toowhich die deze mediaservice behoort.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-380">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="dd9f5-381">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-381">Aliases</span></span> | <span data-ttu-id="dd9f5-382">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-383">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-383">Required?</span></span> |<span data-ttu-id="dd9f5-384">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-384">true</span></span> |
| <span data-ttu-id="dd9f5-385">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-385">Position?</span></span> |<span data-ttu-id="dd9f5-386">0</span><span class="sxs-lookup"><span data-stu-id="dd9f5-386">0</span></span> |
| <span data-ttu-id="dd9f5-387">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-387">Default value</span></span> |<span data-ttu-id="dd9f5-388">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-388">none</span></span> |
| <span data-ttu-id="dd9f5-389">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-389">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-390">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-391">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-391">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-392">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-392">false</span></span> |

<span data-ttu-id="dd9f5-393">**-AccountName &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-394">Geeft de naam Hallo van Hallo mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-394">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="dd9f5-395">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-395">Aliases</span></span> | <span data-ttu-id="dd9f5-396">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-397">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-397">Required?</span></span> |<span data-ttu-id="dd9f5-398">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-398">true</span></span> |
| <span data-ttu-id="dd9f5-399">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-399">Position?</span></span> |<span data-ttu-id="dd9f5-400">1</span><span class="sxs-lookup"><span data-stu-id="dd9f5-400">1</span></span> |
| <span data-ttu-id="dd9f5-401">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-401">Default value</span></span> |<span data-ttu-id="dd9f5-402">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-402">none</span></span> |
| <span data-ttu-id="dd9f5-403">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-403">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-404">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-405">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-405">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-406">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-406">false</span></span> |

<span data-ttu-id="dd9f5-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="dd9f5-408">Deze cmdlet ondersteunt Hallo algemene parameters:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, -InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction en -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-408">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="dd9f5-409">Invoer</span><span class="sxs-lookup"><span data-stu-id="dd9f5-409">Inputs</span></span>
<span data-ttu-id="dd9f5-410">Hallo-invoertype is Hallo Hallo type objecten dat u toohello cmdlet kunt overbrengen.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-410">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="dd9f5-411">uitvoer</span><span class="sxs-lookup"><span data-stu-id="dd9f5-411">Outputs</span></span>
<span data-ttu-id="dd9f5-412">Hallo-uitvoertype is Hallo type Hallo-objecten dat Hallo cmdlet verzendt.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-412">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="dd9f5-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="dd9f5-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="dd9f5-414">Genereert opnieuw een primaire of secundaire sleutel van een mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="dd9f5-415">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="dd9f5-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="dd9f5-416">Parameters</span><span class="sxs-lookup"><span data-stu-id="dd9f5-416">Parameters</span></span>
<span data-ttu-id="dd9f5-417">**-ResourceGroupName &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-418">Geeft de naam Hallo van Hallo resource groep toowhich die deze mediaservice behoort.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-418">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="dd9f5-419">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-419">Aliases</span></span> | <span data-ttu-id="dd9f5-420">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-421">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-421">Required?</span></span> |<span data-ttu-id="dd9f5-422">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-422">true</span></span> |
| <span data-ttu-id="dd9f5-423">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-423">Position?</span></span> |<span data-ttu-id="dd9f5-424">0</span><span class="sxs-lookup"><span data-stu-id="dd9f5-424">0</span></span> |
| <span data-ttu-id="dd9f5-425">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-425">Default value</span></span> |<span data-ttu-id="dd9f5-426">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-426">none</span></span> |
| <span data-ttu-id="dd9f5-427">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-427">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-428">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-429">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-429">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-430">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-430">false</span></span> |

<span data-ttu-id="dd9f5-431">**-AccountName &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-432">Geeft de naam Hallo van Hallo mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-432">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="dd9f5-433">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-433">Aliases</span></span> | <span data-ttu-id="dd9f5-434">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-435">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-435">Required?</span></span> |<span data-ttu-id="dd9f5-436">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-436">true</span></span> |
| <span data-ttu-id="dd9f5-437">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-437">Position?</span></span> |<span data-ttu-id="dd9f5-438">1</span><span class="sxs-lookup"><span data-stu-id="dd9f5-438">1</span></span> |
| <span data-ttu-id="dd9f5-439">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-439">Default value</span></span> |<span data-ttu-id="dd9f5-440">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-440">none</span></span> |
| <span data-ttu-id="dd9f5-441">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-441">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-442">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-443">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-443">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-444">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-444">false</span></span> |

<span data-ttu-id="dd9f5-445">**KeyType - &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="dd9f5-446">Hiermee geeft u Hallo sleuteltype van Hallo mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-446">Specifies hello key type of hello media service.</span></span>

* <span data-ttu-id="dd9f5-447">Primaire of secundaire</span><span class="sxs-lookup"><span data-stu-id="dd9f5-447">Primary or Secondary</span></span>

| <span data-ttu-id="dd9f5-448">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-448">Aliases</span></span> | <span data-ttu-id="dd9f5-449">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-450">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-450">Required?</span></span> |<span data-ttu-id="dd9f5-451">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-451">true</span></span> |
| <span data-ttu-id="dd9f5-452">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-452">Position?</span></span> |<span data-ttu-id="dd9f5-453">2</span><span class="sxs-lookup"><span data-stu-id="dd9f5-453">2</span></span> |
| <span data-ttu-id="dd9f5-454">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-454">Default value</span></span> |<span data-ttu-id="dd9f5-455">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-455">none</span></span> |
| <span data-ttu-id="dd9f5-456">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-456">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-457">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-457">false</span></span> |
| <span data-ttu-id="dd9f5-458">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-458">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-459">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-459">false</span></span> |

<span data-ttu-id="dd9f5-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="dd9f5-461">Deze cmdlet ondersteunt Hallo algemene parameters:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, -InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction en -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-461">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="dd9f5-462">Invoer</span><span class="sxs-lookup"><span data-stu-id="dd9f5-462">Inputs</span></span>
<span data-ttu-id="dd9f5-463">Hallo-invoertype is Hallo Hallo type objecten dat u toothe cmdlet kunt overbrengen.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-463">hello input type is hello type of hello objects that you can pipe toothe cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="dd9f5-464">uitvoer</span><span class="sxs-lookup"><span data-stu-id="dd9f5-464">Outputs</span></span>
<span data-ttu-id="dd9f5-465">Hallo-uitvoertype is Hallo type Hallo-objecten dat Hallo cmdlet verzendt.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-465">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="dd9f5-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="dd9f5-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="dd9f5-467">Toegangscodes voor opslag voor een opslagaccount die is gekoppeld aan Hallo mediaservice synchroniseert.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-467">Synchronizes storage account keys for a storage account associated with hello media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="dd9f5-468">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="dd9f5-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="dd9f5-469">Parameters</span><span class="sxs-lookup"><span data-stu-id="dd9f5-469">Parameters</span></span>
<span data-ttu-id="dd9f5-470">**-ResourceGroupName &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-471">Geeft de naam Hallo van Hallo resource groep toowhich die deze mediaservice behoort.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-471">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="dd9f5-472">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-472">Aliases</span></span> | <span data-ttu-id="dd9f5-473">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-474">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-474">Required?</span></span> |<span data-ttu-id="dd9f5-475">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-475">true</span></span> |
| <span data-ttu-id="dd9f5-476">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-476">Position?</span></span> |<span data-ttu-id="dd9f5-477">0</span><span class="sxs-lookup"><span data-stu-id="dd9f5-477">0</span></span> |
| <span data-ttu-id="dd9f5-478">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-478">Default value</span></span> |<span data-ttu-id="dd9f5-479">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-479">none</span></span> |
| <span data-ttu-id="dd9f5-480">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-480">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-481">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-482">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-482">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-483">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-483">false</span></span> |

<span data-ttu-id="dd9f5-484">**-AccountName &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-485">Geeft de naam Hallo van Hallo mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-485">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="dd9f5-486">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-486">Aliases</span></span> | <span data-ttu-id="dd9f5-487">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-488">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-488">Required?</span></span> |<span data-ttu-id="dd9f5-489">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-489">true</span></span> |
| <span data-ttu-id="dd9f5-490">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-490">Position?</span></span> |<span data-ttu-id="dd9f5-491">1</span><span class="sxs-lookup"><span data-stu-id="dd9f5-491">1</span></span> |
| <span data-ttu-id="dd9f5-492">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-492">Default value</span></span> |<span data-ttu-id="dd9f5-493">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-493">none</span></span> |
| <span data-ttu-id="dd9f5-494">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-494">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-495">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-496">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-496">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-497">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-497">false</span></span> |

<span data-ttu-id="dd9f5-498">**-StorageAccountId &lt;tekenreeks&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="dd9f5-499">Hiermee geeft u Hallo storage-account zijn gekoppeld aan Hallo mediaservice.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-499">Specifies hello storage account associated with hello media service.</span></span>

| <span data-ttu-id="dd9f5-500">Aliassen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-500">Aliases</span></span> | <span data-ttu-id="dd9f5-501">Id</span><span class="sxs-lookup"><span data-stu-id="dd9f5-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="dd9f5-502">Vereist?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-502">Required?</span></span> |<span data-ttu-id="dd9f5-503">De waarde True</span><span class="sxs-lookup"><span data-stu-id="dd9f5-503">true</span></span> |
| <span data-ttu-id="dd9f5-504">Positie?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-504">Position?</span></span> |<span data-ttu-id="dd9f5-505">2</span><span class="sxs-lookup"><span data-stu-id="dd9f5-505">2</span></span> |
| <span data-ttu-id="dd9f5-506">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="dd9f5-506">Default value</span></span> |<span data-ttu-id="dd9f5-507">Geen</span><span class="sxs-lookup"><span data-stu-id="dd9f5-507">none</span></span> |
| <span data-ttu-id="dd9f5-508">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-508">Accept pipeline input?</span></span> |<span data-ttu-id="dd9f5-509">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd9f5-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="dd9f5-510">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="dd9f5-510">Accept wildcard characters?</span></span> |<span data-ttu-id="dd9f5-511">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="dd9f5-511">false</span></span> |

<span data-ttu-id="dd9f5-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd9f5-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="dd9f5-513">Deze cmdlet ondersteunt Hallo algemene parameters:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, -InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction en -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-513">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="dd9f5-514">Invoer</span><span class="sxs-lookup"><span data-stu-id="dd9f5-514">Inputs</span></span>
<span data-ttu-id="dd9f5-515">Hallo-invoertype is Hallo Hallo type objecten dat u toohello cmdlet kunt overbrengen.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-515">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="dd9f5-516">uitvoer</span><span class="sxs-lookup"><span data-stu-id="dd9f5-516">Outputs</span></span>
<span data-ttu-id="dd9f5-517">Hallo-uitvoertype is Hallo type Hallo-objecten dat Hallo cmdlet verzendt.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-517">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="dd9f5-518">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="dd9f5-518">Next step</span></span>
<span data-ttu-id="dd9f5-519">Media Services-leertrajecten uitchecken.</span><span class="sxs-lookup"><span data-stu-id="dd9f5-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="dd9f5-520">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="dd9f5-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

