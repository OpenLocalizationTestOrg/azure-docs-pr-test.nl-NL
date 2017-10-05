---
title: 'Azure Active Directory B2C: Configuratie Microsoft-account | Microsoft Docs'
description: Registreren en aanmelden gebruikers met een Microsoft-account in uw toepassingen die zijn beveiligd met Azure Active Directory B2C bieden.
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 59879dc0b3fc1d7af3e2a1f67f1701f451de9126
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-microsoft-accounts"></a><span data-ttu-id="a3206-103">Azure Active Directory B2C: Zich kunnen registreren en aanmelden gebruikers bieden met Microsoft-accounts</span><span class="sxs-lookup"><span data-stu-id="a3206-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="a3206-104">Een toepassing van Microsoft-account maken</span><span class="sxs-lookup"><span data-stu-id="a3206-104">Create a Microsoft account application</span></span>
<span data-ttu-id="a3206-105">Voor het gebruik van Microsoft-account als een id-provider in Azure Active Directory (Azure AD) B2C, moet u een toepassing van Microsoft-account maken en geeft deze met de juiste parameters.</span><span class="sxs-lookup"><span data-stu-id="a3206-105">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span></span> <span data-ttu-id="a3206-106">U moet een Microsoft-account om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="a3206-106">You need a Microsoft account to do this.</span></span> <span data-ttu-id="a3206-107">Als u niet hebt, kunt u krijgen op het [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="a3206-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="a3206-108">Ga naar de [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) en meld u aan met uw Microsoft-accountreferenties.</span><span class="sxs-lookup"><span data-stu-id="a3206-108">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="a3206-109">Klik op **een app toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a3206-109">Click **Add an app**.</span></span>
   
    ![Microsoft-account: een nieuwe app toevoegen](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="a3206-111">Geef een **naam** voor uw toepassing en klik op **-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="a3206-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Microsoft-account - App-naam](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="a3206-113">Kopieer de waarde van **toepassings-Id**. U hebt deze Microsoft-account configureren als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="a3206-113">Copy the value of **Application Id**. You will need it to configure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Microsoft-account - toepassings-Id](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="a3206-115">Klik op **toevoegen platform** en kies **Web**.</span><span class="sxs-lookup"><span data-stu-id="a3206-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Microsoft-account - platform toevoegen](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Microsoft-account - webservice](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="a3206-118">Voer `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in de **omleidings-URI's** veld.</span><span class="sxs-lookup"><span data-stu-id="a3206-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Redirect URIs** field.</span></span> <span data-ttu-id="a3206-119">Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="a3206-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Microsoft-account - Omleidings-URL](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="a3206-121">Klik op **nieuw wachtwoord genereren** onder de **toepassing geheimen** sectie.</span><span class="sxs-lookup"><span data-stu-id="a3206-121">Click on **Generate New Password** under the **Application Secrets** section.</span></span> <span data-ttu-id="a3206-122">Kopieer het nieuwe wachtwoord op het scherm wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a3206-122">Copy the new password displayed on screen.</span></span> <span data-ttu-id="a3206-123">U hebt deze Microsoft-account configureren als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="a3206-123">You will need it to configure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="a3206-124">Dit wachtwoord is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="a3206-124">This password is an important security credential.</span></span>
   
    ![Microsoft-account: nieuw wachtwoord genereren](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Microsoft-account - nieuw wachtwoord](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="a3206-127">Schakel het selectievakje waarin staat dat **ondersteuning voor Live SDK** onder de **geavanceerde opties** sectie.</span><span class="sxs-lookup"><span data-stu-id="a3206-127">Check the box that says **Live SDK support** under the **Advanced Options** section.</span></span> <span data-ttu-id="a3206-128">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a3206-128">Click **Save**.</span></span>
   
    ![Microsoft-account - ondersteuning voor Live SDK](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="a3206-130">Microsoft-account configureren als een id-provider in uw tenant</span><span class="sxs-lookup"><span data-stu-id="a3206-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="a3206-131">Volg deze stappen voor [gaat u naar de blade B2C-functies](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a3206-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="a3206-132">Klik op de blade B2C-functies op **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="a3206-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="a3206-133">Klik op **+Toevoegen** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="a3206-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="a3206-134">Geef een beschrijvende **naam** voor de configuratie van de id-provider.</span><span class="sxs-lookup"><span data-stu-id="a3206-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="a3206-135">Voer bijvoorbeeld 'MSA'.</span><span class="sxs-lookup"><span data-stu-id="a3206-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="a3206-136">Klik op **identiteit providertype**, selecteer **Microsoft-account**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a3206-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="a3206-137">Klik op **instellen van deze id-provider** en voer de toepassings-Id en het wachtwoord van de Microsoft-account-toepassing die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a3206-137">Click **Set up this identity provider** and enter the Application Id and password of the Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="a3206-138">Klik op **OK** en klik vervolgens op **maken** om op te slaan van de configuratie van uw Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="a3206-138">Click **OK** and then click **Create** to save your Microsoft account configuration.</span></span>

