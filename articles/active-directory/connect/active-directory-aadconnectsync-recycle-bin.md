---
title: 'Azure AD Connect-synchronisatie: AD-Prullenbak inschakelen | Microsoft Docs'
description: In dit onderwerp raadt het gebruik van de functie Prullenbak van AD met Azure AD Connect.
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
ms.openlocfilehash: eb455477547f3db8245cf3601576eba9c6fdc56f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="6a8c8-104">Azure AD Connect-synchronisatie: AD-Prullenbak inschakelen</span><span class="sxs-lookup"><span data-stu-id="6a8c8-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="6a8c8-105">Het is raadzaam dat u de Prullenbak van AD-functie inschakelen voor uw lokale Active Directory's die worden gesynchroniseerd naar Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a8c8-105">It is recommended that you enable the AD Recycle Bin feature for your on-premises Active Directories, which are synchronized to Azure AD.</span></span> 

<span data-ttu-id="6a8c8-106">Als u een on-premises per ongeluk hebt verwijderd AD-gebruiker-object maken en terugzetten met de functie, Azure AD worden hersteld het bijbehorende object van de Azure AD-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6a8c8-106">If you accidentally deleted an on-premises AD user object and restore it using the feature, Azure AD restores the corresponding Azure AD user object.</span></span>  <span data-ttu-id="6a8c8-107">Raadpleeg voor informatie over de Prullenbak van AD-functie, artikel [Scenario-overzicht voor het herstellen van verwijderde Active Directory-objecten](https://technet.microsoft.com/library/dd379542.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a8c8-107">For information about the AD Recycle Bin feature, refer to article [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-the-ad-recycle-bin"></a><span data-ttu-id="6a8c8-108">Voordelen van de AD-Prullenbak inschakelen</span><span class="sxs-lookup"><span data-stu-id="6a8c8-108">Benefits of enabling the AD recycle bin</span></span>
<span data-ttu-id="6a8c8-109">Deze functie helpt bij het herstellen van Azure AD-gebruikersobjecten als volgt:</span><span class="sxs-lookup"><span data-stu-id="6a8c8-109">This feature helps with restoring Azure AD user objects by doing the following:</span></span>

* <span data-ttu-id="6a8c8-110">Als u een on-premises per ongeluk hebt verwijderd object AD-gebruiker, het bijbehorende object van de Azure AD-gebruiker wordt verwijderd in de volgende synchronisatiecyclus.</span><span class="sxs-lookup"><span data-stu-id="6a8c8-110">If you accidentally deleted an on-premises AD user object, the corresponding Azure AD user object will be deleted in the next sync cycle.</span></span> <span data-ttu-id="6a8c8-111">Standaard Azure AD houdt het verwijderde object van Azure AD-gebruiker voorlopig verwijderde status voor 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="6a8c8-111">By default, Azure AD keeps the deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="6a8c8-112">Als u beschikt over on-premises AD Recycle Bin functie is ingeschakeld, kunt u de verwijderde herstellen lokale AD-gebruiker-object zonder dat u de waarde Bronanker wijzigt.</span><span class="sxs-lookup"><span data-stu-id="6a8c8-112">If you have on-premises AD Recycle Bin feature enabled, you can restore the deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="6a8c8-113">Wanneer de herstelde on-premises AD-gebruiker-object wordt gesynchroniseerd naar Azure AD, Azure AD wordt gebruikersobject terugzetten van de bijbehorende voorlopig verwijderde Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a8c8-113">When the recovered on-premises AD user object is synchronized to Azure AD, Azure AD will restore the corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="6a8c8-114">Raadpleeg voor informatie over Bronanker kenmerk artikel [Azure AD Connect: concepten ontwerpen](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="6a8c8-114">For information about Source Anchor attribute, refer to article [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="6a8c8-115">Als u geen lokale AD-Prullenbak-functie is ingeschakeld, kan u worden gevraagd een AD-gebruikersobject ter vervanging van het verwijderde object te maken.</span><span class="sxs-lookup"><span data-stu-id="6a8c8-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required to create an AD user object to replace the deleted object.</span></span> <span data-ttu-id="6a8c8-116">Als Azure AD Connect-synchronisatieservice is geconfigureerd voor het systeem gegenereerde AD-kenmerk (zoals ObjectGuid) gebruiken voor het kenmerk Bronanker, is het gemaakte object van de AD-gebruiker heeft niet dezelfde Bronanker waarde als het verwijderde object van de AD-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6a8c8-116">If Azure AD Connect Synchronization Service is configured to use system-generated AD attribute (such as ObjectGuid) for the Source Anchor attribute, the newly created AD user object will not have the same Source Anchor value as the deleted AD user object.</span></span> <span data-ttu-id="6a8c8-117">Wanneer het gemaakte object van de AD-gebruiker is gesynchroniseerd met Azure AD, Azure AD maakt een nieuw object van de Azure AD-gebruiker in plaats van het herstellen van het voorlopig verwijderde object in de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a8c8-117">When the newly created AD user object is synchronized to Azure AD, Azure AD creates a new Azure AD user object instead of restoring the soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="6a8c8-118">Standaard verwijderd Azure AD houdt objecten van Azure AD-gebruiker in staat voorlopig verwijderde voor 30 dagen voordat ze worden permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6a8c8-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="6a8c8-119">Beheerders kunnen echter de verwijdering van dergelijke objecten te versnellen.</span><span class="sxs-lookup"><span data-stu-id="6a8c8-119">However, administrators can accelerate the deletion of such objects.</span></span> <span data-ttu-id="6a8c8-120">Zodra de objecten worden permanent verwijderd, kunnen ze niet meer worden hersteld, zelfs als lokale AD-Prullenbak-functie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6a8c8-120">Once the objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="6a8c8-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6a8c8-121">Next steps</span></span>
<span data-ttu-id="6a8c8-122">**Overzichtsonderwerpen**</span><span class="sxs-lookup"><span data-stu-id="6a8c8-122">**Overview topics**</span></span>

* [<span data-ttu-id="6a8c8-123">Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="6a8c8-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="6a8c8-124">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a8c8-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
