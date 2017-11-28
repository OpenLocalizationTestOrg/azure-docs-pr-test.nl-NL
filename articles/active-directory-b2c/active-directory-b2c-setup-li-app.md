---
title: 'Azure Active Directory B2C: LinkedIn configuratie | Microsoft Docs'
description: Registreren en aanmelden tooconsumers voorzien van LinkedIn accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a><span data-ttu-id="0ffd9-103">Azure Active Directory B2C: Bieden LinkedIn accounts zich kunnen registreren en aanmelden tooconsumers</span><span class="sxs-lookup"><span data-stu-id="0ffd9-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="0ffd9-104">Een LinkedIn-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="0ffd9-104">Create a LinkedIn application</span></span>
<span data-ttu-id="0ffd9-105">toouse LinkedIn als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een toepassing LinkedIn toocreate en leveren met de juiste parameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-105">toouse LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a LinkedIn application and supply it with hello right parameters.</span></span> <span data-ttu-id="0ffd9-106">U moet een account LinkedIn toodo dit.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-106">You need a LinkedIn account toodo this.</span></span> <span data-ttu-id="0ffd9-107">Als u niet hebt, kunt u krijgen op het [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="0ffd9-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="0ffd9-108">Ga toohello [LinkedIn ontwikkelaars website](https://www.developer.linkedin.com/) en meld u aan met de referenties van uw LinkedIn-account.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-108">Go toohello [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="0ffd9-109">Klik op **mijn Apps** in Hallo bovenste menubalk en klik vervolgens op **toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-109">Click **My Apps** in hello top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn - nieuwe app](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="0ffd9-111">In Hallo **Maak een nieuwe toepassing** Vul Hallo relevante informatie (**bedrijfsnaam**, **naam**, **beschrijving**, **Toepassing Logo URL**, **toepassing gebruik**, **Website-URL**, **zakelijke e** en **telefoon (werk)**).</span><span class="sxs-lookup"><span data-stu-id="0ffd9-111">In hello **Create a New Application** form, fill in hello relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="0ffd9-112">Ik ga hiermee akkoord toohello **LinkedIn API gebruiksvoorwaarden** en klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-112">Agree toohello **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - app registreren](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="0ffd9-114">Kopieer de waarden Hallo van **Client-ID** en **Clientgeheim**.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-114">Copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="0ffd9-115">(U vindt deze onder **verificatiesleutels**.) U moet ze tooconfigure LinkedIn als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-115">(You can find them under **Authentication Keys**.) You will need both of them tooconfigure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0ffd9-116">**Clientgeheim** is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="0ffd9-117">Voer `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in Hallo **geautoriseerd Omleidings-URL's** veld (onder **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="0ffd9-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="0ffd9-118">Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld: contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="0ffd9-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="0ffd9-119">Klik op **toevoegen**, en klik vervolgens op **Update**.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="0ffd9-120">Hallo **{tenant}** hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-120">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn - Setup-app](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="0ffd9-122">LinkedIn configureren als een id-provider in uw tenant</span><span class="sxs-lookup"><span data-stu-id="0ffd9-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="0ffd9-123">Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-123">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="0ffd9-124">Klik op de blade Hallo B2C-functies, **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-124">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="0ffd9-125">Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-125">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="0ffd9-126">Geef een beschrijvende **naam** voor Hallo identiteit provider configureren.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-126">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="0ffd9-127">Voer bijvoorbeeld 'LI'.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="0ffd9-128">Klik op **identiteit providertype**, selecteer **LinkedIn**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="0ffd9-129">Klik op **instellen van deze id-provider** en Voer Hallo-ID en client clientgeheim Hallo LinkedIn-toepassing die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-129">Click **Set up this identity provider** and enter hello client ID and client secret of hello LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="0ffd9-130">Klik op **OK** en klik vervolgens op **maken** toosave uw LinkedIn-configuratie.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-130">Click **OK** and then click **Create** toosave your LinkedIn configuration.</span></span>

