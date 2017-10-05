---
title: 'Azure Active Directory B2C: Facebook-configuratie | Microsoft Docs'
description: Registreren en aanmelden gebruikers met Facebook-accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C bieden.
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
ms.openlocfilehash: 8c2154fcf33537358b549395d15b4ba937371cd0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-facebook-accounts"></a><span data-ttu-id="8464a-103">Azure Active Directory B2C: Zich kunnen registreren en aanmelden gebruikers bieden met Facebook-accounts</span><span class="sxs-lookup"><span data-stu-id="8464a-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="8464a-104">Een Facebook-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="8464a-104">Create a Facebook application</span></span>
<span data-ttu-id="8464a-105">Als u wilt gebruiken als een id-provider in Azure Active Directory (Azure AD) B2C Facebook gebruikt, moet u een Facebook-toepassing maken en geeft deze met de juiste parameters.</span><span class="sxs-lookup"><span data-stu-id="8464a-105">To use Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Facebook application and supply it with the right parameters.</span></span> <span data-ttu-id="8464a-106">U moet een Facebook-account om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="8464a-106">You need a Facebook account to do this.</span></span> <span data-ttu-id="8464a-107">Als u niet hebt, kunt u krijgen op het [https://www.facebook.com/](https://www.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="8464a-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="8464a-108">Ga naar de [Facebook voor ontwikkelaars](https://developers.facebook.com/) website en meld u aan met uw Facebook-accountreferenties.</span><span class="sxs-lookup"><span data-stu-id="8464a-108">Go to the [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="8464a-109">Als u dit nog niet hebt gedaan, moet u registreren als een ontwikkelaar Facebook.</span><span class="sxs-lookup"><span data-stu-id="8464a-109">If you have not already done so, you need to register as a Facebook developer.</span></span> <span data-ttu-id="8464a-110">Om dit te doen, klikt u op **registreren** (in de rechterbovenhoek van de pagina), accepteert de Facebook-beleid en voltooi de stappen registratie.</span><span class="sxs-lookup"><span data-stu-id="8464a-110">To do this, click **Register** (on the upper-right corner of the page), accept Facebook's policies, and complete the registration steps.</span></span>
3. <span data-ttu-id="8464a-111">Klik op **mijn Apps** en klik vervolgens op **toevoegen van een nieuwe App**.</span><span class="sxs-lookup"><span data-stu-id="8464a-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="8464a-112">Geef in het formulier een **weergavenaam** en een geldig **Neem contact op met E-mail**.</span><span class="sxs-lookup"><span data-stu-id="8464a-112">In the form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="8464a-113">Klik op **maken van App-ID**.</span><span class="sxs-lookup"><span data-stu-id="8464a-113">Click **Create App ID**.</span></span> <span data-ttu-id="8464a-114">Mogelijk moet u Facebook platform beleidsregels accepteren en een online security-controle voltooien.</span><span class="sxs-lookup"><span data-stu-id="8464a-114">This may require you to accept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="8464a-115">Klik in de linkerkolom **instellingen** en selecteer vervolgens **Basic** als niet al is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8464a-115">In the left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="8464a-116">Selecteer een **categorie**.</span><span class="sxs-lookup"><span data-stu-id="8464a-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="8464a-117">Klik op **+ toevoegen Platform** en selecteer **Website**.</span><span class="sxs-lookup"><span data-stu-id="8464a-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - instellingen](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - instellingen - Website](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="8464a-120">Voer `https://login.microsoftonline.com/` in de **Site-URL** veld en klik vervolgens op **wijzigingen opslaan** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="8464a-120">Enter `https://login.microsoftonline.com/` in the **Site URL** field and then click **Save Changes** at the bottom of the page.</span></span>
   
    ![Facebook - Site-URL](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="8464a-122">Kopieer de waarde van **App-ID**.</span><span class="sxs-lookup"><span data-stu-id="8464a-122">Copy the value of **App ID**.</span></span> <span data-ttu-id="8464a-123">Klik op **weergeven** en kopieer de waarde van **App geheim**.</span><span class="sxs-lookup"><span data-stu-id="8464a-123">Click **Show** and copy the value of **App Secret**.</span></span> <span data-ttu-id="8464a-124">U moet beide Facebook configureren als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="8464a-124">You will need both of them to configure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="8464a-125">**App-geheim** is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="8464a-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - App-ID en App-geheim](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="8464a-127">Klik op **+ Product toevoegen** voor het linkernavigatiegedeelte en vervolgens de **instellen** knop voor **Facebook aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="8464a-127">Click **+ Add Product** on the left navigation and then the **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - Facebook-aanmelding](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="8464a-129">Klik op **instellingen** op de juiste nav onder **Facebook-aanmelding**</span><span class="sxs-lookup"><span data-stu-id="8464a-129">Click **Settings** on the right nav under **Facebook Login**</span></span>

    ![Facebook - instellingen voor Facebook-aanmelding](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="8464a-131">Voer `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in de **geldig OAuth omleidings-URI's** veld in de **OAuth clientinstellingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="8464a-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Valid OAuth redirect URIs** field in the **Client OAuth Settings** section.</span></span> <span data-ttu-id="8464a-132">Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="8464a-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="8464a-133">Klik op **wijzigingen opslaan** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="8464a-133">Click **Save Changes** at the bottom of the page.</span></span>
    
    ![Facebook - OAuth omleidings-URI](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="8464a-135">Als u uw Facebook-toepassing gebruikt door Azure AD B2C, moet u het openbaar beschikbaar maken.</span><span class="sxs-lookup"><span data-stu-id="8464a-135">To make your Facebook application usable by Azure AD B2C, you need to make it publicly available.</span></span> <span data-ttu-id="8464a-136">U kunt dit doen door te klikken op **App revisie** voor het linkernavigatiegedeelte en door het inschakelen van de switch aan de bovenkant van de pagina **Ja** en te klikken op **bevestigen**.</span><span class="sxs-lookup"><span data-stu-id="8464a-136">You can do this by clicking **App Review** on the left navigation and by turning the switch at the top of the page to **YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - App openbare](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="8464a-138">Facebook configureren als een id-provider in uw tenant</span><span class="sxs-lookup"><span data-stu-id="8464a-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="8464a-139">Volg deze stappen voor [gaat u naar de blade B2C-functies](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8464a-139">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="8464a-140">Klik op de blade B2C-functies op **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="8464a-140">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="8464a-141">Klik op **+Toevoegen** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="8464a-141">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="8464a-142">Geef een beschrijvende **naam** voor de configuratie van de id-provider.</span><span class="sxs-lookup"><span data-stu-id="8464a-142">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="8464a-143">Voer bijvoorbeeld 'Facebook'.</span><span class="sxs-lookup"><span data-stu-id="8464a-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="8464a-144">Klik op **identiteit providertype**, selecteer **Facebook**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8464a-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="8464a-145">Klik op **instellen van deze id-provider** en voer de app-ID en app-geheim (van de Facebook-toepassing die u eerder hebt gemaakt) in de **Client-ID** en **clientgeheim** respectievelijk de velden.</span><span class="sxs-lookup"><span data-stu-id="8464a-145">Click **Set up this identity provider** and enter the app ID and app secret (of the Facebook application that you created earlier) in the **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="8464a-146">Klik op **OK**, en klik vervolgens op **maken** naar uw Facebook-configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="8464a-146">Click **OK**, and then click **Create** to save your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="8464a-147">Toevoegen van een **identiteitsprovider** in uw tenant, uw bestaande beleidsregels niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8464a-147">Adding an **Identity provider** to your tenant does not modify your existing policies.</span></span> <span data-ttu-id="8464a-148">Vergeet niet uw beleidsregels bijwerken door de identiteitsprovider die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8464a-148">Remember to update your policies by including the identity provider you just created.</span></span>
>