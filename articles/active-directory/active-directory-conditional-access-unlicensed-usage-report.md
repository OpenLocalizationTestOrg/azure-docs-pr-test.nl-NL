---
title: aaaUnlicensed gebruiksrapport | Microsoft Docs
description: Hallo niet-gelicentieerde gebruiksrapport kunt die u niet-gelicentieerde gebruikers die gebruikmaken van identificeren betaalde Azure AD-functies.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="32ebf-103">Niet-gelicentieerde gebruiksrapport</span><span class="sxs-lookup"><span data-stu-id="32ebf-103">Unlicensed usage report</span></span>
<span data-ttu-id="32ebf-104">Hallo niet-gelicentieerde gebruiksrapport kunt die u niet-gelicentieerde gebruikers die gebruikmaken van identificeren betaalde Azure AD-functies.</span><span class="sxs-lookup"><span data-stu-id="32ebf-104">hello unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="32ebf-105">Hiermee kunt u beter gebruik van licenties dat u hebt aangeschaft en u weet wanneer moet u mogelijk aanvullende licenties tooidentify toomake.</span><span class="sxs-lookup"><span data-stu-id="32ebf-105">This allows you toomake better use of licenses that you have purchased and tooidentify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="32ebf-106">Hallo-rapport geeft de actieve gebruik van Hallo betaalde functies in Hallo afgelopen 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="32ebf-106">hello report shows active usage of hello paid features in hello last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="32ebf-107">Rapport structuur</span><span class="sxs-lookup"><span data-stu-id="32ebf-107">Report structure</span></span>
| <span data-ttu-id="32ebf-108">Kolomnaam</span><span class="sxs-lookup"><span data-stu-id="32ebf-108">Column name</span></span> | <span data-ttu-id="32ebf-109">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32ebf-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="32ebf-110">Niet-gelicentieerde gebruiker</span><span class="sxs-lookup"><span data-stu-id="32ebf-110">Unlicensed User</span></span> |<span data-ttu-id="32ebf-111">Naam van de gebruiker Hallo</span><span class="sxs-lookup"><span data-stu-id="32ebf-111">Name of hello user</span></span> |
| <span data-ttu-id="32ebf-112">Functie</span><span class="sxs-lookup"><span data-stu-id="32ebf-112">Feature</span></span> |<span data-ttu-id="32ebf-113">Hallo functienaam.</span><span class="sxs-lookup"><span data-stu-id="32ebf-113">hello feature name.</span></span> <span data-ttu-id="32ebf-114">Bijvoorbeeld: voorwaardelijke toegang</span><span class="sxs-lookup"><span data-stu-id="32ebf-114">For example: conditional access</span></span> |
| <span data-ttu-id="32ebf-115">Toepassing geopend</span><span class="sxs-lookup"><span data-stu-id="32ebf-115">Application Accessed</span></span> |<span data-ttu-id="32ebf-116">Hallo-naam van Hallo-toepassing die wordt geopend met Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="32ebf-116">hello name of hello application that is being accessed with hello feature.</span></span> <span data-ttu-id="32ebf-117">Bijvoorbeeld: Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="32ebf-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="32ebf-118">Als een gebruikersaccount is verwijderd 'Niet-gelicentieerde User' kolom worden ingevuld met de ID, zoals 1003000090D8B285 Hallo</span><span class="sxs-lookup"><span data-stu-id="32ebf-118">If a user account has been deleted hello ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="32ebf-119">Functie voor voorwaardelijke toegang</span><span class="sxs-lookup"><span data-stu-id="32ebf-119">Conditional access feature</span></span>
<span data-ttu-id="32ebf-120">Niet-gelicentieerde gebruikers gemarkeerd wanneer ze toegang krijgen een service met beleid voor voorwaardelijke toegang toegepast tot als ze geen een Azure AD Premium-licentie hebt.</span><span class="sxs-lookup"><span data-stu-id="32ebf-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="32ebf-121">Dit geldt tooMFA / locatie beleid, evenals een apparaat beleid met Intune.</span><span class="sxs-lookup"><span data-stu-id="32ebf-121">This applies tooMFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="32ebf-122">Zie ook</span><span class="sxs-lookup"><span data-stu-id="32ebf-122">See also</span></span>
* [<span data-ttu-id="32ebf-123">Voorwaardelijke toegang gebruiken met Office 365 en andere Azure Active Directory verbonden apps</span><span class="sxs-lookup"><span data-stu-id="32ebf-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="32ebf-124">Aan de slag met voorwaardelijke toegang tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="32ebf-124">Getting started with conditional access tooAzure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

