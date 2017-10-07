---
title: 'Zelfstudie: Azure Active Directory-integratie met QuickHelp | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en QuickHelp.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: bbde5eb9bdad89680923ccd36c321b6923f91789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="cc3a0-103">Zelfstudie: Azure Active Directory-integratie met QuickHelp</span><span class="sxs-lookup"><span data-stu-id="cc3a0-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="cc3a0-104">In deze zelfstudie leert u hoe toointegrate QuickHelp met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc3a0-104">In this tutorial, you learn how toointegrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc3a0-105">QuickHelp integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="cc3a0-105">Integrating QuickHelp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cc3a0-106">U kunt beheren in Azure AD die tooQuickHelp toegang heeft</span><span class="sxs-lookup"><span data-stu-id="cc3a0-106">You can control in Azure AD who has access tooQuickHelp</span></span>
- <span data-ttu-id="cc3a0-107">U kunt uw gebruikers tooautomatically get aangemelde tooQuickHelp (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="cc3a0-107">You can enable your users tooautomatically get signed-on tooQuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc3a0-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="cc3a0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cc3a0-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc3a0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc3a0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cc3a0-110">Prerequisites</span></span>

<span data-ttu-id="cc3a0-111">Azure AD-integratie met QuickHelp tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="cc3a0-111">tooconfigure Azure AD integration with QuickHelp, you need hello following items:</span></span>

- <span data-ttu-id="cc3a0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="cc3a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc3a0-113">Een QuickHelp eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="cc3a0-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc3a0-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc3a0-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="cc3a0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc3a0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc3a0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc3a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc3a0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="cc3a0-118">Scenario description</span></span>
<span data-ttu-id="cc3a0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc3a0-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="cc3a0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc3a0-121">Het toevoegen van QuickHelp van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="cc3a0-121">Adding QuickHelp from hello gallery</span></span>
2. <span data-ttu-id="cc3a0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cc3a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-hello-gallery"></a><span data-ttu-id="cc3a0-123">Het toevoegen van QuickHelp van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="cc3a0-123">Adding QuickHelp from hello gallery</span></span>
<span data-ttu-id="cc3a0-124">tooconfigure hello integratie van QuickHelp in Azure AD, moet u tooadd QuickHelp uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-124">tooconfigure hello integration of QuickHelp into Azure AD, you need tooadd QuickHelp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cc3a0-125">**tooadd QuickHelp via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cc3a0-125">**tooadd QuickHelp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc3a0-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cc3a0-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cc3a0-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="cc3a0-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="cc3a0-133">Typ in het zoekvak Hallo **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-133">In hello search box, type **QuickHelp**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="cc3a0-135">Selecteer in het deelvenster resultaten hello, **QuickHelp**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-135">In hello results panel, select **QuickHelp**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc3a0-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cc3a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc3a0-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met QuickHelp op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cc3a0-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in QuickHelp is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp is tooa user in Azure AD.</span></span> <span data-ttu-id="cc3a0-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in QuickHelp toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-140">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="cc3a0-141">Wijs in QuickHelp, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-141">In QuickHelp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cc3a0-142">tooconfigure en eenmalige aanmelding Azure AD-test met QuickHelp, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc3a0-142">tooconfigure and test Azure AD single sign-on with QuickHelp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cc3a0-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cc3a0-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc3a0-145">**[Maken van een testgebruiker QuickHelp](#creating-a-quickhelp-test-user)**  -toohave een equivalent van Britta Simon in QuickHelp die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - toohave a counterpart of Britta Simon in QuickHelp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc3a0-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc3a0-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc3a0-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="cc3a0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc3a0-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing QuickHelp configureren.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="cc3a0-150">**Azure AD tooconfigure eenmalige aanmelding met QuickHelp, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cc3a0-150">**tooconfigure Azure AD single sign-on with QuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc3a0-151">In de Azure-portal op Hallo Hallo **QuickHelp** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-151">In hello Azure portal, on hello **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="cc3a0-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="cc3a0-155">Op Hallo **QuickHelp domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc3a0-155">On hello **QuickHelp Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="cc3a0-157">a.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-157">a.</span></span> <span data-ttu-id="cc3a0-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://quickhelp.com/<instancename>/#/Login`</span><span class="sxs-lookup"><span data-stu-id="cc3a0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="cc3a0-159">b.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-159">b.</span></span> <span data-ttu-id="cc3a0-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="cc3a0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cc3a0-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-161">These values are not real.</span></span> <span data-ttu-id="cc3a0-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cc3a0-163">Neem contact op met [QuickHelp Client ondersteuningsteam](https://support.quickhelp.com/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="cc3a0-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="cc3a0-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="cc3a0-168">Eenmalige aanmelding tooyour QuickHelp bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-168">Sign-on tooyour QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="cc3a0-169">Klik in het menu bovenaan Hallo Hallo **Admin**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Eenmalige aanmelding configureren][21]

8. <span data-ttu-id="cc3a0-171">In Hallo **QuickHelp Admin** menu, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-171">In hello **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Eenmalige aanmelding configureren][22]

9. <span data-ttu-id="cc3a0-173">Klik op **verificatie-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="cc3a0-174">Op Hallo **verificatie-instellingen** pagina, voert u Hallo stappen te volgen</span><span class="sxs-lookup"><span data-stu-id="cc3a0-174">On hello **Authentication Settings** page, perform hello following steps</span></span>
   
    ![Eenmalige aanmelding configureren][23]
   
    <span data-ttu-id="cc3a0-176">a.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-176">a.</span></span> <span data-ttu-id="cc3a0-177">Als **SSO Type**, selecteer **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="cc3a0-178">b.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-178">b.</span></span> <span data-ttu-id="cc3a0-179">tooupload uw gedownloade Azure metagegevensbestand, klikt u op **Bladeren**, navigeer toohello bestand, beëindigen, klikt u vervolgens op **metagegevens uploaden**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-179">tooupload your downloaded Azure metadata file, click **Browse**, navigate toohello file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="cc3a0-180">c.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-180">c.</span></span> <span data-ttu-id="cc3a0-181">In Hallo **e** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-181">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="cc3a0-182">d.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-182">d.</span></span> <span data-ttu-id="cc3a0-183">In Hallo **voornaam** textbox `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-183">In hello **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="cc3a0-184">e.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-184">e.</span></span> <span data-ttu-id="cc3a0-185">In Hallo **achternaam** textbox `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-185">In hello **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="cc3a0-186">f.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-186">f.</span></span> <span data-ttu-id="cc3a0-187">In Hallo **actiebalk**, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-187">In hello **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="cc3a0-188">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cc3a0-189">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cc3a0-190">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc3a0-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc3a0-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="cc3a0-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc3a0-192">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="cc3a0-194">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cc3a0-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc3a0-195">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cc3a0-197">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cc3a0-199">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cc3a0-201">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc3a0-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc3a0-203">a.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-203">a.</span></span> <span data-ttu-id="cc3a0-204">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc3a0-205">b.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-205">b.</span></span> <span data-ttu-id="cc3a0-206">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cc3a0-207">c.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-207">c.</span></span> <span data-ttu-id="cc3a0-208">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cc3a0-209">d.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-209">d.</span></span> <span data-ttu-id="cc3a0-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="cc3a0-211">Een testgebruiker QuickHelp maken</span><span class="sxs-lookup"><span data-stu-id="cc3a0-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="cc3a0-212">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in QuickHelp van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-212">hello objective of this section is toocreate a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="cc3a0-213">Voor één aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in QuickHelp tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-213">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp tooa user in Azure AD is.</span></span> <span data-ttu-id="cc3a0-214">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in QuickHelp toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-214">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="cc3a0-215">QuickHelp ondersteuning biedt voor just-in-time-inrichting.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="cc3a0-216">Dit betekent dat, indien nodig, een gebruikersaccount wordt automatisch gemaakt in QuickHelp en Hallo-account is gekoppeld toohello Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-216">This means, if necessary, a user account is automatically created in QuickHelp and hello account is linked toohello Azure AD account.</span></span>

<span data-ttu-id="cc3a0-217">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-217">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cc3a0-218">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc3a0-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cc3a0-219">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooQuickHelp toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQuickHelp.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="cc3a0-221">**tooassign Britta Simon tooQuickHelp, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cc3a0-221">**tooassign Britta Simon tooQuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc3a0-222">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="cc3a0-224">Selecteer in de lijst met de toepassingen van Hallo **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-224">In hello applications list, select **QuickHelp**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="cc3a0-226">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="cc3a0-228">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-228">Click **Add** button.</span></span> <span data-ttu-id="cc3a0-229">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="cc3a0-231">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cc3a0-232">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc3a0-233">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc3a0-234">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cc3a0-234">Testing single sign-on</span></span>

<span data-ttu-id="cc3a0-235">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="cc3a0-236">Als u op Hallo QuickHelp tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour QuickHelp toepassing.</span><span class="sxs-lookup"><span data-stu-id="cc3a0-236">When you click hello QuickHelp tile in hello Access Panel, you should get automatically signed-on tooyour QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="cc3a0-237">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="cc3a0-237">Additional resources</span></span>

* [<span data-ttu-id="cc3a0-238">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc3a0-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc3a0-239">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cc3a0-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png
