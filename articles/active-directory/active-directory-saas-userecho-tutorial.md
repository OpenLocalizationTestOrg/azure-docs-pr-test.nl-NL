---
title: 'Zelfstudie: Azure Active Directory-integratie met UserEcho | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en UserEcho.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: efe4a94ed6e5d22d153565d4782850eac4dff37b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="31ab6-103">Zelfstudie: Azure Active Directory-integratie met UserEcho</span><span class="sxs-lookup"><span data-stu-id="31ab6-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>

<span data-ttu-id="31ab6-104">In deze zelfstudie leert u hoe toointegrate UserEcho met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="31ab6-104">In this tutorial, you learn how toointegrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31ab6-105">UserEcho integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="31ab6-105">Integrating UserEcho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="31ab6-106">U kunt beheren in Azure AD die tooUserEcho toegang heeft</span><span class="sxs-lookup"><span data-stu-id="31ab6-106">You can control in Azure AD who has access tooUserEcho</span></span>
- <span data-ttu-id="31ab6-107">U kunt uw gebruikers tooautomatically get aangemelde tooUserEcho (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="31ab6-107">You can enable your users tooautomatically get signed-on tooUserEcho (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31ab6-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="31ab6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="31ab6-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="31ab6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31ab6-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="31ab6-110">Prerequisites</span></span>

<span data-ttu-id="31ab6-111">Azure AD-integratie met UserEcho tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="31ab6-111">tooconfigure Azure AD integration with UserEcho, you need hello following items:</span></span>

- <span data-ttu-id="31ab6-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="31ab6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="31ab6-113">Een UserEcho eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="31ab6-113">A UserEcho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31ab6-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="31ab6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31ab6-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="31ab6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31ab6-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="31ab6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="31ab6-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="31ab6-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31ab6-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="31ab6-118">Scenario description</span></span>
<span data-ttu-id="31ab6-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="31ab6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31ab6-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="31ab6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31ab6-121">Het toevoegen van UserEcho van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="31ab6-121">Adding UserEcho from hello gallery</span></span>
2. <span data-ttu-id="31ab6-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="31ab6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-userecho-from-hello-gallery"></a><span data-ttu-id="31ab6-123">Het toevoegen van UserEcho van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="31ab6-123">Adding UserEcho from hello gallery</span></span>
<span data-ttu-id="31ab6-124">tooconfigure hello integratie van UserEcho in Azure AD, moet u tooadd UserEcho uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="31ab6-124">tooconfigure hello integration of UserEcho into Azure AD, you need tooadd UserEcho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="31ab6-125">**tooadd UserEcho via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="31ab6-125">**tooadd UserEcho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="31ab6-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="31ab6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="31ab6-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="31ab6-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="31ab6-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="31ab6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="31ab6-133">Typ in het zoekvak Hallo **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-133">In hello search box, type **UserEcho**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. <span data-ttu-id="31ab6-135">Selecteer in het deelvenster resultaten hello, **UserEcho**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="31ab6-135">In hello results panel, select **UserEcho**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31ab6-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="31ab6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31ab6-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met UserEcho op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="31ab6-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="31ab6-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in UserEcho is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31ab6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserEcho is tooa user in Azure AD.</span></span> <span data-ttu-id="31ab6-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in UserEcho toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="31ab6-140">In other words, a link relationship between an Azure AD user and hello related user in UserEcho needs toobe established.</span></span>

<span data-ttu-id="31ab6-141">Wijs in UserEcho, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="31ab6-141">In UserEcho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="31ab6-142">tooconfigure en eenmalige aanmelding Azure AD-test met UserEcho, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="31ab6-142">tooconfigure and test Azure AD single sign-on with UserEcho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="31ab6-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="31ab6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="31ab6-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31ab6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31ab6-145">**[Maken van een testgebruiker UserEcho](#creating-a-userecho-test-user)**  -toohave een equivalent van Britta Simon in UserEcho die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="31ab6-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - toohave a counterpart of Britta Simon in UserEcho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="31ab6-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="31ab6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31ab6-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="31ab6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31ab6-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="31ab6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31ab6-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing UserEcho configureren.</span><span class="sxs-lookup"><span data-stu-id="31ab6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserEcho application.</span></span>

<span data-ttu-id="31ab6-150">**Azure AD tooconfigure eenmalige aanmelding met UserEcho, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="31ab6-150">**tooconfigure Azure AD single sign-on with UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="31ab6-151">In de Azure-portal op Hallo Hallo **UserEcho** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-151">In hello Azure portal, on hello **UserEcho** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="31ab6-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="31ab6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. <span data-ttu-id="31ab6-155">Op Hallo **UserEcho domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="31ab6-155">On hello **UserEcho Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    <span data-ttu-id="31ab6-157">a.</span><span class="sxs-lookup"><span data-stu-id="31ab6-157">a.</span></span> <span data-ttu-id="31ab6-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.userecho.com/`</span><span class="sxs-lookup"><span data-stu-id="31ab6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/`</span></span>

    <span data-ttu-id="31ab6-159">b.</span><span class="sxs-lookup"><span data-stu-id="31ab6-159">b.</span></span> <span data-ttu-id="31ab6-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.userecho.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="31ab6-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="31ab6-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="31ab6-161">These values are not real.</span></span> <span data-ttu-id="31ab6-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="31ab6-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="31ab6-163">Neem contact op met [UserEcho Client ondersteuningsteam](https://feedback.userecho.com/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="31ab6-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) tooget these values.</span></span> 

4. <span data-ttu-id="31ab6-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="31ab6-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. <span data-ttu-id="31ab6-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="31ab6-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="31ab6-168">Op Hallo **UserEcho configuratie** sectie, klikt u op **configureren UserEcho** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="31ab6-168">On hello **UserEcho Configuration** section, click **Configure UserEcho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="31ab6-169">Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="31ab6-169">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. <span data-ttu-id="31ab6-171">Een ander browservenster geopend Meld u aan bij tooyour UserEcho bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="31ab6-171">In another browser window, sign on tooyour UserEcho company site as an administrator.</span></span>

8. <span data-ttu-id="31ab6-172">Klik op het menu voor uw gebruiker naam tooexpand Hallo Hallo werkbalk bovenaan Hallo en klik vervolgens op **Setup**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-172">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. <span data-ttu-id="31ab6-174">Klik op **integraties**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-174">Click **Integrations**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. <span data-ttu-id="31ab6-176">Klik op **Website**, en klik vervolgens op **eenmalige aanmelding (SAML2)**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. <span data-ttu-id="31ab6-178">Op Hallo **eenmalige aanmelding (SAML)** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="31ab6-178">On hello **Single sign-on (SAML)** page, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    <span data-ttu-id="31ab6-180">a.</span><span class="sxs-lookup"><span data-stu-id="31ab6-180">a.</span></span> <span data-ttu-id="31ab6-181">Als **SAML ingeschakeld**, selecteer **Ja**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-181">As **SAML-enabled**, select **Yes**.</span></span>
    
    <span data-ttu-id="31ab6-182">b.</span><span class="sxs-lookup"><span data-stu-id="31ab6-182">b.</span></span> <span data-ttu-id="31ab6-183">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd uit hello Azure-portal in Hallo **SAML SSO URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="31ab6-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SAML SSO URL** textbox.</span></span>
    
    <span data-ttu-id="31ab6-184">c.</span><span class="sxs-lookup"><span data-stu-id="31ab6-184">c.</span></span> <span data-ttu-id="31ab6-185">Plakken **Sign-Out URL**, die u hebt gekopieerd uit hello Azure-portal in Hallo **externe logoout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="31ab6-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Remote logoout URL** textbox.</span></span>
    
    <span data-ttu-id="31ab6-186">d.</span><span class="sxs-lookup"><span data-stu-id="31ab6-186">d.</span></span> <span data-ttu-id="31ab6-187">Open uw gedownloade certificaat in Kladblok, kopieer Hallo inhoud, en plak deze in Hallo **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="31ab6-187">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="31ab6-188">e.</span><span class="sxs-lookup"><span data-stu-id="31ab6-188">e.</span></span> <span data-ttu-id="31ab6-189">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="31ab6-190">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="31ab6-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="31ab6-191">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="31ab6-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="31ab6-192">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="31ab6-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31ab6-193">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="31ab6-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="31ab6-194">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="31ab6-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="31ab6-196">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="31ab6-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="31ab6-197">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="31ab6-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="31ab6-199">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="31ab6-201">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="31ab6-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="31ab6-203">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="31ab6-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31ab6-205">a.</span><span class="sxs-lookup"><span data-stu-id="31ab6-205">a.</span></span> <span data-ttu-id="31ab6-206">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31ab6-207">b.</span><span class="sxs-lookup"><span data-stu-id="31ab6-207">b.</span></span> <span data-ttu-id="31ab6-208">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="31ab6-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31ab6-209">c.</span><span class="sxs-lookup"><span data-stu-id="31ab6-209">c.</span></span> <span data-ttu-id="31ab6-210">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="31ab6-211">d.</span><span class="sxs-lookup"><span data-stu-id="31ab6-211">d.</span></span> <span data-ttu-id="31ab6-212">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-212">Click **Create**.</span></span>
 
### <a name="creating-a-userecho-test-user"></a><span data-ttu-id="31ab6-213">Een testgebruiker UserEcho maken</span><span class="sxs-lookup"><span data-stu-id="31ab6-213">Creating a UserEcho test user</span></span>

<span data-ttu-id="31ab6-214">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in UserEcho van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="31ab6-214">hello objective of this section is toocreate a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="31ab6-215">**een gebruiker Britta Simon aangeroepen in UserEcho, toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="31ab6-215">**toocreate a user called Britta Simon in UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="31ab6-216">Eenmalige aanmelding tooyour UserEcho bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="31ab6-216">Sign-on tooyour UserEcho company site as an administrator.</span></span>

2. <span data-ttu-id="31ab6-217">Klik op het menu voor uw gebruiker naam tooexpand Hallo Hallo werkbalk bovenaan Hallo en klik vervolgens op **Setup**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-217">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. <span data-ttu-id="31ab6-219">Klik op **gebruikers**, tooexpand hello **gebruikers** sectie.</span><span class="sxs-lookup"><span data-stu-id="31ab6-219">Click **Users**, tooexpand hello **Users** section.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. <span data-ttu-id="31ab6-221">Klik op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-221">Click **Users**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. <span data-ttu-id="31ab6-223">Klik op **een nieuwe gebruiker uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-223">Click **Invite a new user**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. <span data-ttu-id="31ab6-225">Op Hallo **een nieuwe gebruiker uitnodigen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="31ab6-225">On hello **Invite a new user** dialog, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    <span data-ttu-id="31ab6-227">a.</span><span class="sxs-lookup"><span data-stu-id="31ab6-227">a.</span></span> <span data-ttu-id="31ab6-228">In Hallo **naam** textbox typenaam van de gebruiker Hallo zoals Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31ab6-228">In hello **Name** textbox, type name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="31ab6-229">b.</span><span class="sxs-lookup"><span data-stu-id="31ab6-229">b.</span></span>  <span data-ttu-id="31ab6-230">In Hallo **e** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="31ab6-230">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="31ab6-231">c.</span><span class="sxs-lookup"><span data-stu-id="31ab6-231">c.</span></span> <span data-ttu-id="31ab6-232">Klik op **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-232">Click **Invite**.</span></span>

<span data-ttu-id="31ab6-233">Een uitnodiging verzonden tooBritta waarmee haar toostart UserEcho gebruiken.</span><span class="sxs-lookup"><span data-stu-id="31ab6-233">An invitation is sent tooBritta, which enables her toostart using UserEcho.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="31ab6-234">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="31ab6-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="31ab6-235">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooUserEcho toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="31ab6-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserEcho.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="31ab6-237">**tooassign Britta Simon tooUserEcho, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="31ab6-237">**tooassign Britta Simon tooUserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="31ab6-238">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="31ab6-240">Selecteer in de lijst met de toepassingen van Hallo **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-240">In hello applications list, select **UserEcho**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. <span data-ttu-id="31ab6-242">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="31ab6-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="31ab6-244">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="31ab6-244">Click **Add** button.</span></span> <span data-ttu-id="31ab6-245">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="31ab6-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="31ab6-247">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="31ab6-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="31ab6-248">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="31ab6-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31ab6-249">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="31ab6-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31ab6-250">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="31ab6-250">Testing single sign-on</span></span>

<span data-ttu-id="31ab6-251">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="31ab6-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="31ab6-252">Als u op Hallo UserEcho tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour UserEcho toepassing.</span><span class="sxs-lookup"><span data-stu-id="31ab6-252">When you click hello UserEcho tile in hello Access Panel, you should get automatically signed-on tooyour UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="31ab6-253">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="31ab6-253">Additional resources</span></span>

* [<span data-ttu-id="31ab6-254">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31ab6-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31ab6-255">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="31ab6-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

