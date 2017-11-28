---
title: Problemen oplossen van Azure Active Directory-activiteit inhoudspakket fouten-Logboeken | Microsoft Docs
description: Biedt u een lijst met foutberichten van hello Azure Active Directory-activiteit inhoud Inpakken en stappen toofix ze.
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
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="08117-103">Het oplossen van Azure Active Directory-activiteit registreert inhoudspakket fouten</span><span class="sxs-lookup"><span data-stu-id="08117-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="08117-104">Als u werkt met Hallo Power BI-inhoudspakket voor Azure Active Directory-Preview, is het mogelijk dat u uitvoert in Hallo volgende fouten:</span><span class="sxs-lookup"><span data-stu-id="08117-104">When working with hello Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into hello following errors:</span></span> 

- [<span data-ttu-id="08117-105">Vernieuwen is mislukt</span><span class="sxs-lookup"><span data-stu-id="08117-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="08117-106">Mislukte tooupdate referenties voor gegevensbron</span><span class="sxs-lookup"><span data-stu-id="08117-106">Failed tooupdate data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="08117-107">Importeren van gegevens duurt te lang is</span><span class="sxs-lookup"><span data-stu-id="08117-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="08117-108">Dit onderwerp vindt u informatie over de mogelijke oorzaken Hallo en hoe toofix deze fouten.</span><span class="sxs-lookup"><span data-stu-id="08117-108">This topic provides you with information about hello possible causes and how toofix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="08117-109">Vernieuwen is mislukt</span><span class="sxs-lookup"><span data-stu-id="08117-109">Refresh failed</span></span> 
 
<span data-ttu-id="08117-110">**Hoe deze fout wordt opgehaald**: e-mailbericht met Power BI- of mislukte status in de geschiedenis van Hallo vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="08117-110">**How this error is surfaced**: Email from Power BI or failed status in hello refresh history.</span></span> 


| <span data-ttu-id="08117-111">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="08117-111">Cause</span></span> | <span data-ttu-id="08117-112">Hoe toofix</span><span class="sxs-lookup"><span data-stu-id="08117-112">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="08117-113">Fout fouten kunnen worden veroorzaakt wanneer de referenties op Hallo van Hallo gebruikers verbinding maken met het inhoudspakket toohello zijn opnieuw ingesteld, maar niet bijgewerkt in de verbindingsinstellingen Hallo Hallo van Hallo-inhoudspakket worden vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="08117-113">Refresh failure errors can be caused when hello credentials of hello users connecting toohello content pack have been reset but not updated in hello connection settings of hello of hello content pack.</span></span> | <span data-ttu-id="08117-114">Hallo gegevensset bijbehorende toohello Azure Active Directory-activiteit logboeken dashboard (Azure Active Directory-activiteit Logboeken) vinden in Power BI, kies schema vernieuwen en voer uw Azure AD-referenties.</span><span class="sxs-lookup"><span data-stu-id="08117-114">In Power BI, locate hello dataset corresponding toohello Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="08117-115">Vernieuwen kan mislukken vanwege toodata problemen in Hallo onderliggende inhoudspakket.</span><span class="sxs-lookup"><span data-stu-id="08117-115">A refresh can fail due toodata issues in hello underlying content pack.</span></span> | <span data-ttu-id="08117-116">Een ondersteuningsticket-bestand.</span><span class="sxs-lookup"><span data-stu-id="08117-116">File a support ticket.</span></span> <span data-ttu-id="08117-117">Zie voor meer informatie [hoe tooget ondersteuning bieden voor Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="08117-117">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a><span data-ttu-id="08117-118">Mislukte tooupdate referenties voor gegevensbron</span><span class="sxs-lookup"><span data-stu-id="08117-118">Failed tooupdate data source credentials</span></span> 
 
<span data-ttu-id="08117-119">**Hoe deze fout wordt opgehaald**: In Power BI, wanneer u verbinding toohello Azure Active Directory-activiteit Logboeken (preview)-inhoudspakket maakt.</span><span class="sxs-lookup"><span data-stu-id="08117-119">**How this error is surfaced**: In Power BI, when you are connecting toohello Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="08117-120">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="08117-120">Cause</span></span> | <span data-ttu-id="08117-121">Hoe toofix</span><span class="sxs-lookup"><span data-stu-id="08117-121">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="08117-122">de gebruiker verbinding maakt Hallo is een globale beheerder noch een lezer beveiliging of een beheerder beveiliging.</span><span class="sxs-lookup"><span data-stu-id="08117-122">hello connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="08117-123">Gebruik een account dat een globale beheerder of een lezer beveiliging of een beveiliging admin tooaccess Hallo inhoudspakketten.</span><span class="sxs-lookup"><span data-stu-id="08117-123">Use an account that is either a global admin or a security reader or a security admin tooaccess hello content packs.</span></span> |
| <span data-ttu-id="08117-124">Uw tenant is niet een Premium-tenant of beschikt niet over ten minste één gebruiker met Premium-licentie bestand.</span><span class="sxs-lookup"><span data-stu-id="08117-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="08117-125">Een ondersteuningsticket-bestand.</span><span class="sxs-lookup"><span data-stu-id="08117-125">File a support ticket.</span></span> <span data-ttu-id="08117-126">Zie voor meer informatie [hoe tooget ondersteuning bieden voor Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="08117-126">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="08117-127">Importeren van gegevens duurt te lang is</span><span class="sxs-lookup"><span data-stu-id="08117-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="08117-128">**Hoe deze fout wordt opgehaald**: In Power BI zodra u verbinding hebt gemaakt met uw inhoudspakket importproces Hallo gestart tooprepare uw dashboard voor Azure Active Directory-logboek.</span><span class="sxs-lookup"><span data-stu-id="08117-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, hello data import process starts tooprepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="08117-129">U ziet het Hallo-bericht: '*importeren van gegevens...* '</span><span class="sxs-lookup"><span data-stu-id="08117-129">You see hello message: “*Importing data...*”</span></span>  

| <span data-ttu-id="08117-130">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="08117-130">Cause</span></span> | <span data-ttu-id="08117-131">Hoe toofix</span><span class="sxs-lookup"><span data-stu-id="08117-131">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="08117-132">Afhankelijk van de grootte van de Hallo van uw tenant, kan deze stap duren een paar minuten too30 minuten.</span><span class="sxs-lookup"><span data-stu-id="08117-132">Depending on hello size of your tenant, this step could take anywhere from a few mins too30 minutes.</span></span> | <span data-ttu-id="08117-133">NET worden geduld.</span><span class="sxs-lookup"><span data-stu-id="08117-133">Just be patient.</span></span> <span data-ttu-id="08117-134">Als het Hallo-bericht niet tooshowing uw dashboard binnen een uur verandert, moet u een ondersteuningsticket bestand.</span><span class="sxs-lookup"><span data-stu-id="08117-134">If hello message does not change tooshowing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="08117-135">Zie voor meer informatie [hoe tooget ondersteuning bieden voor Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="08117-135">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="08117-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08117-136">Next steps</span></span>

<span data-ttu-id="08117-137">tooinstall hello Power BI-inhoudspakket voor Azure Active Directory-Preview, klikt u op [hier](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="08117-137">tooinstall hello Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


