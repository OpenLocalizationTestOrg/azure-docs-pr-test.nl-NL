---
title: 'Azure Active Directory B2C: LinkedIn configuratie | Microsoft Docs'
description: Gebruikers met een account in uw toepassingen die zijn beveiligd met Azure Active Directory B2C LinkedIn bieden zich kunnen registreren en aanmelden
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
ms.openlocfilehash: 1a6c4b19261aa34e668554ccad2b6340cddf9bf5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-linkedin-accounts"></a><span data-ttu-id="98c23-103">Azure Active Directory B2C: Zich kunnen registreren en aanmelden gebruikers bieden met LinkedIn-accounts</span><span class="sxs-lookup"><span data-stu-id="98c23-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="98c23-104">Een LinkedIn-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="98c23-104">Create a LinkedIn application</span></span>
<span data-ttu-id="98c23-105">Als u wilt gebruiken als een id-provider in Azure Active Directory (Azure AD) B2C LinkedIn gebruikt, moet u een LinkedIn-toepassing maken en geeft deze met de juiste parameters.</span><span class="sxs-lookup"><span data-stu-id="98c23-105">To use LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a LinkedIn application and supply it with the right parameters.</span></span> <span data-ttu-id="98c23-106">U moet een LinkedIn-account om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="98c23-106">You need a LinkedIn account to do this.</span></span> <span data-ttu-id="98c23-107">Als u niet hebt, kunt u krijgen op het [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="98c23-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="98c23-108">Ga naar de [LinkedIn ontwikkelaars website](https://www.developer.linkedin.com/) en meld u aan met de referenties van uw LinkedIn-account.</span><span class="sxs-lookup"><span data-stu-id="98c23-108">Go to the [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="98c23-109">Klik op **mijn Apps** in de bovenste menubalk en klik vervolgens op **toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="98c23-109">Click **My Apps** in the top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn - nieuwe app](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="98c23-111">In de **Maak een nieuwe toepassing** Vul de relevante informatie (**bedrijfsnaam**, **naam**, **beschrijving**, **Toepassing Logo URL**, **toepassing gebruik**, **Website-URL**, **zakelijke e** en **telefoon (werk)**).</span><span class="sxs-lookup"><span data-stu-id="98c23-111">In the **Create a New Application** form, fill in the relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="98c23-112">Ga akkoord met de **LinkedIn API gebruiksvoorwaarden** en klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="98c23-112">Agree to the **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - app registreren](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="98c23-114">Kopieer de waarden van **Client-ID** en **Clientgeheim**.</span><span class="sxs-lookup"><span data-stu-id="98c23-114">Copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="98c23-115">(U vindt deze onder **verificatiesleutels**.) U moet beide LinkedIn configureren als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="98c23-115">(You can find them under **Authentication Keys**.) You will need both of them to configure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="98c23-116">**Clientgeheim** is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="98c23-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="98c23-117">Voer `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in de **geautoriseerd Omleidings-URL's** veld (onder **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="98c23-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="98c23-118">Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld: contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="98c23-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="98c23-119">Klik op **toevoegen**, en klik vervolgens op **Update**.</span><span class="sxs-lookup"><span data-stu-id="98c23-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="98c23-120">De **{tenant}** hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="98c23-120">The **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn - Setup-app](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="98c23-122">LinkedIn configureren als een id-provider in uw tenant</span><span class="sxs-lookup"><span data-stu-id="98c23-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="98c23-123">Volg deze stappen voor [gaat u naar de blade B2C-functies](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="98c23-123">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="98c23-124">Klik op de blade B2C-functies op **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="98c23-124">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="98c23-125">Klik op **+Toevoegen** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="98c23-125">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="98c23-126">Geef een beschrijvende **naam** voor de configuratie van de id-provider.</span><span class="sxs-lookup"><span data-stu-id="98c23-126">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="98c23-127">Voer bijvoorbeeld 'LI'.</span><span class="sxs-lookup"><span data-stu-id="98c23-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="98c23-128">Klik op **identiteit providertype**, selecteer **LinkedIn**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="98c23-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="98c23-129">Klik op **instellen van deze id-provider** en voer de client-ID en clientgeheim van de LinkedIn-toepassing die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="98c23-129">Click **Set up this identity provider** and enter the client ID and client secret of the LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="98c23-130">Klik op **OK** en klik vervolgens op **maken** naar uw LinkedIn-configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="98c23-130">Click **OK** and then click **Create** to save your LinkedIn configuration.</span></span>

