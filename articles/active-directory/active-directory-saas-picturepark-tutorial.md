---
title: 'Zelfstudie: Azure Active Directory-integratie met Picturepark | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Picturepark.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="a47f7-103">Zelfstudie: Azure Active Directory-integratie met Picturepark</span><span class="sxs-lookup"><span data-stu-id="a47f7-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="a47f7-104">In deze zelfstudie leert u hoe toointegrate Picturepark met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a47f7-104">In this tutorial, you learn how toointegrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a47f7-105">Picturepark integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a47f7-105">Integrating Picturepark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a47f7-106">U kunt beheren in Azure AD die tooPicturepark toegang heeft</span><span class="sxs-lookup"><span data-stu-id="a47f7-106">You can control in Azure AD who has access tooPicturepark</span></span>
- <span data-ttu-id="a47f7-107">U kunt uw gebruikers tooautomatically get aangemelde tooPicturepark (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="a47f7-107">You can enable your users tooautomatically get signed-on tooPicturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a47f7-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a47f7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a47f7-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a47f7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a47f7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a47f7-110">Prerequisites</span></span>

<span data-ttu-id="a47f7-111">Azure AD-integratie met Picturepark tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="a47f7-111">tooconfigure Azure AD integration with Picturepark, you need hello following items:</span></span>

- <span data-ttu-id="a47f7-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a47f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a47f7-113">Een Picturepark eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a47f7-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a47f7-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a47f7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a47f7-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a47f7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a47f7-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a47f7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a47f7-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a47f7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a47f7-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a47f7-118">Scenario description</span></span>
<span data-ttu-id="a47f7-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a47f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a47f7-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a47f7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a47f7-121">Het toevoegen van Picturepark van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a47f7-121">Adding Picturepark from hello gallery</span></span>
2. <span data-ttu-id="a47f7-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a47f7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-hello-gallery"></a><span data-ttu-id="a47f7-123">Het toevoegen van Picturepark van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a47f7-123">Adding Picturepark from hello gallery</span></span>
<span data-ttu-id="a47f7-124">tooconfigure hello integratie van Picturepark in Azure AD, moet u tooadd Picturepark uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a47f7-124">tooconfigure hello integration of Picturepark into Azure AD, you need tooadd Picturepark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a47f7-125">**tooadd Picturepark via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a47f7-125">**tooadd Picturepark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a47f7-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a47f7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a47f7-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a47f7-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a47f7-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a47f7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a47f7-133">Typ in het zoekvak Hallo **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-133">In hello search box, type **Picturepark**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="a47f7-135">Selecteer in het deelvenster resultaten hello, **Picturepark**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a47f7-135">In hello results panel, select **Picturepark**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a47f7-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a47f7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a47f7-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Picturepark op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a47f7-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a47f7-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Picturepark is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a47f7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Picturepark is tooa user in Azure AD.</span></span> <span data-ttu-id="a47f7-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Picturepark toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="a47f7-140">In other words, a link relationship between an Azure AD user and hello related user in Picturepark needs toobe established.</span></span>

<span data-ttu-id="a47f7-141">Wijs in Picturepark, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="a47f7-141">In Picturepark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a47f7-142">tooconfigure en eenmalige aanmelding Azure AD-test met Picturepark, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a47f7-142">tooconfigure and test Azure AD single sign-on with Picturepark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a47f7-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="a47f7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a47f7-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a47f7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a47f7-145">**[Maken van een testgebruiker Picturepark](#creating-a-picturepark-test-user)**  -toohave een equivalent van Britta Simon in Picturepark die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a47f7-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - toohave a counterpart of Britta Simon in Picturepark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a47f7-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a47f7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a47f7-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a47f7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a47f7-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a47f7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a47f7-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Picturepark configureren.</span><span class="sxs-lookup"><span data-stu-id="a47f7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="a47f7-150">**Azure AD tooconfigure eenmalige aanmelding met Picturepark, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a47f7-150">**tooconfigure Azure AD single sign-on with Picturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="a47f7-151">In de Azure-portal op Hallo Hallo **Picturepark** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-151">In hello Azure portal, on hello **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a47f7-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a47f7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="a47f7-155">Op Hallo **Picturepark domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a47f7-155">On hello **Picturepark Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="a47f7-157">a.</span><span class="sxs-lookup"><span data-stu-id="a47f7-157">a.</span></span> <span data-ttu-id="a47f7-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="a47f7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="a47f7-159">b.</span><span class="sxs-lookup"><span data-stu-id="a47f7-159">b.</span></span> <span data-ttu-id="a47f7-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="a47f7-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="a47f7-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="a47f7-161">These values are not real.</span></span> <span data-ttu-id="a47f7-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="a47f7-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a47f7-163">Neem contact op met [Picturepark Client ondersteuningsteam](https://picturepark.com/about/contact/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a47f7-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="a47f7-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="a47f7-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="a47f7-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a47f7-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a47f7-168">Op Hallo **Picturepark configuratie** sectie, klikt u op **configureren Picturepark** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="a47f7-168">On hello **Picturepark Configuration** section, click **Configure Picturepark** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a47f7-169">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="a47f7-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="a47f7-171">In een ander browservenster, meld u bij uw bedrijf Picturepark site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a47f7-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="a47f7-172">Klik in de werkbalk bovenaan Hallo Hallo op **Systeembeheer**, en klik vervolgens op **beheerconsole**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-172">In hello toolbar on hello top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="a47f7-173">![Beheerconsole](./media/active-directory-saas-picturepark-tutorial/ic795062.png "-beheerconsole")</span><span class="sxs-lookup"><span data-stu-id="a47f7-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="a47f7-174">Klik op **verificatie**, en klik vervolgens op **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="a47f7-175">![Verificatie](./media/active-directory-saas-picturepark-tutorial/ic795063.png "verificatie")</span><span class="sxs-lookup"><span data-stu-id="a47f7-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="a47f7-176">In Hallo **identiteit providerconfiguratie** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a47f7-176">In hello **Identity provider configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="a47f7-177">![Configuratie van de provider identiteit](./media/active-directory-saas-picturepark-tutorial/ic795064.png "providerconfiguratie identiteit")</span><span class="sxs-lookup"><span data-stu-id="a47f7-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="a47f7-178">a.</span><span class="sxs-lookup"><span data-stu-id="a47f7-178">a.</span></span> <span data-ttu-id="a47f7-179">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-179">Click **Add**.</span></span>
  
    <span data-ttu-id="a47f7-180">b.</span><span class="sxs-lookup"><span data-stu-id="a47f7-180">b.</span></span> <span data-ttu-id="a47f7-181">Typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="a47f7-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="a47f7-182">c.</span><span class="sxs-lookup"><span data-stu-id="a47f7-182">c.</span></span> <span data-ttu-id="a47f7-183">Selecteer **ingesteld als standaard**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="a47f7-184">d.</span><span class="sxs-lookup"><span data-stu-id="a47f7-184">d.</span></span> <span data-ttu-id="a47f7-185">In **verlener URI** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a47f7-185">In **Issuer URI** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="a47f7-186">e.</span><span class="sxs-lookup"><span data-stu-id="a47f7-186">e.</span></span> <span data-ttu-id="a47f7-187">In **vertrouwde verlener miniatuur afdrukken** textbox plakken Hallo-waarde van **vingerafdruk** die u hebt gekopieerd uit **certificaat voor ondertekening van SAML** sectie.</span><span class="sxs-lookup"><span data-stu-id="a47f7-187">In **Trusted Issuer Thumb Print** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="a47f7-188">Klik op **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="a47f7-189">Hallo tooset **Emailaddress** kenmerk in Hallo **Claim** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-189">tooset hello **Emailaddress** attribute in hello **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="a47f7-190">![Configuratie](./media/active-directory-saas-picturepark-tutorial/ic795065.png "configuratie")</span><span class="sxs-lookup"><span data-stu-id="a47f7-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="a47f7-191">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="a47f7-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a47f7-192">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="a47f7-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a47f7-193">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a47f7-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a47f7-194">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a47f7-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="a47f7-195">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a47f7-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a47f7-197">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a47f7-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a47f7-198">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a47f7-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a47f7-200">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a47f7-202">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="a47f7-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a47f7-204">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a47f7-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a47f7-206">a.</span><span class="sxs-lookup"><span data-stu-id="a47f7-206">a.</span></span> <span data-ttu-id="a47f7-207">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a47f7-208">b.</span><span class="sxs-lookup"><span data-stu-id="a47f7-208">b.</span></span> <span data-ttu-id="a47f7-209">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a47f7-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a47f7-210">c.</span><span class="sxs-lookup"><span data-stu-id="a47f7-210">c.</span></span> <span data-ttu-id="a47f7-211">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a47f7-212">d.</span><span class="sxs-lookup"><span data-stu-id="a47f7-212">d.</span></span> <span data-ttu-id="a47f7-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="a47f7-214">Een testgebruiker Picturepark maken</span><span class="sxs-lookup"><span data-stu-id="a47f7-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="a47f7-215">In de volgorde tooenable Azure AD gebruikers toolog in Picturepark, moeten ze worden ingericht in Picturepark.</span><span class="sxs-lookup"><span data-stu-id="a47f7-215">In order tooenable Azure AD users toolog into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="a47f7-216">In geval van Picturepark Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="a47f7-216">In hello case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="a47f7-217">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a47f7-217">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a47f7-218">Meld u bij tooyour **Picturepark** tenant.</span><span class="sxs-lookup"><span data-stu-id="a47f7-218">Log in tooyour **Picturepark** tenant.</span></span>

2. <span data-ttu-id="a47f7-219">Klik in de werkbalk bovenaan Hallo Hallo op **Systeembeheer**, en klik vervolgens op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-219">In hello toolbar on hello top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="a47f7-220">![Gebruikers](./media/active-directory-saas-picturepark-tutorial/ic795067.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="a47f7-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="a47f7-221">In Hallo **overzicht van gebruikers** tabblad **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-221">In hello **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="a47f7-222">![Gebruikersbeheer](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Gebruikersbeheer")</span><span class="sxs-lookup"><span data-stu-id="a47f7-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="a47f7-223">Op Hallo **gebruiker maken** dialoogvenster Hallo uitvoeren na de stappen van een geldige Azure Active Directory-gebruiker gewenste tooprovision:</span><span class="sxs-lookup"><span data-stu-id="a47f7-223">On hello **Create User** dialog, perform hello following steps of a valid Azure Active Directory User you want tooprovision:</span></span>
   
    <span data-ttu-id="a47f7-224">![Gebruiker maken](./media/active-directory-saas-picturepark-tutorial/ic795069.png "gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="a47f7-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="a47f7-225">a.</span><span class="sxs-lookup"><span data-stu-id="a47f7-225">a.</span></span> <span data-ttu-id="a47f7-226">In Hallo **e-mailadres** textbox type Hallo **e-mailadres** van Hallo gebruiker  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="a47f7-226">In hello **Email Address** textbox, type hello **email address** of hello user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="a47f7-227">b.</span><span class="sxs-lookup"><span data-stu-id="a47f7-227">b.</span></span> <span data-ttu-id="a47f7-228">In Hallo **wachtwoord** en **wachtwoord bevestigen** tekstvakken, type Hallo **wachtwoord** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a47f7-228">In hello **Password** and **Confirm Password** textboxes, type hello **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="a47f7-229">c.</span><span class="sxs-lookup"><span data-stu-id="a47f7-229">c.</span></span> <span data-ttu-id="a47f7-230">In Hallo **voornaam** textbox type Hallo **voornaam** van Hallo gebruiker **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-230">In hello **First Name** textbox, type hello **First Name** of hello user **Britta**.</span></span> 
   
    <span data-ttu-id="a47f7-231">d.</span><span class="sxs-lookup"><span data-stu-id="a47f7-231">d.</span></span> <span data-ttu-id="a47f7-232">In Hallo **achternaam** textbox type Hallo **achternaam** van Hallo gebruiker **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-232">In hello **Last Name** textbox, type hello **Last Name** of hello user **Simon**.</span></span>
   
    <span data-ttu-id="a47f7-233">e.</span><span class="sxs-lookup"><span data-stu-id="a47f7-233">e.</span></span> <span data-ttu-id="a47f7-234">In Hallo **bedrijf** textbox type Hallo **bedrijfsnaam** van Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a47f7-234">In hello **Company** textbox, type hello **Company name** of hello user.</span></span> 
   
    <span data-ttu-id="a47f7-235">f.</span><span class="sxs-lookup"><span data-stu-id="a47f7-235">f.</span></span> <span data-ttu-id="a47f7-236">In Hallo **land** textbox, selecteer Hallo **land** van Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a47f7-236">In hello **Country** textbox, select hello **Country** of hello user.</span></span>
  
    <span data-ttu-id="a47f7-237">g.</span><span class="sxs-lookup"><span data-stu-id="a47f7-237">g.</span></span> <span data-ttu-id="a47f7-238">In Hallo **ZIP** textbox type Hallo **postcode** van Hallo plaats.</span><span class="sxs-lookup"><span data-stu-id="a47f7-238">In hello **ZIP** textbox, type hello **ZIP code** of hello city.</span></span>
   
    <span data-ttu-id="a47f7-239">h.</span><span class="sxs-lookup"><span data-stu-id="a47f7-239">h.</span></span> <span data-ttu-id="a47f7-240">In Hallo **stad** textbox type Hallo **plaatsnaam** van Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a47f7-240">In hello **City** textbox, type hello **City name** of hello user.</span></span>

    <span data-ttu-id="a47f7-241">ik.</span><span class="sxs-lookup"><span data-stu-id="a47f7-241">i.</span></span> <span data-ttu-id="a47f7-242">Selecteer een **taal**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="a47f7-243">j.</span><span class="sxs-lookup"><span data-stu-id="a47f7-243">j.</span></span> <span data-ttu-id="a47f7-244">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="a47f7-245">U kunt andere Picturepark gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Picturepark tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="a47f7-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a47f7-246">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a47f7-246">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a47f7-247">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooPicturepark toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="a47f7-247">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPicturepark.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a47f7-249">**tooassign Britta Simon tooPicturepark, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a47f7-249">**tooassign Britta Simon tooPicturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="a47f7-250">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-250">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a47f7-252">Selecteer in de lijst met de toepassingen van Hallo **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-252">In hello applications list, select **Picturepark**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="a47f7-254">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-254">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a47f7-256">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a47f7-256">Click **Add** button.</span></span> <span data-ttu-id="a47f7-257">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a47f7-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a47f7-259">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="a47f7-259">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a47f7-260">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a47f7-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a47f7-261">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a47f7-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a47f7-262">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a47f7-262">Testing single sign-on</span></span>

<span data-ttu-id="a47f7-263">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="a47f7-263">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a47f7-264">Als u op Hallo Picturepark tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Picturepark toepassing.</span><span class="sxs-lookup"><span data-stu-id="a47f7-264">When you click hello Picturepark tile in hello Access Panel, you should get automatically signed-on tooyour Picturepark application.</span></span> <span data-ttu-id="a47f7-265">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a47f7-265">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a47f7-266">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a47f7-266">Additional resources</span></span>

* [<span data-ttu-id="a47f7-267">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a47f7-267">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a47f7-268">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a47f7-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

