---
title: 'Zelfstudie: Azure Active Directory-integratie met JobScore | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en JobScore.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f51b32-e55c-4c66-96e8-50a2f9c2194a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6693a5fd96bfd7fbcd7197983b5f04d061970bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscore"></a><span data-ttu-id="ad9ad-103">Zelfstudie: Azure Active Directory-integratie met JobScore</span><span class="sxs-lookup"><span data-stu-id="ad9ad-103">Tutorial: Azure Active Directory integration with JobScore</span></span>

<span data-ttu-id="ad9ad-104">In deze zelfstudie leert u hoe toointegrate JobScore met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad9ad-104">In this tutorial, you learn how toointegrate JobScore with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad9ad-105">JobScore integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ad9ad-105">Integrating JobScore with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ad9ad-106">U kunt beheren in Azure AD die tooJobScore toegang heeft</span><span class="sxs-lookup"><span data-stu-id="ad9ad-106">You can control in Azure AD who has access tooJobScore</span></span>
- <span data-ttu-id="ad9ad-107">U kunt uw gebruikers tooautomatically get aangemelde tooJobScore (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ad9ad-107">You can enable your users tooautomatically get signed-on tooJobScore (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ad9ad-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ad9ad-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ad9ad-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad9ad-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad9ad-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ad9ad-110">Prerequisites</span></span>

<span data-ttu-id="ad9ad-111">Azure AD-integratie met JobScore tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ad9ad-111">tooconfigure Azure AD integration with JobScore, you need hello following items:</span></span>

- <span data-ttu-id="ad9ad-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ad9ad-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ad9ad-113">Een JobScore eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ad9ad-113">A JobScore single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad9ad-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ad9ad-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ad9ad-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad9ad-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ad9ad-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad9ad-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad9ad-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ad9ad-118">Scenario description</span></span>
<span data-ttu-id="ad9ad-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad9ad-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ad9ad-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad9ad-121">Het toevoegen van JobScore van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ad9ad-121">Adding JobScore from hello gallery</span></span>
2. <span data-ttu-id="ad9ad-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ad9ad-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscore-from-hello-gallery"></a><span data-ttu-id="ad9ad-123">Het toevoegen van JobScore van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ad9ad-123">Adding JobScore from hello gallery</span></span>
<span data-ttu-id="ad9ad-124">tooconfigure hello integratie van JobScore in Azure AD, moet u tooadd JobScore uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-124">tooconfigure hello integration of JobScore into Azure AD, you need tooadd JobScore from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ad9ad-125">**tooadd JobScore via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ad9ad-125">**tooadd JobScore from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad9ad-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ad9ad-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ad9ad-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ad9ad-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ad9ad-133">Typ in het zoekvak Hallo **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-133">In hello search box, type **JobScore**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_search.png)

5. <span data-ttu-id="ad9ad-135">Selecteer in het deelvenster resultaten hello, **JobScore**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-135">In hello results panel, select **JobScore**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ad9ad-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ad9ad-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ad9ad-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met JobScore op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="ad9ad-138">In this section, you configure and test Azure AD single sign-on with JobScore based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ad9ad-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in JobScore is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in JobScore is tooa user in Azure AD.</span></span> <span data-ttu-id="ad9ad-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in JobScore toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-140">In other words, a link relationship between an Azure AD user and hello related user in JobScore needs toobe established.</span></span>

<span data-ttu-id="ad9ad-141">Wijs in JobScore, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-141">In JobScore, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ad9ad-142">tooconfigure en eenmalige aanmelding Azure AD-test met JobScore, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ad9ad-142">tooconfigure and test Azure AD single sign-on with JobScore, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ad9ad-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ad9ad-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ad9ad-145">**[Maken van een testgebruiker JobScore](#creating-a-jobscore-test-user)**  -toohave een equivalent van Britta Simon in JobScore die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-145">**[Creating a JobScore test user](#creating-a-jobscore-test-user)** - toohave a counterpart of Britta Simon in JobScore that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ad9ad-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad9ad-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ad9ad-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ad9ad-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ad9ad-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing JobScore configureren.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your JobScore application.</span></span>

<span data-ttu-id="ad9ad-150">**Azure AD tooconfigure eenmalige aanmelding met JobScore, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ad9ad-150">**tooconfigure Azure AD single sign-on with JobScore, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad9ad-151">In de Azure-portal op Hallo Hallo **JobScore** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-151">In hello Azure portal, on hello **JobScore** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ad9ad-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_samlbase.png)

3. <span data-ttu-id="ad9ad-155">Op Hallo **JobScore domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ad9ad-155">On hello **JobScore Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_url.png)

    <span data-ttu-id="ad9ad-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://hire.jobscore.com/auth/adfs/<company name>`</span><span class="sxs-lookup"><span data-stu-id="ad9ad-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://hire.jobscore.com/auth/adfs/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ad9ad-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-158">This value is not real.</span></span> <span data-ttu-id="ad9ad-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ad9ad-160">Neem contact op met [JobScore Client ondersteuningsteam](mailto:support@jobscore.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-160">Contact [JobScore Client support team](mailto:support@jobscore.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="ad9ad-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_certificate.png) 

5. <span data-ttu-id="ad9ad-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscore-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ad9ad-165">tooconfigure eenmalige aanmelding op **JobScore** zijde, moet u toosend Hallo gedownload **Metadata XML** te[JobScore ondersteuningsteam](mailto:support@jobscore.com).</span><span class="sxs-lookup"><span data-stu-id="ad9ad-165">tooconfigure single sign-on on **JobScore** side, you need toosend hello downloaded **Metadata XML** too[JobScore support team](mailto:support@jobscore.com).</span></span> 

> [!TIP]
> <span data-ttu-id="ad9ad-166">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ad9ad-167">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ad9ad-168">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ad9ad-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ad9ad-169">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ad9ad-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="ad9ad-170">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ad9ad-172">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ad9ad-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad9ad-173">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscore-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ad9ad-175">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscore-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ad9ad-177">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscore-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ad9ad-179">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ad9ad-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobscore-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ad9ad-181">a.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-181">a.</span></span> <span data-ttu-id="ad9ad-182">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad9ad-183">b.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-183">b.</span></span> <span data-ttu-id="ad9ad-184">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ad9ad-185">c.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-185">c.</span></span> <span data-ttu-id="ad9ad-186">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ad9ad-187">d.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-187">d.</span></span> <span data-ttu-id="ad9ad-188">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-188">Click **Create**.</span></span>
 
### <a name="creating-a-jobscore-test-user"></a><span data-ttu-id="ad9ad-189">Een testgebruiker JobScore maken</span><span class="sxs-lookup"><span data-stu-id="ad9ad-189">Creating a JobScore test user</span></span>

<span data-ttu-id="ad9ad-190">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in JobScore maken.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-190">In this section, you create a user called Britta Simon in JobScore.</span></span> <span data-ttu-id="ad9ad-191">Werken met [JobScore ondersteuningsteam](mailto:support@jobscore.com) tooadd Hallo gebruikers in Hallo JobScore platform.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-191">Work with [JobScore support team](mailto:support@jobscore.com) tooadd hello users in hello JobScore platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ad9ad-192">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad9ad-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ad9ad-193">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooJobScore toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobScore.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ad9ad-195">**tooassign Britta Simon tooJobScore, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ad9ad-195">**tooassign Britta Simon tooJobScore, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad9ad-196">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-196">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ad9ad-198">Selecteer in de lijst met de toepassingen van Hallo **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-198">In hello applications list, select **JobScore**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_app.png) 

3. <span data-ttu-id="ad9ad-200">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ad9ad-202">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-202">Click **Add** button.</span></span> <span data-ttu-id="ad9ad-203">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ad9ad-205">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ad9ad-206">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ad9ad-207">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ad9ad-208">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ad9ad-208">Testing single sign-on</span></span>

<span data-ttu-id="ad9ad-209">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-209">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ad9ad-210">Als u op Hallo JobScore tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour JobScore toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad9ad-210">When you click hello JobScore tile in hello Access Panel, you should get automatically signed-on tooyour JobScore application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad9ad-211">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ad9ad-211">Additional resources</span></span>

* [<span data-ttu-id="ad9ad-212">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad9ad-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad9ad-213">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ad9ad-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_203.png

