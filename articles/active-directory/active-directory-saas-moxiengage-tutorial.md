---
title: 'Zelfstudie: Azure Active Directory-integratie met Moxi benaderen | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Moxi benaderen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1135a879-8f00-43b0-ac8a-831593d9586d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: ff3242a0981aff6dff9ec6e3f66f0e7c4a9b5b20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxi-engage"></a><span data-ttu-id="bd53c-103">Zelfstudie: Azure Active Directory-integratie met Moxi benaderen</span><span class="sxs-lookup"><span data-stu-id="bd53c-103">Tutorial: Azure Active Directory integration with Moxi Engage</span></span>

<span data-ttu-id="bd53c-104">In deze zelfstudie leert u hoe toointegrate Moxi benaderen met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd53c-104">In this tutorial, you learn how toointegrate Moxi Engage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd53c-105">Moxi benaderen integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="bd53c-105">Integrating Moxi Engage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bd53c-106">U kunt beheren in Azure AD wie toegang tot tooMoxi Engage heeft</span><span class="sxs-lookup"><span data-stu-id="bd53c-106">You can control in Azure AD who has access tooMoxi Engage</span></span>
- <span data-ttu-id="bd53c-107">U kunt uw gebruikers tooautomatically get aangemelde tooMoxi Engage (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="bd53c-107">You can enable your users tooautomatically get signed-on tooMoxi Engage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bd53c-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="bd53c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bd53c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bd53c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd53c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bd53c-110">Prerequisites</span></span>

<span data-ttu-id="bd53c-111">Azure AD-integratie met Moxi benaderen tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="bd53c-111">tooconfigure Azure AD integration with Moxi Engage, you need hello following items:</span></span>

- <span data-ttu-id="bd53c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="bd53c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bd53c-113">Een Moxi benaderen eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="bd53c-113">A Moxi Engage single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bd53c-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="bd53c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bd53c-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="bd53c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd53c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="bd53c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bd53c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd53c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bd53c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="bd53c-118">Scenario description</span></span>
<span data-ttu-id="bd53c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="bd53c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd53c-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="bd53c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd53c-121">Het toevoegen van Moxi benaderen van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="bd53c-121">Adding Moxi Engage from hello gallery</span></span>
2. <span data-ttu-id="bd53c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bd53c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxi-engage-from-hello-gallery"></a><span data-ttu-id="bd53c-123">Het toevoegen van Moxi benaderen van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="bd53c-123">Adding Moxi Engage from hello gallery</span></span>
<span data-ttu-id="bd53c-124">tooconfigure hello integratie van Moxi benaderen in Azure AD, moet u tooadd Moxi benaderen uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="bd53c-124">tooconfigure hello integration of Moxi Engage into Azure AD, you need tooadd Moxi Engage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bd53c-125">**tooadd Moxi benaderen via Hallo gallery Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bd53c-125">**tooadd Moxi Engage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd53c-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bd53c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bd53c-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bd53c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bd53c-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bd53c-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="bd53c-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bd53c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="bd53c-133">Typ in het zoekvak Hallo **Moxi benaderen**.</span><span class="sxs-lookup"><span data-stu-id="bd53c-133">In hello search box, type **Moxi Engage**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_search.png)

5. <span data-ttu-id="bd53c-135">Selecteer in het deelvenster resultaten hello, **Moxi benaderen**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="bd53c-135">In hello results panel, select **Moxi Engage**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bd53c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bd53c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bd53c-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Moxi benaderen op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="bd53c-138">In this section, you configure and test Azure AD single sign-on with Moxi Engage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bd53c-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Moxi benaderen is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd53c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Moxi Engage is tooa user in Azure AD.</span></span> <span data-ttu-id="bd53c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Moxi benaderen toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="bd53c-140">In other words, a link relationship between an Azure AD user and hello related user in Moxi Engage needs toobe established.</span></span>

<span data-ttu-id="bd53c-141">Wijs in het Moxi benaderen, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="bd53c-141">In Moxi Engage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bd53c-142">tooconfigure en eenmalige aanmelding Azure AD-test met Moxi benaderen, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bd53c-142">tooconfigure and test Azure AD single sign-on with Moxi Engage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bd53c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="bd53c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bd53c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bd53c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd53c-145">**[Maken van een testgebruiker Moxi benaderen](#creating-a-moxi-engage-test-user)**  -toohave een equivalent van Britta Simon in Moxi benaderen die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="bd53c-145">**[Creating a Moxi Engage test user](#creating-a-moxi-engage-test-user)** - toohave a counterpart of Britta Simon in Moxi Engage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bd53c-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="bd53c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd53c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="bd53c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bd53c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="bd53c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bd53c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Moxi benaderen.</span><span class="sxs-lookup"><span data-stu-id="bd53c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Moxi Engage application.</span></span>

<span data-ttu-id="bd53c-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Moxi benaderen, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bd53c-150">**tooconfigure Azure AD single sign-on with Moxi Engage, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd53c-151">In de Azure-portal op Hallo Hallo **Moxi benaderen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="bd53c-151">In hello Azure portal, on hello **Moxi Engage** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="bd53c-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="bd53c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_samlbase.png)

3. <span data-ttu-id="bd53c-155">Op Hallo **Moxi benaderen domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bd53c-155">On hello **Moxi Engage Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_url.png)

    <span data-ttu-id="bd53c-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://svc.<moxiworks-integration-domain>/service/v1/auth/inbound/saml/aad`</span><span class="sxs-lookup"><span data-stu-id="bd53c-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://svc.<moxiworks-integration-domain>/service/v1/auth/inbound/saml/aad`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bd53c-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="bd53c-158">This value is not real.</span></span> <span data-ttu-id="bd53c-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="bd53c-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="bd53c-160">Neem contact op met [Moxi benaderen Client ondersteuningsteam](mailto:support@moxiworks.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="bd53c-160">Contact [Moxi Engage Client support team](mailto:support@moxiworks.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="bd53c-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bd53c-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_certificate.png) 

5. <span data-ttu-id="bd53c-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="bd53c-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxiengage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bd53c-165">tooconfigure eenmalige aanmelding op **Moxi benaderen** zijde, moet u toosend Hallo gedownload **Metadata XML** te[ondersteuningsteam Moxi benaderen](mailto:support@moxiworks.com).</span><span class="sxs-lookup"><span data-stu-id="bd53c-165">tooconfigure single sign-on on **Moxi Engage** side, you need toosend hello downloaded **Metadata XML** too[Moxi Engage support team](mailto:support@moxiworks.com).</span></span> <span data-ttu-id="bd53c-166">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="bd53c-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="bd53c-167">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="bd53c-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bd53c-168">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="bd53c-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bd53c-169">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bd53c-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bd53c-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="bd53c-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="bd53c-171">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="bd53c-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="bd53c-173">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bd53c-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd53c-174">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bd53c-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bd53c-176">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bd53c-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bd53c-178">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="bd53c-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd53c-180">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bd53c-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bd53c-182">a.</span><span class="sxs-lookup"><span data-stu-id="bd53c-182">a.</span></span> <span data-ttu-id="bd53c-183">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bd53c-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd53c-184">b.</span><span class="sxs-lookup"><span data-stu-id="bd53c-184">b.</span></span> <span data-ttu-id="bd53c-185">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bd53c-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bd53c-186">c.</span><span class="sxs-lookup"><span data-stu-id="bd53c-186">c.</span></span> <span data-ttu-id="bd53c-187">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="bd53c-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bd53c-188">d.</span><span class="sxs-lookup"><span data-stu-id="bd53c-188">d.</span></span> <span data-ttu-id="bd53c-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="bd53c-189">Click **Create**.</span></span>
 
### <a name="creating-a-moxi-engage-test-user"></a><span data-ttu-id="bd53c-190">Maken van een testgebruiker Moxi benaderen</span><span class="sxs-lookup"><span data-stu-id="bd53c-190">Creating a Moxi Engage test user</span></span>

<span data-ttu-id="bd53c-191">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in het benaderen van Moxi maken.</span><span class="sxs-lookup"><span data-stu-id="bd53c-191">In this section, you create a user called Britta Simon in Moxi Engage.</span></span> <span data-ttu-id="bd53c-192">Werken met [ondersteuningsteam Moxi benaderen](mailto:support@moxiworks.com) Hallo gebruikers toevoegen in Hallo Moxi benaderen platform.</span><span class="sxs-lookup"><span data-stu-id="bd53c-192">Work with [Moxi Engage support team](mailto:support@moxiworks.com) to add hello users in hello Moxi Engage platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bd53c-193">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd53c-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bd53c-194">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooMoxi Engage.</span><span class="sxs-lookup"><span data-stu-id="bd53c-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMoxi Engage.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="bd53c-196">**tooassign Britta Simon tooMoxi Engage, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bd53c-196">**tooassign Britta Simon tooMoxi Engage, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd53c-197">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bd53c-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="bd53c-199">Selecteer in de lijst met de toepassingen van Hallo **Moxi benaderen**.</span><span class="sxs-lookup"><span data-stu-id="bd53c-199">In hello applications list, select **Moxi Engage**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_app.png) 

3. <span data-ttu-id="bd53c-201">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="bd53c-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="bd53c-203">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="bd53c-203">Click **Add** button.</span></span> <span data-ttu-id="bd53c-204">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bd53c-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="bd53c-206">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="bd53c-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bd53c-207">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bd53c-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd53c-208">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bd53c-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bd53c-209">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bd53c-209">Testing single sign-on</span></span>

<span data-ttu-id="bd53c-210">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="bd53c-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bd53c-211">Als u op Hallo Moxi benaderen tegel in Hallo Toegangsvenster, krijgt u automatische aanmelding tooMoxi uitoefenen toepassing.</span><span class="sxs-lookup"><span data-stu-id="bd53c-211">When you click hello Moxi Engage tile in hello Access Panel, you should get automatic login tooMoxi Engage application.</span></span>
<span data-ttu-id="bd53c-212">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bd53c-212">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bd53c-213">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="bd53c-213">Additional resources</span></span>

* [<span data-ttu-id="bd53c-214">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd53c-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd53c-215">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bd53c-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_203.png

