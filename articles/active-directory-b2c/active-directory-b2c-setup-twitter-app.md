---
title: 'Azure Active Directory B2C: Twitter configuratie | Microsoft Docs'
description: Geef tooconsumers zich kunnen registreren en aanmelden met Twitter-accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a><span data-ttu-id="dbfe5-103">Azure Active Directory B2C: Tooconsumers zich kunnen registreren en aanmelden met Twitter-accounts bieden</span><span class="sxs-lookup"><span data-stu-id="dbfe5-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="dbfe5-104">Deze functie is in preview.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="dbfe5-105">Een Twitter-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="dbfe5-105">Create a Twitter application</span></span>
<span data-ttu-id="dbfe5-106">toouse Twitter als een id-provider in Azure Active Directory (Azure AD) B2C, u toocreate Twitter-toepassing nodig hebt en deze met de juiste parameters Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-106">toouse Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Twitter application and supply it with hello right parameters.</span></span> <span data-ttu-id="dbfe5-107">U moet een Twitter developer-account toodo dit.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-107">You need a Twitter developer account toodo this.</span></span> <span data-ttu-id="dbfe5-108">Als u niet hebt, kunt u krijgen op het [https://dev.twitter.com/](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="dbfe5-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="dbfe5-109">Ga toohello [Twitter-website voor ontwikkelaars van](https://dev.twitter.com/) en meld u aan met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-109">Go toohello [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="dbfe5-110">Klik op **mijn apps** onder **hulpprogramma's en ondersteuning** en klik vervolgens op **nieuwe App maken**.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="dbfe5-111">In de vorm hello, kunt u een waarde opgeven voor Hallo **naam**, **beschrijving**, en **Website**.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-111">In hello form, provide a value for hello **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="dbfe5-112">Voor Hallo **retouraanroep URL**, voer `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-112">For hello **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="dbfe5-113">Zorg ervoor dat tooreplace **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="dbfe5-113">Make sure tooreplace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="dbfe5-114">Controleer Hallo vak tooagree toohello **Developer overeenkomst** en klik op **uw Twitter-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-114">Check hello box tooagree toohello **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="dbfe5-115">Zodra het Hallo-app is gemaakt, klikt u op **sleutels en toegangstokens**.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-115">Once hello app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="dbfe5-116">Hallo-waarde van kopiëren **consumentsleutel** en **consumentgeheim**.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-116">Copy hello value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="dbfe5-117">U moet ze tooconfigure Twitter als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-117">You will need both of them tooconfigure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="dbfe5-118">Twitter configureren als een id-provider in uw tenant</span><span class="sxs-lookup"><span data-stu-id="dbfe5-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="dbfe5-119">Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-119">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="dbfe5-120">Klik op de blade Hallo B2C-functies, **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-120">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="dbfe5-121">Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-121">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="dbfe5-122">Geef een beschrijvende **naam** voor Hallo identiteit provider configureren.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-122">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="dbfe5-123">Voer bijvoorbeeld 'Twitter'.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="dbfe5-124">Klik op **identiteit providertype**, selecteer **Twitter**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="dbfe5-125">Klik op **instellen van deze id-provider** en Voer Hallo Twitter **consumentsleutel** voor Hallo **Client-id** en Twitter Hallo **consumentgeheim**voor Hallo **clientgeheim**.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-125">Click **Set up this identity provider** and enter hello Twitter **Consumer Key** for hello **Client id** and hello Twitter **Consumer Secret** for hello **Client secret**.</span></span>
7. <span data-ttu-id="dbfe5-126">Klik op **OK**, en klik vervolgens op **maken** toosave uw Twitter-configuratie.</span><span class="sxs-lookup"><span data-stu-id="dbfe5-126">Click **OK**, and then click **Create** toosave your Twitter configuration.</span></span>

