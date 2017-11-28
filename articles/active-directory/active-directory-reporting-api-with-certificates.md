---
title: aaaGet gegevens met Azure AD rapportage-API met certificaten Hallo | Microsoft Docs
description: Legt uit hoe toouse hello Azure AD rapportage-API met referenties tooget certificaatgegevens van Directory's zonder tussenkomst van de gebruiker.
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="be147-103">Gegevens hello Azure AD-rapportage-API gebruiken met certificaten ophalen</span><span class="sxs-lookup"><span data-stu-id="be147-103">Get data using hello Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="be147-104">Dit artikel wordt beschreven hoe toouse hello Azure AD rapportage-API met referenties tooget certificaatgegevens van Directory's zonder tussenkomst van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="be147-104">This article discusses how toouse hello Azure AD Reporting API with certificate credentials tooget data from directories without user intervention.</span></span> 

## <a name="use-hello-azure-ad-reporting-api"></a><span data-ttu-id="be147-105">Gebruik hello Azure AD rapportage-API</span><span class="sxs-lookup"><span data-stu-id="be147-105">Use hello Azure AD Reporting API</span></span> 
<span data-ttu-id="be147-106">Azure AD rapportage-API is vereist dat Hallo stappen te voltooien:</span><span class="sxs-lookup"><span data-stu-id="be147-106">Azure AD Reporting API requires that you complete hello following steps:</span></span>
 *  <span data-ttu-id="be147-107">Vereiste onderdelen installeren</span><span class="sxs-lookup"><span data-stu-id="be147-107">Install prerequisites</span></span>
 *  <span data-ttu-id="be147-108">Hallo-certificaat in uw app instellen</span><span class="sxs-lookup"><span data-stu-id="be147-108">Set hello certificate in your app</span></span>
 *  <span data-ttu-id="be147-109">Een toegangstoken opvragen</span><span class="sxs-lookup"><span data-stu-id="be147-109">Get an access token</span></span>
 *  <span data-ttu-id="be147-110">Hallo access token toocall Hallo Graph API gebruiken</span><span class="sxs-lookup"><span data-stu-id="be147-110">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="be147-111">Zie [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils) (Rapportage-API-module gebruiken) voor meer informatie over broncode.</span><span class="sxs-lookup"><span data-stu-id="be147-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="be147-112">Vereiste onderdelen installeren</span><span class="sxs-lookup"><span data-stu-id="be147-112">Install prerequisites</span></span>
<span data-ttu-id="be147-113">U moet toohave Azure AD PowerShell V2 en AzureADUtils-module geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="be147-113">You will need toohave Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="be147-114">Download en installeer Azure AD Powershell V2, Hallo instructies te volgen op [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="be147-114">Download and install Azure AD Powershell V2, following hello instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="be147-115">Download hello Azure AD Utils module op basis van [AzureAD/azure-Active Directory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="be147-115">Download hello Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="be147-116">Deze module biedt verschillende cmdlets, waaronder:</span><span class="sxs-lookup"><span data-stu-id="be147-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="be147-117">Hallo meest recente versie van Nuget met ADAL</span><span class="sxs-lookup"><span data-stu-id="be147-117">hello latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="be147-118">Toegangstokens van gebruiker, toepassingssleutels en certificaten met behulp van ADAL</span><span class="sxs-lookup"><span data-stu-id="be147-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="be147-119">Afhandeling van pagina's met zoekresultaten door Graph API</span><span class="sxs-lookup"><span data-stu-id="be147-119">Graph API handling paged results</span></span>

<span data-ttu-id="be147-120">**tooinstall hello Utils van Azure AD-module:**</span><span class="sxs-lookup"><span data-stu-id="be147-120">**tooinstall hello Azure AD Utils module:**</span></span>

1. <span data-ttu-id="be147-121">Maken van een directory toosave Hallo hulpprogramma's-module (bijvoorbeeld c:\azureAD) en Hallo module vanuit GitHub downloaden.</span><span class="sxs-lookup"><span data-stu-id="be147-121">Create a directory toosave hello utilities module (for example, c:\azureAD) and download hello module from GitHub.</span></span>
2. <span data-ttu-id="be147-122">Open een PowerShell-sessie en gaat u toohello directory die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="be147-122">Open a PowerShell session, and go toohello directory you just created.</span></span> 
3. <span data-ttu-id="be147-123">Hallo-module importeren en installeer het in Hallo PowerShell-module pad met de cmdlet Install-AzureADUtilsModule Hallo.</span><span class="sxs-lookup"><span data-stu-id="be147-123">Import hello module, and install it in hello PowerShell module path using hello Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="be147-124">Hallo-sessie ziet vergelijkbare toothis scherm:</span><span class="sxs-lookup"><span data-stu-id="be147-124">hello session should look similar toothis screen:</span></span>

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a><span data-ttu-id="be147-126">Hallo-certificaat in uw app instellen</span><span class="sxs-lookup"><span data-stu-id="be147-126">Set hello certificate in your app</span></span>
1. <span data-ttu-id="be147-127">Als u een app al hebt, moet u de Object-ID ophalen van hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="be147-127">If you already have an app, get its Object ID from hello Azure Portal.</span></span> 

  ![Azure Portal](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="be147-129">Open een PowerShell-sessie en tooAzure AD verbinding maken met de cmdlet Hallo Connect-AzureAD.</span><span class="sxs-lookup"><span data-stu-id="be147-129">Open a PowerShell session and connect tooAzure AD using hello Connect-AzureAD cmdlet.</span></span>

  ![Azure Portal](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="be147-131">Hallo nieuw AzureADApplicationCertificateCredential cmdlet van AzureADUtils tooadd een certificaat referentie tooit gebruiken.</span><span class="sxs-lookup"><span data-stu-id="be147-131">Use hello New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils tooadd a certificate credential tooit.</span></span> 

>[!Note]
><span data-ttu-id="be147-132">U moet tooprovide Hallo toepassing Object-ID die u eerder hebt vastgelegd, evenals Hallo certificaatobject (ophalen deze met Hallo Cert: station).</span><span class="sxs-lookup"><span data-stu-id="be147-132">You need tooprovide hello application Object ID that you captured earlier, as well as hello certificate object (get this using hello Cert: drive).</span></span>
>


  ![Azure Portal](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="be147-134">Een toegangstoken opvragen</span><span class="sxs-lookup"><span data-stu-id="be147-134">Get an access token</span></span>

<span data-ttu-id="be147-135">tooget een toegangstoken Hallo Get AzureADGraphAPIAccessTokenFromCert cmdlet van AzureADUtils gebruiken.</span><span class="sxs-lookup"><span data-stu-id="be147-135">tooget an access token, use hello Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="be147-136">U moet toouse Hallo toepassings-ID in plaats van de Object-ID die u hebt gebruikt in de laatste sectie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="be147-136">You need toouse hello Application ID instead of hello Object ID that you used in hello last section.</span></span>
>

 ![Azure Portal](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a><span data-ttu-id="be147-138">Hallo access token toocall Hallo Graph API gebruiken</span><span class="sxs-lookup"><span data-stu-id="be147-138">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="be147-139">U kunt nu Hallo script maken.</span><span class="sxs-lookup"><span data-stu-id="be147-139">Now you can create hello script.</span></span> <span data-ttu-id="be147-140">Hieronder vindt u een voorbeeld met de cmdlet Invoke-AzureADGraphAPIQuery Hallo van Hallo AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="be147-140">Below is an example using hello Invoke-AzureADGraphAPIQuery cmdlet from hello AzureADUtils.</span></span> <span data-ttu-id="be147-141">Deze cmdlet verwerkt met meerdere pagina's met zoekresultaten en stuurt vervolgens deze resultaten toohello PowerShell-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="be147-141">This cmdlet handles multi-paged results, and then sends those results toohello PowerShell pipeline.</span></span> 

 ![Azure Portal](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="be147-143">U bent nu klaar tooexport tooa CSV en slaat tooa SIEM-systeem.</span><span class="sxs-lookup"><span data-stu-id="be147-143">You are now ready tooexport tooa CSV and save tooa SIEM system.</span></span> <span data-ttu-id="be147-144">U kunt ook inpakken uw script in een geplande taak tooget Azure AD-gegevens van uw tenant periodiek zonder toostore toepassing sleutels in de broncode Hallo.</span><span class="sxs-lookup"><span data-stu-id="be147-144">You can also wrap your script in a scheduled task tooget Azure AD data from your tenant periodically without having toostore application keys in hello source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="be147-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="be147-145">Next steps</span></span>
[<span data-ttu-id="be147-146">Hallo grondbeginselen van Azure identity management</span><span class="sxs-lookup"><span data-stu-id="be147-146">hello fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



