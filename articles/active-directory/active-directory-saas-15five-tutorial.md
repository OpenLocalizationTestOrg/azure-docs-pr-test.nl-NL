---
title: 'Zelfstudie: Azure Active Directory-integratie met 15Five | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en 15Five.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 9e531615c16331ce000e285d13d9adce13735a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="6e8bc-103">Zelfstudie: Azure Active Directory-integratie met 15Five</span><span class="sxs-lookup"><span data-stu-id="6e8bc-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="6e8bc-104">In deze zelfstudie leert u hoe toointegrate 15Five met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6e8bc-104">In this tutorial, you learn how toointegrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e8bc-105">15Five integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6e8bc-105">Integrating 15Five with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6e8bc-106">U kunt beheren in Azure AD die too15Five toegang heeft</span><span class="sxs-lookup"><span data-stu-id="6e8bc-106">You can control in Azure AD who has access too15Five</span></span>
- <span data-ttu-id="6e8bc-107">U kunt uw gebruikers tooautomatically get aangemelde too15Five inschakelen (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="6e8bc-107">You can enable your users tooautomatically get signed-on too15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6e8bc-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6e8bc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6e8bc-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6e8bc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e8bc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6e8bc-110">Prerequisites</span></span>

<span data-ttu-id="6e8bc-111">Azure AD-integratie met 15Five tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="6e8bc-111">tooconfigure Azure AD integration with 15Five, you need hello following items:</span></span>

- <span data-ttu-id="6e8bc-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6e8bc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e8bc-113">Een 15Five eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6e8bc-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e8bc-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e8bc-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6e8bc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e8bc-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e8bc-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e8bc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e8bc-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6e8bc-118">Scenario description</span></span>
<span data-ttu-id="6e8bc-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e8bc-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6e8bc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e8bc-121">Het toevoegen van 15Five van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="6e8bc-121">Adding 15Five from hello gallery</span></span>
2. <span data-ttu-id="6e8bc-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6e8bc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-hello-gallery"></a><span data-ttu-id="6e8bc-123">Het toevoegen van 15Five van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="6e8bc-123">Adding 15Five from hello gallery</span></span>
<span data-ttu-id="6e8bc-124">tooconfigure hello integratie van 15Five in Azure AD, moet u tooadd 15Five uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-124">tooconfigure hello integration of 15Five into Azure AD, you need tooadd 15Five from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6e8bc-125">**tooadd 15Five via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6e8bc-125">**tooadd 15Five from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e8bc-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6e8bc-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6e8bc-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6e8bc-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6e8bc-133">Typ in het zoekvak Hallo **15Five**.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-133">In hello search box, type **15Five**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="6e8bc-135">Selecteer in het deelvenster resultaten hello, **15Five**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-135">In hello results panel, select **15Five**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6e8bc-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6e8bc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6e8bc-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met 15Five op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6e8bc-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6e8bc-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in 15Five is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 15Five is tooa user in Azure AD.</span></span> <span data-ttu-id="6e8bc-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in 15Five toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-140">In other words, a link relationship between an Azure AD user and hello related user in 15Five needs toobe established.</span></span>

<span data-ttu-id="6e8bc-141">Wijs in 15Five, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-141">In 15Five, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6e8bc-142">tooconfigure en eenmalige aanmelding Azure AD-test met 15Five, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e8bc-142">tooconfigure and test Azure AD single sign-on with 15Five, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6e8bc-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6e8bc-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6e8bc-145">**[Maken van een testgebruiker 15Five](#creating-a-15five-test-user)**  -toohave een equivalent van Britta Simon in 15Five die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - toohave a counterpart of Britta Simon in 15Five that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6e8bc-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6e8bc-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6e8bc-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6e8bc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6e8bc-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing 15Five configureren.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="6e8bc-150">**Azure AD tooconfigure eenmalige aanmelding met 15Five, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6e8bc-150">**tooconfigure Azure AD single sign-on with 15Five, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e8bc-151">In de Azure-portal op Hallo Hallo **15Five** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-151">In hello Azure portal, on hello **15Five** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6e8bc-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="6e8bc-155">Op Hallo **15Five domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e8bc-155">On hello **15Five Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="6e8bc-157">a.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-157">a.</span></span> <span data-ttu-id="6e8bc-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.15five.com`</span><span class="sxs-lookup"><span data-stu-id="6e8bc-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="6e8bc-159">b.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-159">b.</span></span> <span data-ttu-id="6e8bc-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.15five.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="6e8bc-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6e8bc-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-161">These values are not real.</span></span> <span data-ttu-id="6e8bc-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6e8bc-163">Neem contact op met [15Five Client ondersteuningsteam](https://www.15five.com/contact/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-163">Contact [15Five Client support team](https://www.15five.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="6e8bc-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="6e8bc-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6e8bc-168">tooconfigure eenmalige aanmelding op **15Five** zijde, moet u toosend Hallo gedownload **Metadata XML** te[15Five ondersteuningsteam](https://www.15five.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="6e8bc-168">tooconfigure single sign-on on **15Five** side, you need toosend hello downloaded **Metadata XML** too[15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="6e8bc-169">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6e8bc-170">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6e8bc-171">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6e8bc-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6e8bc-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6e8bc-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="6e8bc-173">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6e8bc-175">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6e8bc-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e8bc-176">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6e8bc-178">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6e8bc-180">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6e8bc-182">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e8bc-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6e8bc-184">a.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-184">a.</span></span> <span data-ttu-id="6e8bc-185">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e8bc-186">b.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-186">b.</span></span> <span data-ttu-id="6e8bc-187">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6e8bc-188">c.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-188">c.</span></span> <span data-ttu-id="6e8bc-189">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6e8bc-190">d.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-190">d.</span></span> <span data-ttu-id="6e8bc-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="6e8bc-192">Een testgebruiker 15Five maken</span><span class="sxs-lookup"><span data-stu-id="6e8bc-192">Creating a 15Five test user</span></span>

<span data-ttu-id="6e8bc-193">Azure AD tooenable gebruikers toolog in too15Five, ze in 15Five moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-193">tooenable Azure AD users toolog in too15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="6e8bc-194">Wanneer 15Five, inrichting is een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="6e8bc-195">tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e8bc-195">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="6e8bc-196">Meld u bij tooyour **15Five** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-196">Log in tooyour **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="6e8bc-197">Ga te**beheren bedrijf**.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-197">Go too**Manage Company**.</span></span>
   
    <span data-ttu-id="6e8bc-198">![Bedrijf beheren](./media/active-directory-saas-15five-tutorial/IC784675.png "bedrijf beheren")</span><span class="sxs-lookup"><span data-stu-id="6e8bc-198">![Manage Company](./media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="6e8bc-199">Ga te**mensen \> mensen toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-199">Go too**People \> Add People**.</span></span>
   
    <span data-ttu-id="6e8bc-200">![Mensen](./media/active-directory-saas-15five-tutorial/IC784676.png "personen")</span><span class="sxs-lookup"><span data-stu-id="6e8bc-200">![People](./media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="6e8bc-201">Uitvoeren in de sectie nieuwe persoon toevoegen Hallo, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e8bc-201">In hello Add New Person section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6e8bc-202">![Toevoegen van nieuwe persoon](./media/active-directory-saas-15five-tutorial/IC784677.png "nieuwe persoon toevoegen")</span><span class="sxs-lookup"><span data-stu-id="6e8bc-202">![Add New Person](./media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="6e8bc-203">a.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-203">a.</span></span> <span data-ttu-id="6e8bc-204">Type Hallo **voornaam**, **achternaam**, **titel**, **e-mailadres** een geldig Azure Active Directory-account dat u wilt dat tooprovision in Hallo gerelateerd tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-204">Type hello **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="6e8bc-205">b.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-205">b.</span></span> <span data-ttu-id="6e8bc-206">Klik op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="6e8bc-207">Hello Azure AD-account houder ontvangt een e-mailbericht met inbegrip van een account koppelen tooconfirm Hallo voordat deze wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-207">hello Azure AD account holder receives an email including a link tooconfirm hello account before it becomes active.</span></span>
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6e8bc-208">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e8bc-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6e8bc-209">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen too15Five toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too15Five.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6e8bc-211">**tooassign Britta Simon too15Five, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6e8bc-211">**tooassign Britta Simon too15Five, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e8bc-212">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6e8bc-214">Selecteer in de lijst met de toepassingen van Hallo **15Five**.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-214">In hello applications list, select **15Five**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="6e8bc-216">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6e8bc-218">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-218">Click **Add** button.</span></span> <span data-ttu-id="6e8bc-219">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6e8bc-221">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6e8bc-222">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6e8bc-223">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6e8bc-224">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6e8bc-224">Testing single sign-on</span></span>

<span data-ttu-id="6e8bc-225">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6e8bc-226">Als u op Hallo 15Five tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina van 15Five toepassing.</span><span class="sxs-lookup"><span data-stu-id="6e8bc-226">When you click hello 15Five tile in hello Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="6e8bc-227">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6e8bc-227">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6e8bc-228">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6e8bc-228">Additional resources</span></span>

* [<span data-ttu-id="6e8bc-229">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e8bc-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6e8bc-230">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6e8bc-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png

