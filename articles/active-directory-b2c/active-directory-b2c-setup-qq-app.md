---
title: 'Azure Active Directory B2C: Q configuratie | Microsoft Docs'
description: Bieden zich kunnen registreren en aanmelden tooconsumers q-accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a><span data-ttu-id="f20a2-103">Azure Active Directory B2C: Tooconsumers zich kunnen registreren en aanmelden met q-accounts bieden</span><span class="sxs-lookup"><span data-stu-id="f20a2-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="f20a2-104">Deze functie is in preview.</span><span class="sxs-lookup"><span data-stu-id="f20a2-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="f20a2-105">Een q-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="f20a2-105">Create a QQ application</span></span>

<span data-ttu-id="f20a2-106">toouse q als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een toepassing q toocreate en leveren met de juiste parameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="f20a2-106">toouse QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a QQ application and supply it with hello right parameters.</span></span> <span data-ttu-id="f20a2-107">U moet een account q toodo dit.</span><span class="sxs-lookup"><span data-stu-id="f20a2-107">You need a QQ account toodo this.</span></span> <span data-ttu-id="f20a2-108">Als u niet hebt, kunt u één voor één [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span><span class="sxs-lookup"><span data-stu-id="f20a2-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-hello-qq-developer-program"></a><span data-ttu-id="f20a2-109">Registreren voor Hallo q Ontwikkelaarsprogramma</span><span class="sxs-lookup"><span data-stu-id="f20a2-109">Register for hello QQ developer program</span></span>

1. <span data-ttu-id="f20a2-110">Ga toohello [q-portal voor ontwikkelaars](http://open.qq.com) en meld u aan met de referenties van uw q-account.</span><span class="sxs-lookup"><span data-stu-id="f20a2-110">Go toohello [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="f20a2-111">Na het aanmelden, ga te[http://open.qq.com/reg](http://open.qq.com/reg) tooregister zelf als ontwikkelaar.</span><span class="sxs-lookup"><span data-stu-id="f20a2-111">After signing in, go too[http://open.qq.com/reg](http://open.qq.com/reg) tooregister yourself as a developer.</span></span>
3. <span data-ttu-id="f20a2-112">Selecteer in het menu Hallo**个人**(afzonderlijke developer).</span><span class="sxs-lookup"><span data-stu-id="f20a2-112">In hello menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="f20a2-113">Hallo vereist gegevens invoeren in Hallo-formulier en klik op**下一步**(volgende stap).</span><span class="sxs-lookup"><span data-stu-id="f20a2-113">Enter hello required information into hello form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="f20a2-114">Hallo e-verificatieproces voltooien.</span><span class="sxs-lookup"><span data-stu-id="f20a2-114">Complete hello email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="f20a2-115">U moet een paar dagen toobe goedgekeurd na de registratie als ontwikkelaar toowait.</span><span class="sxs-lookup"><span data-stu-id="f20a2-115">You will need toowait a few days toobe approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="f20a2-116">Een q-toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="f20a2-116">Register a QQ application</span></span>

1. <span data-ttu-id="f20a2-117">Ga te[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span><span class="sxs-lookup"><span data-stu-id="f20a2-117">Go too[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="f20a2-118">Klik op**应用管理**(app management).</span><span class="sxs-lookup"><span data-stu-id="f20a2-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="f20a2-119">Klik op**创建应用**(app maken).</span><span class="sxs-lookup"><span data-stu-id="f20a2-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="f20a2-120">Geef informatie op Hallo app nodig.</span><span class="sxs-lookup"><span data-stu-id="f20a2-120">Enter hello necessary app information.</span></span>
5. <span data-ttu-id="f20a2-121">Klik op**创建应用**(app maken).</span><span class="sxs-lookup"><span data-stu-id="f20a2-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="f20a2-122">Geef informatie op Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="f20a2-122">Enter hello required information.</span></span>
7. <span data-ttu-id="f20a2-123">Voor Hallo**授权回调域**(callback URL) Voer `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="f20a2-123">For hello **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="f20a2-124">Bijvoorbeeld, als uw `tenant_name` contoso.onmicrosoft.com, set Hallo URL toobe is `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="f20a2-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="f20a2-125">Klik op**创建应用**(app maken).</span><span class="sxs-lookup"><span data-stu-id="f20a2-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="f20a2-126">Klik op de pagina Bevestiging Hallo op**应用管理**(app management) tooreturn toohello app management-pagina.</span><span class="sxs-lookup"><span data-stu-id="f20a2-126">On hello confirmation page, click on **应用管理** (app management) tooreturn toohello app management page.</span></span>
10. <span data-ttu-id="f20a2-127">Klik op**查看**(weergave) volgende toohello app die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f20a2-127">Click on **查看** (view) next toohello app you just created.</span></span>
11. <span data-ttu-id="f20a2-128">Klik op**修改**(bewerken).</span><span class="sxs-lookup"><span data-stu-id="f20a2-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="f20a2-129">Kopiëren van Hallo bovenaan pagina Hallo Hallo **APP-ID** en **APP-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="f20a2-129">From hello top of hello page, copy hello **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="f20a2-130">Q configureren als een id-provider in uw tenant</span><span class="sxs-lookup"><span data-stu-id="f20a2-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="f20a2-131">Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f20a2-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="f20a2-132">Klik op de blade Hallo B2C-functies, **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="f20a2-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="f20a2-133">Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="f20a2-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="f20a2-134">Geef een beschrijvende **naam** voor Hallo identiteit provider configureren.</span><span class="sxs-lookup"><span data-stu-id="f20a2-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="f20a2-135">Voer bijvoorbeeld 'Q'.</span><span class="sxs-lookup"><span data-stu-id="f20a2-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="f20a2-136">Klik op **identiteit providertype**, selecteer **q**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f20a2-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="f20a2-137">Klik op **instellen van deze id-provider**</span><span class="sxs-lookup"><span data-stu-id="f20a2-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="f20a2-138">Voer Hallo **App-sleutel** die u eerder hebt gekopieerd als Hallo **Client-ID**.</span><span class="sxs-lookup"><span data-stu-id="f20a2-138">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="f20a2-139">Voer Hallo **App geheim** die u eerder hebt gekopieerd als Hallo **Clientgeheim**.</span><span class="sxs-lookup"><span data-stu-id="f20a2-139">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="f20a2-140">Klik op **OK** en klik vervolgens op **maken** toosave uw q-configuratie.</span><span class="sxs-lookup"><span data-stu-id="f20a2-140">Click **OK** and then click **Create** toosave your QQ configuration.</span></span>

