---
title: 'Zelfstudie: Azure Active Directory-integratie met Sciforma | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Sciforma.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: abbfb5ac-7687-4153-b263-8090102dae37
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: jeedes
ms.openlocfilehash: fca6237196061355e38d431e958964a45246f965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciforma"></a><span data-ttu-id="91d4d-103">Zelfstudie: Azure Active Directory-integratie met Sciforma</span><span class="sxs-lookup"><span data-stu-id="91d4d-103">Tutorial: Azure Active Directory integration with Sciforma</span></span>

<span data-ttu-id="91d4d-104">In deze zelfstudie leert u hoe toointegrate Sciforma met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="91d4d-104">In this tutorial, you learn how toointegrate Sciforma with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91d4d-105">Sciforma integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="91d4d-105">Integrating Sciforma with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="91d4d-106">U kunt beheren in Azure AD die tooSciforma toegang heeft</span><span class="sxs-lookup"><span data-stu-id="91d4d-106">You can control in Azure AD who has access tooSciforma</span></span>
- <span data-ttu-id="91d4d-107">U kunt uw gebruikers tooautomatically get aangemelde tooSciforma (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="91d4d-107">You can enable your users tooautomatically get signed-on tooSciforma (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="91d4d-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="91d4d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="91d4d-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="91d4d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91d4d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="91d4d-110">Prerequisites</span></span>

<span data-ttu-id="91d4d-111">Azure AD-integratie met Sciforma tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="91d4d-111">tooconfigure Azure AD integration with Sciforma, you need hello following items:</span></span>

- <span data-ttu-id="91d4d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="91d4d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91d4d-113">Een Sciforma eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="91d4d-113">A Sciforma single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91d4d-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="91d4d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91d4d-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="91d4d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91d4d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="91d4d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91d4d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91d4d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91d4d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="91d4d-118">Scenario description</span></span>
<span data-ttu-id="91d4d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="91d4d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91d4d-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="91d4d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91d4d-121">Het toevoegen van Sciforma van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="91d4d-121">Adding Sciforma from hello gallery</span></span>
2. <span data-ttu-id="91d4d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="91d4d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciforma-from-hello-gallery"></a><span data-ttu-id="91d4d-123">Het toevoegen van Sciforma van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="91d4d-123">Adding Sciforma from hello gallery</span></span>
<span data-ttu-id="91d4d-124">tooconfigure hello integratie van Sciforma in Azure AD, moet u tooadd Sciforma uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="91d4d-124">tooconfigure hello integration of Sciforma into Azure AD, you need tooadd Sciforma from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="91d4d-125">**tooadd Sciforma via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="91d4d-125">**tooadd Sciforma from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="91d4d-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="91d4d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="91d4d-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="91d4d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="91d4d-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="91d4d-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="91d4d-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="91d4d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="91d4d-133">Typ in het zoekvak Hallo **Sciforma**.</span><span class="sxs-lookup"><span data-stu-id="91d4d-133">In hello search box, type **Sciforma**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_search.png)

5. <span data-ttu-id="91d4d-135">Selecteer in het deelvenster resultaten hello, **Sciforma**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="91d4d-135">In hello results panel, select **Sciforma**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="91d4d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="91d4d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="91d4d-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Sciforma op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="91d4d-138">In this section, you configure and test Azure AD single sign-on with Sciforma based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="91d4d-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Sciforma is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91d4d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sciforma is tooa user in Azure AD.</span></span> <span data-ttu-id="91d4d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Sciforma toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="91d4d-140">In other words, a link relationship between an Azure AD user and hello related user in Sciforma needs toobe established.</span></span>

<span data-ttu-id="91d4d-141">Wijs in Sciforma, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="91d4d-141">In Sciforma, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="91d4d-142">tooconfigure en eenmalige aanmelding Azure AD-test met Sciforma, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="91d4d-142">tooconfigure and test Azure AD single sign-on with Sciforma, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="91d4d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="91d4d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="91d4d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91d4d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="91d4d-145">**[Maken van een testgebruiker Sciforma](#creating-a-sciforma-test-user)**  -toohave een equivalent van Britta Simon in Sciforma die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="91d4d-145">**[Creating a Sciforma test user](#creating-a-sciforma-test-user)** - toohave a counterpart of Britta Simon in Sciforma that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="91d4d-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="91d4d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="91d4d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="91d4d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="91d4d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="91d4d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="91d4d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Sciforma configureren.</span><span class="sxs-lookup"><span data-stu-id="91d4d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sciforma application.</span></span>

<span data-ttu-id="91d4d-150">**Azure AD tooconfigure eenmalige aanmelding met Sciforma, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="91d4d-150">**tooconfigure Azure AD single sign-on with Sciforma, perform hello following steps:**</span></span>

1. <span data-ttu-id="91d4d-151">In de Azure-portal op Hallo Hallo **Sciforma** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="91d4d-151">In hello Azure portal, on hello **Sciforma** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="91d4d-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="91d4d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_samlbase.png)

3. <span data-ttu-id="91d4d-155">Op Hallo **Sciforma domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="91d4d-155">On hello **Sciforma Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_url.png)

    <span data-ttu-id="91d4d-157">a.</span><span class="sxs-lookup"><span data-stu-id="91d4d-157">a.</span></span> <span data-ttu-id="91d4d-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.sciforma.net/sciforma/main.html`</span><span class="sxs-lookup"><span data-stu-id="91d4d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sciforma.net/sciforma/main.html`</span></span>

    <span data-ttu-id="91d4d-159">b.</span><span class="sxs-lookup"><span data-stu-id="91d4d-159">b.</span></span> <span data-ttu-id="91d4d-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.sciforma.net/sciforma/saml`</span><span class="sxs-lookup"><span data-stu-id="91d4d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sciforma.net/sciforma/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="91d4d-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="91d4d-161">These values are not real.</span></span> <span data-ttu-id="91d4d-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="91d4d-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="91d4d-163">Neem contact op met [Sciforma Client ondersteuningsteam](http://www.sciforma.com/company/contact_us) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="91d4d-163">Contact [Sciforma Client support team](http://www.sciforma.com/company/contact_us) tooget these values.</span></span> 
 


4. <span data-ttu-id="91d4d-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="91d4d-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_certificate.png) 

5. <span data-ttu-id="91d4d-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="91d4d-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sciforma-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="91d4d-168">tooconfigure eenmalige aanmelding op **Sciforma** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Sciforma ondersteuningsteam](http://www.sciforma.com/company/contact_us).</span><span class="sxs-lookup"><span data-stu-id="91d4d-168">tooconfigure single sign-on on **Sciforma** side, you need toosend hello downloaded **Metadata XML** too[Sciforma support team](http://www.sciforma.com/company/contact_us).</span></span>

> [!TIP]
> <span data-ttu-id="91d4d-169">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="91d4d-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="91d4d-170">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="91d4d-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="91d4d-171">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="91d4d-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="91d4d-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="91d4d-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="91d4d-173">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="91d4d-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="91d4d-175">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="91d4d-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="91d4d-176">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="91d4d-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sciforma-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="91d4d-178">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="91d4d-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sciforma-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="91d4d-180">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="91d4d-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sciforma-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="91d4d-182">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="91d4d-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sciforma-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="91d4d-184">a.</span><span class="sxs-lookup"><span data-stu-id="91d4d-184">a.</span></span> <span data-ttu-id="91d4d-185">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="91d4d-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91d4d-186">b.</span><span class="sxs-lookup"><span data-stu-id="91d4d-186">b.</span></span> <span data-ttu-id="91d4d-187">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="91d4d-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="91d4d-188">c.</span><span class="sxs-lookup"><span data-stu-id="91d4d-188">c.</span></span> <span data-ttu-id="91d4d-189">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="91d4d-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="91d4d-190">d.</span><span class="sxs-lookup"><span data-stu-id="91d4d-190">d.</span></span> <span data-ttu-id="91d4d-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="91d4d-191">Click **Create**.</span></span>
 
### <a name="creating-a-sciforma-test-user"></a><span data-ttu-id="91d4d-192">Een testgebruiker Sciforma maken</span><span class="sxs-lookup"><span data-stu-id="91d4d-192">Creating a Sciforma test user</span></span>

<span data-ttu-id="91d4d-193">Er is geen actie-item voor u tooconfigure gebruikers inrichten tooSciforma.</span><span class="sxs-lookup"><span data-stu-id="91d4d-193">There is no action item for you tooconfigure user provisioning tooSciforma.</span></span> <span data-ttu-id="91d4d-194">Wanneer een toegewezen gebruiker toolog in tooSciforma met behulp van het toegangsvenster hello probeert, controleert Sciforma of Hallo gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="91d4d-194">When an assigned user tries toolog in tooSciforma using hello access panel, Sciforma checks whether hello user exists.</span></span>  

* <span data-ttu-id="91d4d-195">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Sciforma.</span><span class="sxs-lookup"><span data-stu-id="91d4d-195">If there is no user account available yet, it is automatically created by Sciforma.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="91d4d-196">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="91d4d-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="91d4d-197">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSciforma toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="91d4d-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSciforma.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="91d4d-199">**tooassign Britta Simon tooSciforma, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="91d4d-199">**tooassign Britta Simon tooSciforma, perform hello following steps:**</span></span>

1. <span data-ttu-id="91d4d-200">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="91d4d-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="91d4d-202">Selecteer in de lijst met de toepassingen van Hallo **Sciforma**.</span><span class="sxs-lookup"><span data-stu-id="91d4d-202">In hello applications list, select **Sciforma**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_app.png) 

3. <span data-ttu-id="91d4d-204">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="91d4d-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="91d4d-206">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="91d4d-206">Click **Add** button.</span></span> <span data-ttu-id="91d4d-207">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="91d4d-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="91d4d-209">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="91d4d-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="91d4d-210">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="91d4d-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="91d4d-211">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="91d4d-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="91d4d-212">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="91d4d-212">Testing single sign-on</span></span>

<span data-ttu-id="91d4d-213">Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="91d4d-213">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="91d4d-214">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="91d4d-214">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="91d4d-215">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="91d4d-215">Additional resources</span></span>

* [<span data-ttu-id="91d4d-216">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91d4d-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91d4d-217">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="91d4d-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_203.png

