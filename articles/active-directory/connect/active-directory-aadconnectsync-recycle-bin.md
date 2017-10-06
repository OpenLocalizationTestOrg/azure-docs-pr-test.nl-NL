---
title: 'Azure AD Connect-synchronisatie: AD-Prullenbak inschakelen | Microsoft Docs'
description: In dit onderwerp adviseert Hallo gebruik van AD-Prullenbak-functie met Azure AD Connect.
services: active-directory
keywords: Prullenbak van AD, per ongeluk verwijderen, bronanker
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="9aebc-104">Azure AD Connect-synchronisatie: AD-Prullenbak inschakelen</span><span class="sxs-lookup"><span data-stu-id="9aebc-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="9aebc-105">Het verdient aanbeveling dat u voor uw lokale Active Directory's die gesynchroniseerd tooAzure AD zijn Hallo AD-Prullenbak-functie inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9aebc-105">It is recommended that you enable hello AD Recycle Bin feature for your on-premises Active Directories, which are synchronized tooAzure AD.</span></span> 

<span data-ttu-id="9aebc-106">Als u een on-premises per ongeluk hebt verwijderd AD-gebruiker-object maken en terugzetten met de functie hello, Azure AD worden hersteld Hallo bijbehorende Azure AD-gebruikersobject.</span><span class="sxs-lookup"><span data-stu-id="9aebc-106">If you accidentally deleted an on-premises AD user object and restore it using hello feature, Azure AD restores hello corresponding Azure AD user object.</span></span>  <span data-ttu-id="9aebc-107">Raadpleeg voor informatie over de functie Prullenbak Hallo AD tooarticle [Scenario-overzicht voor het herstellen van verwijderde Active Directory-objecten](https://technet.microsoft.com/library/dd379542.aspx).</span><span class="sxs-lookup"><span data-stu-id="9aebc-107">For information about hello AD Recycle Bin feature, refer tooarticle [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a><span data-ttu-id="9aebc-108">Prullenbak van de voordelen van het Hallo AD inschakelen</span><span class="sxs-lookup"><span data-stu-id="9aebc-108">Benefits of enabling hello AD recycle bin</span></span>
<span data-ttu-id="9aebc-109">Deze functie helpt bij het herstellen van objecten voor Azure AD-gebruiker door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="9aebc-109">This feature helps with restoring Azure AD user objects by doing hello following:</span></span>

* <span data-ttu-id="9aebc-110">Als u een on-premises per ongeluk hebt verwijderd AD-gebruiker object, bijbehorende Azure AD-gebruikersobject Hallo verwijderd in Hallo volgende synchronisatiecyclus.</span><span class="sxs-lookup"><span data-stu-id="9aebc-110">If you accidentally deleted an on-premises AD user object, hello corresponding Azure AD user object will be deleted in hello next sync cycle.</span></span> <span data-ttu-id="9aebc-111">Standaard houdt Azure AD verwijderd hello Azure AD-gebruikersobject voorlopig verwijderde status heeft voor 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="9aebc-111">By default, Azure AD keeps hello deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="9aebc-112">Als u beschikt over on-premises AD-Prullenbak-functie is ingeschakeld, kunt u Hallo verwijderd herstellen lokale AD-gebruiker-object zonder dat u de waarde Bronanker wijzigt.</span><span class="sxs-lookup"><span data-stu-id="9aebc-112">If you have on-premises AD Recycle Bin feature enabled, you can restore hello deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="9aebc-113">Wanneer Hallo hersteld lokale AD-gebruiker-object is gesynchroniseerd tooAzure AD, Azure AD wordt hersteld Hallo overeenkomt voorlopig verwijderde Azure AD-gebruiker-object.</span><span class="sxs-lookup"><span data-stu-id="9aebc-113">When hello recovered on-premises AD user object is synchronized tooAzure AD, Azure AD will restore hello corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="9aebc-114">Raadpleeg voor informatie over Bronanker kenmerk tooarticle [Azure AD Connect: concepten ontwerpen](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="9aebc-114">For information about Source Anchor attribute, refer tooarticle [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="9aebc-115">Als u geen lokale AD Recycle Bin functie is ingeschakeld, hebt u mogelijk vereist toocreate een AD-object tooreplace Hallo verwijderde gebruikersobject.</span><span class="sxs-lookup"><span data-stu-id="9aebc-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required toocreate an AD user object tooreplace hello deleted object.</span></span> <span data-ttu-id="9aebc-116">Als Azure AD Connect-synchronisatieservice geconfigureerde toouse systeem gegenereerde AD kenmerk is (zoals ObjectGuid) voor Hallo Bronanker kenmerk, wordt hello gemaakte AD-gebruiker-object niet hebben Hallo dezelfde Bronanker-waarde als Hallo AD-gebruikersobject verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9aebc-116">If Azure AD Connect Synchronization Service is configured toouse system-generated AD attribute (such as ObjectGuid) for hello Source Anchor attribute, hello newly created AD user object will not have hello same Source Anchor value as hello deleted AD user object.</span></span> <span data-ttu-id="9aebc-117">Wanneer hello gemaakte object voor AD-gebruiker gesynchroniseerd tooAzure AD is, Azure AD maakt een nieuw object van de Azure AD-gebruiker in plaats van Azure AD-gebruikersobject Hallo voorlopig verwijderde herstellen.</span><span class="sxs-lookup"><span data-stu-id="9aebc-117">When hello newly created AD user object is synchronized tooAzure AD, Azure AD creates a new Azure AD user object instead of restoring hello soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="9aebc-118">Standaard verwijderd Azure AD houdt objecten van Azure AD-gebruiker in staat voorlopig verwijderde voor 30 dagen voordat ze worden permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9aebc-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="9aebc-119">Beheerders kunnen echter Hallo verwijderen van dergelijke objecten te versnellen.</span><span class="sxs-lookup"><span data-stu-id="9aebc-119">However, administrators can accelerate hello deletion of such objects.</span></span> <span data-ttu-id="9aebc-120">Zodra het Hallo-objecten worden permanent verwijderd, kunnen ze niet meer worden hersteld, zelfs als lokale AD-Prullenbak-functie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9aebc-120">Once hello objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="9aebc-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9aebc-121">Next steps</span></span>
<span data-ttu-id="9aebc-122">**Overzichtsonderwerpen**</span><span class="sxs-lookup"><span data-stu-id="9aebc-122">**Overview topics**</span></span>

* [<span data-ttu-id="9aebc-123">Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="9aebc-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="9aebc-124">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9aebc-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
