---
title: 'Zelfstudie: Azure Active Directory-integratie met ICIMS | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ICIMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3fa970f008e64e84b0a1280f691f0181851b757c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="01b32-103">Zelfstudie: Azure Active Directory-integratie met ICIMS</span><span class="sxs-lookup"><span data-stu-id="01b32-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>

<span data-ttu-id="01b32-104">In deze zelfstudie leert u hoe toointegrate ICIMS met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="01b32-104">In this tutorial, you learn how toointegrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="01b32-105">ICIMS integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="01b32-105">Integrating ICIMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="01b32-106">U kunt beheren in Azure AD die tooICIMS toegang heeft</span><span class="sxs-lookup"><span data-stu-id="01b32-106">You can control in Azure AD who has access tooICIMS</span></span>
- <span data-ttu-id="01b32-107">U kunt uw gebruikers tooautomatically get aangemelde tooICIMS (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="01b32-107">You can enable your users tooautomatically get signed-on tooICIMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="01b32-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="01b32-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="01b32-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="01b32-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01b32-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="01b32-110">Prerequisites</span></span>

<span data-ttu-id="01b32-111">Azure AD-integratie met ICIMS tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="01b32-111">tooconfigure Azure AD integration with ICIMS, you need hello following items:</span></span>

- <span data-ttu-id="01b32-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="01b32-112">An Azure AD subscription</span></span>
- <span data-ttu-id="01b32-113">Een ICIMS eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="01b32-113">An ICIMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="01b32-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="01b32-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="01b32-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="01b32-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="01b32-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="01b32-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="01b32-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="01b32-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="01b32-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="01b32-118">Scenario description</span></span>
<span data-ttu-id="01b32-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="01b32-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="01b32-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="01b32-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="01b32-121">Het toevoegen van ICIMS van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="01b32-121">Adding ICIMS from hello gallery</span></span>
2. <span data-ttu-id="01b32-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="01b32-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icims-from-hello-gallery"></a><span data-ttu-id="01b32-123">Het toevoegen van ICIMS van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="01b32-123">Adding ICIMS from hello gallery</span></span>
<span data-ttu-id="01b32-124">tooconfigure hello integratie van ICIMS in Azure AD, moet u tooadd ICIMS uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="01b32-124">tooconfigure hello integration of ICIMS into Azure AD, you need tooadd ICIMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="01b32-125">**tooadd ICIMS via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="01b32-125">**tooadd ICIMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="01b32-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="01b32-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="01b32-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="01b32-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="01b32-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="01b32-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="01b32-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="01b32-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="01b32-133">Typ in het zoekvak Hallo **ICIMS**, selecteer **ICIMS** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="01b32-133">In hello search box, type **ICIMS**, select **ICIMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ICIMS in de lijst met resultaten Hallo](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="01b32-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="01b32-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="01b32-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met ICIMS op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="01b32-136">In this section, you configure and test Azure AD single sign-on with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="01b32-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ICIMS is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01b32-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ICIMS is tooa user in Azure AD.</span></span> <span data-ttu-id="01b32-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in ICIMS toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="01b32-138">In other words, a link relationship between an Azure AD user and hello related user in ICIMS needs toobe established.</span></span>

<span data-ttu-id="01b32-139">Wijs in ICIMS, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="01b32-139">In ICIMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="01b32-140">tooconfigure en eenmalige aanmelding Azure AD-test met ICIMS, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="01b32-140">tooconfigure and test Azure AD single sign-on with ICIMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="01b32-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="01b32-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="01b32-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="01b32-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="01b32-143">**[Maken van een testgebruiker ICIMS](#create-an-icims-test-user)**  -toohave een equivalent van Britta Simon in ICIMS die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="01b32-143">**[Create an ICIMS test user](#create-an-icims-test-user)** - toohave a counterpart of Britta Simon in ICIMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="01b32-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="01b32-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="01b32-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="01b32-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="01b32-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="01b32-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="01b32-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing ICIMS configureren.</span><span class="sxs-lookup"><span data-stu-id="01b32-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ICIMS application.</span></span>

<span data-ttu-id="01b32-148">**Azure AD tooconfigure eenmalige aanmelding met ICIMS, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="01b32-148">**tooconfigure Azure AD single sign-on with ICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="01b32-149">In de Azure-portal op Hallo Hallo **ICIMS** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="01b32-149">In hello Azure portal, on hello **ICIMS** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="01b32-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="01b32-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. <span data-ttu-id="01b32-153">Op Hallo **ICIMS domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="01b32-153">On hello **ICIMS Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en ICIMS domein eenmalige aanmelding informatie](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    <span data-ttu-id="01b32-155">a.</span><span class="sxs-lookup"><span data-stu-id="01b32-155">a.</span></span> <span data-ttu-id="01b32-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="01b32-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    <span data-ttu-id="01b32-157">b.</span><span class="sxs-lookup"><span data-stu-id="01b32-157">b.</span></span> <span data-ttu-id="01b32-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="01b32-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="01b32-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="01b32-159">These values are not real.</span></span> <span data-ttu-id="01b32-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="01b32-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="01b32-161">Neem contact op met [ICIMS Client ondersteuningsteam](https://www.icims.com/contact-us) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="01b32-161">Contact [ICIMS Client support team](https://www.icims.com/contact-us) tooget these values.</span></span> 
 
4. <span data-ttu-id="01b32-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="01b32-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. <span data-ttu-id="01b32-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="01b32-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="01b32-166">Op Hallo **ICIMS configuratie** sectie, klikt u op **configureren ICIMS** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="01b32-166">On hello **ICIMS Configuration** section, click **Configure ICIMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="01b32-167">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="01b32-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![ICIMS configuratie](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. <span data-ttu-id="01b32-169">tooconfigure eenmalige aanmelding op **ICIMS** zijde, moet u toosend Hallo gedownload **Metadata XML**, **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** te [ICIMS ondersteuningsteam](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="01b32-169">tooconfigure single sign-on on **ICIMS** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ICIMS support team](https://www.icims.com/contact-us).</span></span> <span data-ttu-id="01b32-170">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="01b32-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="01b32-171">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="01b32-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="01b32-172">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="01b32-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="01b32-173">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="01b32-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="01b32-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="01b32-174">Create an Azure AD test user</span></span>
<span data-ttu-id="01b32-175">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="01b32-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="01b32-177">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="01b32-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="01b32-178">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="01b32-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="01b32-180">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="01b32-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="01b32-182">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="01b32-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="01b32-184">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="01b32-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="01b32-186">a.</span><span class="sxs-lookup"><span data-stu-id="01b32-186">a.</span></span> <span data-ttu-id="01b32-187">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="01b32-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="01b32-188">b.</span><span class="sxs-lookup"><span data-stu-id="01b32-188">b.</span></span> <span data-ttu-id="01b32-189">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="01b32-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="01b32-190">c.</span><span class="sxs-lookup"><span data-stu-id="01b32-190">c.</span></span> <span data-ttu-id="01b32-191">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="01b32-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="01b32-192">d.</span><span class="sxs-lookup"><span data-stu-id="01b32-192">d.</span></span> <span data-ttu-id="01b32-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="01b32-193">Click **Create**.</span></span>
 
### <a name="create-an-icims-test-user"></a><span data-ttu-id="01b32-194">Een testgebruiker ICIMS maken</span><span class="sxs-lookup"><span data-stu-id="01b32-194">Create an ICIMS test user</span></span>

<span data-ttu-id="01b32-195">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in ICIMS van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="01b32-195">hello objective of this section is toocreate a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="01b32-196">Werken met [ICIMS ondersteuningsteam](https://www.icims.com/contact-us) tooadd Hallo gebruikers in Hallo ICIMS-account.</span><span class="sxs-lookup"><span data-stu-id="01b32-196">Work with [ICIMS support team](https://www.icims.com/contact-us) tooadd hello users in hello ICIMS account.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="01b32-197">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="01b32-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="01b32-198">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooICIMS toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="01b32-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooICIMS.</span></span>

![Hallo-gebruikersrollen toewijzen][200]

<span data-ttu-id="01b32-200">**tooassign Britta Simon tooICIMS, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="01b32-200">**tooassign Britta Simon tooICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="01b32-201">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="01b32-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="01b32-203">Selecteer in de lijst met de toepassingen van Hallo **ICIMS**.</span><span class="sxs-lookup"><span data-stu-id="01b32-203">In hello applications list, select **ICIMS**.</span></span>

    ![Hallo ICIMS koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. <span data-ttu-id="01b32-205">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="01b32-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. <span data-ttu-id="01b32-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="01b32-207">Click **Add** button.</span></span> <span data-ttu-id="01b32-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="01b32-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="01b32-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="01b32-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="01b32-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="01b32-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="01b32-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="01b32-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="01b32-213">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="01b32-213">Test single sign-on</span></span>

<span data-ttu-id="01b32-214">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="01b32-214">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="01b32-215">Als u op Hallo ICIMS-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ICIMS toepassing.</span><span class="sxs-lookup"><span data-stu-id="01b32-215">When you click hello ICIMS tile in hello Access Panel, you should get automatically signed-on tooyour ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="01b32-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="01b32-216">Additional resources</span></span>

* [<span data-ttu-id="01b32-217">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01b32-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="01b32-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="01b32-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png

