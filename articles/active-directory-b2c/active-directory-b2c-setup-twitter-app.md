---
title: 'Azure Active Directory B2C: Twitter configuratie | Microsoft Docs'
description: Registreren en aanmelden gebruikers met Twitter-accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C bieden.
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
ms.openlocfilehash: 82a001dd53cdddcf3b360090f3250af593c96fbb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-twitter-accounts"></a><span data-ttu-id="97929-103">Azure Active Directory B2C: Zich kunnen registreren en aanmelden gebruikers bieden met Twitter-accounts</span><span class="sxs-lookup"><span data-stu-id="97929-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="97929-104">Deze functie is in preview.</span><span class="sxs-lookup"><span data-stu-id="97929-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="97929-105">Een Twitter-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="97929-105">Create a Twitter application</span></span>
<span data-ttu-id="97929-106">Als u wilt gebruiken als een id-provider in Azure Active Directory (Azure AD) B2C Twitter gebruikt, moet u een Twitter-toepassing maken en geeft deze met de juiste parameters.</span><span class="sxs-lookup"><span data-stu-id="97929-106">To use Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Twitter application and supply it with the right parameters.</span></span> <span data-ttu-id="97929-107">U moet een Twitter-ontwikkelaarsaccount om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="97929-107">You need a Twitter developer account to do this.</span></span> <span data-ttu-id="97929-108">Als u niet hebt, kunt u krijgen op het [https://dev.twitter.com/](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="97929-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="97929-109">Ga naar de [Twitter-website voor ontwikkelaars van](https://dev.twitter.com/) en meld u aan met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="97929-109">Go to the [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="97929-110">Klik op **mijn apps** onder **hulpprogramma's en ondersteuning** en klik vervolgens op **nieuwe App maken**.</span><span class="sxs-lookup"><span data-stu-id="97929-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="97929-111">Klik in het formulier geeft een waarde op voor de **naam**, **beschrijving**, en **Website**.</span><span class="sxs-lookup"><span data-stu-id="97929-111">In the form, provide a value for the **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="97929-112">Voor de **retouraanroep URL**, voer `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="97929-112">For the **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="97929-113">Zorg ervoor dat u **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="97929-113">Make sure to replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="97929-114">Schakel het selectievakje in om te accepteren de **Developer overeenkomst** en klik op **uw Twitter-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="97929-114">Check the box to agree to the **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="97929-115">Zodra de app is gemaakt, klikt u op **sleutels en toegangstokens**.</span><span class="sxs-lookup"><span data-stu-id="97929-115">Once the app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="97929-116">Kopieer de waarde van **consumentsleutel** en **consumentgeheim**.</span><span class="sxs-lookup"><span data-stu-id="97929-116">Copy the value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="97929-117">U moet beide Twitter configureren als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="97929-117">You will need both of them to configure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="97929-118">Twitter configureren als een id-provider in uw tenant</span><span class="sxs-lookup"><span data-stu-id="97929-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="97929-119">Volg deze stappen voor [gaat u naar de blade B2C-functies](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="97929-119">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="97929-120">Klik op de blade B2C-functies op **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="97929-120">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="97929-121">Klik op **+Toevoegen** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="97929-121">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="97929-122">Geef een beschrijvende **naam** voor de configuratie van de id-provider.</span><span class="sxs-lookup"><span data-stu-id="97929-122">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="97929-123">Voer bijvoorbeeld 'Twitter'.</span><span class="sxs-lookup"><span data-stu-id="97929-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="97929-124">Klik op **identiteit providertype**, selecteer **Twitter**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="97929-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="97929-125">Klik op **instellen van deze id-provider** en voer de Twitter **consumentsleutel** voor de **Client-id** en de Twitter **consumentgeheim** voor de **clientgeheim**.</span><span class="sxs-lookup"><span data-stu-id="97929-125">Click **Set up this identity provider** and enter the Twitter **Consumer Key** for the **Client id** and the Twitter **Consumer Secret** for the **Client secret**.</span></span>
7. <span data-ttu-id="97929-126">Klik op **OK**, en klik vervolgens op **maken** naar uw Twitter-configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="97929-126">Click **OK**, and then click **Create** to save your Twitter configuration.</span></span>

