---
title: 'Probleemoplossing: Ontbrekende gegevens in activiteitenlogboeken van Azure Active Directory | Microsoft Docs'
description: Bevat een lijst met de diverse beschikbare rapporten voor Azure Active Directory
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 7cbe4337-bb77-4ee0-b254-3e368be06db7
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 47617f8f727027de113a0f503308c8accc58859e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="i-cant-find-some-actions-that-i-performed-in-the-azure-active-directory-activity-log"></a><span data-ttu-id="ea2d5-103">Ik kan een aantal acties die ik heb uitgevoerd, niet terugvinden in de activiteitenlogboeken van Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea2d5-103">I can’t find some actions that I performed in the Azure Active Directory activity log</span></span>


## <a name="symptoms"></a><span data-ttu-id="ea2d5-104">Symptomen</span><span class="sxs-lookup"><span data-stu-id="ea2d5-104">Symptoms</span></span>

<span data-ttu-id="ea2d5-105">Ik heb enkele acties uitgevoerd in Azure Portal en had verwacht de auditlogboeken voor deze acties te zien op de blade `Activity logs > Audit Logs`, maar ik kan ze niet vinden.</span><span class="sxs-lookup"><span data-stu-id="ea2d5-105">I performed some actions in the Azure portal and expected to see the audit logs for those actions in the `Activity logs > Audit Logs` blade, but I can’t find them.</span></span>

 ![Rapportage](./media/active-directory-reporting-troubleshoot-missing-audit-data/01.png)
 

## <a name="cause"></a><span data-ttu-id="ea2d5-107">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="ea2d5-107">Cause</span></span>

<span data-ttu-id="ea2d5-108">Acties worden niet direct weergegeven in het auditlogboek voor activiteiten.</span><span class="sxs-lookup"><span data-stu-id="ea2d5-108">Actions don’t appear immediately in the Activity Audit log.</span></span> <span data-ttu-id="ea2d5-109">Vanaf het moment dat de bewerking is uitgevoerd, kan het tussen 15 minuten tot een uur duren voordat de auditlogboeken beschikbaar zijn in de portal.</span><span class="sxs-lookup"><span data-stu-id="ea2d5-109">It can take anywhere from 15 minutes to an hour to see the audit logs in the portal from the time the operation is performed.</span></span>

## <a name="resolution"></a><span data-ttu-id="ea2d5-110">Oplossing</span><span class="sxs-lookup"><span data-stu-id="ea2d5-110">Resolution</span></span>

<span data-ttu-id="ea2d5-111">Wacht 15 minuten tot een uur en kijk of de acties nu wel worden vermeld in het logboek.</span><span class="sxs-lookup"><span data-stu-id="ea2d5-111">Wait for 15 minutes to an hour and see if the actions appear in the log.</span></span> <span data-ttu-id="ea2d5-112">Als u ze nog steeds niet ziet, kunt u een ondersteuningsaanvraag indien en dan zullen we ernaar kijken.</span><span class="sxs-lookup"><span data-stu-id="ea2d5-112">If you still don’t see them, please raise a support ticket with us and we will look into it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ea2d5-113">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ea2d5-113">Next steps</span></span>
<span data-ttu-id="ea2d5-114">Zie [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md) (Veelgestelde vragen over Azure Active Directory-rapportage).</span><span class="sxs-lookup"><span data-stu-id="ea2d5-114">See the [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

