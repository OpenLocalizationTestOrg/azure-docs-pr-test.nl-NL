---
title: 'Azure Active Directory B2C: Facebook-configuratie | Microsoft Docs'
description: Geef tooconsumers zich kunnen registreren en aanmelden met Facebook-accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a><span data-ttu-id="5d5f6-103">Azure Active Directory B2C: Tooconsumers zich kunnen registreren en aanmelden met Facebook-accounts bieden</span><span class="sxs-lookup"><span data-stu-id="5d5f6-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="5d5f6-104">Een Facebook-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="5d5f6-104">Create a Facebook application</span></span>
<span data-ttu-id="5d5f6-105">toouse Facebook als een id-provider in Azure Active Directory (Azure AD) B2C, u moet toocreate Facebook-toepassing en leveren met de juiste parameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-105">toouse Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Facebook application and supply it with hello right parameters.</span></span> <span data-ttu-id="5d5f6-106">U moet een account Facebook toodo dit.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-106">You need a Facebook account toodo this.</span></span> <span data-ttu-id="5d5f6-107">Als u niet hebt, kunt u krijgen op het [https://www.facebook.com/](https://www.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="5d5f6-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="5d5f6-108">Ga toohello [Facebook voor ontwikkelaars](https://developers.facebook.com/) website en meld u aan met uw Facebook-accountreferenties.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-108">Go toohello [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="5d5f6-109">Als u dit nog niet hebt gedaan, moet u tooregister als ontwikkelaar Facebook.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-109">If you have not already done so, you need tooregister as a Facebook developer.</span></span> <span data-ttu-id="5d5f6-110">toodo, klikt u op **registreren** (op Hallo rechterbovenhoek van Hallo pagina), Facebook van beleidsregels accepteren en Hallo registratie stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-110">toodo this, click **Register** (on hello upper-right corner of hello page), accept Facebook's policies, and complete hello registration steps.</span></span>
3. <span data-ttu-id="5d5f6-111">Klik op **mijn Apps** en klik vervolgens op **toevoegen van een nieuwe App**.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="5d5f6-112">Hallo formulier, geeft u een **weergavenaam** en een geldig **Neem contact op met E-mail**.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-112">In hello form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="5d5f6-113">Klik op **maken van App-ID**.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-113">Click **Create App ID**.</span></span> <span data-ttu-id="5d5f6-114">Dit mogelijk dat u beleidsregels voor tooaccept Facebook-platform en een online security-controle voltooien.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-114">This may require you tooaccept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="5d5f6-115">Klik in de linkerkolom hello, **instellingen** en selecteer vervolgens **Basic** als niet al is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-115">In hello left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="5d5f6-116">Selecteer een **categorie**.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="5d5f6-117">Klik op **+ toevoegen Platform** en selecteer **Website**.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - instellingen](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - instellingen - Website](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="5d5f6-120">Voer `https://login.microsoftonline.com/` in Hallo **Site-URL** veld en klik vervolgens op **wijzigingen opslaan** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-120">Enter `https://login.microsoftonline.com/` in hello **Site URL** field and then click **Save Changes** at hello bottom of hello page.</span></span>
   
    ![Facebook - Site-URL](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="5d5f6-122">Hallo-waarde van kopiëren **App-ID**.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-122">Copy hello value of **App ID**.</span></span> <span data-ttu-id="5d5f6-123">Klik op **weergeven** en kopieer de waarde van Hallo **App geheim**.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-123">Click **Show** and copy hello value of **App Secret**.</span></span> <span data-ttu-id="5d5f6-124">U moet ze tooconfigure Facebook als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-124">You will need both of them tooconfigure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="5d5f6-125">**App-geheim** is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - App-ID en App-geheim](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="5d5f6-127">Klik op **+ Product toevoegen** Hallo linkernavigatiegedeelte en worden vervolgens Hallo **instellen** knop voor **Facebook aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-127">Click **+ Add Product** on hello left navigation and then hello **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - Facebook-aanmelding](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="5d5f6-129">Klik op **instellingen** op de juiste nav Hallo onder **Facebook-aanmelding**</span><span class="sxs-lookup"><span data-stu-id="5d5f6-129">Click **Settings** on hello right nav under **Facebook Login**</span></span>

    ![Facebook - instellingen voor Facebook-aanmelding](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="5d5f6-131">Voer `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in Hallo **geldig OAuth omleidings-URI's** veld Hallo **OAuth clientinstellingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Valid OAuth redirect URIs** field in hello **Client OAuth Settings** section.</span></span> <span data-ttu-id="5d5f6-132">Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="5d5f6-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="5d5f6-133">Klik op **wijzigingen opslaan** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-133">Click **Save Changes** at hello bottom of hello page.</span></span>
    
    ![Facebook - OAuth omleidings-URI](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="5d5f6-135">toomake uw Facebook-toepassing gebruikt door Azure AD B2C, moet u toomake deze openbaar beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-135">toomake your Facebook application usable by Azure AD B2C, you need toomake it publicly available.</span></span> <span data-ttu-id="5d5f6-136">U kunt dit doen door te klikken op **App revisie** op Hallo linkernavigatiebalk en door Hallo schakelen overschakelen bovenaan Hallo Hallo pagina te**Ja** en te klikken op **bevestigen**.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-136">You can do this by clicking **App Review** on hello left navigation and by turning hello switch at hello top of hello page too**YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - App openbare](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="5d5f6-138">Facebook configureren als een id-provider in uw tenant</span><span class="sxs-lookup"><span data-stu-id="5d5f6-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="5d5f6-139">Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-139">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="5d5f6-140">Klik op de blade Hallo B2C-functies, **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-140">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="5d5f6-141">Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-141">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="5d5f6-142">Geef een beschrijvende **naam** voor Hallo identiteit provider configureren.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-142">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="5d5f6-143">Voer bijvoorbeeld 'Facebook'.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="5d5f6-144">Klik op **identiteit providertype**, selecteer **Facebook**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="5d5f6-145">Klik op **instellen van deze id-provider** en Voer Hallo app-ID en app geheim (van Hallo Facebook-toepassing die u eerder hebt gemaakt) in Hallo **Client-ID** en **clientgeheim**respectievelijk velden.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-145">Click **Set up this identity provider** and enter hello app ID and app secret (of hello Facebook application that you created earlier) in hello **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="5d5f6-146">Klik op **OK**, en klik vervolgens op **maken** toosave uw Facebook-configuratie.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-146">Click **OK**, and then click **Create** toosave your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="5d5f6-147">Toevoegen van een **identiteitsprovider** tooyour tenant niet uw bestaande beleidsregels wijzigt.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-147">Adding an **Identity provider** tooyour tenant does not modify your existing policies.</span></span> <span data-ttu-id="5d5f6-148">Houd er rekening mee tooupdate uw beleid door Hallo-identiteitsprovider die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d5f6-148">Remember tooupdate your policies by including hello identity provider you just created.</span></span>
>