---
title: Gegevens opvragen met de rapportage-API van Azure AD met certificaten | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe u de rapportage-API van Azure AD gebruikt met certificaatreferenties om zonder tussenkomst van de gebruiker gegevens op te halen uit directory's.
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
ms.openlocfilehash: c1345dcda6e52267a8037ffd7207e6bc3b0d3b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-data-using-the-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="23605-103">Gegevens ophalen met de rapportage-API van Azure AD met certificaten</span><span class="sxs-lookup"><span data-stu-id="23605-103">Get data using the Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="23605-104">In dit artikel wordt uitgelegd hoe u de rapportage-API van Azure AD gebruikt met certificaatreferenties om zonder tussenkomst van de gebruiker gegevens op te halen uit directory's.</span><span class="sxs-lookup"><span data-stu-id="23605-104">This article discusses how to use the Azure AD Reporting API with certificate credentials to get data from directories without user intervention.</span></span> 

## <a name="use-the-azure-ad-reporting-api"></a><span data-ttu-id="23605-105">De rapportage-API voor Azure AD gebruiken</span><span class="sxs-lookup"><span data-stu-id="23605-105">Use the Azure AD Reporting API</span></span> 
<span data-ttu-id="23605-106">U moet de volgende stappen uitvoeren voordat u de rapportage-API van Azure AD kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="23605-106">Azure AD Reporting API requires that you complete the following steps:</span></span>
 *  <span data-ttu-id="23605-107">Vereiste onderdelen installeren</span><span class="sxs-lookup"><span data-stu-id="23605-107">Install prerequisites</span></span>
 *  <span data-ttu-id="23605-108">Het certificaat instellen in uw app</span><span class="sxs-lookup"><span data-stu-id="23605-108">Set the certificate in your app</span></span>
 *  <span data-ttu-id="23605-109">Een toegangstoken opvragen</span><span class="sxs-lookup"><span data-stu-id="23605-109">Get an access token</span></span>
 *  <span data-ttu-id="23605-110">Het toegangstoken gebruiken om de Graph API aan te roepen</span><span class="sxs-lookup"><span data-stu-id="23605-110">Use the access token to call the Graph API</span></span>

<span data-ttu-id="23605-111">Zie [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils) (Rapportage-API-module gebruiken) voor meer informatie over broncode.</span><span class="sxs-lookup"><span data-stu-id="23605-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="23605-112">Vereiste onderdelen installeren</span><span class="sxs-lookup"><span data-stu-id="23605-112">Install prerequisites</span></span>
<span data-ttu-id="23605-113">Azure AD PowerShell V2 en de module AzureADUtils moeten zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="23605-113">You will need to have Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="23605-114">Download en installeer Azure AD Powershell V2 met behulp van de instructies in [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="23605-114">Download and install Azure AD Powershell V2, following the instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="23605-115">Download de Azure AD Utils-module van [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="23605-115">Download the Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="23605-116">Deze module biedt verschillende cmdlets, waaronder:</span><span class="sxs-lookup"><span data-stu-id="23605-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="23605-117">De nieuwste versie van ADAL met Nuget</span><span class="sxs-lookup"><span data-stu-id="23605-117">The latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="23605-118">Toegangstokens van gebruiker, toepassingssleutels en certificaten met behulp van ADAL</span><span class="sxs-lookup"><span data-stu-id="23605-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="23605-119">Afhandeling van pagina's met zoekresultaten door Graph API</span><span class="sxs-lookup"><span data-stu-id="23605-119">Graph API handling paged results</span></span>

<span data-ttu-id="23605-120">**De Azure AD Utils-module installeren:**</span><span class="sxs-lookup"><span data-stu-id="23605-120">**To install the Azure AD Utils module:**</span></span>

1. <span data-ttu-id="23605-121">Maak een directory voor het opslaan van de module met hulpprogramma's (bijvoorbeeld c:\azureAD) en downloadt de module in GitHub.</span><span class="sxs-lookup"><span data-stu-id="23605-121">Create a directory to save the utilities module (for example, c:\azureAD) and download the module from GitHub.</span></span>
2. <span data-ttu-id="23605-122">Open een PowerShell-sessie en ga naar de directory die u net hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="23605-122">Open a PowerShell session, and go to the directory you just created.</span></span> 
3. <span data-ttu-id="23605-123">Importeer de module en installeer deze met de cmdlet Install-AzureADUtilsModule in het pad van de PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="23605-123">Import the module, and install it in the PowerShell module path using the Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="23605-124">De sessie moet er ongeveer uitzien zoals op dit scherm:</span><span class="sxs-lookup"><span data-stu-id="23605-124">The session should look similar to this screen:</span></span>

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-the-certificate-in-your-app"></a><span data-ttu-id="23605-126">Het certificaat instellen in uw app</span><span class="sxs-lookup"><span data-stu-id="23605-126">Set the certificate in your app</span></span>
1. <span data-ttu-id="23605-127">Als u al een app hebt, vraagt u de bijbehorende object-id op uit Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="23605-127">If you already have an app, get its Object ID from the Azure Portal.</span></span> 

  ![Azure Portal](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="23605-129">Open een PowerShell-sessie en maak verbinding met Azure AD via de cmdlet Connect-AzureAD.</span><span class="sxs-lookup"><span data-stu-id="23605-129">Open a PowerShell session and connect to Azure AD using the Connect-AzureAD cmdlet.</span></span>

  ![Azure Portal](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="23605-131">Gebruik de cmdlet New-AzureADApplicationCertificateCredential van AzureADUtils om er een certificaatreferentie aan toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="23605-131">Use the New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils to add a certificate credential to it.</span></span> 

>[!Note]
><span data-ttu-id="23605-132">U moet de object-id van de toepassing opgeven die u eerder hebt opgevraagd, evenals het certificaatobject (vraag dit op met behulp van het Cert:-station).</span><span class="sxs-lookup"><span data-stu-id="23605-132">You need to provide the application Object ID that you captured earlier, as well as the certificate object (get this using the Cert: drive).</span></span>
>


  ![Azure Portal](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="23605-134">Een toegangstoken opvragen</span><span class="sxs-lookup"><span data-stu-id="23605-134">Get an access token</span></span>

<span data-ttu-id="23605-135">U kunt een toegangstoken opvragen met de cmdlet Get-AzureADGraphAPIAccessTokenFromCert van AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="23605-135">To get an access token, use the Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="23605-136">Gebruik de toepassings-id en niet de object-id die u in de laatste sectie hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="23605-136">You need to use the Application ID instead of the Object ID that you used in the last section.</span></span>
>

 ![Azure Portal](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-the-access-token-to-call-the-graph-api"></a><span data-ttu-id="23605-138">Het toegangstoken gebruiken om de Graph API aan te roepen</span><span class="sxs-lookup"><span data-stu-id="23605-138">Use the access token to call the Graph API</span></span>

<span data-ttu-id="23605-139">U kunt nu het script maken.</span><span class="sxs-lookup"><span data-stu-id="23605-139">Now you can create the script.</span></span> <span data-ttu-id="23605-140">Hieronder ziet u een voorbeeld waarin de cmdlet Invoke-AzureADGraphAPIQuery van AzureADUtils wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="23605-140">Below is an example using the Invoke-AzureADGraphAPIQuery cmdlet from the AzureADUtils.</span></span> <span data-ttu-id="23605-141">Met deze cmdlet worden meerdere pagina's met zoekresultaten verwerkt, waarna deze resultaten naar de PowerShell-pijplijn worden verstuurd.</span><span class="sxs-lookup"><span data-stu-id="23605-141">This cmdlet handles multi-paged results, and then sends those results to the PowerShell pipeline.</span></span> 

 ![Azure Portal](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="23605-143">U bent nu klaar om te gaan exporteren naar een CSV-bestand en dit bestand op te slaan in een SIEM-systeem.</span><span class="sxs-lookup"><span data-stu-id="23605-143">You are now ready to export to a CSV and save to a SIEM system.</span></span> <span data-ttu-id="23605-144">U kunt uw script ook verpakken in een geplande taak om periodiek gegevens van Azure AD op te halen uit uw tenant zonder dat u toepassingssleutels hoeft op te slaan in de broncode.</span><span class="sxs-lookup"><span data-stu-id="23605-144">You can also wrap your script in a scheduled task to get Azure AD data from your tenant periodically without having to store application keys in the source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="23605-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="23605-145">Next steps</span></span>
<span data-ttu-id="23605-146">[The fundamentals of Azure identity management](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity) (De grondbeginselen van Azure-identiteitsbeheer)</span><span class="sxs-lookup"><span data-stu-id="23605-146">[The fundamentals of Azure identity management](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)</span></span><br>



