---
title: 'Zelfstudie: Azure Active Directory-integratie met mensen | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en personen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: d540c31867c92c4dc09db9c0833f8a8a7c02b371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="2d28a-103">Zelfstudie: Azure Active Directory-integratie met mensen</span><span class="sxs-lookup"><span data-stu-id="2d28a-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="2d28a-104">In deze zelfstudie leert u hoe toointegrate mensen met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2d28a-104">In this tutorial, you learn how toointegrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2d28a-105">Mensen integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2d28a-105">Integrating People with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2d28a-106">U kunt beheren in Azure AD die tooPeople toegang heeft</span><span class="sxs-lookup"><span data-stu-id="2d28a-106">You can control in Azure AD who has access tooPeople</span></span>
- <span data-ttu-id="2d28a-107">U kunt uw gebruikers tooautomatically get aangemelde tooPeople (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="2d28a-107">You can enable your users tooautomatically get signed-on tooPeople (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2d28a-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2d28a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2d28a-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2d28a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d28a-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2d28a-110">Prerequisites</span></span>

<span data-ttu-id="2d28a-111">Azure AD-integratie met mensen tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="2d28a-111">tooconfigure Azure AD integration with People, you need hello following items:</span></span>

- <span data-ttu-id="2d28a-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2d28a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2d28a-113">Een mensen eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2d28a-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2d28a-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2d28a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2d28a-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2d28a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2d28a-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2d28a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2d28a-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d28a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2d28a-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2d28a-118">Scenario description</span></span>
<span data-ttu-id="2d28a-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2d28a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2d28a-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2d28a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2d28a-121">Toevoegen van personen uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2d28a-121">Adding People from hello gallery</span></span>
2. <span data-ttu-id="2d28a-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2d28a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-hello-gallery"></a><span data-ttu-id="2d28a-123">Toevoegen van personen uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2d28a-123">Adding People from hello gallery</span></span>
<span data-ttu-id="2d28a-124">tooconfigure hello integratie van mensen in Azure AD, moet u tooadd mensen uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2d28a-124">tooconfigure hello integration of People into Azure AD, you need tooadd People from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2d28a-125">**tooadd mensen uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2d28a-125">**tooadd People from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d28a-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2d28a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2d28a-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2d28a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2d28a-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2d28a-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2d28a-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2d28a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2d28a-133">Typ in het zoekvak Hallo **mensen**.</span><span class="sxs-lookup"><span data-stu-id="2d28a-133">In hello search box, type **People**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="2d28a-135">Selecteer in het deelvenster resultaten hello, **mensen**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2d28a-135">In hello results panel, select **People**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2d28a-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2d28a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2d28a-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met personen op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2d28a-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2d28a-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in mensen is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d28a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in People is tooa user in Azure AD.</span></span> <span data-ttu-id="2d28a-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in mensen toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="2d28a-140">In other words, a link relationship between an Azure AD user and hello related user in People needs toobe established.</span></span>

<span data-ttu-id="2d28a-141">In de mensen, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="2d28a-141">In People, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2d28a-142">tooconfigure en test eenmalige aanmelding Azure AD met gebruikers, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d28a-142">tooconfigure and test Azure AD single sign-on with People, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2d28a-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="2d28a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2d28a-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d28a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2d28a-145">**[Maken van een testgebruiker mensen](#creating-a-people-test-user)**  -toohave een equivalent van Britta Simon in de personen die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2d28a-145">**[Creating a People test user](#creating-a-people-test-user)** - toohave a counterpart of Britta Simon in People that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2d28a-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2d28a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2d28a-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2d28a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2d28a-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2d28a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2d28a-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing personen.</span><span class="sxs-lookup"><span data-stu-id="2d28a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="2d28a-150">**Voer tooconfigure Azure AD eenmalige aanmelding met mensen, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2d28a-150">**tooconfigure Azure AD single sign-on with People, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d28a-151">In de Azure-portal op Hallo Hallo **mensen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2d28a-151">In hello Azure portal, on hello **People** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2d28a-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2d28a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="2d28a-155">Op Hallo **mensen domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d28a-155">On hello **People Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="2d28a-157">a.</span><span class="sxs-lookup"><span data-stu-id="2d28a-157">a.</span></span> <span data-ttu-id="2d28a-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.peoplehr.com/`</span><span class="sxs-lookup"><span data-stu-id="2d28a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="2d28a-159">b.</span><span class="sxs-lookup"><span data-stu-id="2d28a-159">b.</span></span> <span data-ttu-id="2d28a-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="2d28a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="2d28a-161">c.</span><span class="sxs-lookup"><span data-stu-id="2d28a-161">c.</span></span> <span data-ttu-id="2d28a-162">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="2d28a-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2d28a-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="2d28a-163">These values are not real.</span></span> <span data-ttu-id="2d28a-164">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="2d28a-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2d28a-165">Neem contact op met [mensen Client ondersteuningsteam](mailto:customerservices@peoplehr.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2d28a-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) tooget these values.</span></span>

5. <span data-ttu-id="2d28a-166">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2d28a-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="2d28a-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2d28a-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="2d28a-170">tooget SSO is geconfigureerd voor uw toepassing, moet u toosign op tooyour mensen tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="2d28a-170">tooget SSO configured for your application, you need toosign-on tooyour People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="2d28a-171">Klik in het menu aan de linkerkant Hallo Hallo op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="2d28a-171">In hello menu on hello left side, click **Settings**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="2d28a-173">Klik op **bedrijf**.</span><span class="sxs-lookup"><span data-stu-id="2d28a-173">Click **Company**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="2d28a-175">Op Hallo **uploaden 'Eenmalige aanmelding' SAML meta-gegevensbestand**, klikt u op **Bladeren** tooupload Hallo gedownload bestand met metagegevens.</span><span class="sxs-lookup"><span data-stu-id="2d28a-175">On hello **Upload 'Single Sign On' SAML meta-data file**, click **Browse** tooupload hello downloaded metadata file.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="2d28a-177">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="2d28a-177">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2d28a-178">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="2d28a-178">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2d28a-179">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2d28a-179">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2d28a-180">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2d28a-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="2d28a-181">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2d28a-181">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2d28a-183">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2d28a-183">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d28a-184">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2d28a-184">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2d28a-186">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2d28a-186">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2d28a-188">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="2d28a-188">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2d28a-190">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d28a-190">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2d28a-192">a.</span><span class="sxs-lookup"><span data-stu-id="2d28a-192">a.</span></span> <span data-ttu-id="2d28a-193">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2d28a-193">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2d28a-194">b.</span><span class="sxs-lookup"><span data-stu-id="2d28a-194">b.</span></span> <span data-ttu-id="2d28a-195">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2d28a-195">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2d28a-196">c.</span><span class="sxs-lookup"><span data-stu-id="2d28a-196">c.</span></span> <span data-ttu-id="2d28a-197">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2d28a-197">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2d28a-198">d.</span><span class="sxs-lookup"><span data-stu-id="2d28a-198">d.</span></span> <span data-ttu-id="2d28a-199">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2d28a-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="2d28a-200">Maken van een testgebruiker personen</span><span class="sxs-lookup"><span data-stu-id="2d28a-200">Creating a People test user</span></span>

<span data-ttu-id="2d28a-201">In deze sectie maakt u Britta Simon aangeroepen in mensen van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2d28a-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="2d28a-202">Werken met [mensen Client ondersteuningsteam](mailto:customerservices@peoplehr.com) Hallo gebruikers toevoegen in Hallo mensen platform.</span><span class="sxs-lookup"><span data-stu-id="2d28a-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add hello users in hello People platform.</span></span> <span data-ttu-id="2d28a-203">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2d28a-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2d28a-204">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d28a-204">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2d28a-205">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooPeople toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="2d28a-205">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPeople.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2d28a-207">**tooassign Britta Simon tooPeople, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2d28a-207">**tooassign Britta Simon tooPeople, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d28a-208">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2d28a-208">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2d28a-210">Selecteer in de lijst met de toepassingen van Hallo **mensen**.</span><span class="sxs-lookup"><span data-stu-id="2d28a-210">In hello applications list, select **People**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="2d28a-212">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2d28a-212">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2d28a-214">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2d28a-214">Click **Add** button.</span></span> <span data-ttu-id="2d28a-215">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2d28a-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2d28a-217">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="2d28a-217">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2d28a-218">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2d28a-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2d28a-219">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2d28a-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2d28a-220">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2d28a-220">Testing single sign-on</span></span>

<span data-ttu-id="2d28a-221">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="2d28a-221">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="2d28a-222">Als u op Hallo mensen-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour mensen toepassing.</span><span class="sxs-lookup"><span data-stu-id="2d28a-222">When you click hello People tile in hello Access Panel, you should get automatically signed-on tooyour People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2d28a-223">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2d28a-223">Additional resources</span></span>

* [<span data-ttu-id="2d28a-224">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d28a-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2d28a-225">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2d28a-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png

