---
title: Self-service portal voor registratie voor Azure Active Directory B2B-samenwerking | Microsoft Docs
description: Azure Active Directory B2B-samenwerking ondersteunt uw externe bedrijfsrelaties door zakelijke partners selectief toegang te verlenen tot uw zakelijke toepassingen
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 307373c75bbb87cec683f7a3097f8f159c9d5e61
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a><span data-ttu-id="0ba31-103">Self-service portal voor Azure AD B2B-samenwerking aanmelding</span><span class="sxs-lookup"><span data-stu-id="0ba31-103">Self-service portal for Azure AD B2B collaboration sign-up</span></span>

<span data-ttu-id="0ba31-104">Klanten kunnen veel doen met de ingebouwde functies die beschikbaar worden gesteld via onze IT-beheerder [Azure-portal](https://portal.azure.com) en onze [toepassing Toegangsvenster](https://myapps.microsoft.com) voor eindgebruikers.</span><span class="sxs-lookup"><span data-stu-id="0ba31-104">Customers can do a lot with the built-in features that are exposed through our IT admin [Azure portal](https://portal.azure.com) and our [Application Access Panel](https://myapps.microsoft.com) for end users.</span></span> <span data-ttu-id="0ba31-105">Maar er zijn ook op de hoogte dat bedrijven nodig hebben voor het aanpassen van de werkstroom voorbereiden voor B2B-gebruikers aan de behoeften van hun organisatie.</span><span class="sxs-lookup"><span data-stu-id="0ba31-105">But we are also aware that businesses need to customize the onboarding workflow for B2B users to fit their organization’s needs.</span></span> <span data-ttu-id="0ba31-106">Ze kunnen doen dat met [onze API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span><span class="sxs-lookup"><span data-stu-id="0ba31-106">They can do that with [our API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span></span>

<span data-ttu-id="0ba31-107">In als u discussies met onze klanten zien we een gemeenschappelijke nodig toename up boven alle andere gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0ba31-107">In discussions with our customers, we see one common need rise up above all others.</span></span> <span data-ttu-id="0ba31-108">De uitnodiging organisatie kan niet van tevoren weet die de afzonderlijke externe deelnemers zijn die toegang tot hun bronnen nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="0ba31-108">The inviting organization may not know ahead of time who the individual external collaborators are who need access to their resources.</span></span> <span data-ttu-id="0ba31-109">Ze wilden een manier voor gebruikers van partnerbedrijven zich aanmelden met een reeks beleidsregels die u de organisatie uitnodigen beheert.</span><span class="sxs-lookup"><span data-stu-id="0ba31-109">They wanted a way for users from partner companies to  sign themselves up with a set of policies that the inviting organization controls.</span></span> <span data-ttu-id="0ba31-110">Dit scenario is mogelijk via onze API's, zodat we een project op Github die u zojuist hebt die is gepubliceerd: [Github-voorbeeldproject](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="0ba31-110">This scenario is possible through our APIs,  so we published a project on Github that did just that: [sample Github project](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

<span data-ttu-id="0ba31-111">Onze Github-project wordt gedemonstreerd hoe organisaties kunnen onze API's gebruiken en bieden een aanmelding op basis van beleid, selfservice-functie voor hun vertrouwde partners, met regels die bepalen van de toegang te krijgen tot apps.</span><span class="sxs-lookup"><span data-stu-id="0ba31-111">Our Github project demonstrates how organizations can use our APIs, and provide a policy-based, self-service sign-up capability for their trusted partners, with rules that determine the apps they can access.</span></span> <span data-ttu-id="0ba31-112">Gebruikers van de accountpartner kunnen toegang krijgen tot resources wanneer ze nodig hebben, veilig, zonder dat de organisatie van uitnodigen om handmatig vrijgeven ze.</span><span class="sxs-lookup"><span data-stu-id="0ba31-112">Partner users can get access to resources when they need them, securely, without requiring the inviting organization to manually onboard them.</span></span> <span data-ttu-id="0ba31-113">U kunt gemakkelijk het project implementeren in een Azure-abonnement van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="0ba31-113">You can easily deploy the project into an Azure subscription of your choice.</span></span>

## <a name="as-is-code"></a><span data-ttu-id="0ba31-114">Als-code</span><span class="sxs-lookup"><span data-stu-id="0ba31-114">As-is code</span></span>

<span data-ttu-id="0ba31-115">Houd er rekening mee dat deze code als voorbeeld voor het demonstreren van informatie over het gebruik van de Azure Active Directory B2B-uitnodiging API beschikbaar wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0ba31-115">Remember that this code is made available as a sample to demonstrate usage of the Azure Active Directory B2B invitation API.</span></span> <span data-ttu-id="0ba31-116">Deze moet worden aangepast door uw team dev of een partner en moet worden gecontroleerd voordat ze worden geïmplementeerd in een productiescenario.</span><span class="sxs-lookup"><span data-stu-id="0ba31-116">It should be customized by your dev team or a partner, and should be reviewed before being deployed in a production scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ba31-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0ba31-117">Next steps</span></span>

<span data-ttu-id="0ba31-118">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="0ba31-118">Browse our other articles on Azure AD B2B collaboration:</span></span>
* [<span data-ttu-id="0ba31-119">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="0ba31-119">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="0ba31-120">Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?</span><span class="sxs-lookup"><span data-stu-id="0ba31-120">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="0ba31-121">Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen</span><span class="sxs-lookup"><span data-stu-id="0ba31-121">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="0ba31-122">De elementen van de uitnodigingsmail voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="0ba31-122">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="0ba31-123">B2B-samenwerking uitnodiging inwisseling</span><span class="sxs-lookup"><span data-stu-id="0ba31-123">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="0ba31-124">Azure AD B2B-samenwerking licentieverlening</span><span class="sxs-lookup"><span data-stu-id="0ba31-124">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="0ba31-125">Het oplossen van Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="0ba31-125">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="0ba31-126">Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)</span><span class="sxs-lookup"><span data-stu-id="0ba31-126">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="0ba31-127">Multi-Factor Authentication voor gebruikers van B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="0ba31-127">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="0ba31-128">B2B-samenwerking gebruikers zonder een uitnodiging toevoegen</span><span class="sxs-lookup"><span data-stu-id="0ba31-128">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* <span data-ttu-id="0ba31-129">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="0ba31-129">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>