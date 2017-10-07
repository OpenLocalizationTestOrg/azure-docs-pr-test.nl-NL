---
title: 'Zelfstudie: Azure Active Directory-integratie met handel | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en handel.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 1a7cdd00c4f2b15a1afc89522d79af22f4c5d866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a><span data-ttu-id="51124-103">Zelfstudie: Azure Active Directory-integratie met handel</span><span class="sxs-lookup"><span data-stu-id="51124-103">Tutorial: Azure Active Directory integration with Greenhouse</span></span>

<span data-ttu-id="51124-104">In deze zelfstudie leert u hoe toointegrate handel met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="51124-104">In this tutorial, you learn how toointegrate Greenhouse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="51124-105">Handel integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="51124-105">Integrating Greenhouse with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="51124-106">U kunt beheren in Azure AD die tooGreenhouse toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="51124-106">You can control in Azure AD who has access tooGreenhouse.</span></span>
- <span data-ttu-id="51124-107">U kunt uw gebruikers tooautomatically get aangemelde tooGreenhouse (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="51124-107">You can enable your users tooautomatically get signed-on tooGreenhouse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="51124-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="51124-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="51124-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="51124-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51124-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="51124-110">Prerequisites</span></span>

<span data-ttu-id="51124-111">Azure AD-integratie met handel tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="51124-111">tooconfigure Azure AD integration with Greenhouse, you need hello following items:</span></span>

- <span data-ttu-id="51124-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="51124-112">An Azure AD subscription</span></span>
- <span data-ttu-id="51124-113">Een handel eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="51124-113">A Greenhouse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="51124-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="51124-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="51124-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="51124-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="51124-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="51124-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="51124-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="51124-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="51124-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="51124-118">Scenario description</span></span>
<span data-ttu-id="51124-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="51124-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="51124-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="51124-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="51124-121">Het toevoegen van handel van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="51124-121">Adding Greenhouse from hello gallery</span></span>
2. <span data-ttu-id="51124-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="51124-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-greenhouse-from-hello-gallery"></a><span data-ttu-id="51124-123">Het toevoegen van handel van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="51124-123">Adding Greenhouse from hello gallery</span></span>
<span data-ttu-id="51124-124">tooconfigure hello integratie van handel in Azure AD, moet u tooadd handel in Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="51124-124">tooconfigure hello integration of Greenhouse into Azure AD, you need tooadd Greenhouse from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="51124-125">**tooadd handel via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="51124-125">**tooadd Greenhouse from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="51124-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="51124-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="51124-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="51124-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="51124-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="51124-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="51124-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="51124-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="51124-133">Typ in het zoekvak Hallo **handel**, selecteer **handel** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="51124-133">In hello search box, type **Greenhouse**, select **Greenhouse** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Handel in de lijst met resultaten Hallo](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="51124-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="51124-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="51124-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met handel op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="51124-136">In this section, you configure and test Azure AD single sign-on with Greenhouse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="51124-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de handel is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51124-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Greenhouse is tooa user in Azure AD.</span></span> <span data-ttu-id="51124-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in de handel Hallo toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="51124-138">In other words, a link relationship between an Azure AD user and hello related user in Greenhouse needs toobe established.</span></span>

<span data-ttu-id="51124-139">In de handel, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="51124-139">In Greenhouse, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="51124-140">tooconfigure en eenmalige aanmelding Azure AD-test met handel, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="51124-140">tooconfigure and test Azure AD single sign-on with Greenhouse, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="51124-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="51124-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="51124-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="51124-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="51124-143">**[Maak een testgebruiker handel](#create-a-greenhouse-test-user)**  -toohave een equivalent van Britta Simon in handel die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="51124-143">**[Create a Greenhouse test user](#create-a-greenhouse-test-user)** - toohave a counterpart of Britta Simon in Greenhouse that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="51124-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="51124-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="51124-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="51124-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="51124-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="51124-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="51124-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing handel configureren.</span><span class="sxs-lookup"><span data-stu-id="51124-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Greenhouse application.</span></span>

<span data-ttu-id="51124-148">**Azure AD tooconfigure eenmalige aanmelding met handel, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="51124-148">**tooconfigure Azure AD single sign-on with Greenhouse, perform hello following steps:**</span></span>

1. <span data-ttu-id="51124-149">In de Azure-portal op Hallo Hallo **handel** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="51124-149">In hello Azure portal, on hello **Greenhouse** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="51124-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="51124-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_samlbase.png)

3. <span data-ttu-id="51124-153">Op Hallo **handel domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="51124-153">On hello **Greenhouse Domain and URLs** section, perform hello following steps:</span></span>

    ![Handel domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_url.png)

    <span data-ttu-id="51124-155">a.</span><span class="sxs-lookup"><span data-stu-id="51124-155">a.</span></span> <span data-ttu-id="51124-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="51124-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.greenhouse.io`</span></span>

    <span data-ttu-id="51124-157">b.</span><span class="sxs-lookup"><span data-stu-id="51124-157">b.</span></span> <span data-ttu-id="51124-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="51124-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.greenhouse.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="51124-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="51124-159">These values are not real.</span></span> <span data-ttu-id="51124-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="51124-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="51124-161">Neem contact op met [handel Client ondersteuningsteam](https://www.greenhouse.io/contact) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="51124-161">Contact [Greenhouse Client support team](https://www.greenhouse.io/contact) tooget these values.</span></span> 
 


4. <span data-ttu-id="51124-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="51124-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_certificate.png) 

5. <span data-ttu-id="51124-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="51124-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-greenhouse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="51124-166">tooconfigure eenmalige aanmelding op **handel** zijde, moet u toosend Hallo gedownload **Metadata XML** te[handel ondersteuningsteam](http://www.greenhouse.io/contact).</span><span class="sxs-lookup"><span data-stu-id="51124-166">tooconfigure single sign-on on **Greenhouse** side, you need toosend hello downloaded **Metadata XML** too[Greenhouse support team](http://www.greenhouse.io/contact).</span></span>

> [!TIP]
> <span data-ttu-id="51124-167">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="51124-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="51124-168">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="51124-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="51124-169">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="51124-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="51124-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="51124-170">Create an Azure AD test user</span></span>

<span data-ttu-id="51124-171">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="51124-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="51124-173">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="51124-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="51124-174">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="51124-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="51124-176">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="51124-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="51124-178">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="51124-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="51124-180">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="51124-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="51124-182">a.</span><span class="sxs-lookup"><span data-stu-id="51124-182">a.</span></span> <span data-ttu-id="51124-183">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="51124-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="51124-184">b.</span><span class="sxs-lookup"><span data-stu-id="51124-184">b.</span></span> <span data-ttu-id="51124-185">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="51124-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="51124-186">c.</span><span class="sxs-lookup"><span data-stu-id="51124-186">c.</span></span> <span data-ttu-id="51124-187">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="51124-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="51124-188">d.</span><span class="sxs-lookup"><span data-stu-id="51124-188">d.</span></span> <span data-ttu-id="51124-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="51124-189">Click **Create**.</span></span>
 
### <a name="create-a-greenhouse-test-user"></a><span data-ttu-id="51124-190">Een testgebruiker handel maken</span><span class="sxs-lookup"><span data-stu-id="51124-190">Create a Greenhouse test user</span></span>

<span data-ttu-id="51124-191">In volgorde tooenable Azure AD gebruikers toolog in handel, moeten ze worden ingericht in de handel.</span><span class="sxs-lookup"><span data-stu-id="51124-191">In order tooenable Azure AD users toolog into Greenhouse, they must be provisioned into Greenhouse.</span></span> <span data-ttu-id="51124-192">In geval van handel Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="51124-192">In hello case of Greenhouse, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="51124-193">U kunt andere handel gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door handel tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="51124-193">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="51124-194">**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**</span><span class="sxs-lookup"><span data-stu-id="51124-194">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="51124-195">Meld u bij tooyour **handel** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="51124-195">Log in tooyour **Greenhouse** company site as an administrator.</span></span>

2. <span data-ttu-id="51124-196">Klik in het menu bovenaan Hallo Hallo **configureren**, en klik vervolgens op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="51124-196">In hello menu on hello top, click **Configure**, and then click **Users**.</span></span>
   
   <span data-ttu-id="51124-197">![Gebruikers](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="51124-197">![Users](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Users")</span></span>

3. <span data-ttu-id="51124-198">Klik op **nieuwe gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="51124-198">Click **New Users**.</span></span>
   
   <span data-ttu-id="51124-199">![Nieuwe gebruiker](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="51124-199">![New User](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "New User")</span></span>

4. <span data-ttu-id="51124-200">In Hallo **nieuwe gebruiker toevoegen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="51124-200">In hello **Add New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="51124-201">![Nieuwe gebruiker toevoegen](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "nieuwe gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="51124-201">![Add New User](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Add New User")</span></span>

   <span data-ttu-id="51124-202">a.</span><span class="sxs-lookup"><span data-stu-id="51124-202">a.</span></span> <span data-ttu-id="51124-203">In Hallo **e-mails van de gebruiker invoeren** textbox type Hallo e-mailadres van een geldige Azure Active Directory-account dat u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="51124-203">In hello **Enter user emails** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision.</span></span>

   <span data-ttu-id="51124-204">b.</span><span class="sxs-lookup"><span data-stu-id="51124-204">b.</span></span> <span data-ttu-id="51124-205">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="51124-205">Click **Save**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="51124-206">Hello Azure Active Directory met een kinderaccount ontvangt een e-mailbericht met inbegrip van een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="51124-206">hello Azure Active Directory account holders will receive an email including a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="51124-207">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="51124-207">Assign hello Azure AD test user</span></span>

<span data-ttu-id="51124-208">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooGreenhouse toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="51124-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGreenhouse.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="51124-210">**tooassign Britta Simon tooGreenhouse, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="51124-210">**tooassign Britta Simon tooGreenhouse, perform hello following steps:**</span></span>

1. <span data-ttu-id="51124-211">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="51124-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="51124-213">Selecteer in de lijst met de toepassingen van Hallo **handel**.</span><span class="sxs-lookup"><span data-stu-id="51124-213">In hello applications list, select **Greenhouse**.</span></span>

    ![Hallo handel koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_app.png)  

3. <span data-ttu-id="51124-215">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="51124-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="51124-217">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="51124-217">Click **Add** button.</span></span> <span data-ttu-id="51124-218">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="51124-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="51124-220">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="51124-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="51124-221">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="51124-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="51124-222">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="51124-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="51124-223">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="51124-223">Test single sign-on</span></span>

<span data-ttu-id="51124-224">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="51124-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="51124-225">Als u op Hallo handel tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour handel toepassing.</span><span class="sxs-lookup"><span data-stu-id="51124-225">When you click hello Greenhouse tile in hello Access Panel, you should get automatically signed-on tooyour Greenhouse application.</span></span>
<span data-ttu-id="51124-226">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="51124-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="51124-227">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="51124-227">Additional resources</span></span>

* [<span data-ttu-id="51124-228">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="51124-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="51124-229">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="51124-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_203.png

