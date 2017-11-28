---
title: 'Zelfstudie: Azure Active Directory-integratie met UserVoice | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en UserVoice.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: 9eade8435ae6c6a3821bbbec9ab7c27ed7ad91ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="bed30-103">Zelfstudie: Azure Active Directory-integratie met UserVoice</span><span class="sxs-lookup"><span data-stu-id="bed30-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="bed30-104">In deze zelfstudie leert u hoe toointegrate UserVoice met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bed30-104">In this tutorial, you learn how toointegrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bed30-105">UserVoice integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="bed30-105">Integrating UserVoice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bed30-106">U kunt beheren in Azure AD die tooUserVoice toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="bed30-106">You can control in Azure AD who has access tooUserVoice.</span></span>
- <span data-ttu-id="bed30-107">U kunt uw gebruikers tooautomatically get aangemelde tooUserVoice (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bed30-107">You can enable your users tooautomatically get signed-on tooUserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="bed30-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="bed30-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="bed30-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bed30-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bed30-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bed30-110">Prerequisites</span></span>

<span data-ttu-id="bed30-111">Azure AD-integratie met UserVoice tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="bed30-111">tooconfigure Azure AD integration with UserVoice, you need hello following items:</span></span>

- <span data-ttu-id="bed30-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="bed30-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bed30-113">Een UserVoice eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="bed30-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bed30-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="bed30-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bed30-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="bed30-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bed30-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="bed30-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bed30-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bed30-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bed30-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="bed30-118">Scenario description</span></span>
<span data-ttu-id="bed30-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="bed30-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bed30-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="bed30-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bed30-121">Het toevoegen van UserVoice van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="bed30-121">Adding UserVoice from hello gallery</span></span>
2. <span data-ttu-id="bed30-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bed30-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-hello-gallery"></a><span data-ttu-id="bed30-123">Het toevoegen van UserVoice van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="bed30-123">Adding UserVoice from hello gallery</span></span>
<span data-ttu-id="bed30-124">tooconfigure hello integratie van UserVoice in Azure AD, moet u tooadd UserVoice uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="bed30-124">tooconfigure hello integration of UserVoice into Azure AD, you need tooadd UserVoice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bed30-125">**tooadd UserVoice via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bed30-125">**tooadd UserVoice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bed30-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bed30-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="bed30-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bed30-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bed30-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bed30-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="bed30-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bed30-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="bed30-133">Typ in het zoekvak Hallo **UserVoice**, selecteer **UserVoice** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="bed30-133">In hello search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button tooadd hello application.</span></span>

    ![UserVoice in de lijst met resultaten Hallo](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bed30-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="bed30-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bed30-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met UserVoice op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="bed30-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bed30-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in UserVoice is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bed30-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserVoice is tooa user in Azure AD.</span></span> <span data-ttu-id="bed30-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in UserVoice toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="bed30-138">In other words, a link relationship between an Azure AD user and hello related user in UserVoice needs toobe established.</span></span>

<span data-ttu-id="bed30-139">Wijs in UserVoice, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="bed30-139">In UserVoice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bed30-140">tooconfigure en eenmalige aanmelding Azure AD-test met UserVoice, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bed30-140">tooconfigure and test Azure AD single sign-on with UserVoice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bed30-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="bed30-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bed30-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bed30-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bed30-143">**[Maak een testgebruiker UserVoice](#create-a-uservoice-test-user)**  -toohave een equivalent van Britta Simon in UserVoice die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="bed30-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - toohave a counterpart of Britta Simon in UserVoice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bed30-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="bed30-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bed30-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="bed30-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bed30-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="bed30-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bed30-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw UserVoice-toepassing.</span><span class="sxs-lookup"><span data-stu-id="bed30-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="bed30-148">**Azure AD tooconfigure eenmalige aanmelding met UserVoice, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bed30-148">**tooconfigure Azure AD single sign-on with UserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="bed30-149">In de Azure-portal op Hallo Hallo **UserVoice** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="bed30-149">In hello Azure portal, on hello **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="bed30-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="bed30-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="bed30-153">Op Hallo **UserVoice domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bed30-153">On hello **UserVoice Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's voor UserVoice-domein en één aanmelding informatie](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="bed30-155">a.</span><span class="sxs-lookup"><span data-stu-id="bed30-155">a.</span></span> <span data-ttu-id="bed30-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="bed30-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="bed30-157">b.</span><span class="sxs-lookup"><span data-stu-id="bed30-157">b.</span></span> <span data-ttu-id="bed30-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="bed30-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bed30-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="bed30-159">These values are not real.</span></span> <span data-ttu-id="bed30-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="bed30-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bed30-161">Neem contact op met [UserVoice Client ondersteuningsteam](https://www.uservoice.com/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="bed30-161">Contact [UserVoice Client support team](https://www.uservoice.com/) tooget these values.</span></span>

4. <span data-ttu-id="bed30-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="bed30-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="bed30-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="bed30-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bed30-166">Op Hallo **UserVoice configuratie** sectie, klikt u op **configureren UserVoice** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="bed30-166">On hello **UserVoice Configuration** section, click **Configure UserVoice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bed30-167">Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="bed30-167">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![UserVoice-configuratie](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="bed30-169">In een ander browservenster, meld u aan tooyour UserVoice bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="bed30-169">In a different web browser window, log in tooyour UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="bed30-170">Klik in de werkbalk bovenaan Hallo Hallo op **instellingen**, en selecteer vervolgens **webportal** in Hallo menu.</span><span class="sxs-lookup"><span data-stu-id="bed30-170">In hello toolbar on hello top, click **Settings**, and then select **Web portal** from hello menu.</span></span>
   
    <span data-ttu-id="bed30-171">![Sectie met App-zijde](./media/active-directory-saas-uservoice-tutorial/ic777519.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="bed30-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="bed30-172">Op Hallo **webportal** tabblad in Hallo **gebruikersverificatie** sectie, klikt u op **bewerken** tooopen hello **gebruikersverificatie bewerken** dialoogvenster pagina.</span><span class="sxs-lookup"><span data-stu-id="bed30-172">On hello **Web portal** tab, in hello **User authentication** section, click **Edit** tooopen hello **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="bed30-173">![Web-portal tabblad](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web-portal")</span><span class="sxs-lookup"><span data-stu-id="bed30-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="bed30-174">Op Hallo **gebruikersverificatie bewerken** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bed30-174">On hello **Edit User Authentication** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="bed30-175">![Verificatie van gebruikers bewerken](./media/active-directory-saas-uservoice-tutorial/ic777521.png "gebruikersverificatie bewerken")</span><span class="sxs-lookup"><span data-stu-id="bed30-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="bed30-176">a.</span><span class="sxs-lookup"><span data-stu-id="bed30-176">a.</span></span> <span data-ttu-id="bed30-177">Klik op **eenmalige aanmelding (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="bed30-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="bed30-178">b.</span><span class="sxs-lookup"><span data-stu-id="bed30-178">b.</span></span> <span data-ttu-id="bed30-179">Plakken Hallo **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **extern aanmelden SSO** textbox.</span><span class="sxs-lookup"><span data-stu-id="bed30-179">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="bed30-180">c.</span><span class="sxs-lookup"><span data-stu-id="bed30-180">c.</span></span> <span data-ttu-id="bed30-181">Plakken Hallo **Sign-Out URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **SSO externe Sign-Out textbox**.</span><span class="sxs-lookup"><span data-stu-id="bed30-181">Paste hello **Sign-Out URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="bed30-182">d.</span><span class="sxs-lookup"><span data-stu-id="bed30-182">d.</span></span> <span data-ttu-id="bed30-183">Plakken Hallo **vingerafdruk** waarde, die u hebt gekopieerd vanuit Azure-portal in de **huidige vingerafdruk van certificaat SHA1** textbox.</span><span class="sxs-lookup"><span data-stu-id="bed30-183">Paste hello **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="bed30-184">e.</span><span class="sxs-lookup"><span data-stu-id="bed30-184">e.</span></span> <span data-ttu-id="bed30-185">Klik op **verificatie-instellingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bed30-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="bed30-186">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="bed30-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bed30-187">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="bed30-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bed30-188">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bed30-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bed30-189">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="bed30-189">Create an Azure AD test user</span></span>

<span data-ttu-id="bed30-190">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="bed30-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="bed30-192">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bed30-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bed30-193">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="bed30-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="bed30-195">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bed30-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="bed30-197">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bed30-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="bed30-199">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bed30-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="bed30-201">a.</span><span class="sxs-lookup"><span data-stu-id="bed30-201">a.</span></span> <span data-ttu-id="bed30-202">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bed30-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bed30-203">b.</span><span class="sxs-lookup"><span data-stu-id="bed30-203">b.</span></span> <span data-ttu-id="bed30-204">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="bed30-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="bed30-205">c.</span><span class="sxs-lookup"><span data-stu-id="bed30-205">c.</span></span> <span data-ttu-id="bed30-206">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="bed30-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="bed30-207">d.</span><span class="sxs-lookup"><span data-stu-id="bed30-207">d.</span></span> <span data-ttu-id="bed30-208">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="bed30-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="bed30-209">Maak een testgebruiker UserVoice</span><span class="sxs-lookup"><span data-stu-id="bed30-209">Create a UserVoice test user</span></span>

<span data-ttu-id="bed30-210">Azure AD tooenable gebruikers toolog in tooUserVoice, moeten ze worden ingericht in UserVoice.</span><span class="sxs-lookup"><span data-stu-id="bed30-210">tooenable Azure AD users toolog in tooUserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="bed30-211">In geval van UserVoice Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="bed30-211">In hello case of UserVoice, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="bed30-212">een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bed30-212">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="bed30-213">Meld u bij tooyour **UserVoice** tenant.</span><span class="sxs-lookup"><span data-stu-id="bed30-213">Log in tooyour **UserVoice** tenant.</span></span>

2. <span data-ttu-id="bed30-214">Ga te**instellingen**.</span><span class="sxs-lookup"><span data-stu-id="bed30-214">Go too**Settings**.</span></span>
   
    <span data-ttu-id="bed30-215">![Instellingen](./media/active-directory-saas-uservoice-tutorial/ic777811.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="bed30-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="bed30-216">Klik op **algemene**.</span><span class="sxs-lookup"><span data-stu-id="bed30-216">Click **General**.</span></span>

4. <span data-ttu-id="bed30-217">Klik op **Agents en machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="bed30-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="bed30-218">![Agents en machtigingen](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents en machtigingen")</span><span class="sxs-lookup"><span data-stu-id="bed30-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="bed30-219">Klik op **toevoegen admins**.</span><span class="sxs-lookup"><span data-stu-id="bed30-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="bed30-220">![Toevoegen van beheerders](./media/active-directory-saas-uservoice-tutorial/ic777813.png "admins toevoegen")</span><span class="sxs-lookup"><span data-stu-id="bed30-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="bed30-221">Op Hallo **uitnodigen admins** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="bed30-221">On hello **Invite admins** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="bed30-222">![Beheerders uitnodigen](./media/active-directory-saas-uservoice-tutorial/ic777814.png "admins uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="bed30-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="bed30-223">a.</span><span class="sxs-lookup"><span data-stu-id="bed30-223">a.</span></span> <span data-ttu-id="bed30-224">Typ in Hallo e-mailberichten textbox Hallo e-mailadres van Hallo account u wilt tooprovision en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bed30-224">In hello Emails textbox, type hello email address of hello account you want tooprovision, and then click **Add**.</span></span>
   
    <span data-ttu-id="bed30-225">b.</span><span class="sxs-lookup"><span data-stu-id="bed30-225">b.</span></span> <span data-ttu-id="bed30-226">Klik op **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="bed30-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="bed30-227">U kunt andere UserVoice gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door UserVoice tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="bed30-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice tooprovision AAD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="bed30-228">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bed30-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="bed30-229">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooUserVoice toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="bed30-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserVoice.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="bed30-231">**tooassign Britta Simon tooUserVoice, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bed30-231">**tooassign Britta Simon tooUserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="bed30-232">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bed30-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="bed30-234">Selecteer in de lijst met de toepassingen van Hallo **UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="bed30-234">In hello applications list, select **UserVoice**.</span></span>

    ![Hallo UserVoice-koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="bed30-236">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="bed30-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="bed30-238">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="bed30-238">Click **Add** button.</span></span> <span data-ttu-id="bed30-239">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bed30-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="bed30-241">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="bed30-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bed30-242">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bed30-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bed30-243">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bed30-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bed30-244">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bed30-244">Test single sign-on</span></span>

<span data-ttu-id="bed30-245">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="bed30-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bed30-246">Als u op Hallo UserVoice-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour UserVoice toepassing.</span><span class="sxs-lookup"><span data-stu-id="bed30-246">When you click hello UserVoice tile in hello Access Panel, you should get automatically signed-on tooyour UserVoice application.</span></span>
<span data-ttu-id="bed30-247">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bed30-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bed30-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="bed30-248">Additional resources</span></span>

* [<span data-ttu-id="bed30-249">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bed30-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bed30-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bed30-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

