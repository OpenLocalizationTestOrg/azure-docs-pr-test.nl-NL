---
title: aaaSelf-registratie serviceportal voor Azure Active Directory B2B-samenwerking | Microsoft Docs
description: Azure Active Directory B2B-samenwerking ondersteunt uw externe bedrijfsrelaties door zakelijke partners tooselectively toegang tot uw zakelijke toepassingen inschakelen
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
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a><span data-ttu-id="1ce29-103">Self-service portal voor Azure AD B2B-samenwerking aanmelding</span><span class="sxs-lookup"><span data-stu-id="1ce29-103">Self-service portal for Azure AD B2B collaboration sign-up</span></span>

<span data-ttu-id="1ce29-104">Klanten kunnen veel doen met Hallo ingebouwde functies die beschikbaar worden gesteld via onze IT-beheerder [Azure-portal](https://portal.azure.com) en onze [toepassing Toegangsvenster](https://myapps.microsoft.com) voor eindgebruikers.</span><span class="sxs-lookup"><span data-stu-id="1ce29-104">Customers can do a lot with hello built-in features that are exposed through our IT admin [Azure portal](https://portal.azure.com) and our [Application Access Panel](https://myapps.microsoft.com) for end users.</span></span> <span data-ttu-id="1ce29-105">Maar er zijn ook op de hoogte dat bedrijven toocustomize Hallo onboarding werkstroom voor B2B gebruikers toofit de behoeften van hun organisatie moeten.</span><span class="sxs-lookup"><span data-stu-id="1ce29-105">But we are also aware that businesses need toocustomize hello onboarding workflow for B2B users toofit their organization’s needs.</span></span> <span data-ttu-id="1ce29-106">Ze kunnen doen dat met [onze API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span><span class="sxs-lookup"><span data-stu-id="1ce29-106">They can do that with [our API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span></span>

<span data-ttu-id="1ce29-107">In als u discussies met onze klanten zien we een gemeenschappelijke nodig toename up boven alle andere gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1ce29-107">In discussions with our customers, we see one common need rise up above all others.</span></span> <span data-ttu-id="1ce29-108">Hallo organisatie uitnodigen kan niet van tevoren weet die Hallo afzonderlijke externe deelnemers zijn die bronnen tootheir moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1ce29-108">hello inviting organization may not know ahead of time who hello individual external collaborators are who need access tootheir resources.</span></span> <span data-ttu-id="1ce29-109">Ze wilden een manier voor gebruikers van partnerbedrijven te registreren zichzelf met een reeks beleidsregels die Hallo besturingselementen organisatie uitnodigen.</span><span class="sxs-lookup"><span data-stu-id="1ce29-109">They wanted a way for users from partner companies too sign themselves up with a set of policies that hello inviting organization controls.</span></span> <span data-ttu-id="1ce29-110">Dit scenario is mogelijk via onze API's, zodat we een project op Github die u zojuist hebt die is gepubliceerd: [Github-voorbeeldproject](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="1ce29-110">This scenario is possible through our APIs,  so we published a project on Github that did just that: [sample Github project](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

<span data-ttu-id="1ce29-111">Onze Github-project wordt gedemonstreerd hoe organisaties kunnen onze API's gebruiken en bieden een aanmelding op basis van beleid, selfservice-functie voor hun vertrouwde partners, met regels die bepalen Hallo apps die toegang te krijgen tot.</span><span class="sxs-lookup"><span data-stu-id="1ce29-111">Our Github project demonstrates how organizations can use our APIs, and provide a policy-based, self-service sign-up capability for their trusted partners, with rules that determine hello apps they can access.</span></span> <span data-ttu-id="1ce29-112">Partner gebruikers tooresources toegang kunnen krijgen als ze nodig hebben, veilig, zonder Hallo vrijgeven toomanually organisatie uitnodigen ze.</span><span class="sxs-lookup"><span data-stu-id="1ce29-112">Partner users can get access tooresources when they need them, securely, without requiring hello inviting organization toomanually onboard them.</span></span> <span data-ttu-id="1ce29-113">U kunt eenvoudig hello project implementeren in een Azure-abonnement van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="1ce29-113">You can easily deploy hello project into an Azure subscription of your choice.</span></span>

## <a name="as-is-code"></a><span data-ttu-id="1ce29-114">Als-code</span><span class="sxs-lookup"><span data-stu-id="1ce29-114">As-is code</span></span>

<span data-ttu-id="1ce29-115">Houd er rekening mee dat deze code als een toodemonstrate voorbeeldgebruik van hello Azure Active Directory B2B uitnodiging API beschikbaar wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1ce29-115">Remember that this code is made available as a sample toodemonstrate usage of hello Azure Active Directory B2B invitation API.</span></span> <span data-ttu-id="1ce29-116">Deze moet worden aangepast door uw team dev of een partner en moet worden gecontroleerd voordat ze worden geïmplementeerd in een productiescenario.</span><span class="sxs-lookup"><span data-stu-id="1ce29-116">It should be customized by your dev team or a partner, and should be reviewed before being deployed in a production scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ce29-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1ce29-117">Next steps</span></span>

<span data-ttu-id="1ce29-118">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="1ce29-118">Browse our other articles on Azure AD B2B collaboration:</span></span>
* [<span data-ttu-id="1ce29-119">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="1ce29-119">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="1ce29-120">Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?</span><span class="sxs-lookup"><span data-stu-id="1ce29-120">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="1ce29-121">Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen</span><span class="sxs-lookup"><span data-stu-id="1ce29-121">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="1ce29-122">Hallo-elementen van Hallo uitnodigingsmail voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="1ce29-122">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="1ce29-123">B2B-samenwerking uitnodiging inwisseling</span><span class="sxs-lookup"><span data-stu-id="1ce29-123">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="1ce29-124">Azure AD B2B-samenwerking licentieverlening</span><span class="sxs-lookup"><span data-stu-id="1ce29-124">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="1ce29-125">Het oplossen van Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="1ce29-125">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="1ce29-126">Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)</span><span class="sxs-lookup"><span data-stu-id="1ce29-126">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="1ce29-127">Multi-Factor Authentication voor gebruikers van B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="1ce29-127">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="1ce29-128">B2B-samenwerking gebruikers zonder een uitnodiging toevoegen</span><span class="sxs-lookup"><span data-stu-id="1ce29-128">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* <span data-ttu-id="1ce29-129">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="1ce29-129">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>