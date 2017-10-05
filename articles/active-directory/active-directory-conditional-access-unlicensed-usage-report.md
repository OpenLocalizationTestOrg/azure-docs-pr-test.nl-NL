---
title: Niet-gelicentieerde gebruiksrapport | Microsoft Docs
description: Het gebruik van niet-gelicentieerde rapport helpt bij het identificeren van niet-gelicentieerde gebruikers die gebruikmaken van betaald Azure AD-functies.
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
ms.openlocfilehash: c0b4f455f067e825362bdecc02ea62d7984f0d31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="2c539-103">Niet-gelicentieerde gebruiksrapport</span><span class="sxs-lookup"><span data-stu-id="2c539-103">Unlicensed usage report</span></span>
<span data-ttu-id="2c539-104">Het gebruik van niet-gelicentieerde rapport helpt bij het identificeren van niet-gelicentieerde gebruikers die gebruikmaken van betaald Azure AD-functies.</span><span class="sxs-lookup"><span data-stu-id="2c539-104">The unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="2c539-105">Hiermee kunt u beter te maken van de licenties die u hebt aangeschaft en om te identificeren die u weet wanneer u aanvullende licenties moet mogelijk.</span><span class="sxs-lookup"><span data-stu-id="2c539-105">This allows you to make better use of licenses that you have purchased and to identify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="2c539-106">Dit rapport bevat actieve informatie over het gebruik van de betaalde functies in de afgelopen 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="2c539-106">The report shows active usage of the paid features in the last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="2c539-107">Rapport structuur</span><span class="sxs-lookup"><span data-stu-id="2c539-107">Report structure</span></span>
| <span data-ttu-id="2c539-108">Kolomnaam</span><span class="sxs-lookup"><span data-stu-id="2c539-108">Column name</span></span> | <span data-ttu-id="2c539-109">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2c539-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2c539-110">Niet-gelicentieerde gebruiker</span><span class="sxs-lookup"><span data-stu-id="2c539-110">Unlicensed User</span></span> |<span data-ttu-id="2c539-111">Naam van de gebruiker</span><span class="sxs-lookup"><span data-stu-id="2c539-111">Name of the user</span></span> |
| <span data-ttu-id="2c539-112">Functie</span><span class="sxs-lookup"><span data-stu-id="2c539-112">Feature</span></span> |<span data-ttu-id="2c539-113">De naam van de functie.</span><span class="sxs-lookup"><span data-stu-id="2c539-113">The feature name.</span></span> <span data-ttu-id="2c539-114">Bijvoorbeeld: voorwaardelijke toegang</span><span class="sxs-lookup"><span data-stu-id="2c539-114">For example: conditional access</span></span> |
| <span data-ttu-id="2c539-115">Toepassing geopend</span><span class="sxs-lookup"><span data-stu-id="2c539-115">Application Accessed</span></span> |<span data-ttu-id="2c539-116">De naam van de toepassing die wordt geopend met de functie.</span><span class="sxs-lookup"><span data-stu-id="2c539-116">The name of the application that is being accessed with the feature.</span></span> <span data-ttu-id="2c539-117">Bijvoorbeeld: Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="2c539-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="2c539-118">Als een gebruikersaccount is verwijderd. de kolom 'Niet-gelicentieerde User' worden ingevuld met de ID, zoals 1003000090D8B285</span><span class="sxs-lookup"><span data-stu-id="2c539-118">If a user account has been deleted the ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="2c539-119">Functie voor voorwaardelijke toegang</span><span class="sxs-lookup"><span data-stu-id="2c539-119">Conditional access feature</span></span>
<span data-ttu-id="2c539-120">Niet-gelicentieerde gebruikers gemarkeerd wanneer ze toegang krijgen een service met beleid voor voorwaardelijke toegang toegepast tot als ze geen een Azure AD Premium-licentie hebt.</span><span class="sxs-lookup"><span data-stu-id="2c539-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="2c539-121">Dit geldt voor MFA / locatie beleid, evenals een apparaat beleid met Intune.</span><span class="sxs-lookup"><span data-stu-id="2c539-121">This applies to MFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="2c539-122">Zie ook</span><span class="sxs-lookup"><span data-stu-id="2c539-122">See also</span></span>
* [<span data-ttu-id="2c539-123">Voorwaardelijke toegang gebruiken met Office 365 en andere Azure Active Directory verbonden apps</span><span class="sxs-lookup"><span data-stu-id="2c539-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="2c539-124">Aan de slag met voorwaardelijke toegang tot Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c539-124">Getting started with conditional access to Azure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

