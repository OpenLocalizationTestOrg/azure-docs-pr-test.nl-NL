---
title: 'Azure Active Directory B2C: Google + configuratie | Microsoft Docs'
description: Geef tooconsumers zich kunnen registreren en aanmelden met Google + accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a><span data-ttu-id="ede32-103">Azure Active Directory B2C: Bieden tooconsumers zich kunnen registreren en aanmelden met Google + accounts</span><span class="sxs-lookup"><span data-stu-id="ede32-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="ede32-104">Een Google +-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="ede32-104">Create a Google+ application</span></span>
<span data-ttu-id="ede32-105">toouse Google + als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een Google +-toepassing toocreate en leveren met de juiste parameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="ede32-105">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="ede32-106">U moet een Google + account toodo dit.</span><span class="sxs-lookup"><span data-stu-id="ede32-106">You need a Google+ account toodo this.</span></span> <span data-ttu-id="ede32-107">Als u niet hebt, kunt u krijgen op het [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="ede32-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="ede32-108">Ga toohello [Google ontwikkelaars Console](https://console.developers.google.com/) en meld u aan met de referenties van uw Google + account.</span><span class="sxs-lookup"><span data-stu-id="ede32-108">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="ede32-109">Klik op **project maken**, voer een **projectnaam**, en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="ede32-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google + - aan de slag](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google + - nieuw project](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="ede32-112">Klik op **API Manager** en klik vervolgens op **referenties** in Hallo linkernavigatiebalk.</span><span class="sxs-lookup"><span data-stu-id="ede32-112">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
4. <span data-ttu-id="ede32-113">Klik op Hallo **OAuth toestemming scherm** Hallo boven op tabblad.</span><span class="sxs-lookup"><span data-stu-id="ede32-113">Click hello **OAuth consent screen** tab at hello top.</span></span>
   
    ![Google + - referenties](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="ede32-115">Selecteer of geef een geldige **e-mailadres**, bieden een **Productnaam**, en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ede32-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google + - OAuth toestemming scherm](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="ede32-117">Klik op **nieuwe referenties** en kies vervolgens **OAuth-Clientidentiteit**.</span><span class="sxs-lookup"><span data-stu-id="ede32-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google + - OAuth toestemming scherm](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="ede32-119">Onder **toepassingstype**, selecteer **webtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="ede32-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google + - OAuth toestemming scherm](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="ede32-121">Geef een **naam** voor uw toepassing, voert u `https://login.microsoftonline.com` in Hallo **geautoriseerd JavaScript oorsprongen** veld en `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in Hallo **geautoriseerde omleidings-URI's**veld.</span><span class="sxs-lookup"><span data-stu-id="ede32-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="ede32-122">Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="ede32-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="ede32-123">Hallo **{tenant}** hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="ede32-123">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="ede32-124">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ede32-124">Click **Create**.</span></span>
   
    ![Google + - client-ID maken](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="ede32-126">Kopieer de waarden Hallo van **Client-ID** en **clientgeheim**.</span><span class="sxs-lookup"><span data-stu-id="ede32-126">Copy hello values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="ede32-127">U moet ze tooconfigure Google + als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="ede32-127">You will need both of them tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="ede32-128">**Clientgeheim** is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="ede32-128">**Client secret** is an important security credential.</span></span>
   
    ![Google + - clientgeheim](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="ede32-130">Google + als een id-provider in uw tenant configureren</span><span class="sxs-lookup"><span data-stu-id="ede32-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="ede32-131">Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ede32-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="ede32-132">Klik op de blade Hallo B2C-functies, **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="ede32-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="ede32-133">Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="ede32-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="ede32-134">Geef een beschrijvende **naam** voor Hallo identiteit provider configureren.</span><span class="sxs-lookup"><span data-stu-id="ede32-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="ede32-135">Voer bijvoorbeeld "G +".</span><span class="sxs-lookup"><span data-stu-id="ede32-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="ede32-136">Klik op **identiteit providertype**, selecteer **Google**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ede32-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="ede32-137">Klik op **instellen van deze id-provider** en Voer Hallo-ID en client clientgeheim Hallo Google +-toepassing die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ede32-137">Click **Set up this identity provider** and enter hello client ID and client secret of hello Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="ede32-138">Klik op **OK** en klik vervolgens op **maken** toosave uw Google +-configuratie.</span><span class="sxs-lookup"><span data-stu-id="ede32-138">Click **OK** and then click **Create** toosave your Google+ configuration.</span></span>

