---
title: 'Azure Active Directory B2C: WeChat configuratie | Microsoft Docs'
description: Registreren en aanmelden gebruikers met een account in uw toepassingen die zijn beveiligd met Azure Active Directory B2C WeChat bieden.
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
ms.openlocfilehash: a54aec23d951610118246e9f70cdd27752ef39a6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-wechat-accounts"></a><span data-ttu-id="6901a-103">Azure Active Directory B2C: Zich kunnen registreren en aanmelden gebruikers bieden met WeChat-accounts</span><span class="sxs-lookup"><span data-stu-id="6901a-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="6901a-104">Deze functie is in preview.</span><span class="sxs-lookup"><span data-stu-id="6901a-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="6901a-105">Een toepassing WeChat maken</span><span class="sxs-lookup"><span data-stu-id="6901a-105">Create a WeChat application</span></span>

<span data-ttu-id="6901a-106">Als u wilt gebruiken als een id-provider in Azure Active Directory (Azure AD) B2C WeChat gebruikt, moet u een WeChat-toepassing maken en geeft deze met de juiste parameters.</span><span class="sxs-lookup"><span data-stu-id="6901a-106">To use WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a WeChat application and supply it with the right parameters.</span></span> <span data-ttu-id="6901a-107">U moet een account WeChat om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="6901a-107">You need a WeChat account to do this.</span></span> <span data-ttu-id="6901a-108">Als u niet hebt, kunt u een aanmelden via een van hun mobiele apps of via het nummer van uw q krijgen.</span><span class="sxs-lookup"><span data-stu-id="6901a-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="6901a-109">Hierna is uw account is geregistreerd bij de Ontwikkelaarsprogramma WeChat worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="6901a-109">After that, get your account registered with the WeChat developer program.</span></span> <span data-ttu-id="6901a-110">U vindt meer informatie [hier](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span><span class="sxs-lookup"><span data-stu-id="6901a-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="6901a-111">Een toepassing WeChat registreren</span><span class="sxs-lookup"><span data-stu-id="6901a-111">Register a WeChat application</span></span>

1. <span data-ttu-id="6901a-112">Ga naar [https://open.weixin.qq.com/](https://open.weixin.qq.com/) en zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="6901a-112">Go to [https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="6901a-113">Klik op**管理中心**(center management).</span><span class="sxs-lookup"><span data-stu-id="6901a-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="6901a-114">De benodigde stappen voor het registreren van een nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="6901a-114">Follow the necessary steps to register a new application.</span></span>
4. <span data-ttu-id="6901a-115">Voor**授权回调域**(callback URL), voer `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="6901a-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="6901a-116">Bijvoorbeeld, als uw `tenant_name` is contoso.onmicrosoft.com, de URL moet worden ingesteld `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="6901a-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="6901a-117">Vindt en kopieert de **APP-ID** en **APP-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="6901a-117">Find and copy the **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="6901a-118">U moet deze later.</span><span class="sxs-lookup"><span data-stu-id="6901a-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="6901a-119">WeChat configureren als een id-provider in uw tenant</span><span class="sxs-lookup"><span data-stu-id="6901a-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="6901a-120">Volg deze stappen voor [gaat u naar de blade B2C-functies](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6901a-120">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="6901a-121">Klik op de blade B2C-functies op **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="6901a-121">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="6901a-122">Klik op **+Toevoegen** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="6901a-122">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="6901a-123">Geef een beschrijvende **naam** voor de configuratie van de id-provider.</span><span class="sxs-lookup"><span data-stu-id="6901a-123">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="6901a-124">Voer bijvoorbeeld 'WeChat'.</span><span class="sxs-lookup"><span data-stu-id="6901a-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="6901a-125">Klik op **identiteit providertype**, selecteer **WeChat**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6901a-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="6901a-126">Klik op **instellen van deze id-provider**</span><span class="sxs-lookup"><span data-stu-id="6901a-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="6901a-127">Voer de **App-sleutel** die u eerder hebt gekopieerd als het **Client-ID**.</span><span class="sxs-lookup"><span data-stu-id="6901a-127">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="6901a-128">Voer de **App geheim** die u eerder hebt gekopieerd als het **Clientgeheim**.</span><span class="sxs-lookup"><span data-stu-id="6901a-128">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="6901a-129">Klik op **OK** en klik vervolgens op **maken** naar uw WeChat-configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="6901a-129">Click **OK** and then click **Create** to save your WeChat configuration.</span></span>

