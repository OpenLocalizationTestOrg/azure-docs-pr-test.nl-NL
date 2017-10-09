---
title: 'Zelfstudie: Azure Active Directory-integratie met ThousandEyes | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ThousandEyes.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="852f9-103">Zelfstudie: Azure Active Directory-integratie met ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="852f9-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>

<span data-ttu-id="852f9-104">In deze zelfstudie leert u hoe toointegrate ThousandEyes met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="852f9-104">In this tutorial, you learn how toointegrate ThousandEyes with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="852f9-105">ThousandEyes integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="852f9-105">Integrating ThousandEyes with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="852f9-106">U kunt beheren in Azure AD die tooThousandEyes toegang heeft</span><span class="sxs-lookup"><span data-stu-id="852f9-106">You can control in Azure AD who has access tooThousandEyes</span></span>
- <span data-ttu-id="852f9-107">U kunt uw gebruikers tooautomatically get aangemelde tooThousandEyes (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="852f9-107">You can enable your users tooautomatically get signed-on tooThousandEyes (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="852f9-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="852f9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="852f9-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="852f9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="852f9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="852f9-110">Prerequisites</span></span>

<span data-ttu-id="852f9-111">Azure AD-integratie met ThousandEyes tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="852f9-111">tooconfigure Azure AD integration with ThousandEyes, you need hello following items:</span></span>

- <span data-ttu-id="852f9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="852f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="852f9-113">Een ThousandEyes eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="852f9-113">A ThousandEyes single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="852f9-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="852f9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="852f9-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="852f9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="852f9-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="852f9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="852f9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="852f9-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="852f9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="852f9-118">Scenario description</span></span>
<span data-ttu-id="852f9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="852f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="852f9-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="852f9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="852f9-121">Het toevoegen van ThousandEyes van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="852f9-121">Adding ThousandEyes from hello gallery</span></span>
2. <span data-ttu-id="852f9-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="852f9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thousandeyes-from-hello-gallery"></a><span data-ttu-id="852f9-123">Het toevoegen van ThousandEyes van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="852f9-123">Adding ThousandEyes from hello gallery</span></span>
<span data-ttu-id="852f9-124">tooconfigure hello integratie van ThousandEyes in Azure AD, moet u tooadd ThousandEyes uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="852f9-124">tooconfigure hello integration of ThousandEyes into Azure AD, you need tooadd ThousandEyes from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="852f9-125">**tooadd ThousandEyes via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="852f9-125">**tooadd ThousandEyes from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="852f9-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="852f9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="852f9-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="852f9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="852f9-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="852f9-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="852f9-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="852f9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="852f9-133">Typ in het zoekvak Hallo **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="852f9-133">In hello search box, type **ThousandEyes**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. <span data-ttu-id="852f9-135">Selecteer in het deelvenster resultaten hello, **ThousandEyes**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="852f9-135">In hello results panel, select **ThousandEyes**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="852f9-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="852f9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="852f9-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met ThousandEyes op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="852f9-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="852f9-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ThousandEyes is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="852f9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThousandEyes is tooa user in Azure AD.</span></span> <span data-ttu-id="852f9-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in ThousandEyes toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="852f9-140">In other words, a link relationship between an Azure AD user and hello related user in ThousandEyes needs toobe established.</span></span>

<span data-ttu-id="852f9-141">Wijs in ThousandEyes, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="852f9-141">In ThousandEyes, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="852f9-142">tooconfigure en eenmalige aanmelding Azure AD-test met ThousandEyes, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="852f9-142">tooconfigure and test Azure AD single sign-on with ThousandEyes, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="852f9-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="852f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="852f9-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="852f9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="852f9-145">**[Maken van een testgebruiker ThousandEyes](#creating-a-thousandeyes-test-user)**  -toohave een equivalent van Britta Simon in ThousandEyes die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="852f9-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - toohave a counterpart of Britta Simon in ThousandEyes that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="852f9-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="852f9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="852f9-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="852f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="852f9-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="852f9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="852f9-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing ThousandEyes configureren.</span><span class="sxs-lookup"><span data-stu-id="852f9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThousandEyes application.</span></span>

<span data-ttu-id="852f9-150">**Azure AD tooconfigure eenmalige aanmelding met ThousandEyes, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="852f9-150">**tooconfigure Azure AD single sign-on with ThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="852f9-151">In de Azure-portal op Hallo Hallo **ThousandEyes** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="852f9-151">In hello Azure portal, on hello **ThousandEyes** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="852f9-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="852f9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. <span data-ttu-id="852f9-155">Op Hallo **ThousandEyes domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="852f9-155">On hello **ThousandEyes Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    <span data-ttu-id="852f9-157">In Hallo **aanmeldings-URL** textbox, typ een URL als:`https://app.thousandeyes.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="852f9-157">In hello **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span></span>

4. <span data-ttu-id="852f9-158">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="852f9-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. <span data-ttu-id="852f9-160">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="852f9-160">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="852f9-162">Op Hallo **ThousandEyes configuratie** sectie, klikt u op **configureren ThousandEyes** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="852f9-162">On hello **ThousandEyes Configuration** section, click **Configure ThousandEyes** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="852f9-163">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="852f9-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. <span data-ttu-id="852f9-165">Een ander browservenster, meld u aan bij tooyour **ThousandEyes** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="852f9-165">In a different web browser window, sign on tooyour **ThousandEyes** company site as an administrator.</span></span>

8. <span data-ttu-id="852f9-166">Klik in het menu bovenaan Hallo Hallo **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="852f9-166">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="852f9-167">![Instellingen](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="852f9-167">![Settings](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Settings")</span></span>

9. <span data-ttu-id="852f9-168">Klik op **Account**</span><span class="sxs-lookup"><span data-stu-id="852f9-168">Click **Account**</span></span>
   
    <span data-ttu-id="852f9-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span><span class="sxs-lookup"><span data-stu-id="852f9-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span></span>

10. <span data-ttu-id="852f9-170">Klik op Hallo **beveiliging & verificatie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="852f9-170">Click hello **Security & Authentication** tab.</span></span>
   
    <span data-ttu-id="852f9-171">![Beveiliging en verificatie](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "beveiliging en verificatie")</span><span class="sxs-lookup"><span data-stu-id="852f9-171">![Security & Authentication](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security & Authentication")</span></span>

11. <span data-ttu-id="852f9-172">In Hallo **Setup Single Sign-On** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="852f9-172">In hello **Setup Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="852f9-173">![Instellen van eenmalige aanmelding](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "eenmalige aanmelding instellen")</span><span class="sxs-lookup"><span data-stu-id="852f9-173">![Setup Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span></span>
  
    <span data-ttu-id="852f9-174">a.</span><span class="sxs-lookup"><span data-stu-id="852f9-174">a.</span></span> <span data-ttu-id="852f9-175">Selecteer **eenmalige aanmelding inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="852f9-175">Select **Enable Single Sign-On**.</span></span>
  
    <span data-ttu-id="852f9-176">b.</span><span class="sxs-lookup"><span data-stu-id="852f9-176">b.</span></span> <span data-ttu-id="852f9-177">In **URL aanmeldingspagina** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="852f9-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="852f9-178">c.</span><span class="sxs-lookup"><span data-stu-id="852f9-178">c.</span></span> <span data-ttu-id="852f9-179">In **pagina-URL voor afmelden** textbox plakken **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="852f9-179">In **Logout Page URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="852f9-180">d.</span><span class="sxs-lookup"><span data-stu-id="852f9-180">d.</span></span> <span data-ttu-id="852f9-181">**ID-Provider verlener** textbox plakken **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="852f9-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="852f9-182">e.</span><span class="sxs-lookup"><span data-stu-id="852f9-182">e.</span></span> <span data-ttu-id="852f9-183">In **verificatiecertificaat**, klikt u op **bestand kiezen**, en u hebt gedownload vanuit Azure-portal Hallo-certificaat uploaden.</span><span class="sxs-lookup"><span data-stu-id="852f9-183">In **Verification Certificate**, click **Choose file**, and then upload hello certificate you have downloaded from Azure portal.</span></span>
  
    <span data-ttu-id="852f9-184">f.</span><span class="sxs-lookup"><span data-stu-id="852f9-184">f.</span></span> <span data-ttu-id="852f9-185">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="852f9-185">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="852f9-186">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="852f9-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="852f9-187">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="852f9-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="852f9-188">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="852f9-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="852f9-189">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="852f9-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="852f9-190">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="852f9-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="852f9-192">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="852f9-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="852f9-193">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="852f9-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="852f9-195">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="852f9-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="852f9-197">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="852f9-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="852f9-199">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="852f9-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="852f9-201">a.</span><span class="sxs-lookup"><span data-stu-id="852f9-201">a.</span></span> <span data-ttu-id="852f9-202">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="852f9-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="852f9-203">b.</span><span class="sxs-lookup"><span data-stu-id="852f9-203">b.</span></span> <span data-ttu-id="852f9-204">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="852f9-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="852f9-205">c.</span><span class="sxs-lookup"><span data-stu-id="852f9-205">c.</span></span> <span data-ttu-id="852f9-206">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="852f9-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="852f9-207">d.</span><span class="sxs-lookup"><span data-stu-id="852f9-207">d.</span></span> <span data-ttu-id="852f9-208">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="852f9-208">Click **Create**.</span></span>
 
### <a name="creating-a-thousandeyes-test-user"></a><span data-ttu-id="852f9-209">Een testgebruiker ThousandEyes maken</span><span class="sxs-lookup"><span data-stu-id="852f9-209">Creating a ThousandEyes test user</span></span>

<span data-ttu-id="852f9-210">In de volgorde tooenable Azure AD gebruikers toolog in ThousandEyes, moeten ze worden ingericht in ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="852f9-210">In order tooenable Azure AD users toolog into ThousandEyes, they must be provisioned into ThousandEyes.</span></span>  
<span data-ttu-id="852f9-211">In geval van ThousandEyes Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="852f9-211">In hello case of ThousandEyes, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="852f9-212">U kunt andere ThousandEyes gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door ThousandEyes tooprovision Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="852f9-212">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="852f9-213">**een gebruiker account-tooThousandEyes tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="852f9-213">**tooprovision a user account tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="852f9-214">Meld u aan bij uw bedrijf ThousandEyes site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="852f9-214">Log into your ThousandEyes company site as an administrator.</span></span>

2. <span data-ttu-id="852f9-215">Klik op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="852f9-215">Click **Settings**.</span></span>
   
    <span data-ttu-id="852f9-216">![Instellingen](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="852f9-216">![Settings](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

3. <span data-ttu-id="852f9-217">Klik op **Account**.</span><span class="sxs-lookup"><span data-stu-id="852f9-217">Click **Account**.</span></span>
   
    <span data-ttu-id="852f9-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span><span class="sxs-lookup"><span data-stu-id="852f9-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

4. <span data-ttu-id="852f9-219">Klik op Hallo **Accounts gebr & uikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="852f9-219">Click hello **Accounts & Users** tab.</span></span>
   
    <span data-ttu-id="852f9-220">![Accounts gebr & uikers](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts gebr & uikers")</span><span class="sxs-lookup"><span data-stu-id="852f9-220">![Accounts & Users](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

5. <span data-ttu-id="852f9-221">In Hallo **gebruikers toevoegen & Accounts** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="852f9-221">In hello **Add Users & Accounts** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="852f9-222">![Gebruikersaccounts toevoegen](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "gebruikersaccounts toevoegen")</span><span class="sxs-lookup"><span data-stu-id="852f9-222">![Add User Accounts](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>   
  
    <span data-ttu-id="852f9-223">a.</span><span class="sxs-lookup"><span data-stu-id="852f9-223">a.</span></span> <span data-ttu-id="852f9-224">In **naam** textbox Hallo-typenaam van de gebruiker zoals **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="852f9-224">In **Name** textbox, type hello name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="852f9-225">b.</span><span class="sxs-lookup"><span data-stu-id="852f9-225">b.</span></span> <span data-ttu-id="852f9-226">In **e** textbox type Hallo e-mailadres van de gebruiker, zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="852f9-226">In **Email** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="852f9-227">b.</span><span class="sxs-lookup"><span data-stu-id="852f9-227">b.</span></span> <span data-ttu-id="852f9-228">Klik op **nieuwe gebruiker toevoegen tooAccount**.</span><span class="sxs-lookup"><span data-stu-id="852f9-228">Click **Add New User tooAccount**.</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="852f9-229">Hello Azure Active Directory-accounthouder wordt een e-mailbericht een koppeling tooconfirm inclusief ophalen en activeer Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="852f9-229">hello Azure Active Directory account holder will get an email including a link tooconfirm and activate hello account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="852f9-230">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="852f9-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="852f9-231">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooThousandEyes toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="852f9-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThousandEyes.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="852f9-233">**tooassign Britta Simon tooThousandEyes, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="852f9-233">**tooassign Britta Simon tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="852f9-234">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="852f9-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="852f9-236">Selecteer in de lijst met de toepassingen van Hallo **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="852f9-236">In hello applications list, select **ThousandEyes**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. <span data-ttu-id="852f9-238">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="852f9-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="852f9-240">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="852f9-240">Click **Add** button.</span></span> <span data-ttu-id="852f9-241">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="852f9-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="852f9-243">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="852f9-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="852f9-244">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="852f9-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="852f9-245">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="852f9-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="852f9-246">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="852f9-246">Testing single sign-on</span></span>

<span data-ttu-id="852f9-247">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="852f9-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="852f9-248">Als u op Hallo ThousandEyes-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ThousandEyes toepassing.</span><span class="sxs-lookup"><span data-stu-id="852f9-248">When you click hello ThousandEyes tile in hello Access Panel, you should get automatically signed-on tooyour ThousandEyes application.</span></span>

<span data-ttu-id="852f9-249">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="852f9-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="852f9-250">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="852f9-250">Additional resources</span></span>

* [<span data-ttu-id="852f9-251">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="852f9-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="852f9-252">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="852f9-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

