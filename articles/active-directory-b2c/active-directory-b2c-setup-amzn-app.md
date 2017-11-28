---
title: 'Azure Active Directory B2C: Amazon configuratie | Microsoft Docs'
description: Geef tooconsumers zich kunnen registreren en aanmelden met Amazon-accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a><span data-ttu-id="cae95-103">Azure Active Directory B2C: Tooconsumers zich kunnen registreren en aanmelden met Amazon-accounts bieden</span><span class="sxs-lookup"><span data-stu-id="cae95-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="cae95-104">Een Amazon-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="cae95-104">Create an Amazon application</span></span>
<span data-ttu-id="cae95-105">toouse Amazon als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een toepassing Amazon toocreate en leveren met de juiste parameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="cae95-105">toouse Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an Amazon application and supply it with hello right parameters.</span></span> <span data-ttu-id="cae95-106">U moet een Amazon-account toodo dit.</span><span class="sxs-lookup"><span data-stu-id="cae95-106">You need an Amazon account toodo this.</span></span> <span data-ttu-id="cae95-107">Als u niet hebt, kunt u krijgen op het [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="cae95-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="cae95-108">Ga toohello [Amazon Developer Center](https://login.amazon.com/) en meld u aan met de referenties van uw Amazon-account.</span><span class="sxs-lookup"><span data-stu-id="cae95-108">Go toohello [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="cae95-109">Als u dit nog niet hebt gedaan, klikt u op **aanmelden**stappen Hallo developer-registratie en Hallo beleid accepteren.</span><span class="sxs-lookup"><span data-stu-id="cae95-109">If you have not already done so, click **Sign Up**, follow hello developer registration steps, and accept hello policy.</span></span>
3. <span data-ttu-id="cae95-110">Klik op **nieuwe toepassing registreren**.</span><span class="sxs-lookup"><span data-stu-id="cae95-110">Click **Register new application**.</span></span>
   
    ![Registreren van een nieuwe toepassing op Hallo Amazon-website](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="cae95-112">Bevatten toepassingsinformatie (**naam**, **beschrijving**, en **Privacy-URL voor kennisgeving**) en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cae95-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Informatie over de toepassing voor het registreren van een nieuwe toepassing op de Amazon bieden](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="cae95-114">In Hallo **Webinstellingen** sectie kopiëren Hallo waarden van **Client-ID** en **Clientgeheim**.</span><span class="sxs-lookup"><span data-stu-id="cae95-114">In hello **Web Settings** section, copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="cae95-115">(U moet tooclick hello **geheim weergeven** toosee knop dit.) U moet beide tooconfigure Amazon als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="cae95-115">(You need tooclick hello **Show Secret** button toosee this.) You need both of them tooconfigure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="cae95-116">Klik op **bewerken** onderaan Hallo Hallo-sectie.</span><span class="sxs-lookup"><span data-stu-id="cae95-116">Click **Edit** at hello bottom of hello section.</span></span> <span data-ttu-id="cae95-117">**Clientgeheim** is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="cae95-117">**Client Secret** is an important security credential.</span></span>
   
    ![Client-ID en Clientgeheim bieden voor uw nieuwe toepassing op de Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="cae95-119">Voer `https://login.microsoftonline.com` in Hallo **toegestaan JavaScript oorsprongen** veld en `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in Hallo **retourneren URL's toegestaan** veld.</span><span class="sxs-lookup"><span data-stu-id="cae95-119">Enter `https://login.microsoftonline.com` in hello **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Allowed Return URLs** field.</span></span> <span data-ttu-id="cae95-120">Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld: contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="cae95-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="cae95-121">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cae95-121">Click **Save**.</span></span> <span data-ttu-id="cae95-122">Hallo **{tenant}** hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="cae95-122">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![Oorsprongen JavaScript en retourneren URL's voorziet in uw nieuwe toepassing op de Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="cae95-124">Amazon configureren als een id-provider in uw tenant</span><span class="sxs-lookup"><span data-stu-id="cae95-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="cae95-125">Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cae95-125">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="cae95-126">Klik op de blade Hallo B2C-functies, **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="cae95-126">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="cae95-127">Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="cae95-127">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="cae95-128">Geef een beschrijvende **naam** voor Hallo identiteit provider configureren.</span><span class="sxs-lookup"><span data-stu-id="cae95-128">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="cae95-129">Voer bijvoorbeeld 'Amzn'.</span><span class="sxs-lookup"><span data-stu-id="cae95-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="cae95-130">Klik op **identiteit providertype**, selecteer **Amazon**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="cae95-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="cae95-131">Klik op **instellen van deze id-provider** en Voer Hallo-ID en client clientgeheim Hallo Amazon-toepassing die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cae95-131">Click **Set up this identity provider** and enter hello client ID and client secret of hello Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="cae95-132">Klik op **OK** en klik vervolgens op **maken** toosave uw Amazon-configuratie.</span><span class="sxs-lookup"><span data-stu-id="cae95-132">Click **OK** and then click **Create** toosave your Amazon configuration.</span></span>

