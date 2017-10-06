---
title: 'Zelfstudie: Azure Active Directory-integratie met Citrix ShareFile | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Citrix ShareFile.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="edbb0-103">Zelfstudie: Azure Active Directory-integratie met Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="edbb0-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="edbb0-104">In deze zelfstudie leert u hoe toointegrate Citrix ShareFile met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="edbb0-104">In this tutorial, you learn how toointegrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="edbb0-105">Citrix ShareFile integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="edbb0-105">Integrating Citrix ShareFile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="edbb0-106">U kunt beheren in Azure AD die toegang tooCitrix ShareFile heeft.</span><span class="sxs-lookup"><span data-stu-id="edbb0-106">You can control in Azure AD who has access tooCitrix ShareFile.</span></span>
- <span data-ttu-id="edbb0-107">U kunt uw gebruikers tooautomatically get aangemelde tooCitrix ShareFile (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="edbb0-107">You can enable your users tooautomatically get signed-on tooCitrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="edbb0-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="edbb0-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="edbb0-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="edbb0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edbb0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="edbb0-110">Prerequisites</span></span>

<span data-ttu-id="edbb0-111">Azure AD-integratie met Citrix ShareFile tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="edbb0-111">tooconfigure Azure AD integration with Citrix ShareFile, you need hello following items:</span></span>

- <span data-ttu-id="edbb0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="edbb0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="edbb0-113">Een Citrix ShareFile eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="edbb0-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="edbb0-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="edbb0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="edbb0-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="edbb0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="edbb0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="edbb0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="edbb0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="edbb0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="edbb0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="edbb0-118">Scenario description</span></span>
<span data-ttu-id="edbb0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="edbb0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="edbb0-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="edbb0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="edbb0-121">Citrix ShareFile van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="edbb0-121">Add Citrix ShareFile from hello gallery</span></span>
2. <span data-ttu-id="edbb0-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="edbb0-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-hello-gallery"></a><span data-ttu-id="edbb0-123">Citrix ShareFile van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="edbb0-123">Add Citrix ShareFile from hello gallery</span></span>
<span data-ttu-id="edbb0-124">tooconfigure hello integratie van Citrix ShareFile in Azure AD, moet u Citrix ShareFile tooadd uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="edbb0-124">tooconfigure hello integration of Citrix ShareFile into Azure AD, you need tooadd Citrix ShareFile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="edbb0-125">**tooadd Citrix ShareFile via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="edbb0-125">**tooadd Citrix ShareFile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="edbb0-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="edbb0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="edbb0-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="edbb0-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="edbb0-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="edbb0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="edbb0-133">Typ in het zoekvak Hallo **Citrix ShareFile**, selecteer **Citrix ShareFile** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="edbb0-133">In hello search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lijst met zoekresultaten Citrix ShareFile in Hallo](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="edbb0-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="edbb0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="edbb0-136">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Citrix ShareFile op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="edbb0-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="edbb0-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Citrix ShareFile is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="edbb0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix ShareFile is tooa user in Azure AD.</span></span> <span data-ttu-id="edbb0-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Citrix ShareFile toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="edbb0-138">In other words, a link relationship between an Azure AD user and hello related user in Citrix ShareFile needs toobe established.</span></span>

<span data-ttu-id="edbb0-139">In Citrix ShareFile, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="edbb0-139">In Citrix ShareFile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="edbb0-140">tooconfigure en eenmalige aanmelding Azure AD-test met Citrix ShareFile, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="edbb0-140">tooconfigure and test Azure AD single sign-on with Citrix ShareFile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="edbb0-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="edbb0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="edbb0-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="edbb0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="edbb0-143">**[Maak een testgebruiker Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  -toohave een equivalent van Britta Simon in Citrix ShareFile die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="edbb0-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - toohave a counterpart of Britta Simon in Citrix ShareFile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="edbb0-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="edbb0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="edbb0-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="edbb0-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="edbb0-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="edbb0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="edbb0-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Citrix ShareFile configureren.</span><span class="sxs-lookup"><span data-stu-id="edbb0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="edbb0-148">**Azure AD tooconfigure eenmalige aanmelding met Citrix ShareFile, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="edbb0-148">**tooconfigure Azure AD single sign-on with Citrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="edbb0-149">In de Azure-portal op Hallo Hallo **Citrix ShareFile** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-149">In hello Azure portal, on hello **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="edbb0-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="edbb0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="edbb0-153">Op Hallo **Citrix ShareFile domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="edbb0-153">On hello **Citrix ShareFile Domain and URLs** section, perform hello following steps:</span></span>

    ![Citrix ShareFile domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="edbb0-155">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="edbb0-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="edbb0-156">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="edbb0-156">This value is not real.</span></span> <span data-ttu-id="edbb0-157">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="edbb0-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="edbb0-158">Neem contact op met [Citrix ShareFile Client ondersteuningsteam](https://www.citrix.co.in/products/sharefile/support.html) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="edbb0-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) tooget this value.</span></span> 

4. <span data-ttu-id="edbb0-159">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="edbb0-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="edbb0-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="edbb0-161">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="edbb0-163">Op Hallo **Citrix-configuratie voor ShareFile** sectie, klikt u op **configureren Citrix ShareFile** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="edbb0-163">On hello **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="edbb0-164">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="edbb0-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Citrix ShareFile-configuratie](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="edbb0-166">In een ander browservenster, meld u aan bij uw **Citrix ShareFile** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="edbb0-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="edbb0-167">Klik in de werkbalk bovenaan Hallo Hallo op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-167">In hello toolbar on hello top, click **Admin**.</span></span>

9. <span data-ttu-id="edbb0-168">Selecteer in de Hallo navigatiedeelvenster links **configureren Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-168">In hello left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="edbb0-169">![Beheer account](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account beheer")</span><span class="sxs-lookup"><span data-stu-id="edbb0-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="edbb0-170">Op Hallo **Single Sign-On / SAML 2.0-configuratie** dialoogvenster pagina onder **basisinstellingen**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="edbb0-170">On hello **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform hello following steps:</span></span>
   
    <span data-ttu-id="edbb0-171">![Eenmalige aanmelding](./media/active-directory-saas-sharefile-tutorial/ic773628.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="edbb0-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="edbb0-172">a.</span><span class="sxs-lookup"><span data-stu-id="edbb0-172">a.</span></span> <span data-ttu-id="edbb0-173">Klik op **SAML inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="edbb0-174">b.</span><span class="sxs-lookup"><span data-stu-id="edbb0-174">b.</span></span> <span data-ttu-id="edbb0-175">In **uw IDP verlener / entiteit-ID** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="edbb0-175">In **Your IDP Issuer/ Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="edbb0-176">c.</span><span class="sxs-lookup"><span data-stu-id="edbb0-176">c.</span></span> <span data-ttu-id="edbb0-177">Klik op **wijziging** volgende toohello **X.509-certificaat** veld en klikt u vervolgens uploaden Hallo certificaat u hebt gedownload van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="edbb0-177">Click **Change** next toohello **X.509 Certificate** field and then upload hello certificate you downloaded from hello Azure portal.</span></span>
    
    <span data-ttu-id="edbb0-178">d.</span><span class="sxs-lookup"><span data-stu-id="edbb0-178">d.</span></span> <span data-ttu-id="edbb0-179">In **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="edbb0-179">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="edbb0-180">e.</span><span class="sxs-lookup"><span data-stu-id="edbb0-180">e.</span></span> <span data-ttu-id="edbb0-181">In **afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="edbb0-181">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="edbb0-182">Klik op **opslaan** op Hallo Citrix ShareFile-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="edbb0-182">Click **Save** on hello Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="edbb0-183">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="edbb0-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="edbb0-184">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="edbb0-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="edbb0-185">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="edbb0-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="edbb0-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="edbb0-186">Create an Azure AD test user</span></span>

<span data-ttu-id="edbb0-187">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="edbb0-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="edbb0-189">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="edbb0-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="edbb0-190">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="edbb0-190">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="edbb0-192">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-192">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="edbb0-194">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="edbb0-194">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="edbb0-196">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="edbb0-196">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="edbb0-198">a.</span><span class="sxs-lookup"><span data-stu-id="edbb0-198">a.</span></span> <span data-ttu-id="edbb0-199">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-199">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="edbb0-200">b.</span><span class="sxs-lookup"><span data-stu-id="edbb0-200">b.</span></span> <span data-ttu-id="edbb0-201">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="edbb0-201">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="edbb0-202">c.</span><span class="sxs-lookup"><span data-stu-id="edbb0-202">c.</span></span> <span data-ttu-id="edbb0-203">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="edbb0-203">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="edbb0-204">d.</span><span class="sxs-lookup"><span data-stu-id="edbb0-204">d.</span></span> <span data-ttu-id="edbb0-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="edbb0-206">Een testgebruiker Citrix ShareFile maken</span><span class="sxs-lookup"><span data-stu-id="edbb0-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="edbb0-207">In de volgorde tooenable Azure AD gebruikers toolog in Citrix ShareFile, moeten ze worden ingericht in Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="edbb0-207">In order tooenable Azure AD users toolog into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="edbb0-208">In geval van Citrix ShareFile Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="edbb0-208">In hello case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="edbb0-209">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="edbb0-209">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="edbb0-210">Meld u bij tooyour **Citrix ShareFile** tenant.</span><span class="sxs-lookup"><span data-stu-id="edbb0-210">Log in tooyour **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="edbb0-211">Klik op **gebruikers beheren \> beheren van gebruikers Home \> + werknemer**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="edbb0-212">![Maken van de werknemer](./media/active-directory-saas-sharefile-tutorial/IC781050.png "werknemer maken")</span><span class="sxs-lookup"><span data-stu-id="edbb0-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="edbb0-213">Op Hallo **basisinformatie** sectie, voert u onderstaande stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="edbb0-213">On hello **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="edbb0-214">![Algemene informatie](./media/active-directory-saas-sharefile-tutorial/IC799951.png "basisinformatie")</span><span class="sxs-lookup"><span data-stu-id="edbb0-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="edbb0-215">a.</span><span class="sxs-lookup"><span data-stu-id="edbb0-215">a.</span></span> <span data-ttu-id="edbb0-216">In Hallo **e-mailadres** textbox type Hallo e-mailadres van Britta Simon als  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="edbb0-216">In hello **Email Address** textbox, type hello email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="edbb0-217">b.</span><span class="sxs-lookup"><span data-stu-id="edbb0-217">b.</span></span> <span data-ttu-id="edbb0-218">In Hallo **voornaam** textbox type **voornaam** van gebruiker als **Britta**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-218">In hello **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="edbb0-219">c.</span><span class="sxs-lookup"><span data-stu-id="edbb0-219">c.</span></span> <span data-ttu-id="edbb0-220">In Hallo **achternaam** textbox type **achternaam** van gebruiker als **Simon**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-220">In hello **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="edbb0-221">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="edbb0-222">Hello Azure AD-accounthouder wordt een e-mailbericht ontvangen en volg een koppeling tooconfirm hun account maken voordat deze geactiveerd wordt. U kunt andere Citrix ShareFile gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Citrix ShareFile tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="edbb0-222">hello Azure AD account holder will receive an email and follow a link tooconfirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="edbb0-223">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="edbb0-223">Assign hello Azure AD test user</span></span>

<span data-ttu-id="edbb0-224">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooCitrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="edbb0-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix ShareFile.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="edbb0-226">**tooassign Britta Simon tooCitrix ShareFile, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="edbb0-226">**tooassign Britta Simon tooCitrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="edbb0-227">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="edbb0-229">Selecteer in de lijst met de toepassingen van Hallo **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-229">In hello applications list, select **Citrix ShareFile**.</span></span>

    ![Hallo Citrix ShareFile koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="edbb0-231">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="edbb0-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="edbb0-233">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="edbb0-233">Click **Add** button.</span></span> <span data-ttu-id="edbb0-234">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="edbb0-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="edbb0-236">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="edbb0-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="edbb0-237">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="edbb0-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="edbb0-238">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="edbb0-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="edbb0-239">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="edbb0-239">Test single sign-on</span></span>

<span data-ttu-id="edbb0-240">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="edbb0-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="edbb0-241">Als u op Hallo Citrix ShareFile-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Citrix ShareFile-toepassing.</span><span class="sxs-lookup"><span data-stu-id="edbb0-241">When you click hello Citrix ShareFile tile in hello Access Panel, you should get automatically signed-on tooyour Citrix ShareFile application.</span></span>
<span data-ttu-id="edbb0-242">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="edbb0-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="edbb0-243">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="edbb0-243">Additional resources</span></span>

* [<span data-ttu-id="edbb0-244">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="edbb0-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="edbb0-245">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="edbb0-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

