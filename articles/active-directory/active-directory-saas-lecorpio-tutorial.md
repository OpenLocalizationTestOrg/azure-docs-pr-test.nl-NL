---
title: 'Zelfstudie: Azure Active Directory-integratie met Lecorpio | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Lecorpio.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 963eb36678c589f942f63c7ab555161255324717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a><span data-ttu-id="1cc12-103">Zelfstudie: Azure Active Directory-integratie met Lecorpio</span><span class="sxs-lookup"><span data-stu-id="1cc12-103">Tutorial: Azure Active Directory integration with Lecorpio</span></span>

<span data-ttu-id="1cc12-104">In deze zelfstudie leert u hoe toointegrate Lecorpio met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1cc12-104">In this tutorial, you learn how toointegrate Lecorpio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1cc12-105">Lecorpio integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1cc12-105">Integrating Lecorpio with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1cc12-106">U kunt beheren in Azure AD die tooLecorpio toegang heeft</span><span class="sxs-lookup"><span data-stu-id="1cc12-106">You can control in Azure AD who has access tooLecorpio</span></span>
- <span data-ttu-id="1cc12-107">U kunt uw gebruikers tooautomatically get aangemelde tooLecorpio (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="1cc12-107">You can enable your users tooautomatically get signed-on tooLecorpio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1cc12-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1cc12-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1cc12-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1cc12-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1cc12-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1cc12-110">Prerequisites</span></span>

<span data-ttu-id="1cc12-111">Azure AD-integratie met Lecorpio tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="1cc12-111">tooconfigure Azure AD integration with Lecorpio, you need hello following items:</span></span>

- <span data-ttu-id="1cc12-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1cc12-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1cc12-113">Een Lecorpio eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1cc12-113">A Lecorpio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1cc12-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1cc12-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1cc12-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1cc12-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1cc12-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1cc12-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1cc12-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1cc12-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1cc12-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1cc12-118">Scenario description</span></span>
<span data-ttu-id="1cc12-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1cc12-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1cc12-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1cc12-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1cc12-121">Het toevoegen van Lecorpio van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="1cc12-121">Adding Lecorpio from hello gallery</span></span>
2. <span data-ttu-id="1cc12-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1cc12-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lecorpio-from-hello-gallery"></a><span data-ttu-id="1cc12-123">Het toevoegen van Lecorpio van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="1cc12-123">Adding Lecorpio from hello gallery</span></span>
<span data-ttu-id="1cc12-124">tooconfigure hello integratie van Lecorpio in Azure AD, moet u tooadd Lecorpio uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1cc12-124">tooconfigure hello integration of Lecorpio into Azure AD, you need tooadd Lecorpio from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1cc12-125">**tooadd Lecorpio via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1cc12-125">**tooadd Lecorpio from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1cc12-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1cc12-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1cc12-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1cc12-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1cc12-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1cc12-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1cc12-131">Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="1cc12-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1cc12-133">Typ in het zoekvak Hallo **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="1cc12-133">In hello search box, type **Lecorpio**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_search.png)

5. <span data-ttu-id="1cc12-135">Selecteer in het deelvenster resultaten hello, **Lecorpio**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1cc12-135">In hello results panel, select **Lecorpio**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1cc12-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1cc12-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1cc12-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Lecorpio op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="1cc12-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1cc12-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Lecorpio is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1cc12-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lecorpio is tooa user in Azure AD.</span></span> <span data-ttu-id="1cc12-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Lecorpio toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="1cc12-140">In other words, a link relationship between an Azure AD user and hello related user in Lecorpio needs toobe established.</span></span>

<span data-ttu-id="1cc12-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="1cc12-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Lecorpio.</span></span>

<span data-ttu-id="1cc12-142">tooconfigure en eenmalige aanmelding Azure AD-test met Lecorpio, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1cc12-142">tooconfigure and test Azure AD single sign-on with Lecorpio, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1cc12-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="1cc12-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1cc12-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1cc12-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1cc12-145">**[Maken van een testgebruiker Lecorpio](#creating-a-lecorpio-test-user)**  -toohave een equivalent van Britta Simon in Lecorpio die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1cc12-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - toohave a counterpart of Britta Simon in Lecorpio that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1cc12-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1cc12-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1cc12-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1cc12-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1cc12-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1cc12-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1cc12-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Lecorpio configureren.</span><span class="sxs-lookup"><span data-stu-id="1cc12-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lecorpio application.</span></span>

<span data-ttu-id="1cc12-150">**Azure AD tooconfigure eenmalige aanmelding met Lecorpio, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1cc12-150">**tooconfigure Azure AD single sign-on with Lecorpio, perform hello following steps:**</span></span>

1. <span data-ttu-id="1cc12-151">In de Azure-portal op Hallo Hallo **Lecorpio** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1cc12-151">In hello Azure portal, on hello **Lecorpio** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1cc12-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1cc12-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

3. <span data-ttu-id="1cc12-155">Op Hallo **Lecorpio domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1cc12-155">On hello **Lecorpio Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_url.png)

    <span data-ttu-id="1cc12-157">a.</span><span class="sxs-lookup"><span data-stu-id="1cc12-157">a.</span></span> <span data-ttu-id="1cc12-158">In Hallo **aanmeldings-URL** textbox Hallo typewaarde met Hallo patroon volgen:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="1cc12-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    <span data-ttu-id="1cc12-159">b.</span><span class="sxs-lookup"><span data-stu-id="1cc12-159">b.</span></span> <span data-ttu-id="1cc12-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="1cc12-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1cc12-161">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="1cc12-161">These values are not hello real.</span></span> <span data-ttu-id="1cc12-162">Deze waarden bijwerken met Hallo werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="1cc12-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="1cc12-163">We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id.</span><span class="sxs-lookup"><span data-stu-id="1cc12-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="1cc12-164">Neem contact op met [Lecorpio Client ondersteuningsteam](mailto:info@lecorpio.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="1cc12-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="1cc12-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1cc12-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

5. <span data-ttu-id="1cc12-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1cc12-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lecorpio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1cc12-169">tooconfigure eenmalige aanmelding op **Lecorpio** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Lecorpio ondersteuningsteam](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="1cc12-169">tooconfigure single sign-on on **Lecorpio** side, you need toosend hello downloaded **Metadata XML** too[Lecorpio support team](mailto:info@lecorpio.com).</span></span>

> [!TIP]
> <span data-ttu-id="1cc12-170">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="1cc12-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1cc12-171">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="1cc12-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1cc12-172">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1cc12-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1cc12-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1cc12-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="1cc12-174">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1cc12-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1cc12-176">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1cc12-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1cc12-177">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1cc12-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1cc12-179">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1cc12-179">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1cc12-181">Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1cc12-181">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1cc12-183">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1cc12-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1cc12-185">a.</span><span class="sxs-lookup"><span data-stu-id="1cc12-185">a.</span></span> <span data-ttu-id="1cc12-186">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1cc12-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1cc12-187">b.</span><span class="sxs-lookup"><span data-stu-id="1cc12-187">b.</span></span> <span data-ttu-id="1cc12-188">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1cc12-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1cc12-189">c.</span><span class="sxs-lookup"><span data-stu-id="1cc12-189">c.</span></span> <span data-ttu-id="1cc12-190">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1cc12-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1cc12-191">d.</span><span class="sxs-lookup"><span data-stu-id="1cc12-191">d.</span></span> <span data-ttu-id="1cc12-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1cc12-192">Click **Create**.</span></span>
 
### <a name="creating-a-lecorpio-test-user"></a><span data-ttu-id="1cc12-193">Een testgebruiker Lecorpio maken</span><span class="sxs-lookup"><span data-stu-id="1cc12-193">Creating a Lecorpio test user</span></span>

<span data-ttu-id="1cc12-194">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Lecorpio maken.</span><span class="sxs-lookup"><span data-stu-id="1cc12-194">In this section, you create a user called Britta Simon in Lecorpio.</span></span> 

<span data-ttu-id="1cc12-195">Neem contact op met [Lecorpio Client ondersteuningsteam](mailto:info@lecorpio.com) tooadd Hallo gebruikers in Hallo Lecorpio toepassing.</span><span class="sxs-lookup"><span data-stu-id="1cc12-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) tooadd hello users in hello Lecorpio application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1cc12-196">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1cc12-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1cc12-197">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooLecorpio toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="1cc12-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLecorpio.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1cc12-199">**tooassign Britta Simon tooLecorpio, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1cc12-199">**tooassign Britta Simon tooLecorpio, perform hello following steps:**</span></span>

1. <span data-ttu-id="1cc12-200">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1cc12-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1cc12-202">Selecteer in de lijst met de toepassingen van Hallo **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="1cc12-202">In hello applications list, select **Lecorpio**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_app.png) 

3. <span data-ttu-id="1cc12-204">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1cc12-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1cc12-206">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1cc12-206">Click **Add** button.</span></span> <span data-ttu-id="1cc12-207">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1cc12-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1cc12-209">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="1cc12-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1cc12-210">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1cc12-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1cc12-211">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1cc12-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1cc12-212">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1cc12-212">Testing single sign-on</span></span>

<span data-ttu-id="1cc12-213">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="1cc12-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1cc12-214">Als u op Hallo Lecorpio tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Lecorpio toepassing.</span><span class="sxs-lookup"><span data-stu-id="1cc12-214">When you click hello Lecorpio tile in hello Access Panel, you should get automatically signed-on tooyour Lecorpio application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1cc12-215">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1cc12-215">Additional resources</span></span>

* [<span data-ttu-id="1cc12-216">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1cc12-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1cc12-217">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1cc12-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_203.png

