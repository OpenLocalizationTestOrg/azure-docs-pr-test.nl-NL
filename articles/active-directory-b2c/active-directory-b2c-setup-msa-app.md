---
title: 'Azure Active Directory B2C: Configuratie Microsoft-account | Microsoft Docs'
description: Tooconsumers zich kunnen registreren en aanmelden met Microsoft-accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C opgeven.
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
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a><span data-ttu-id="dbca9-103">Azure Active Directory B2C: Tooconsumers zich kunnen registreren en aanmelden met Microsoft-accounts bieden</span><span class="sxs-lookup"><span data-stu-id="dbca9-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="dbca9-104">Een toepassing van Microsoft-account maken</span><span class="sxs-lookup"><span data-stu-id="dbca9-104">Create a Microsoft account application</span></span>
<span data-ttu-id="dbca9-105">toouse Microsoft account toe als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een Microsoft-account-toepassing toocreate en leveren met de juiste parameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="dbca9-105">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="dbca9-106">U moet een Microsoft-account toodo dit.</span><span class="sxs-lookup"><span data-stu-id="dbca9-106">You need a Microsoft account toodo this.</span></span> <span data-ttu-id="dbca9-107">Als u niet hebt, kunt u krijgen op het [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="dbca9-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="dbca9-108">Ga toohello [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) en meld u aan met uw Microsoft-accountreferenties.</span><span class="sxs-lookup"><span data-stu-id="dbca9-108">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="dbca9-109">Klik op **een app toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="dbca9-109">Click **Add an app**.</span></span>
   
    ![Microsoft-account: een nieuwe app toevoegen](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="dbca9-111">Geef een **naam** voor uw toepassing en klik op **-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="dbca9-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Microsoft-account - App-naam](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="dbca9-113">Hallo-waarde van kopiëren **toepassings-Id**. U hebt deze tooconfigure Microsoft-account als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="dbca9-113">Copy hello value of **Application Id**. You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Microsoft-account - toepassings-Id](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="dbca9-115">Klik op **toevoegen platform** en kies **Web**.</span><span class="sxs-lookup"><span data-stu-id="dbca9-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Microsoft-account - platform toevoegen](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Microsoft-account - webservice](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="dbca9-118">Voer `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in Hallo **omleidings-URI's** veld.</span><span class="sxs-lookup"><span data-stu-id="dbca9-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="dbca9-119">Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="dbca9-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Microsoft-account - Omleidings-URL](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="dbca9-121">Klik op **nieuw wachtwoord genereren** onder Hallo **toepassing geheimen** sectie.</span><span class="sxs-lookup"><span data-stu-id="dbca9-121">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="dbca9-122">Kopieer Hallo nieuw wachtwoord op het scherm wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="dbca9-122">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="dbca9-123">U hebt deze tooconfigure Microsoft-account als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="dbca9-123">You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="dbca9-124">Dit wachtwoord is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="dbca9-124">This password is an important security credential.</span></span>
   
    ![Microsoft-account: nieuw wachtwoord genereren](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Microsoft-account - nieuw wachtwoord](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="dbca9-127">Selectievakje Hallo waarin staat dat **ondersteuning voor Live SDK** onder Hallo **geavanceerde opties** sectie.</span><span class="sxs-lookup"><span data-stu-id="dbca9-127">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="dbca9-128">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="dbca9-128">Click **Save**.</span></span>
   
    ![Microsoft-account - ondersteuning voor Live SDK](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="dbca9-130">Microsoft-account configureren als een id-provider in uw tenant</span><span class="sxs-lookup"><span data-stu-id="dbca9-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="dbca9-131">Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="dbca9-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="dbca9-132">Klik op de blade Hallo B2C-functies, **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="dbca9-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="dbca9-133">Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="dbca9-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="dbca9-134">Geef een beschrijvende **naam** voor Hallo identiteit provider configureren.</span><span class="sxs-lookup"><span data-stu-id="dbca9-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="dbca9-135">Voer bijvoorbeeld 'MSA'.</span><span class="sxs-lookup"><span data-stu-id="dbca9-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="dbca9-136">Klik op **identiteit providertype**, selecteer **Microsoft-account**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="dbca9-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="dbca9-137">Klik op **instellen van deze id-provider** en Voer Hallo toepassings-Id en het wachtwoord van Hallo Microsoft-account-toepassing die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="dbca9-137">Click **Set up this identity provider** and enter hello Application Id and password of hello Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="dbca9-138">Klik op **OK** en klik vervolgens op **maken** toosave je Microsoft-account configureren.</span><span class="sxs-lookup"><span data-stu-id="dbca9-138">Click **OK** and then click **Create** toosave your Microsoft account configuration.</span></span>

