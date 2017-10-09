---
title: aaaHow toocomplete een onderzoek toegang | Microsoft Docs
description: Nadat u een revisie toegang in Azure AD Privileged Identity Management gestart, informatie over hoe toocomplete deze en bekijkt hello resultaten
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="2afa5-103">Hoe toocomplete een toegang controleren in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="2afa5-103">How toocomplete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="2afa5-104">Bevoorrechte rol beheerders kunnen bekijken voor bevoorrechte toegang eenmaal een [beveiligingsbeoordeling is gestart](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="2afa5-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="2afa5-105">Azure AD Privileged Identity Management (PIM) stuurt automatisch een e-mailbericht waarin wordt gevraagd tooreview gebruikers toegang krijgen.</span><span class="sxs-lookup"><span data-stu-id="2afa5-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users tooreview their access.</span></span> <span data-ttu-id="2afa5-106">Als een gebruiker niet een e-mailbericht ontvangt is, kunt u deze instructies Hallo in verzenden [hoe tooperform beveiliging controleren](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="2afa5-106">If a user did not get an email, you can send them hello instructions in [how tooperform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="2afa5-107">Nadat Hallo beveiliging controleren periode of alle gebruikers van Hallo klaar bent met hun eigen bekijken, Hallo stappen in dit artikel hebt gecontroleerd toomanage hello en Hallo resultaten te zien.</span><span class="sxs-lookup"><span data-stu-id="2afa5-107">After hello security review period is over, or all hello users have finished their self-review, follow hello steps in this article toomanage hello review and see hello results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="2afa5-108">Beoordelingen van beveiliging beheren</span><span class="sxs-lookup"><span data-stu-id="2afa5-108">Manage security reviews</span></span>
1. <span data-ttu-id="2afa5-109">Ga toohello [Azure-portal](https://portal.azure.com/) en selecteer Hallo **Azure AD Privileged Identity Management** toepassing op uw dashboard.</span><span class="sxs-lookup"><span data-stu-id="2afa5-109">Go toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="2afa5-110">Selecteer Hallo **toegang tot beoordelingen** sectie van het Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="2afa5-110">Select hello **Access reviews** section of hello dashboard.</span></span>
3. <span data-ttu-id="2afa5-111">Selecteer Hallo toegang controleren dat u wilt dat toomanage.</span><span class="sxs-lookup"><span data-stu-id="2afa5-111">Select hello access review that you want toomanage.</span></span>

<span data-ttu-id="2afa5-112">Op Hallo toegang controleren detail blade zijn er een aantal opties voor het beheren van deze evaluatie.</span><span class="sxs-lookup"><span data-stu-id="2afa5-112">On hello access review's detail blade there are a number options for managing that review.</span></span>

![PIM toegang controleren knoppen - schermafbeelding][1]

### <a name="remind"></a><span data-ttu-id="2afa5-114">Herinneren</span><span class="sxs-lookup"><span data-stu-id="2afa5-114">Remind</span></span>
<span data-ttu-id="2afa5-115">Als een evaluatie van de toegang is ingesteld zodat Hallo gebruikers zelf bekijken, Hallo **herinnering sturen** knop verstuurt een melding.</span><span class="sxs-lookup"><span data-stu-id="2afa5-115">If an access review is set up so that hello users review themselves, hello **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="2afa5-116">Stoppen</span><span class="sxs-lookup"><span data-stu-id="2afa5-116">Stop</span></span>
<span data-ttu-id="2afa5-117">Alle beoordelingen van toegang tot een einddatum hebben, maar kunt u Hallo **stoppen** knop toofinish deze vroeg.</span><span class="sxs-lookup"><span data-stu-id="2afa5-117">All access reviews have an end date, but you can use hello **Stop** button toofinish it early.</span></span> <span data-ttu-id="2afa5-118">Als gebruikers zich nog niet is gecontroleerd op dit tijdstip, ze niet kunnen tooafter u stopt met het Hallo-revisie.</span><span class="sxs-lookup"><span data-stu-id="2afa5-118">If any users haven't been reviewed by this time, they won't be able tooafter you stop hello review.</span></span> <span data-ttu-id="2afa5-119">U kunt een beoordeling niet opnieuw starten nadat deze gestopt.</span><span class="sxs-lookup"><span data-stu-id="2afa5-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="2afa5-120">Aanvragen</span><span class="sxs-lookup"><span data-stu-id="2afa5-120">Apply</span></span>
<span data-ttu-id="2afa5-121">Nadat een revisie access is voltooid, ofwel omdat u Hallo-einddatum is bereikt of handmatig gestopt Hallo **toepassen** knop Hallo resultaten van Hallo onderzoek implementeert.</span><span class="sxs-lookup"><span data-stu-id="2afa5-121">After an access review is completed, either because you reached hello end date or stopped it manually, hello **Apply** button implements hello outcome of hello review.</span></span> <span data-ttu-id="2afa5-122">Als een gebruiker toegang is geweigerd Hallo gecontroleerd, is dit Hallo stap die hun roltoewijzing wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2afa5-122">If a user's access was denied in hello review, this is hello step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="2afa5-123">Exporteren</span><span class="sxs-lookup"><span data-stu-id="2afa5-123">Export</span></span>
<span data-ttu-id="2afa5-124">Als u handmatig tooapply Hallo resultaten van beveiligingsbeoordeling hello wilt, kunt u Hallo revisie exporteren.</span><span class="sxs-lookup"><span data-stu-id="2afa5-124">If you want tooapply hello results of hello security review manually, you can export hello review.</span></span> <span data-ttu-id="2afa5-125">Hallo **exporteren** knop downloaden van een CSV-bestand wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2afa5-125">hello **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="2afa5-126">Hallo resultaten in Excel of andere programma's die CSV-bestanden worden geopend, kunt u beheren.</span><span class="sxs-lookup"><span data-stu-id="2afa5-126">You can manage hello results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="2afa5-127">Verwijderen</span><span class="sxs-lookup"><span data-stu-id="2afa5-127">Delete</span></span>
<span data-ttu-id="2afa5-128">Als u niet bent geïnteresseerd in Hallo nader bekijken, verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2afa5-128">If you are not interested in hello review any further, delete it.</span></span> <span data-ttu-id="2afa5-129">Hallo **verwijderen** knop Hallo revisie verwijdert uit Hallo PIM-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2afa5-129">hello **Delete** button removes hello review from hello PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2afa5-130">U wordt niet ophalen van een waarschuwing alvorens deze wordt verwijderd, dus wees zeker dat u wilt dat toodelete die bekijken.</span><span class="sxs-lookup"><span data-stu-id="2afa5-130">You will not get a warning before deletion occurs, so be sure that you want toodelete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2afa5-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2afa5-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
