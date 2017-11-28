---
title: 'Azure Active Directory B2C: WeChat configuratie | Microsoft Docs'
description: Bieden zich kunnen registreren en aanmelden tooconsumers WeChat accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a><span data-ttu-id="48d28-103">Azure Active Directory B2C: Bieden WeChat accounts zich kunnen registreren en aanmelden tooconsumers</span><span class="sxs-lookup"><span data-stu-id="48d28-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="48d28-104">Deze functie is in preview.</span><span class="sxs-lookup"><span data-stu-id="48d28-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="48d28-105">Een toepassing WeChat maken</span><span class="sxs-lookup"><span data-stu-id="48d28-105">Create a WeChat application</span></span>

<span data-ttu-id="48d28-106">toouse WeChat als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een toepassing WeChat toocreate en leveren met de juiste parameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="48d28-106">toouse WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a WeChat application and supply it with hello right parameters.</span></span> <span data-ttu-id="48d28-107">U moet een account WeChat toodo dit.</span><span class="sxs-lookup"><span data-stu-id="48d28-107">You need a WeChat account toodo this.</span></span> <span data-ttu-id="48d28-108">Als u niet hebt, kunt u een aanmelden via een van hun mobiele apps of via het nummer van uw q krijgen.</span><span class="sxs-lookup"><span data-stu-id="48d28-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="48d28-109">Hierna is uw account is geregistreerd bij Hallo WeChat Ontwikkelaarsprogramma worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="48d28-109">After that, get your account registered with hello WeChat developer program.</span></span> <span data-ttu-id="48d28-110">U vindt meer informatie [hier](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span><span class="sxs-lookup"><span data-stu-id="48d28-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="48d28-111">Een toepassing WeChat registreren</span><span class="sxs-lookup"><span data-stu-id="48d28-111">Register a WeChat application</span></span>

1. <span data-ttu-id="48d28-112">Ga te[https://open.weixin.qq.com/](https://open.weixin.qq.com/) en zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="48d28-112">Go too[https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="48d28-113">Klik op**管理中心**(center management).</span><span class="sxs-lookup"><span data-stu-id="48d28-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="48d28-114">Ga als volgt Hallo nodige tooregister een nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="48d28-114">Follow hello necessary steps tooregister a new application.</span></span>
4. <span data-ttu-id="48d28-115">Voor**授权回调域**(callback URL), voer `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="48d28-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="48d28-116">Bijvoorbeeld, als uw `tenant_name` contoso.onmicrosoft.com, set Hallo URL toobe is `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="48d28-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="48d28-117">Zoeken en kopieer Hallo **APP-ID** en **APP-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="48d28-117">Find and copy hello **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="48d28-118">U moet deze later.</span><span class="sxs-lookup"><span data-stu-id="48d28-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="48d28-119">WeChat configureren als een id-provider in uw tenant</span><span class="sxs-lookup"><span data-stu-id="48d28-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="48d28-120">Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="48d28-120">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="48d28-121">Klik op de blade Hallo B2C-functies, **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="48d28-121">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="48d28-122">Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="48d28-122">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="48d28-123">Geef een beschrijvende **naam** voor Hallo identiteit provider configureren.</span><span class="sxs-lookup"><span data-stu-id="48d28-123">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="48d28-124">Voer bijvoorbeeld 'WeChat'.</span><span class="sxs-lookup"><span data-stu-id="48d28-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="48d28-125">Klik op **identiteit providertype**, selecteer **WeChat**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="48d28-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="48d28-126">Klik op **instellen van deze id-provider**</span><span class="sxs-lookup"><span data-stu-id="48d28-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="48d28-127">Voer Hallo **App-sleutel** die u eerder hebt gekopieerd als Hallo **Client-ID**.</span><span class="sxs-lookup"><span data-stu-id="48d28-127">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="48d28-128">Voer Hallo **App geheim** die u eerder hebt gekopieerd als Hallo **Clientgeheim**.</span><span class="sxs-lookup"><span data-stu-id="48d28-128">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="48d28-129">Klik op **OK** en klik vervolgens op **maken** toosave uw WeChat-configuratie.</span><span class="sxs-lookup"><span data-stu-id="48d28-129">Click **OK** and then click **Create** toosave your WeChat configuration.</span></span>

