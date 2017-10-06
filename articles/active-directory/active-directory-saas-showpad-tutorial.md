---
title: 'Zelfstudie: Azure Active Directory-integratie met Showpad | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Showpad.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2c8c306b4b94c368a93f92123d3abe9fe35167db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="adddc-103">Zelfstudie: Azure Active Directory-integratie met Showpad</span><span class="sxs-lookup"><span data-stu-id="adddc-103">Tutorial: Azure Active Directory integration with Showpad</span></span>

<span data-ttu-id="adddc-104">In deze zelfstudie leert u hoe toointegrate Showpad met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="adddc-104">In this tutorial, you learn how toointegrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="adddc-105">Showpad integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="adddc-105">Integrating Showpad with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="adddc-106">U kunt beheren in Azure AD die tooShowpad toegang heeft</span><span class="sxs-lookup"><span data-stu-id="adddc-106">You can control in Azure AD who has access tooShowpad</span></span>
- <span data-ttu-id="adddc-107">U kunt uw gebruikers tooautomatically get aangemelde tooShowpad (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="adddc-107">You can enable your users tooautomatically get signed-on tooShowpad (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="adddc-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="adddc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="adddc-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="adddc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="adddc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="adddc-110">Prerequisites</span></span>

<span data-ttu-id="adddc-111">Azure AD-integratie met Showpad tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="adddc-111">tooconfigure Azure AD integration with Showpad, you need hello following items:</span></span>

- <span data-ttu-id="adddc-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="adddc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="adddc-113">Een Showpad eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="adddc-113">A Showpad single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="adddc-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="adddc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="adddc-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="adddc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="adddc-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="adddc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="adddc-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="adddc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="adddc-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="adddc-118">Scenario description</span></span>
<span data-ttu-id="adddc-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="adddc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="adddc-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="adddc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="adddc-121">Het toevoegen van Showpad van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="adddc-121">Adding Showpad from hello gallery</span></span>
2. <span data-ttu-id="adddc-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="adddc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-hello-gallery"></a><span data-ttu-id="adddc-123">Het toevoegen van Showpad van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="adddc-123">Adding Showpad from hello gallery</span></span>

<span data-ttu-id="adddc-124">tooconfigure hello integratie van Showpad in Azure AD, moet u tooadd Showpad uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="adddc-124">tooconfigure hello integration of Showpad into Azure AD, you need tooadd Showpad from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="adddc-125">**tooadd Showpad via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="adddc-125">**tooadd Showpad from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="adddc-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="adddc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="adddc-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="adddc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="adddc-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="adddc-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="adddc-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="adddc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="adddc-133">Typ in het zoekvak Hallo **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="adddc-133">In hello search box, type **Showpad**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_search.png)

5. <span data-ttu-id="adddc-135">Selecteer in het deelvenster resultaten hello, **Showpad**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="adddc-135">In hello results panel, select **Showpad**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="adddc-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="adddc-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="adddc-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Showpad op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="adddc-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="adddc-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Showpad is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="adddc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Showpad is tooa user in Azure AD.</span></span> <span data-ttu-id="adddc-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Showpad toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="adddc-140">In other words, a link relationship between an Azure AD user and hello related user in Showpad needs toobe established.</span></span>

<span data-ttu-id="adddc-141">Wijs in Showpad, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="adddc-141">In Showpad, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="adddc-142">tooconfigure en eenmalige aanmelding Azure AD-test met Showpad, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="adddc-142">tooconfigure and test Azure AD single sign-on with Showpad, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="adddc-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="adddc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="adddc-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="adddc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="adddc-145">**[Maken van een testgebruiker Showpad](#creating-a-showpad-test-user)**  -toohave een equivalent van Britta Simon in Showpad die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="adddc-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - toohave a counterpart of Britta Simon in Showpad that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="adddc-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="adddc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="adddc-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="adddc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="adddc-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="adddc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="adddc-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Showpad configureren.</span><span class="sxs-lookup"><span data-stu-id="adddc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="adddc-150">**Azure AD tooconfigure eenmalige aanmelding met Showpad, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="adddc-150">**tooconfigure Azure AD single sign-on with Showpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="adddc-151">In de Azure-portal op Hallo Hallo **Showpad** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="adddc-151">In hello Azure portal, on hello **Showpad** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="adddc-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="adddc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_samlbase.png)

3. <span data-ttu-id="adddc-155">Op Hallo **Showpad domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="adddc-155">On hello **Showpad Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_url.png)

    <span data-ttu-id="adddc-157">a.</span><span class="sxs-lookup"><span data-stu-id="adddc-157">a.</span></span> <span data-ttu-id="adddc-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<comapany-name>.showpad.biz/login`</span><span class="sxs-lookup"><span data-stu-id="adddc-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<comapany-name>.showpad.biz/login`</span></span>

    <span data-ttu-id="adddc-159">b.</span><span class="sxs-lookup"><span data-stu-id="adddc-159">b.</span></span> <span data-ttu-id="adddc-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<company-name>.showpad.biz`</span><span class="sxs-lookup"><span data-stu-id="adddc-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.showpad.biz`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="adddc-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="adddc-161">These values are not real.</span></span> <span data-ttu-id="adddc-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="adddc-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="adddc-163">Neem contact op met [Showpad ondersteuningsteam](https://help.showpad.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="adddc-163">Contact [Showpad support team](https://help.showpad.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="adddc-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="adddc-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_certificate.png) 

5. <span data-ttu-id="adddc-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="adddc-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="adddc-168">Eenmalige aanmelding tooyour Showpad tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="adddc-168">Sign-on tooyour Showpad tenant as an administrator.</span></span>

7. <span data-ttu-id="adddc-169">Klik op Hallo in het menu bovenaan Hallo Hallo **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="adddc-169">In hello menu on hello top, click hello **Settings**.</span></span>
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_001.png) 

8. <span data-ttu-id="adddc-171">Navigeer te'**Single Sign-On**'en klik op'**inschakelen**. "</span><span class="sxs-lookup"><span data-stu-id="adddc-171">Navigate too"**Single Sign-On**" and click "**Enable**."</span></span>
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_002.png)

9. <span data-ttu-id="adddc-173">Op Hallo **een SAML 2.0-Service toevoegen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="adddc-173">On hello **Add a SAML 2.0 Service** dialog, perform hello following steps:</span></span>
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="adddc-175">a.</span><span class="sxs-lookup"><span data-stu-id="adddc-175">a.</span></span> <span data-ttu-id="adddc-176">In Hallo **naam** textbox Hallo-typenaam van de id-Provider (bijvoorbeeld: naam van uw bedrijf).</span><span class="sxs-lookup"><span data-stu-id="adddc-176">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="adddc-177">b.</span><span class="sxs-lookup"><span data-stu-id="adddc-177">b.</span></span> <span data-ttu-id="adddc-178">Als **metagegevensbron**, selecteer **XML**.</span><span class="sxs-lookup"><span data-stu-id="adddc-178">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="adddc-179">c.</span><span class="sxs-lookup"><span data-stu-id="adddc-179">c.</span></span> <span data-ttu-id="adddc-180">Hallo-inhoud van metagegevens XML-bestand, die u van hello Azure-portal hebt gedownload, kopieert en plakt u deze in Hallo **Metadata XML** textbox.</span><span class="sxs-lookup"><span data-stu-id="adddc-180">Copy hello content of metadata XML file, which you have downloaded from hello Azure portal, and then paste it into hello **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="adddc-181">d.</span><span class="sxs-lookup"><span data-stu-id="adddc-181">d.</span></span> <span data-ttu-id="adddc-182">Selecteer **automatisch inrichten van nieuwe gebruikers gebruikersaccounts wanneer deze zich aanmeldt**.</span><span class="sxs-lookup"><span data-stu-id="adddc-182">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="adddc-183">e.</span><span class="sxs-lookup"><span data-stu-id="adddc-183">e.</span></span> <span data-ttu-id="adddc-184">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="adddc-184">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="adddc-185">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="adddc-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="adddc-186">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="adddc-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="adddc-187">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="adddc-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="adddc-188">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="adddc-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="adddc-189">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="adddc-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="adddc-191">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="adddc-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="adddc-192">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="adddc-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-showpad-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="adddc-194">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="adddc-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-showpad-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="adddc-196">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="adddc-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-showpad-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="adddc-198">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="adddc-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-showpad-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="adddc-200">a.</span><span class="sxs-lookup"><span data-stu-id="adddc-200">a.</span></span> <span data-ttu-id="adddc-201">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="adddc-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="adddc-202">b.</span><span class="sxs-lookup"><span data-stu-id="adddc-202">b.</span></span> <span data-ttu-id="adddc-203">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="adddc-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="adddc-204">c.</span><span class="sxs-lookup"><span data-stu-id="adddc-204">c.</span></span> <span data-ttu-id="adddc-205">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="adddc-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="adddc-206">d.</span><span class="sxs-lookup"><span data-stu-id="adddc-206">d.</span></span> <span data-ttu-id="adddc-207">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="adddc-207">Click **Create**.</span></span>
 
### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="adddc-208">Een testgebruiker Showpad maken</span><span class="sxs-lookup"><span data-stu-id="adddc-208">Creating a Showpad test user</span></span>

<span data-ttu-id="adddc-209">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Showpad van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="adddc-209">hello objective of this section is toocreate a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="adddc-210">Showpad ondersteuning biedt voor just-in-time-inrichting.</span><span class="sxs-lookup"><span data-stu-id="adddc-210">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="adddc-211">U hebt ingeschakeld in inrichting  **[eenmalige aanmelding configureren Azure AD](#configuring-azure-ad-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="adddc-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span></span> 

<span data-ttu-id="adddc-212">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="adddc-212">There is no action item for you in this section.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="adddc-213">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="adddc-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="adddc-214">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooShowpad toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="adddc-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooShowpad.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="adddc-216">**tooassign Britta Simon tooShowpad, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="adddc-216">**tooassign Britta Simon tooShowpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="adddc-217">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="adddc-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="adddc-219">Selecteer in de lijst met de toepassingen van Hallo **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="adddc-219">In hello applications list, select **Showpad**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_app.png) 

3. <span data-ttu-id="adddc-221">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="adddc-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="adddc-223">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="adddc-223">Click **Add** button.</span></span> <span data-ttu-id="adddc-224">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="adddc-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="adddc-226">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="adddc-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="adddc-227">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="adddc-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="adddc-228">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="adddc-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="adddc-229">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="adddc-229">Testing single sign-on</span></span>

<span data-ttu-id="adddc-230">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="adddc-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="adddc-231">Als u op Hallo Showpad tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooShowpad toepassing.</span><span class="sxs-lookup"><span data-stu-id="adddc-231">When you click hello Showpad tile in hello Access Panel, you should get automatically signed-on tooShowpad application.</span></span>
<span data-ttu-id="adddc-232">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="adddc-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="adddc-233">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="adddc-233">Additional resources</span></span>

* [<span data-ttu-id="adddc-234">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="adddc-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="adddc-235">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="adddc-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_203.png

