---
title: 'Zelfstudie: Azure Active Directory-integratie met Convercent | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Convercent.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: e6d09d7de52779dcf05e80215df9369ebc2ed06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="5c710-103">Zelfstudie: Azure Active Directory-integratie met Convercent</span><span class="sxs-lookup"><span data-stu-id="5c710-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="5c710-104">In deze zelfstudie leert u hoe toointegrate Convercent met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c710-104">In this tutorial, you learn how toointegrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c710-105">Convercent integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="5c710-105">Integrating Convercent with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5c710-106">U kunt beheren in Azure AD die tooConvercent toegang heeft</span><span class="sxs-lookup"><span data-stu-id="5c710-106">You can control in Azure AD who has access tooConvercent</span></span>
- <span data-ttu-id="5c710-107">U kunt uw gebruikers tooautomatically get aangemelde tooConvercent (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="5c710-107">You can enable your users tooautomatically get signed-on tooConvercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c710-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="5c710-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5c710-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c710-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c710-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5c710-110">Prerequisites</span></span>

<span data-ttu-id="5c710-111">Azure AD-integratie met Convercent tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="5c710-111">tooconfigure Azure AD integration with Convercent, you need hello following items:</span></span>

- <span data-ttu-id="5c710-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="5c710-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c710-113">Een Convercent eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="5c710-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c710-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="5c710-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c710-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="5c710-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c710-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="5c710-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c710-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c710-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c710-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="5c710-118">Scenario description</span></span>
<span data-ttu-id="5c710-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="5c710-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c710-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="5c710-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c710-121">Het toevoegen van Convercent van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="5c710-121">Adding Convercent from hello gallery</span></span>
2. <span data-ttu-id="5c710-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5c710-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-hello-gallery"></a><span data-ttu-id="5c710-123">Het toevoegen van Convercent van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="5c710-123">Adding Convercent from hello gallery</span></span>
<span data-ttu-id="5c710-124">tooconfigure hello integratie van Convercent in Azure AD, moet u tooadd Convercent uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="5c710-124">tooconfigure hello integration of Convercent into Azure AD, you need tooadd Convercent from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5c710-125">**tooadd Convercent via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="5c710-125">**tooadd Convercent from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c710-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5c710-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c710-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5c710-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5c710-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5c710-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="5c710-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5c710-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="5c710-133">Typ in het zoekvak Hallo **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="5c710-133">In hello search box, type **Convercent**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_search.png)

5. <span data-ttu-id="5c710-135">Selecteer in het deelvenster resultaten hello, **Convercent**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="5c710-135">In hello results panel, select **Convercent**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c710-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5c710-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c710-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Convercent op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="5c710-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5c710-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Convercent is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c710-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Convercent is tooa user in Azure AD.</span></span> <span data-ttu-id="5c710-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Convercent toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="5c710-140">In other words, a link relationship between an Azure AD user and hello related user in Convercent needs toobe established.</span></span>

<span data-ttu-id="5c710-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Convercent.</span><span class="sxs-lookup"><span data-stu-id="5c710-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Convercent.</span></span>

<span data-ttu-id="5c710-142">tooconfigure en eenmalige aanmelding Azure AD-test met Convercent, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5c710-142">tooconfigure and test Azure AD single sign-on with Convercent, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5c710-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="5c710-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5c710-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c710-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c710-145">**[Maken van een testgebruiker Convercent](#creating-a-convercent-test-user)**  -toohave een equivalent van Britta Simon in Convercent die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5c710-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - toohave a counterpart of Britta Simon in Convercent that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c710-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5c710-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c710-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="5c710-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c710-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="5c710-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c710-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Convercent configureren.</span><span class="sxs-lookup"><span data-stu-id="5c710-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="5c710-150">**Azure AD tooconfigure eenmalige aanmelding met Convercent, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="5c710-150">**tooconfigure Azure AD single sign-on with Convercent, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c710-151">In de Azure-portal op Hallo Hallo **Convercent** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="5c710-151">In hello Azure portal, on hello **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="5c710-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5c710-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_samlbase.png)

3. <span data-ttu-id="5c710-155">Op Hallo **Convercent domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP geïnitieerd modus**, Hallo stap uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5c710-155">On hello **Convercent Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="5c710-157">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="5c710-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.convercent.com/`</span></span>
 
4. <span data-ttu-id="5c710-158">U kunt eventueel tooconfigure Hallo toepassing in **SP geïnitieerd modus**, op Hallo **Convercent domein en de URL's** sectie Hallo stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5c710-158">If you wish tooconfigure hello application in **SP initiated mode**, on hello **Convercent Domain and URLs** section perform hello following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="5c710-160">a.</span><span class="sxs-lookup"><span data-stu-id="5c710-160">a.</span></span> <span data-ttu-id="5c710-161">Klik op **'Weergeven geavanceerde instellingen voor de URL'.**</span><span class="sxs-lookup"><span data-stu-id="5c710-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="5c710-162">b.</span><span class="sxs-lookup"><span data-stu-id="5c710-162">b.</span></span> <span data-ttu-id="5c710-163">In Hallo **aanmelding op URL** textbox Hallo typewaarde met Hallo patroon volgen:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="5c710-163">In hello **Sign On URL** textbox, type hello value using hello following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="5c710-164">c.</span><span class="sxs-lookup"><span data-stu-id="5c710-164">c.</span></span> <span data-ttu-id="5c710-165">In Hallo **Relay status** textbox Hallo typewaarde met Hallo patroon volgen:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="5c710-165">In hello **Relay State** textbox, type hello value using hello following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c710-166">Deze waarden zijn niet Hallo echte waarden.</span><span class="sxs-lookup"><span data-stu-id="5c710-166">These values are not hello real values.</span></span> <span data-ttu-id="5c710-167">Bijwerken van deze waarden Hello werkelijke id, meld u op de URL en status van de Relay.</span><span class="sxs-lookup"><span data-stu-id="5c710-167">Update these values with hello actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="5c710-168">Neem contact op met [Convercent Client ondersteuningsteam](http://support.convercent.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="5c710-168">Contact [Convercent Client support team](http://support.convercent.com) tooget these values.</span></span>

5. <span data-ttu-id="5c710-169">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="5c710-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_certificate.png) 

6. <span data-ttu-id="5c710-171">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="5c710-171">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-convercent-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5c710-173">tooget SSO geconfigureerd voor uw toepassing, neem contact op met [Convercent ondersteuningsteam](mailto:support@convercent.com) en voorzien Hallo gedownload **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="5c710-173">tooget SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with hello downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="5c710-174">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="5c710-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5c710-175">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="5c710-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5c710-176">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c710-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c710-177">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="5c710-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c710-178">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="5c710-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="5c710-180">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="5c710-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c710-181">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5c710-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c710-183">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5c710-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c710-185">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="5c710-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c710-187">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5c710-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c710-189">a.</span><span class="sxs-lookup"><span data-stu-id="5c710-189">a.</span></span> <span data-ttu-id="5c710-190">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c710-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c710-191">b.</span><span class="sxs-lookup"><span data-stu-id="5c710-191">b.</span></span> <span data-ttu-id="5c710-192">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5c710-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c710-193">c.</span><span class="sxs-lookup"><span data-stu-id="5c710-193">c.</span></span> <span data-ttu-id="5c710-194">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="5c710-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5c710-195">d.</span><span class="sxs-lookup"><span data-stu-id="5c710-195">d.</span></span> <span data-ttu-id="5c710-196">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="5c710-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="5c710-197">Een testgebruiker Convercent maken</span><span class="sxs-lookup"><span data-stu-id="5c710-197">Creating a Convercent test user</span></span>

<span data-ttu-id="5c710-198">Werken met [Convercent ondersteuningsteam](mailto:support@convercent.com) tooadd Hallo gebruikers in Hallo Convercent platform.</span><span class="sxs-lookup"><span data-stu-id="5c710-198">Work with [Convercent support team](mailto:support@convercent.com) tooadd hello users in hello Convercent platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5c710-199">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c710-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5c710-200">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooConvercent toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="5c710-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConvercent.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="5c710-202">**tooassign Britta Simon tooConvercent, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="5c710-202">**tooassign Britta Simon tooConvercent, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c710-203">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5c710-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="5c710-205">Selecteer in de lijst met de toepassingen van Hallo **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="5c710-205">In hello applications list, select **Convercent**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_app.png) 

3. <span data-ttu-id="5c710-207">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="5c710-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="5c710-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="5c710-209">Click **Add** button.</span></span> <span data-ttu-id="5c710-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5c710-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="5c710-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="5c710-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5c710-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5c710-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c710-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5c710-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c710-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5c710-215">Testing single sign-on</span></span>

<span data-ttu-id="5c710-216">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="5c710-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5c710-217">Als u op Hallo Convercent tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Convercent toepassing.</span><span class="sxs-lookup"><span data-stu-id="5c710-217">When you click hello Convercent tile in hello Access Panel, you should get automatically signed-on tooyour Convercent application.</span></span>
<span data-ttu-id="5c710-218">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5c710-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5c710-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="5c710-219">Additional resources</span></span>

* [<span data-ttu-id="5c710-220">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c710-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c710-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5c710-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_203.png

