---
title: Problemen oplossen van Azure Active Directory-activiteit inhoudspakket fouten-Logboeken | Microsoft Docs
description: Biedt u een lijst met foutberichten van het inhoudspakket van Azure Active Directory-activiteit en werk deze kunt oplossen.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c880e9eb6d48bd1e38075fbd867d3906ec67b547
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="3538a-103">Het oplossen van Azure Active Directory-activiteit registreert inhoudspakket fouten</span><span class="sxs-lookup"><span data-stu-id="3538a-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="3538a-104">Als u werkt met het Power BI-inhoudspakket voor Azure Active Directory-Preview, is het mogelijk dat u in de volgende fouten uitvoert:</span><span class="sxs-lookup"><span data-stu-id="3538a-104">When working with the Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into the following errors:</span></span> 

- [<span data-ttu-id="3538a-105">Vernieuwen is mislukt</span><span class="sxs-lookup"><span data-stu-id="3538a-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="3538a-106">Gegevensbronreferenties bijwerken is mislukt</span><span class="sxs-lookup"><span data-stu-id="3538a-106">Failed to update data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="3538a-107">Importeren van gegevens duurt te lang is</span><span class="sxs-lookup"><span data-stu-id="3538a-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="3538a-108">In dit onderwerp vindt u informatie over de mogelijke oorzaken en hoe deze fouten te herstellen.</span><span class="sxs-lookup"><span data-stu-id="3538a-108">This topic provides you with information about the possible causes and how to fix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="3538a-109">Vernieuwen is mislukt</span><span class="sxs-lookup"><span data-stu-id="3538a-109">Refresh failed</span></span> 
 
<span data-ttu-id="3538a-110">**Hoe deze fout wordt opgehaald**: e-mailbericht met Power BI- of mislukte status in de geschiedenis vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="3538a-110">**How this error is surfaced**: Email from Power BI or failed status in the refresh history.</span></span> 


| <span data-ttu-id="3538a-111">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="3538a-111">Cause</span></span> | <span data-ttu-id="3538a-112">Op te lossen</span><span class="sxs-lookup"><span data-stu-id="3538a-112">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="3538a-113">Vernieuwen van de fout fouten kunnen worden veroorzaakt wanneer de referenties van de gebruikers die verbinding maken met het inhoudspakket is opnieuw ingesteld, maar niet bijgewerkt in de verbindingsinstellingen van de van het inhoudspakket.</span><span class="sxs-lookup"><span data-stu-id="3538a-113">Refresh failure errors can be caused when the credentials of the users connecting to the content pack have been reset but not updated in the connection settings of the of the content pack.</span></span> | <span data-ttu-id="3538a-114">Zoek de gegevensset die overeenkomt met het Azure Active Directory-activiteit logboeken dashboard (Azure Active Directory-activiteit Logboeken), kies schema vernieuwen en voer uw Azure AD-referenties in Power BI.</span><span class="sxs-lookup"><span data-stu-id="3538a-114">In Power BI, locate the dataset corresponding to the Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="3538a-115">Vernieuwen kan mislukken vanwege gegevensproblemen met de in het onderliggende inhoudspakket.</span><span class="sxs-lookup"><span data-stu-id="3538a-115">A refresh can fail due to data issues in the underlying content pack.</span></span> | <span data-ttu-id="3538a-116">Een ondersteuningsticket-bestand.</span><span class="sxs-lookup"><span data-stu-id="3538a-116">File a support ticket.</span></span> <span data-ttu-id="3538a-117">Zie voor meer informatie [ondersteuning voor Azure Active Directory krijgen](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="3538a-117">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-to-update-data-source-credentials"></a><span data-ttu-id="3538a-118">Gegevensbronreferenties bijwerken is mislukt</span><span class="sxs-lookup"><span data-stu-id="3538a-118">Failed to update data source credentials</span></span> 
 
<span data-ttu-id="3538a-119">**Hoe deze fout wordt opgehaald**: In Power BI, wanneer u een verbinding met het inhoudspakket van Azure Active Directory-activiteit Logboeken (preview).</span><span class="sxs-lookup"><span data-stu-id="3538a-119">**How this error is surfaced**: In Power BI, when you are connecting to the Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="3538a-120">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="3538a-120">Cause</span></span> | <span data-ttu-id="3538a-121">Op te lossen</span><span class="sxs-lookup"><span data-stu-id="3538a-121">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="3538a-122">Gebruiker die de verbinding is een globale beheerder noch een lezer beveiliging of een beheerder beveiliging.</span><span class="sxs-lookup"><span data-stu-id="3538a-122">The connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="3538a-123">Gebruik een account dat een globale beheerder of een lezer beveiliging of een beheerder van de beveiliging voor toegang tot de inhoudspakketten.</span><span class="sxs-lookup"><span data-stu-id="3538a-123">Use an account that is either a global admin or a security reader or a security admin to access the content packs.</span></span> |
| <span data-ttu-id="3538a-124">Uw tenant is niet een Premium-tenant of beschikt niet over ten minste één gebruiker met Premium-licentie bestand.</span><span class="sxs-lookup"><span data-stu-id="3538a-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="3538a-125">Een ondersteuningsticket-bestand.</span><span class="sxs-lookup"><span data-stu-id="3538a-125">File a support ticket.</span></span> <span data-ttu-id="3538a-126">Zie voor meer informatie [ondersteuning voor Azure Active Directory krijgen](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="3538a-126">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="3538a-127">Importeren van gegevens duurt te lang is</span><span class="sxs-lookup"><span data-stu-id="3538a-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="3538a-128">**Hoe deze fout wordt opgehaald**: In Power BI zodra u verbinding hebt gemaakt met uw inhoudspakket het importproces gestart uw dashboard voorbereiden voor Azure Active Directory-logboek.</span><span class="sxs-lookup"><span data-stu-id="3538a-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, the data import process starts to prepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="3538a-129">Het bericht: '*importeren van gegevens...* '</span><span class="sxs-lookup"><span data-stu-id="3538a-129">You see the message: “*Importing data...*”</span></span>  

| <span data-ttu-id="3538a-130">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="3538a-130">Cause</span></span> | <span data-ttu-id="3538a-131">Op te lossen</span><span class="sxs-lookup"><span data-stu-id="3538a-131">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="3538a-132">Afhankelijk van de grootte van uw tenant, kan deze stap enkele minuten tot duren 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="3538a-132">Depending on the size of your tenant, this step could take anywhere from a few mins to 30 minutes.</span></span> | <span data-ttu-id="3538a-133">NET worden geduld.</span><span class="sxs-lookup"><span data-stu-id="3538a-133">Just be patient.</span></span> <span data-ttu-id="3538a-134">Als het bericht wordt niet gewijzigd in uw dashboard binnen een uur wordt weergegeven, neem een ondersteuningsticket-bestand.</span><span class="sxs-lookup"><span data-stu-id="3538a-134">If the message does not change to showing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="3538a-135">Zie voor meer informatie [ondersteuning voor Azure Active Directory krijgen](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="3538a-135">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="3538a-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3538a-136">Next steps</span></span>

<span data-ttu-id="3538a-137">Klik op om de Power BI-inhoudspakket voor Azure Active Directory-Preview [hier](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="3538a-137">To install the Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


