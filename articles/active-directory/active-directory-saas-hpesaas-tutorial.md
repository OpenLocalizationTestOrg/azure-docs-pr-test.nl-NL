---
title: 'Zelfstudie: Azure Active Directory-integratie met HPE SaaS | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en HPE SaaS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 314003d6-ca66-4456-88c3-934254d4a9a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: 7a846fb2298e51d249f4a406527130828bf7bbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hpe-saas"></a><span data-ttu-id="53910-103">Zelfstudie: Azure Active Directory-integratie met HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="53910-103">Tutorial: Azure Active Directory integration with HPE SaaS</span></span>

<span data-ttu-id="53910-104">In deze zelfstudie leert u hoe toointegrate HPE SaaS met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="53910-104">In this tutorial, you learn how toointegrate HPE SaaS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="53910-105">HPE SaaS integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="53910-105">Integrating HPE SaaS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="53910-106">U kunt beheren in Azure AD wie toegang tot tooHPE SaaS heeft</span><span class="sxs-lookup"><span data-stu-id="53910-106">You can control in Azure AD who has access tooHPE SaaS</span></span>
- <span data-ttu-id="53910-107">U kunt uw gebruikers tooautomatically get aangemelde tooHPE SaaS (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="53910-107">You can enable your users tooautomatically get signed-on tooHPE SaaS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="53910-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="53910-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="53910-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="53910-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53910-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="53910-110">Prerequisites</span></span>

<span data-ttu-id="53910-111">Azure AD-integratie met HPE SaaS tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="53910-111">tooconfigure Azure AD integration with HPE SaaS, you need hello following items:</span></span>

- <span data-ttu-id="53910-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="53910-112">An Azure AD subscription</span></span>
- <span data-ttu-id="53910-113">Een HPE SaaS eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="53910-113">An HPE SaaS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="53910-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="53910-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="53910-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="53910-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="53910-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="53910-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="53910-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="53910-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="53910-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="53910-118">Scenario description</span></span>
<span data-ttu-id="53910-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="53910-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="53910-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="53910-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="53910-121">Het toevoegen van HPE SaaS van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="53910-121">Adding HPE SaaS from hello gallery</span></span>
2. <span data-ttu-id="53910-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="53910-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hpe-saas-from-hello-gallery"></a><span data-ttu-id="53910-123">Het toevoegen van HPE SaaS van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="53910-123">Adding HPE SaaS from hello gallery</span></span>
<span data-ttu-id="53910-124">tooconfigure hello integratie van HPE SaaS in Azure AD, moet u tooadd HPE SaaS uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="53910-124">tooconfigure hello integration of HPE SaaS into Azure AD, you need tooadd HPE SaaS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="53910-125">**tooadd HPE SaaS via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="53910-125">**tooadd HPE SaaS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="53910-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="53910-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="53910-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="53910-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="53910-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="53910-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="53910-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="53910-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="53910-133">Typ in het zoekvak Hallo **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="53910-133">In hello search box, type **HPE SaaS**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_search.png)

5. <span data-ttu-id="53910-135">Selecteer in het deelvenster resultaten hello, **HPE SaaS**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="53910-135">In hello results panel, select **HPE SaaS**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="53910-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="53910-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="53910-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met HPE SaaS op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="53910-138">In this section, you configure and test Azure AD single sign-on with HPE SaaS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="53910-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in HPE SaaS is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53910-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HPE SaaS is tooa user in Azure AD.</span></span> <span data-ttu-id="53910-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in HPE SaaS toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="53910-140">In other words, a link relationship between an Azure AD user and hello related user in HPE SaaS needs toobe established.</span></span>

<span data-ttu-id="53910-141">In HPE SaaS, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="53910-141">In HPE SaaS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="53910-142">tooconfigure en eenmalige aanmelding Azure AD-test met HPE SaaS, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="53910-142">tooconfigure and test Azure AD single sign-on with HPE SaaS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="53910-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="53910-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="53910-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="53910-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="53910-145">**[Maken van een testgebruiker HPE SaaS](#creating-an-hpe-saas-test-user)**  -toohave een equivalent van Britta Simon in HPE SaaS die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="53910-145">**[Creating an HPE SaaS test user](#creating-an-hpe-saas-test-user)** - toohave a counterpart of Britta Simon in HPE SaaS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="53910-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="53910-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="53910-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="53910-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="53910-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="53910-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="53910-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw HPE SaaS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="53910-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HPE SaaS application.</span></span>

<span data-ttu-id="53910-150">**Azure AD tooconfigure eenmalige aanmelding met HPE SaaS moet uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="53910-150">**tooconfigure Azure AD single sign-on with HPE SaaS, perform hello following steps:**</span></span>

1. <span data-ttu-id="53910-151">In de Azure-portal op Hallo Hallo **HPE SaaS** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="53910-151">In hello Azure portal, on hello **HPE SaaS** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="53910-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="53910-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_samlbase.png)

3. <span data-ttu-id="53910-155">Op Hallo **HPE SaaS-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="53910-155">On hello **HPE SaaS Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_url.png)

    <span data-ttu-id="53910-157">a.</span><span class="sxs-lookup"><span data-stu-id="53910-157">a.</span></span> <span data-ttu-id="53910-158">In Hallo **aanmeldings-URL** textbox, typ een URL als:`https://login.saas.hpe.com/msg`</span><span class="sxs-lookup"><span data-stu-id="53910-158">In hello **Sign-on URL** textbox, type a URL as: `https://login.saas.hpe.com/msg`</span></span>

    <span data-ttu-id="53910-159">b.</span><span class="sxs-lookup"><span data-stu-id="53910-159">b.</span></span> <span data-ttu-id="53910-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.saas.hpe.com`</span><span class="sxs-lookup"><span data-stu-id="53910-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.saas.hpe.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="53910-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="53910-161">These values are not real.</span></span> <span data-ttu-id="53910-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="53910-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="53910-163">Neem contact op met [HPE SaaS Client ondersteuningsteam](https://saas.hpe.com/en-us/contact) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="53910-163">Contact [HPE SaaS Client support team](https://saas.hpe.com/en-us/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="53910-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="53910-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_certificate.png) 

5. <span data-ttu-id="53910-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="53910-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hpesaas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="53910-168">tooconfigure eenmalige aanmelding op **HPE SaaS** zijde, moet u toosend Hallo gedownload **Metadata XML** te[HPE SaaS ondersteuningsteam](https://saas.hpe.com/en-us/contact).</span><span class="sxs-lookup"><span data-stu-id="53910-168">tooconfigure single sign-on on **HPE SaaS** side, you need toosend hello downloaded **Metadata XML** too[HPE SaaS support team](https://saas.hpe.com/en-us/contact).</span></span> <span data-ttu-id="53910-169">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="53910-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="53910-170">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="53910-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="53910-171">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="53910-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="53910-172">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="53910-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="53910-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="53910-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="53910-174">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="53910-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="53910-176">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="53910-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="53910-177">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="53910-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="53910-179">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="53910-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="53910-181">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="53910-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="53910-183">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="53910-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="53910-185">a.</span><span class="sxs-lookup"><span data-stu-id="53910-185">a.</span></span> <span data-ttu-id="53910-186">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="53910-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="53910-187">b.</span><span class="sxs-lookup"><span data-stu-id="53910-187">b.</span></span> <span data-ttu-id="53910-188">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="53910-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="53910-189">c.</span><span class="sxs-lookup"><span data-stu-id="53910-189">c.</span></span> <span data-ttu-id="53910-190">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="53910-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="53910-191">d.</span><span class="sxs-lookup"><span data-stu-id="53910-191">d.</span></span> <span data-ttu-id="53910-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="53910-192">Click **Create**.</span></span>
 
### <a name="creating-an-hpe-saas-test-user"></a><span data-ttu-id="53910-193">De gebruiker van een HPE SaaS-test maken</span><span class="sxs-lookup"><span data-stu-id="53910-193">Creating an HPE SaaS test user</span></span>

<span data-ttu-id="53910-194">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in HPE SaaS van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="53910-194">hello objective of this section is toocreate a user called Britta Simon in HPE SaaS.</span></span> <span data-ttu-id="53910-195">Neem contact op met [HPE SaaS ondersteuningsteam](https://saas.hpe.com/en-us/contact) tooadd Hallo gebruikers in Hallo HPE SaaS-account.</span><span class="sxs-lookup"><span data-stu-id="53910-195">Please work with [HPE SaaS support team](https://saas.hpe.com/en-us/contact) tooadd hello users in hello HPE SaaS account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="53910-196">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="53910-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="53910-197">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooHPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="53910-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHPE SaaS.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="53910-199">**tooassign Britta Simon tooHPE SaaS, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="53910-199">**tooassign Britta Simon tooHPE SaaS, perform hello following steps:**</span></span>

1. <span data-ttu-id="53910-200">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="53910-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="53910-202">Selecteer in de lijst met de toepassingen van Hallo **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="53910-202">In hello applications list, select **HPE SaaS**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_app.png) 

3. <span data-ttu-id="53910-204">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="53910-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="53910-206">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="53910-206">Click **Add** button.</span></span> <span data-ttu-id="53910-207">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="53910-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="53910-209">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="53910-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="53910-210">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="53910-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="53910-211">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="53910-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="53910-212">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="53910-212">Testing single sign-on</span></span>

<span data-ttu-id="53910-213">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="53910-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="53910-214">Als u op Hallo HPE SaaS-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour HPE SaaS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="53910-214">When you click hello HPE SaaS tile in hello Access Panel, you should get automatically signed-on tooyour HPE SaaS application.</span></span>
<span data-ttu-id="53910-215">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="53910-215">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="53910-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="53910-216">Additional resources</span></span>

* [<span data-ttu-id="53910-217">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53910-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="53910-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="53910-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_203.png

