---
title: aaaHow tooadd een multitenant toepassing toohello Azure AD-toepassingsgalerie | Microsoft Docs
description: Legt uit hoe u kunt uw aangepaste ontwikkelde multitenant toepassing vermelden in hello Azure AD-Toepassingsgalerie
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2dc6e0d783835d2639a7e6dda172110ee860a977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-multi-tenant-application-toohello-azure-ad-application-gallery"></a><span data-ttu-id="4257b-103">Hoe een toepassing met meerdere tenants toohello Azure AD-toepassingsgalerie tooadd</span><span class="sxs-lookup"><span data-stu-id="4257b-103">How tooadd a multi-tenant application toohello Azure AD application gallery</span></span>

## <a name="what-is-hello-azure-ad-application-gallery"></a><span data-ttu-id="4257b-104">Wat is Azure AD-Toepassingsgalerie Hallo?</span><span class="sxs-lookup"><span data-stu-id="4257b-104">What is hello Azure AD Application Gallery?</span></span>

<span data-ttu-id="4257b-105">Hello Azure AD-Toepassingsgalerie is een uitstekende manier tooget uw toepassing voor alle Hallo miljoenen van Azure Active Directory klanten toobroaden Hallo impact en bereik van uw toepassing hello marketplace.</span><span class="sxs-lookup"><span data-stu-id="4257b-105">hello Azure AD Application Gallery is a great way tooget your application in front of all hello millions of Azure Active Directory customers toobroaden hello impact and reach of your application in hello marketplace.</span></span> <span data-ttu-id="4257b-106">Hallo onderstaande stappen wordt uitgelegd hoe u uw toepassing in Azure AD-Toepassingsgalerie Hallo kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="4257b-106">hello below steps explain how you can list your application in hello Azure AD Application Gallery.</span></span>

## <a name="if-your-application-supports-saml-or-openidconnect"></a><span data-ttu-id="4257b-107">Als uw toepassing biedt ondersteuning voor SAML- of OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="4257b-107">If your application supports SAML or OpenIDConnect</span></span>
<span data-ttu-id="4257b-108">Als u een multitenant-toepassing die u wilt dat toolist in hello Azure AD-Toepassingsgalerie hebt, moet u eerst controleren of uw toepassing een Hallo na één aanmelding technologieën ondersteunt:</span><span class="sxs-lookup"><span data-stu-id="4257b-108">If you have a multi-tenant application you'd like toolist in hello Azure AD Application Gallery, you must first make sure that your application supports one of hello following single sign-on technologies:</span></span>

1. <span data-ttu-id="4257b-109">**OpenID Connect** - directe integratie met Azure AD met OpenID Connect voor verificatie en Azure AD toestemming API voor configuratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="4257b-109">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and hello Azure AD consent API for configuration.</span></span> <span data-ttu-id="4257b-110">Als u een integratie net begint en SAML biedt geen ondersteuning voor uw toepassing, is dit Hallo aanbevolen modus.</span><span class="sxs-lookup"><span data-stu-id="4257b-110">If you are just starting an integration and your application does not support SAML, then this is hello recommend mode.</span></span>
2. <span data-ttu-id="4257b-111">**SAML** – de toepassing al heeft Hallo mogelijkheid tooconfigure van derden id-providers met Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="4257b-111">**SAML** – Your application already has hello ability tooconfigure third-party identity providers using hello SAML protocol.</span></span>

<span data-ttu-id="4257b-112">Als uw toepassing een van deze modi voor eenmalige aanmelding ondersteunt en u toolist dat wilt uw multitenant-toepassing in Azure AD-Toepassingsgalerie hello, u kunt stappen Hallo in Hallo document hieronder.</span><span class="sxs-lookup"><span data-stu-id="4257b-112">If your application supports one of these single sign-on modes and you'd like toolist your multi-tenant application in hello Azure AD Application Gallery, you can follow hello steps in hello document below.</span></span> <span data-ttu-id="4257b-113">snel aan de slag tooget e-mailbericht te verzenden**waadpartners@microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="4257b-113">tooget started quickly send an email too**waadpartners@microsoft.com**.</span></span>

## <a name="if-your-application-does-not-support-saml-or-openidconnect"></a><span data-ttu-id="4257b-114">Als uw toepassing biedt geen ondersteuning voor SAML of OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="4257b-114">If your application does not support SAML or OpenIDConnect</span></span>
<span data-ttu-id="4257b-115">Zelfs als uw toepassing biedt geen ondersteuning voor een van deze modi, kunnen we het nog steeds integreren in onze galerie met onze wachtwoord Single Sign-on-technologie.</span><span class="sxs-lookup"><span data-stu-id="4257b-115">Even if your application does not support one of these modes, we can still integrate it into our gallery using our Password Single Sign-on technology.</span></span> <span data-ttu-id="4257b-116">Als u tooexplore wilt deze optie, u kunt de een e-mailbericht te verzenden**waadpartners@microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="4257b-116">If you'd like tooexplore this option, you can send an email too**waadpartners@microsoft.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4257b-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4257b-117">Next steps</span></span>
[<span data-ttu-id="4257b-118">Hoe toolist uw toepassing in hello Azure Active Directory-toepassingsgalerie</span><span class="sxs-lookup"><span data-stu-id="4257b-118">How toolist your application in hello Azure Active Directory application gallery</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)
