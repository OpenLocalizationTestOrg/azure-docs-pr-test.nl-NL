---
title: 'Azure Active Directory B2C: Weibo configuratie | Microsoft Docs'
description: Bieden zich kunnen registreren en aanmelden tooconsumers Weibo accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a><span data-ttu-id="94b19-103">Azure Active Directory B2C: Bieden Weibo accounts zich kunnen registreren en aanmelden tooconsumers</span><span class="sxs-lookup"><span data-stu-id="94b19-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="94b19-104">Deze functie is in preview.</span><span class="sxs-lookup"><span data-stu-id="94b19-104">This feature is in preview.</span></span> <span data-ttu-id="94b19-105">Gebruik deze id-provider niet in uw productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="94b19-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="94b19-106">Een toepassing Weibo maken</span><span class="sxs-lookup"><span data-stu-id="94b19-106">Create a Weibo application</span></span>

<span data-ttu-id="94b19-107">toouse Weibo als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een toepassing Weibo toocreate en leveren met de juiste parameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="94b19-107">toouse Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Weibo application and supply it with hello right parameters.</span></span> <span data-ttu-id="94b19-108">U moet een account Weibo toodo dit.</span><span class="sxs-lookup"><span data-stu-id="94b19-108">You need a Weibo account toodo this.</span></span> <span data-ttu-id="94b19-109">Als u niet hebt, kunt u één voor één [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="94b19-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-hello-weibo-developer-program"></a><span data-ttu-id="94b19-110">Registreren voor Hallo Weibo Ontwikkelaarsprogramma</span><span class="sxs-lookup"><span data-stu-id="94b19-110">Register for hello Weibo developer program</span></span>

1. <span data-ttu-id="94b19-111">Ga toohello [Weibo ontwikkelaarsportal](http://open.weibo.com/) en meld u aan met de referenties van uw Weibo-account.</span><span class="sxs-lookup"><span data-stu-id="94b19-111">Go toohello [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="94b19-112">Na het aanmelden, klik op de weergavenaam van uw in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="94b19-112">After signing in, click on your display name in hello top-right corner.</span></span>
3. <span data-ttu-id="94b19-113">Selecteer in de vervolgkeuzelijst Hallo**编辑开发者信息**(informatie voor ontwikkelaars bewerken).</span><span class="sxs-lookup"><span data-stu-id="94b19-113">In hello dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="94b19-114">Hallo vereist gegevens invoeren in Hallo-formulier en klik op**提交**(verzenden).</span><span class="sxs-lookup"><span data-stu-id="94b19-114">Enter hello required information into hello form and click **提交** (submit).</span></span>
5. <span data-ttu-id="94b19-115">Hallo e-verificatieproces voltooien.</span><span class="sxs-lookup"><span data-stu-id="94b19-115">Complete hello email verification process.</span></span>
6. <span data-ttu-id="94b19-116">Ga toohello [identiteitverificatie pagina](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="94b19-116">Go toohello [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="94b19-117">Hallo vereist gegevens invoeren in Hallo-formulier en klik op**提交**(verzenden).</span><span class="sxs-lookup"><span data-stu-id="94b19-117">Enter hello required information into hello form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="94b19-118">Een toepassing Weibo registreren</span><span class="sxs-lookup"><span data-stu-id="94b19-118">Register a Weibo application</span></span>

1. <span data-ttu-id="94b19-119">Ga toohello [app de registratiepagina van nieuwe Weibo](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="94b19-119">Go toohello [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="94b19-120">Geef informatie op Hallo benodigde toepassing.</span><span class="sxs-lookup"><span data-stu-id="94b19-120">Enter hello necessary application information.</span></span>
3. <span data-ttu-id="94b19-121">Klik op**创建**(maken).</span><span class="sxs-lookup"><span data-stu-id="94b19-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="94b19-122">Kopieer de waarden Hallo van **App-sleutel** en **App geheim**.</span><span class="sxs-lookup"><span data-stu-id="94b19-122">Copy hello values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="94b19-123">U nodig deze later.</span><span class="sxs-lookup"><span data-stu-id="94b19-123">You will need this later.</span></span>
5. <span data-ttu-id="94b19-124">Hallo vereist foto's uploaden en voer de benodigde informatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="94b19-124">Upload hello required photos and enter hello necessary information.</span></span>
6. <span data-ttu-id="94b19-125">Klik op**保存以上信息**(opslaan).</span><span class="sxs-lookup"><span data-stu-id="94b19-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="94b19-126">Klik op**高级信息**(Geavanceerd informatie).</span><span class="sxs-lookup"><span data-stu-id="94b19-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="94b19-127">Klik op**编辑**(bewerken) volgende toohello veld voor OAuth2.0**授权设置**(Omleidings-URL).</span><span class="sxs-lookup"><span data-stu-id="94b19-127">Click **编辑** (edit) next toohello field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="94b19-128">Voer `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` voor OAuth2.0**授权设置**(Omleidings-URL).</span><span class="sxs-lookup"><span data-stu-id="94b19-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="94b19-129">Bijvoorbeeld, als uw `tenant_name` contoso.onmicrosoft.com, set Hallo URL toobe is `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="94b19-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="94b19-130">Klik op**提交**(verzenden).</span><span class="sxs-lookup"><span data-stu-id="94b19-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="94b19-131">Weibo configureren als een id-provider in uw tenant</span><span class="sxs-lookup"><span data-stu-id="94b19-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="94b19-132">Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="94b19-132">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="94b19-133">Klik op de blade Hallo B2C-functies, **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="94b19-133">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="94b19-134">Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="94b19-134">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="94b19-135">Geef een beschrijvende **naam** voor Hallo identiteit provider configureren.</span><span class="sxs-lookup"><span data-stu-id="94b19-135">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="94b19-136">Voer bijvoorbeeld 'Weibo'.</span><span class="sxs-lookup"><span data-stu-id="94b19-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="94b19-137">Klik op **identiteit providertype**, selecteer **Weibo**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="94b19-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="94b19-138">Klik op **instellen van deze id-provider**</span><span class="sxs-lookup"><span data-stu-id="94b19-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="94b19-139">Voer Hallo **App-sleutel** die u eerder hebt gekopieerd als Hallo **Client-ID**.</span><span class="sxs-lookup"><span data-stu-id="94b19-139">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="94b19-140">Voer Hallo **App geheim** die u eerder hebt gekopieerd als Hallo **Clientgeheim**.</span><span class="sxs-lookup"><span data-stu-id="94b19-140">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="94b19-141">Klik op **OK** en klik vervolgens op **maken** toosave uw Weibo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="94b19-141">Click **OK** and then click **Create** toosave your Weibo configuration.</span></span>

