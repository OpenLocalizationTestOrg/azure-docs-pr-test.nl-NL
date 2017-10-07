---
title: 'Zelfstudie: Azure Active Directory-integratie met Veracode | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Veracode.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="03db3-103">Zelfstudie: Azure Active Directory-integratie met Veracode</span><span class="sxs-lookup"><span data-stu-id="03db3-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="03db3-104">In deze zelfstudie leert u hoe toointegrate Veracode met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="03db3-104">In this tutorial, you learn how toointegrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="03db3-105">Veracode integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="03db3-105">Integrating Veracode with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="03db3-106">U kunt beheren in Azure AD die tooVeracode toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="03db3-106">You can control in Azure AD who has access tooVeracode.</span></span>
- <span data-ttu-id="03db3-107">U kunt uw gebruikers tooautomatically get aangemelde tooVeracode (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="03db3-107">You can enable your users tooautomatically get signed-on tooVeracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="03db3-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="03db3-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="03db3-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="03db3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03db3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="03db3-110">Prerequisites</span></span>

<span data-ttu-id="03db3-111">Azure AD-integratie met Veracode tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="03db3-111">tooconfigure Azure AD integration with Veracode, you need hello following items:</span></span>

- <span data-ttu-id="03db3-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="03db3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="03db3-113">Een Veracode eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="03db3-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="03db3-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="03db3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="03db3-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="03db3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="03db3-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="03db3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="03db3-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="03db3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="03db3-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="03db3-118">Scenario description</span></span>
<span data-ttu-id="03db3-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="03db3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="03db3-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="03db3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="03db3-121">Veracode van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="03db3-121">Add Veracode from hello gallery</span></span>
2. <span data-ttu-id="03db3-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="03db3-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-hello-gallery"></a><span data-ttu-id="03db3-123">Veracode van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="03db3-123">Add Veracode from hello gallery</span></span>
<span data-ttu-id="03db3-124">tooconfigure hello integratie van Veracode in Azure AD, moet u tooadd Veracode uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="03db3-124">tooconfigure hello integration of Veracode into Azure AD, you need tooadd Veracode from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="03db3-125">**tooadd Veracode via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="03db3-125">**tooadd Veracode from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="03db3-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="03db3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="03db3-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="03db3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="03db3-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="03db3-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="03db3-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="03db3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="03db3-133">Typ in het zoekvak Hallo **Veracode**, selecteer **Veracode** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="03db3-133">In hello search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Veracode in de lijst met resultaten Hallo](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="03db3-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="03db3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="03db3-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Veracode op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="03db3-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="03db3-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Veracode is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03db3-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Veracode is tooa user in Azure AD.</span></span> <span data-ttu-id="03db3-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Veracode toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="03db3-138">In other words, a link relationship between an Azure AD user and hello related user in Veracode needs toobe established.</span></span>

<span data-ttu-id="03db3-139">Wijs in Veracode, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="03db3-139">In Veracode, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="03db3-140">tooconfigure en eenmalige aanmelding Azure AD-test met Veracode, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="03db3-140">tooconfigure and test Azure AD single sign-on with Veracode, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="03db3-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="03db3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="03db3-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="03db3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="03db3-143">**[Maak een testgebruiker Veracode](#create-a-veracode-test-user)**  -toohave een equivalent van Britta Simon in Veracode die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="03db3-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - toohave a counterpart of Britta Simon in Veracode that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="03db3-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="03db3-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="03db3-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="03db3-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="03db3-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="03db3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="03db3-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Veracode configureren.</span><span class="sxs-lookup"><span data-stu-id="03db3-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="03db3-148">**Azure AD tooconfigure eenmalige aanmelding met Veracode, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="03db3-148">**tooconfigure Azure AD single sign-on with Veracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="03db3-149">In de Azure-portal op Hallo Hallo **Veracode** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="03db3-149">In hello Azure portal, on hello **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="03db3-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="03db3-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="03db3-153">Op Hallo **Veracode domein en de URL's** sectie van de gebruiker heeft geen tooperform eventuele stappen zoals Hallo app al vooraf is geïntegreerd met Azure.</span><span class="sxs-lookup"><span data-stu-id="03db3-153">On hello **Veracode Domain and URLs** section, the user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="03db3-155">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="03db3-155">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="03db3-157">Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooVeracode aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="03db3-157">hello objective of this section is toooutline how tooenable users tooauthenticate tooVeracode with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="03db3-158">Uw toepassing Veracode Hallo SAML asserties verwacht in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour **saml-token kenmerken** configuratie.</span><span class="sxs-lookup"><span data-stu-id="03db3-158">Your Veracode application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> <span data-ttu-id="03db3-159">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="03db3-159">hello following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="03db3-160">![Kenmerken](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="03db3-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="03db3-161">Kenmerktoewijzingen tooadd Hallo vereist, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="03db3-161">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="03db3-162">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="03db3-162">Attribute Name</span></span> | <span data-ttu-id="03db3-163">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="03db3-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="03db3-164">Voornaam</span><span class="sxs-lookup"><span data-stu-id="03db3-164">firstname</span></span> |<span data-ttu-id="03db3-165">User.givenName</span><span class="sxs-lookup"><span data-stu-id="03db3-165">User.givenname</span></span> |
    | <span data-ttu-id="03db3-166">Achternaam</span><span class="sxs-lookup"><span data-stu-id="03db3-166">lastname</span></span> |<span data-ttu-id="03db3-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="03db3-167">User.surname</span></span> |
    | <span data-ttu-id="03db3-168">E-mail</span><span class="sxs-lookup"><span data-stu-id="03db3-168">email</span></span> |<span data-ttu-id="03db3-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="03db3-169">User.mail</span></span> |
    
    <span data-ttu-id="03db3-170">a.</span><span class="sxs-lookup"><span data-stu-id="03db3-170">a.</span></span> <span data-ttu-id="03db3-171">Klik voor elke gegevensrij in bovenstaande tabel voor Hallo **gebruikerskenmerk toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="03db3-171">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="03db3-172">![Kenmerken](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="03db3-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="03db3-173">![Kenmerken](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="03db3-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="03db3-174">b.</span><span class="sxs-lookup"><span data-stu-id="03db3-174">b.</span></span> <span data-ttu-id="03db3-175">In Hallo **kenmerknaam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="03db3-175">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="03db3-176">c.</span><span class="sxs-lookup"><span data-stu-id="03db3-176">c.</span></span> <span data-ttu-id="03db3-177">In Hallo **kenmerkwaarde** textbox, selecteer Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="03db3-177">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="03db3-178">d.</span><span class="sxs-lookup"><span data-stu-id="03db3-178">d.</span></span> <span data-ttu-id="03db3-179">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="03db3-179">Click **Ok**.</span></span>

7. <span data-ttu-id="03db3-180">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="03db3-180">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="03db3-182">Op Hallo **Veracode configuratie** sectie, klikt u op **configureren Veracode** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="03db3-182">On hello **Veracode Configuration** section, click **Configure Veracode** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="03db3-183">Kopiëren Hallo **SAML entiteit-ID** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="03db3-183">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Veracode configuratie](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="03db3-185">In een ander browservenster, meld u bij uw bedrijf Veracode site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="03db3-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="03db3-186">Klik in het menu bovenaan Hallo Hallo **instellingen**, en klik vervolgens op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="03db3-186">In hello menu on hello top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="03db3-187">![Beheer](./media/active-directory-saas-veracode-tutorial/ic802911.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="03db3-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="03db3-188">Klik op Hallo **SAML** tabblad.</span><span class="sxs-lookup"><span data-stu-id="03db3-188">Click hello **SAML** tab.</span></span>

12. <span data-ttu-id="03db3-189">In Hallo **organisatie SAML-instellingen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="03db3-189">In hello **Organization SAML Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="03db3-190">![Beheer](./media/active-directory-saas-veracode-tutorial/ic802912.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="03db3-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="03db3-191">a.</span><span class="sxs-lookup"><span data-stu-id="03db3-191">a.</span></span>  <span data-ttu-id="03db3-192">In **verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="03db3-192">In  **Issuer** textbox, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="03db3-193">b.</span><span class="sxs-lookup"><span data-stu-id="03db3-193">b.</span></span> <span data-ttu-id="03db3-194">Klik op tooupload uw gedownloade certificaat vanuit Azure-portal **bestand kiezen**.</span><span class="sxs-lookup"><span data-stu-id="03db3-194">tooupload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="03db3-195">c.</span><span class="sxs-lookup"><span data-stu-id="03db3-195">c.</span></span> <span data-ttu-id="03db3-196">Selecteer **Self-registratie inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="03db3-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="03db3-197">In Hallo **Self-instellingen voor statusregistratie** sectie, het uitvoeren van Hallo volgende stappen uit en klik vervolgens op **opslaan**:</span><span class="sxs-lookup"><span data-stu-id="03db3-197">In hello **Self Registration Settings** section, perform hello following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="03db3-198">![Beheer](./media/active-directory-saas-veracode-tutorial/ic802913.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="03db3-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="03db3-199">a.</span><span class="sxs-lookup"><span data-stu-id="03db3-199">a.</span></span> <span data-ttu-id="03db3-200">Als **nieuwe gebruikersactivering**, selecteer **Nee activering vereist**.</span><span class="sxs-lookup"><span data-stu-id="03db3-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="03db3-201">b.</span><span class="sxs-lookup"><span data-stu-id="03db3-201">b.</span></span> <span data-ttu-id="03db3-202">Als **gebruiker Gegevensupdates**, selecteer **voorkeur Veracode gebruikersgegevens**.</span><span class="sxs-lookup"><span data-stu-id="03db3-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="03db3-203">c.</span><span class="sxs-lookup"><span data-stu-id="03db3-203">c.</span></span> <span data-ttu-id="03db3-204">Voor **Details van SAML-kenmerk**, selecteer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="03db3-204">For **SAML Attribute Details**, select hello following:</span></span>
      * <span data-ttu-id="03db3-205">**Gebruikersrollen**</span><span class="sxs-lookup"><span data-stu-id="03db3-205">**User Roles**</span></span>
      * <span data-ttu-id="03db3-206">**Beleid beheerder**</span><span class="sxs-lookup"><span data-stu-id="03db3-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="03db3-207">**Revisor**</span><span class="sxs-lookup"><span data-stu-id="03db3-207">**Reviewer**</span></span>
      * <span data-ttu-id="03db3-208">**Beveiliging Lead**</span><span class="sxs-lookup"><span data-stu-id="03db3-208">**Security Lead**</span></span>
      * <span data-ttu-id="03db3-209">**Executive**</span><span class="sxs-lookup"><span data-stu-id="03db3-209">**Executive**</span></span>
      * <span data-ttu-id="03db3-210">**Indienings**</span><span class="sxs-lookup"><span data-stu-id="03db3-210">**Submitter**</span></span>
      * <span data-ttu-id="03db3-211">**Maker**</span><span class="sxs-lookup"><span data-stu-id="03db3-211">**Creator**</span></span>
      * <span data-ttu-id="03db3-212">**Alle scannen typen**</span><span class="sxs-lookup"><span data-stu-id="03db3-212">**All Scan Types**</span></span>
      * <span data-ttu-id="03db3-213">**Lidmaatschap van een team**</span><span class="sxs-lookup"><span data-stu-id="03db3-213">**Team Memberships**</span></span>
      * <span data-ttu-id="03db3-214">**Standaardteam**</span><span class="sxs-lookup"><span data-stu-id="03db3-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="03db3-215">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="03db3-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="03db3-216">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="03db3-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="03db3-217">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="03db3-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="03db3-218">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="03db3-218">Create an Azure AD test user</span></span>

<span data-ttu-id="03db3-219">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="03db3-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="03db3-221">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="03db3-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="03db3-222">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="03db3-222">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="03db3-224">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="03db3-224">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="03db3-226">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="03db3-226">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="03db3-228">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="03db3-228">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="03db3-230">a.</span><span class="sxs-lookup"><span data-stu-id="03db3-230">a.</span></span> <span data-ttu-id="03db3-231">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="03db3-231">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="03db3-232">b.</span><span class="sxs-lookup"><span data-stu-id="03db3-232">b.</span></span> <span data-ttu-id="03db3-233">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="03db3-233">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="03db3-234">c.</span><span class="sxs-lookup"><span data-stu-id="03db3-234">c.</span></span> <span data-ttu-id="03db3-235">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="03db3-235">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="03db3-236">d.</span><span class="sxs-lookup"><span data-stu-id="03db3-236">d.</span></span> <span data-ttu-id="03db3-237">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="03db3-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="03db3-238">Een testgebruiker Veracode maken</span><span class="sxs-lookup"><span data-stu-id="03db3-238">Create a Veracode test user</span></span>
<span data-ttu-id="03db3-239">In de volgorde tooenable Azure AD gebruikers toolog in Veracode, moeten ze worden ingericht in Veracode.</span><span class="sxs-lookup"><span data-stu-id="03db3-239">In order tooenable Azure AD users toolog into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="03db3-240">In geval van Veracode Hallo is inrichting een geautomatiseerde taak.</span><span class="sxs-lookup"><span data-stu-id="03db3-240">In hello case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="03db3-241">Er is geen actie-item voor u.</span><span class="sxs-lookup"><span data-stu-id="03db3-241">There is no action item for you.</span></span> <span data-ttu-id="03db3-242">Gebruikers worden automatisch gemaakt indien nodig tijdens Hallo eerste eenmalige aanmelding poging.</span><span class="sxs-lookup"><span data-stu-id="03db3-242">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="03db3-243">U kunt andere Veracode gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Veracode tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="03db3-243">You can use any other Veracode user account creation tools or APIs provided by Veracode tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="03db3-244">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="03db3-244">Assign hello Azure AD test user</span></span>

<span data-ttu-id="03db3-245">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooVeracode toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="03db3-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVeracode.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="03db3-247">**tooassign Britta Simon tooVeracode, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="03db3-247">**tooassign Britta Simon tooVeracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="03db3-248">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="03db3-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="03db3-250">Selecteer in de lijst met de toepassingen van Hallo **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="03db3-250">In hello applications list, select **Veracode**.</span></span>

    ![Hallo Veracode koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="03db3-252">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="03db3-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="03db3-254">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="03db3-254">Click **Add** button.</span></span> <span data-ttu-id="03db3-255">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="03db3-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="03db3-257">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="03db3-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="03db3-258">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="03db3-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="03db3-259">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="03db3-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="03db3-260">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="03db3-260">Test single sign-on</span></span>

<span data-ttu-id="03db3-261">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="03db3-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="03db3-262">Als u op Hallo Veracode tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Veracode toepassing.</span><span class="sxs-lookup"><span data-stu-id="03db3-262">When you click hello Veracode tile in hello Access Panel, you should get automatically signed-on tooyour Veracode application.</span></span>
<span data-ttu-id="03db3-263">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="03db3-263">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="03db3-264">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="03db3-264">Additional resources</span></span>

* [<span data-ttu-id="03db3-265">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03db3-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="03db3-266">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="03db3-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

