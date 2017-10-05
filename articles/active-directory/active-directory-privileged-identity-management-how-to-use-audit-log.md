---
title: Het gebruik van het controlelogboek in Azure AD Privileged Identity Management | Microsoft Docs
description: Informatie over het gebruik van het controlelogboek in de extensie Azure Privileged Identity Management.
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
ms.openlocfilehash: 7d9a5255a64d46c1388d328a606b3f297d61262b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-audit-log-in-pim"></a><span data-ttu-id="d52e8-103">Met behulp van het controlelogboek in PIM</span><span class="sxs-lookup"><span data-stu-id="d52e8-103">Using the audit log in PIM</span></span>
<span data-ttu-id="d52e8-104">U kunt het controlelogboek Privileged Identity Management (PIM) gebruiken om te zien van de toewijzingen van gebruikers en activeringen binnen een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="d52e8-104">You can use the Privileged Identity Management (PIM) audit log to see all the user assignments and activations within a given time period.</span></span> <span data-ttu-id="d52e8-105">Als u zien van de volledige controlegeschiedenis van activiteit in uw tenant wilt, met inbegrip van de beheerder, eindgebruikers en synchronisatieactiviteiten, kunt u de [Azure Active Directory-toegang en gebruik rapporten.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="d52e8-105">If you want to see the full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use the [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-to-the-audit-log"></a><span data-ttu-id="d52e8-106">Navigeer naar het controlelogboek</span><span class="sxs-lookup"><span data-stu-id="d52e8-106">Navigate to the audit log</span></span>
<span data-ttu-id="d52e8-107">Van de [Azure-portal](https://portal.azure.com) dashboard, selecteer de **Azure AD Privileged Identity Management** app.</span><span class="sxs-lookup"><span data-stu-id="d52e8-107">From the [Azure portal](https://portal.azure.com) dashboard, select the **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="d52e8-108">Van daaruit toegang krijgen tot het controlelogboek door te klikken op **bevoorrechte rollen beheren** > **controlegeschiedenis** in het PIM-dashboard.</span><span class="sxs-lookup"><span data-stu-id="d52e8-108">From there, access the audit log by clicking **Manage privileged roles** > **Audit history** in the PIM dashboard.</span></span>

## <a name="the-audit-log-graph"></a><span data-ttu-id="d52e8-109">De audit log-grafiek</span><span class="sxs-lookup"><span data-stu-id="d52e8-109">The audit log graph</span></span>
<span data-ttu-id="d52e8-110">Het controlelogboek kunt u het totale aantal activeringen, max activeringen per dag en gemiddelde activeringen per dag weergeven in een lijndiagram.</span><span class="sxs-lookup"><span data-stu-id="d52e8-110">You can use the audit log to view the total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="d52e8-111">U kunt ook de gegevens filteren per rol als er meer dan één rol in de controlegeschiedenis.</span><span class="sxs-lookup"><span data-stu-id="d52e8-111">You can also filter the data by role if there is more than one role in the audit history.</span></span>

<span data-ttu-id="d52e8-112">Gebruik de **tijd**, **actie**, en **rol** knoppen om te sorteren van het logboek.</span><span class="sxs-lookup"><span data-stu-id="d52e8-112">Use the **time**, **action**, and **role** buttons to sort the log.</span></span>

## <a name="the-audit-log-list"></a><span data-ttu-id="d52e8-113">De lijst van de controle-logboek</span><span class="sxs-lookup"><span data-stu-id="d52e8-113">The audit log list</span></span>
<span data-ttu-id="d52e8-114">De kolommen in de lijst van audit log zijn:</span><span class="sxs-lookup"><span data-stu-id="d52e8-114">The columns in the audit log list are:</span></span>

* <span data-ttu-id="d52e8-115">**Aanvrager** -de gebruiker die de rol activeren of wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d52e8-115">**Requestor** - the user who requested the role activation or change.</span></span>  <span data-ttu-id="d52e8-116">Als de waarde is 'Azure systeem', controleert u het controlelogboek voor Azure voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d52e8-116">If the value is "Azure System", check the Azure audit log for more information.</span></span>
* <span data-ttu-id="d52e8-117">**Gebruiker** -de gebruiker die geactiveerd of is toegewezen aan een rol is.</span><span class="sxs-lookup"><span data-stu-id="d52e8-117">**User** - the user who is activating or assigned to a role.</span></span>
* <span data-ttu-id="d52e8-118">**Rol** -de rol toegewezen of geactiveerd door de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d52e8-118">**Role** - the role assigned or activated by the user.</span></span>
* <span data-ttu-id="d52e8-119">**Actie** : de acties die door de aanvrager.</span><span class="sxs-lookup"><span data-stu-id="d52e8-119">**Action** - the actions taken by the requestor.</span></span> <span data-ttu-id="d52e8-120">Het kan hierbij gaan toewijzing, ongedaan maken, activeren of deactiveren.</span><span class="sxs-lookup"><span data-stu-id="d52e8-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="d52e8-121">**Tijd** : wanneer de actie is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="d52e8-121">**Time** - when the action occurred.</span></span>
* <span data-ttu-id="d52e8-122">**Redeneren** -als de tekst in het veld reden is ingevoerd tijdens de activering, deze hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d52e8-122">**Reasoning** - if any text was entered into the reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="d52e8-123">**Vervaldatum** - alleen relevant voor de activering van rollen.</span><span class="sxs-lookup"><span data-stu-id="d52e8-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-the-audit-log"></a><span data-ttu-id="d52e8-124">Het controlelogboek filteren</span><span class="sxs-lookup"><span data-stu-id="d52e8-124">Filter the audit log</span></span>
<span data-ttu-id="d52e8-125">U kunt de informatie filteren die wordt weergegeven in het controlelogboek door te klikken op de **Filter** knop.</span><span class="sxs-lookup"><span data-stu-id="d52e8-125">You can filter the information that shows up in the audit log by clicking the **Filter** button.</span></span>  <span data-ttu-id="d52e8-126">De **Update grafiek parameters blade** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d52e8-126">The **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="d52e8-127">Nadat u de filters hebt ingesteld, klikt u op **Update** om de gegevens in het logboek te filteren.</span><span class="sxs-lookup"><span data-stu-id="d52e8-127">After you set the filters, click **Update** to filter the data in the log.</span></span>  <span data-ttu-id="d52e8-128">Als de gegevens niet meteen weergegeven, vernieuw de pagina.</span><span class="sxs-lookup"><span data-stu-id="d52e8-128">If the data doesn't appear right away, refresh the page.</span></span>

### <a name="change-the-date-range"></a><span data-ttu-id="d52e8-129">Wijzig het datumbereik</span><span class="sxs-lookup"><span data-stu-id="d52e8-129">Change the date range</span></span>
<span data-ttu-id="d52e8-130">Gebruik de **vandaag**, **afgelopen Week**, **afgelopen maand**, of **aangepaste** knoppen om te wijzigen van het tijdsbereik van het controlelogboek.</span><span class="sxs-lookup"><span data-stu-id="d52e8-130">Use the **Today**, **Past Week**, **Past Month**, or **Custom** buttons to change the time range of the audit log.</span></span>

<span data-ttu-id="d52e8-131">Als u ervoor kiest de **aangepaste** knop, krijgt u een **van** datumveld en een **naar** datumveld om op te geven van een datumbereik voor het logboek.</span><span class="sxs-lookup"><span data-stu-id="d52e8-131">When you choose the **Custom** button, you will be given a **From** date field and a **To** date field to specify a range of dates for the log.</span></span>  <span data-ttu-id="d52e8-132">U kunt datums opgeven in de notatie DD-MM-jjjj of klik op de **kalender** pictogram en kies de datum in een kalender.</span><span class="sxs-lookup"><span data-stu-id="d52e8-132">You can either enter the dates in MM/DD/YYYY format or click on the **calendar** icon and choose the date from a calendar.</span></span>

### <a name="change-the-roles-included-in-the-log"></a><span data-ttu-id="d52e8-133">Wijzigen van de rollen die zijn opgenomen in het logboek</span><span class="sxs-lookup"><span data-stu-id="d52e8-133">Change the roles included in the log</span></span>
<span data-ttu-id="d52e8-134">Schakel of de **rol** selectievakje naast elke rol wilt opnemen of uitsluiten van het logboek.</span><span class="sxs-lookup"><span data-stu-id="d52e8-134">Check or uncheck the **Role** checkbox next to each role to include or exclude it from the log.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="d52e8-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d52e8-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

