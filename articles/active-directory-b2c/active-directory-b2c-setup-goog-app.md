---
title: 'Azure Active Directory B2C: Google + configuratie | Microsoft Docs'
description: Registreren en aanmelden gebruikers met Google + accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C bieden.
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
ms.openlocfilehash: 6ab73e5c79742ab548733f5712dee1e28461db9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-google-accounts"></a><span data-ttu-id="99978-103">Azure Active Directory B2C: Zich kunnen registreren en aanmelden gebruikers bieden met Google + accounts</span><span class="sxs-lookup"><span data-stu-id="99978-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="99978-104">Een Google +-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="99978-104">Create a Google+ application</span></span>
<span data-ttu-id="99978-105">Voor het gebruik van Google + als een id-provider in Azure Active Directory (Azure AD) B2C, moet u een Google +-toepassing maken en geeft deze met de juiste parameters.</span><span class="sxs-lookup"><span data-stu-id="99978-105">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="99978-106">U moet een account Google + om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="99978-106">You need a Google+ account to do this.</span></span> <span data-ttu-id="99978-107">Als u niet hebt, kunt u krijgen op het [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="99978-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="99978-108">Ga naar de [Google ontwikkelaars Console](https://console.developers.google.com/) en meld u aan met de referenties van uw Google + account.</span><span class="sxs-lookup"><span data-stu-id="99978-108">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="99978-109">Klik op **project maken**, voer een **projectnaam**, en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="99978-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google + - aan de slag](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google + - nieuw project](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="99978-112">Klik op **API Manager** en klik vervolgens op **referenties** in de linkernavigatiebalk.</span><span class="sxs-lookup"><span data-stu-id="99978-112">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
4. <span data-ttu-id="99978-113">Klik op de **OAuth toestemming scherm** boven op het tabblad.</span><span class="sxs-lookup"><span data-stu-id="99978-113">Click the **OAuth consent screen** tab at the top.</span></span>
   
    ![Google + - referenties](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="99978-115">Selecteer of geef een geldige **e-mailadres**, bieden een **Productnaam**, en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="99978-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google + - OAuth toestemming scherm](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="99978-117">Klik op **nieuwe referenties** en kies vervolgens **OAuth-Clientidentiteit**.</span><span class="sxs-lookup"><span data-stu-id="99978-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google + - OAuth toestemming scherm](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="99978-119">Onder **toepassingstype**, selecteer **webtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="99978-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google + - OAuth toestemming scherm](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="99978-121">Geef een **naam** voor uw toepassing, voert u `https://login.microsoftonline.com` in de **geautoriseerd JavaScript oorsprongen** veld en `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in de **geautoriseerde omleidings-URI's** veld.</span><span class="sxs-lookup"><span data-stu-id="99978-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="99978-122">Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="99978-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="99978-123">De **{tenant}** hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="99978-123">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="99978-124">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="99978-124">Click **Create**.</span></span>
   
    ![Google + - client-ID maken](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="99978-126">Kopieer de waarden van **Client-ID** en **clientgeheim**.</span><span class="sxs-lookup"><span data-stu-id="99978-126">Copy the values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="99978-127">U moet beide parameters voor het configureren van Google + als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="99978-127">You will need both of them to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="99978-128">**Clientgeheim** is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="99978-128">**Client secret** is an important security credential.</span></span>
   
    ![Google + - clientgeheim](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="99978-130">Google + als een id-provider in uw tenant configureren</span><span class="sxs-lookup"><span data-stu-id="99978-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="99978-131">Volg deze stappen voor [gaat u naar de blade B2C-functies](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="99978-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="99978-132">Klik op de blade B2C-functies op **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="99978-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="99978-133">Klik op **+Toevoegen** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="99978-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="99978-134">Geef een beschrijvende **naam** voor de configuratie van de id-provider.</span><span class="sxs-lookup"><span data-stu-id="99978-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="99978-135">Voer bijvoorbeeld "G +".</span><span class="sxs-lookup"><span data-stu-id="99978-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="99978-136">Klik op **identiteit providertype**, selecteer **Google**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="99978-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="99978-137">Klik op **instellen van deze id-provider** en voer de client-ID en clientgeheim van de Google +-toepassing die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="99978-137">Click **Set up this identity provider** and enter the client ID and client secret of the Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="99978-138">Klik op **OK** en klik vervolgens op **maken** voor uw Google +-configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="99978-138">Click **OK** and then click **Create** to save your Google+ configuration.</span></span>

