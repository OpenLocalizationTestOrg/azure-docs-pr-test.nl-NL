---
title: 'Zelfstudie: Azure Active Directory-integratie met SmarterU | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SmarterU.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: a3b81b557c47e31f09e61bcf75dd23f370e642e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="42667-103">Zelfstudie: Azure Active Directory-integratie met SmarterU</span><span class="sxs-lookup"><span data-stu-id="42667-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="42667-104">In deze zelfstudie leert u hoe toointegrate SmarterU met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42667-104">In this tutorial, you learn how toointegrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42667-105">SmarterU integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="42667-105">Integrating SmarterU with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="42667-106">U kunt beheren in Azure AD die tooSmarterU toegang heeft</span><span class="sxs-lookup"><span data-stu-id="42667-106">You can control in Azure AD who has access tooSmarterU</span></span>
- <span data-ttu-id="42667-107">U kunt uw gebruikers tooautomatically get aangemelde tooSmarterU (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="42667-107">You can enable your users tooautomatically get signed-on tooSmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42667-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="42667-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="42667-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42667-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42667-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="42667-110">Prerequisites</span></span>

<span data-ttu-id="42667-111">Azure AD-integratie met SmarterU tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="42667-111">tooconfigure Azure AD integration with SmarterU, you need hello following items:</span></span>

- <span data-ttu-id="42667-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="42667-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42667-113">Een SmarterU eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="42667-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42667-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="42667-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42667-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="42667-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42667-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="42667-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42667-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42667-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42667-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="42667-118">Scenario description</span></span>
<span data-ttu-id="42667-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="42667-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42667-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="42667-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42667-121">Het toevoegen van SmarterU van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="42667-121">Adding SmarterU from hello gallery</span></span>
2. <span data-ttu-id="42667-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="42667-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-hello-gallery"></a><span data-ttu-id="42667-123">Het toevoegen van SmarterU van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="42667-123">Adding SmarterU from hello gallery</span></span>
<span data-ttu-id="42667-124">tooconfigure hello integratie van SmarterU in Azure AD, moet u tooadd SmarterU uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="42667-124">tooconfigure hello integration of SmarterU into Azure AD, you need tooadd SmarterU from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="42667-125">**tooadd SmarterU via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="42667-125">**tooadd SmarterU from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="42667-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="42667-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42667-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="42667-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="42667-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="42667-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="42667-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="42667-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="42667-133">Typ in het zoekvak Hallo **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="42667-133">In hello search box, type **SmarterU**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="42667-135">Selecteer in het deelvenster resultaten hello, **SmarterU**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="42667-135">In hello results panel, select **SmarterU**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42667-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="42667-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42667-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met SmarterU op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="42667-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="42667-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in SmarterU is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42667-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SmarterU is tooa user in Azure AD.</span></span> <span data-ttu-id="42667-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in SmarterU toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="42667-140">In other words, a link relationship between an Azure AD user and hello related user in SmarterU needs toobe established.</span></span>

<span data-ttu-id="42667-141">Wijs in SmarterU, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="42667-141">In SmarterU, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="42667-142">tooconfigure en eenmalige aanmelding Azure AD-test met SmarterU, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="42667-142">tooconfigure and test Azure AD single sign-on with SmarterU, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="42667-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="42667-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="42667-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42667-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42667-145">**[Maken van een testgebruiker SmarterU](#creating-a-smarteru-test-user)**  -toohave een equivalent van Britta Simon in SmarterU die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="42667-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - toohave a counterpart of Britta Simon in SmarterU that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="42667-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="42667-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42667-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="42667-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42667-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="42667-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42667-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing SmarterU configureren.</span><span class="sxs-lookup"><span data-stu-id="42667-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="42667-150">**Azure AD tooconfigure eenmalige aanmelding met SmarterU, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="42667-150">**tooconfigure Azure AD single sign-on with SmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="42667-151">In de Azure-portal op Hallo Hallo **SmarterU** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="42667-151">In hello Azure portal, on hello **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="42667-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="42667-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="42667-155">Op Hallo **SmarterU domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="42667-155">On hello **SmarterU Domain and URLs** section, perform hello following steps:</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="42667-157">In Hallo **id** textbox type Hallo URL:`https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="42667-157">In hello **Identifier** textbox, type hello URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="42667-158">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="42667-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="42667-160">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="42667-160">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="42667-162">In een ander browservenster, meld u aan tooyour SmarterU bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="42667-162">In a different web browser window, log in tooyour SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="42667-163">Klik in de werkbalk bovenaan Hallo Hallo op **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="42667-163">In hello toolbar on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="42667-164">![Instellingen account](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Accountinstellingen")</span><span class="sxs-lookup"><span data-stu-id="42667-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="42667-165">Voer op Hallo account de configuratiepagina Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="42667-165">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="42667-166">![Externe autorisatie](./media/active-directory-saas-smarteru-tutorial/IC777327.png "externe autorisatie")</span><span class="sxs-lookup"><span data-stu-id="42667-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="42667-167">a.</span><span class="sxs-lookup"><span data-stu-id="42667-167">a.</span></span> <span data-ttu-id="42667-168">Selecteer **inschakelen van externe autorisatie**.</span><span class="sxs-lookup"><span data-stu-id="42667-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="42667-169">b.</span><span class="sxs-lookup"><span data-stu-id="42667-169">b.</span></span> <span data-ttu-id="42667-170">In Hallo **Master aanmelding besturingselement** sectie, selecteer Hallo **SmarterU** tabblad.</span><span class="sxs-lookup"><span data-stu-id="42667-170">In hello **Master Login Control** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="42667-171">c.</span><span class="sxs-lookup"><span data-stu-id="42667-171">c.</span></span> <span data-ttu-id="42667-172">In Hallo **standaard gebruikersaanmelding** sectie, selecteer Hallo **SmarterU** tabblad.</span><span class="sxs-lookup"><span data-stu-id="42667-172">In hello **User Default Login** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="42667-173">d.</span><span class="sxs-lookup"><span data-stu-id="42667-173">d.</span></span> <span data-ttu-id="42667-174">Selecteer **inschakelen, Okta**.</span><span class="sxs-lookup"><span data-stu-id="42667-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="42667-175">e.</span><span class="sxs-lookup"><span data-stu-id="42667-175">e.</span></span> <span data-ttu-id="42667-176">Hallo inhoud van de gedownloade metagegevensbestand Hallo kopieert en plakt u deze in Hallo **Okta Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="42667-176">Copy hello content of hello downloaded metadata file, and then paste it into hello **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="42667-177">f.</span><span class="sxs-lookup"><span data-stu-id="42667-177">f.</span></span> <span data-ttu-id="42667-178">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="42667-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="42667-179">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="42667-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="42667-180">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="42667-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="42667-181">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42667-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42667-182">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="42667-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="42667-183">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="42667-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="42667-185">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="42667-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="42667-186">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="42667-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42667-188">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="42667-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42667-190">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="42667-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42667-192">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="42667-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42667-194">a.</span><span class="sxs-lookup"><span data-stu-id="42667-194">a.</span></span> <span data-ttu-id="42667-195">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42667-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42667-196">b.</span><span class="sxs-lookup"><span data-stu-id="42667-196">b.</span></span> <span data-ttu-id="42667-197">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="42667-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42667-198">c.</span><span class="sxs-lookup"><span data-stu-id="42667-198">c.</span></span> <span data-ttu-id="42667-199">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="42667-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="42667-200">d.</span><span class="sxs-lookup"><span data-stu-id="42667-200">d.</span></span> <span data-ttu-id="42667-201">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="42667-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="42667-202">Een testgebruiker SmarterU maken</span><span class="sxs-lookup"><span data-stu-id="42667-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="42667-203">Azure AD tooenable gebruikers toolog in tooSmarterU, ze in SmarterU moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="42667-203">tooenable Azure AD users toolog in tooSmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="42667-204">SmarterU, inrichting wanneer een handmatige taak is.</span><span class="sxs-lookup"><span data-stu-id="42667-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="42667-205">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="42667-205">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="42667-206">Meld u bij tooyour **SmarterU** tenant.</span><span class="sxs-lookup"><span data-stu-id="42667-206">Log in tooyour **SmarterU** tenant.</span></span>

2. <span data-ttu-id="42667-207">Ga te**gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="42667-207">Go too**Users**.</span></span>

3. <span data-ttu-id="42667-208">Voer in de sectie van de gebruiker Hallo, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="42667-208">In hello user section, perform hello following steps:</span></span>
   
    <span data-ttu-id="42667-209">![Nieuwe gebruiker](./media/active-directory-saas-smarteru-tutorial/IC777329.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="42667-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="42667-210">a.</span><span class="sxs-lookup"><span data-stu-id="42667-210">a.</span></span> <span data-ttu-id="42667-211">Klik op **+ User**.</span><span class="sxs-lookup"><span data-stu-id="42667-211">Click **+User**.</span></span>
    
    <span data-ttu-id="42667-212">b.</span><span class="sxs-lookup"><span data-stu-id="42667-212">b.</span></span> <span data-ttu-id="42667-213">Type Hallo gerelateerde kenmerkwaarden van hello Azure AD-gebruikersaccount in de volgende tekstvakken Hallo: **primaire e**, **werknemer-ID**, **wachtwoord**,  **Bevestig het wachtwoord**, **voornaam**, **achternaam**.</span><span class="sxs-lookup"><span data-stu-id="42667-213">Type hello related attribute values of hello Azure AD user account into hello following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="42667-214">c.</span><span class="sxs-lookup"><span data-stu-id="42667-214">c.</span></span> <span data-ttu-id="42667-215">Klik op **Active**.</span><span class="sxs-lookup"><span data-stu-id="42667-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="42667-216">d.</span><span class="sxs-lookup"><span data-stu-id="42667-216">d.</span></span> <span data-ttu-id="42667-217">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="42667-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="42667-218">U kunt andere SmarterU gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door SmarterU tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="42667-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="42667-219">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="42667-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="42667-220">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSmarterU toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="42667-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmarterU.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="42667-222">**tooassign Britta Simon tooSmarterU, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="42667-222">**tooassign Britta Simon tooSmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="42667-223">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="42667-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="42667-225">Selecteer in de lijst met de toepassingen van Hallo **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="42667-225">In hello applications list, select **SmarterU**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="42667-227">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="42667-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="42667-229">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="42667-229">Click **Add** button.</span></span> <span data-ttu-id="42667-230">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="42667-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="42667-232">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="42667-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="42667-233">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="42667-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42667-234">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="42667-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42667-235">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="42667-235">Testing single sign-on</span></span>

<span data-ttu-id="42667-236">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="42667-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="42667-237">Als u op Hallo SmarterU tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SmarterU toepassing.</span><span class="sxs-lookup"><span data-stu-id="42667-237">When you click hello SmarterU tile in hello Access Panel, you should get automatically signed-on tooyour SmarterU application.</span></span>
<span data-ttu-id="42667-238">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="42667-238">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="42667-239">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="42667-239">Additional resources</span></span>

* [<span data-ttu-id="42667-240">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42667-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42667-241">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="42667-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

