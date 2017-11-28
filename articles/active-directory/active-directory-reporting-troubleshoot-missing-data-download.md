---
title: 'Voor probleemoplossing: Ontbrekende gegevens in Hallo gedownload Azure Active Directory-activiteitenlogboeken | Microsoft Docs'
description: Biedt u de gegevens van een oplossing toomissing in gedownloade activiteitenlogboeken van Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a><span data-ttu-id="d0c47-103">Ik kan geen gegevens vinden in hello Azure Active Directory-activiteitenlogboeken die ik heb gedownload</span><span class="sxs-lookup"><span data-stu-id="d0c47-103">I can’t find any data in hello Azure Active Directory activity logs I have downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="d0c47-104">Symptomen</span><span class="sxs-lookup"><span data-stu-id="d0c47-104">Symptoms</span></span>

<span data-ttu-id="d0c47-105">Ik Hallo activiteitenlogboeken (audit of aanmeldingen) gedownload en alle Hallo records wordt niet weergegeven voor Hallo keer gekozen.</span><span class="sxs-lookup"><span data-stu-id="d0c47-105">I downloaded hello activity logs (audit or sign-ins) and I don’t see all hello records for hello time I chose.</span></span> <span data-ttu-id="d0c47-106">Hoe komt dat?</span><span class="sxs-lookup"><span data-stu-id="d0c47-106">Why?</span></span> 

 ![Rapportage](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="d0c47-108">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d0c47-108">Cause</span></span>

<span data-ttu-id="d0c47-109">Wanneer u activiteitenlogboeken in hello Azure-portal hebt gedownload, beperken we Hallo scale too120K records, gesorteerd op basis van de meeste recente.</span><span class="sxs-lookup"><span data-stu-id="d0c47-109">When you download activity logs in hello Azure portal, we limit hello scale too120K records, sorted by most recent.</span></span> 

## <a name="resolution"></a><span data-ttu-id="d0c47-110">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d0c47-110">Resolution</span></span>

<span data-ttu-id="d0c47-111">U kunt gebruikmaken van [Azure AD rapportage-API's](active-directory-reporting-api-getting-started.md) toofetch tooa miljoen records op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="d0c47-111">You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) toofetch up tooa million records at any given point.</span></span> <span data-ttu-id="d0c47-112">De aanbevolen aanpak is toorun een script dat op vaste tijden die Hallo rapportage-API's toofetch aanroept op incrementele wijze gedurende een periode registreert (bijvoorbeeld dagelijks of wekelijks).</span><span class="sxs-lookup"><span data-stu-id="d0c47-112">Our recommended approach is toorun a script on a scheduled basis that calls hello reporting APIs toofetch records in an incremental fashion over a period of time (e.g., daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0c47-113">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d0c47-113">Next steps</span></span>
<span data-ttu-id="d0c47-114">Zie Hallo [Azure Active Directory-rapportage Veelgestelde vragen over](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="d0c47-114">See hello [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

