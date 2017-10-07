---
title: aaaHow toouse Hallo auditlogboek in Azure AD Privileged Identity Management | Microsoft Docs
description: Meer informatie over hoe toouse Hallo van het controlelogboek in hello Azure Privileged Identity Management-uitbreiding.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a><span data-ttu-id="8bde7-103">Met behulp van het controlelogboek Hallo in PIM</span><span class="sxs-lookup"><span data-stu-id="8bde7-103">Using hello audit log in PIM</span></span>
<span data-ttu-id="8bde7-104">U kunt Hallo Privileged Identity Management (PIM) audit log toosee alle Hallo gebruikerstoewijzingen en activeringen binnen een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="8bde7-104">You can use hello Privileged Identity Management (PIM) audit log toosee all hello user assignments and activations within a given time period.</span></span> <span data-ttu-id="8bde7-105">Als u wilt dat toosee Hallo volledige controlegeschiedenis van activiteit in uw tenant, met inbegrip van de beheerder, eindgebruikers en synchronisatieactiviteiten, kunt u Hallo [Azure Active Directory-toegang en gebruik rapporten.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="8bde7-105">If you want toosee hello full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use hello [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-toohello-audit-log"></a><span data-ttu-id="8bde7-106">Het controlelogboek toohello navigeren</span><span class="sxs-lookup"><span data-stu-id="8bde7-106">Navigate toohello audit log</span></span>
<span data-ttu-id="8bde7-107">Van Hallo [Azure-portal](https://portal.azure.com) dashboard, selecteer Hallo **Azure AD Privileged Identity Management** app.</span><span class="sxs-lookup"><span data-stu-id="8bde7-107">From hello [Azure portal](https://portal.azure.com) dashboard, select hello **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="8bde7-108">Van daaruit toegang krijgen tot het controlelogboek Hallo door te klikken op **bevoorrechte rollen beheren** > **controlegeschiedenis** in Hallo PIM-dashboard.</span><span class="sxs-lookup"><span data-stu-id="8bde7-108">From there, access hello audit log by clicking **Manage privileged roles** > **Audit history** in hello PIM dashboard.</span></span>

## <a name="hello-audit-log-graph"></a><span data-ttu-id="8bde7-109">Hallo audit log-grafiek</span><span class="sxs-lookup"><span data-stu-id="8bde7-109">hello audit log graph</span></span>
<span data-ttu-id="8bde7-110">U kunt Hallo audit log tooview Hallo totaal activeringen, max activeringen per dag en gemiddelde activeringen per dag gebruiken in een lijndiagram.</span><span class="sxs-lookup"><span data-stu-id="8bde7-110">You can use hello audit log tooview hello total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="8bde7-111">U kunt ook Hallo gegevens filteren per rol als er meer dan één rol in de controlegeschiedenis Hallo.</span><span class="sxs-lookup"><span data-stu-id="8bde7-111">You can also filter hello data by role if there is more than one role in hello audit history.</span></span>

<span data-ttu-id="8bde7-112">Gebruik Hallo **tijd**, **actie**, en **rol** knoppen toosort Hallo logboek.</span><span class="sxs-lookup"><span data-stu-id="8bde7-112">Use hello **time**, **action**, and **role** buttons toosort hello log.</span></span>

## <a name="hello-audit-log-list"></a><span data-ttu-id="8bde7-113">Hallo audit log-lijst</span><span class="sxs-lookup"><span data-stu-id="8bde7-113">hello audit log list</span></span>
<span data-ttu-id="8bde7-114">Hallo-kolommen in Hallo audit log lijst zijn:</span><span class="sxs-lookup"><span data-stu-id="8bde7-114">hello columns in hello audit log list are:</span></span>

* <span data-ttu-id="8bde7-115">**Aanvrager** -Hallo-gebruiker die heeft aangevraagd Hallo rol activeren of wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8bde7-115">**Requestor** - hello user who requested hello role activation or change.</span></span>  <span data-ttu-id="8bde7-116">Als het Hallo-waarde is 'Azure systeem', controleert u hello Azure controlelogboek voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8bde7-116">If hello value is "Azure System", check hello Azure audit log for more information.</span></span>
* <span data-ttu-id="8bde7-117">**Gebruiker** -Hallo-gebruiker die wordt geactiveerd of tooa rol is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8bde7-117">**User** - hello user who is activating or assigned tooa role.</span></span>
* <span data-ttu-id="8bde7-118">**Rol** -Hallo rol toegewezen of geactiveerd door Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8bde7-118">**Role** - hello role assigned or activated by hello user.</span></span>
* <span data-ttu-id="8bde7-119">**Actie** - Hallo-acties die door de aanvrager Hallo.</span><span class="sxs-lookup"><span data-stu-id="8bde7-119">**Action** - hello actions taken by hello requestor.</span></span> <span data-ttu-id="8bde7-120">Het kan hierbij gaan toewijzing, ongedaan maken, activeren of deactiveren.</span><span class="sxs-lookup"><span data-stu-id="8bde7-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="8bde7-121">**Tijd** : wanneer het Hallo-actie is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="8bde7-121">**Time** - when hello action occurred.</span></span>
* <span data-ttu-id="8bde7-122">**Redeneren** -als de tekst in Hallo reden veld is ingevoerd tijdens de activering, deze hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8bde7-122">**Reasoning** - if any text was entered into hello reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="8bde7-123">**Vervaldatum** - alleen relevant voor de activering van rollen.</span><span class="sxs-lookup"><span data-stu-id="8bde7-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-hello-audit-log"></a><span data-ttu-id="8bde7-124">Hallo-controlelogboek filteren</span><span class="sxs-lookup"><span data-stu-id="8bde7-124">Filter hello audit log</span></span>
<span data-ttu-id="8bde7-125">U kunt Hallo informatie filteren die wordt weergegeven in het controlelogboek Hallo door te klikken op Hallo **Filter** knop.</span><span class="sxs-lookup"><span data-stu-id="8bde7-125">You can filter hello information that shows up in hello audit log by clicking hello **Filter** button.</span></span>  <span data-ttu-id="8bde7-126">Hallo **Update grafiek parameters blade** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8bde7-126">hello **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="8bde7-127">Wanneer u filters Hallo ingesteld, klikt u op **Update** toofilter Hallo gegevens in Hallo logboek.</span><span class="sxs-lookup"><span data-stu-id="8bde7-127">After you set hello filters, click **Update** toofilter hello data in hello log.</span></span>  <span data-ttu-id="8bde7-128">Als het Hallo-gegevens worden niet meteen weergegeven, moet u Hallo pagina vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="8bde7-128">If hello data doesn't appear right away, refresh hello page.</span></span>

### <a name="change-hello-date-range"></a><span data-ttu-id="8bde7-129">Hallo datumbereik wijzigen</span><span class="sxs-lookup"><span data-stu-id="8bde7-129">Change hello date range</span></span>
<span data-ttu-id="8bde7-130">Gebruik Hallo **vandaag**, **afgelopen Week**, **afgelopen maand**, of **aangepaste** toochange Hallo tijdsbereik van het controlelogboek Hallo knoppen.</span><span class="sxs-lookup"><span data-stu-id="8bde7-130">Use hello **Today**, **Past Week**, **Past Month**, or **Custom** buttons toochange hello time range of hello audit log.</span></span>

<span data-ttu-id="8bde7-131">Wanneer u kiest voor Hallo **aangepaste** knop, krijgt u een **van** datumveld en een **naar** veld toospecify een datumbereik voor Hallo logboek datum.</span><span class="sxs-lookup"><span data-stu-id="8bde7-131">When you choose hello **Custom** button, you will be given a **From** date field and a **To** date field toospecify a range of dates for hello log.</span></span>  <span data-ttu-id="8bde7-132">U kunt Hallo datums opgeven in de notatie DD-MM-jjjj of klik op Hallo **kalender** pictogram en kies Hallo datum in een kalender.</span><span class="sxs-lookup"><span data-stu-id="8bde7-132">You can either enter hello dates in MM/DD/YYYY format or click on hello **calendar** icon and choose hello date from a calendar.</span></span>

### <a name="change-hello-roles-included-in-hello-log"></a><span data-ttu-id="8bde7-133">Hallo-functies die zijn opgenomen in het logboek Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="8bde7-133">Change hello roles included in hello log</span></span>
<span data-ttu-id="8bde7-134">Schakel Hallo of **rol** zich aanmelden op Hallo selectievakje volgende tooeach rol tooinclude of uitsluiten.</span><span class="sxs-lookup"><span data-stu-id="8bde7-134">Check or uncheck hello **Role** checkbox next tooeach role tooinclude or exclude it from hello log.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="8bde7-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8bde7-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

