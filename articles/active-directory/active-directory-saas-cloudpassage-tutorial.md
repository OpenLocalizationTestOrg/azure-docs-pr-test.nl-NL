---
title: 'Zelfstudie: Azure Active Directory-integratie met CloudPassage | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en CloudPassage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 32fb007b90f071626c9b40fb5afc341dd3c1ae99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="28d7b-103">Zelfstudie: Azure Active Directory-integratie met CloudPassage</span><span class="sxs-lookup"><span data-stu-id="28d7b-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="28d7b-104">In deze zelfstudie leert u hoe toointegrate CloudPassage met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="28d7b-104">In this tutorial, you learn how toointegrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="28d7b-105">CloudPassage integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="28d7b-105">Integrating CloudPassage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="28d7b-106">U kunt beheren in Azure AD die tooCloudPassage toegang heeft</span><span class="sxs-lookup"><span data-stu-id="28d7b-106">You can control in Azure AD who has access tooCloudPassage</span></span>
- <span data-ttu-id="28d7b-107">U kunt uw gebruikers tooautomatically get aangemelde tooCloudPassage (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="28d7b-107">You can enable your users tooautomatically get signed-on tooCloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="28d7b-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="28d7b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="28d7b-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="28d7b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28d7b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="28d7b-110">Prerequisites</span></span>

<span data-ttu-id="28d7b-111">Azure AD-integratie met CloudPassage tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="28d7b-111">tooconfigure Azure AD integration with CloudPassage, you need hello following items:</span></span>

- <span data-ttu-id="28d7b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="28d7b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="28d7b-113">Een CloudPassage eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="28d7b-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="28d7b-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="28d7b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="28d7b-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="28d7b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="28d7b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="28d7b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="28d7b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28d7b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="28d7b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="28d7b-118">Scenario description</span></span>
<span data-ttu-id="28d7b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="28d7b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="28d7b-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="28d7b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="28d7b-121">Het toevoegen van CloudPassage van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="28d7b-121">Adding CloudPassage from hello gallery</span></span>
2. <span data-ttu-id="28d7b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="28d7b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-hello-gallery"></a><span data-ttu-id="28d7b-123">Het toevoegen van CloudPassage van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="28d7b-123">Adding CloudPassage from hello gallery</span></span>
<span data-ttu-id="28d7b-124">tooconfigure hello integratie van CloudPassage in Azure AD, moet u tooadd CloudPassage uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="28d7b-124">tooconfigure hello integration of CloudPassage into Azure AD, you need tooadd CloudPassage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="28d7b-125">**tooadd CloudPassage via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="28d7b-125">**tooadd CloudPassage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="28d7b-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="28d7b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="28d7b-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="28d7b-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="28d7b-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="28d7b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="28d7b-133">Typ in het zoekvak Hallo **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-133">In hello search box, type **CloudPassage**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="28d7b-135">Selecteer in het deelvenster resultaten hello, **CloudPassage**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="28d7b-135">In hello results panel, select **CloudPassage**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="28d7b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="28d7b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="28d7b-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met CloudPassage op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="28d7b-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="28d7b-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in CloudPassage is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28d7b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CloudPassage is tooa user in Azure AD.</span></span> <span data-ttu-id="28d7b-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in CloudPassage toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="28d7b-140">In other words, a link relationship between an Azure AD user and hello related user in CloudPassage needs toobe established.</span></span>

<span data-ttu-id="28d7b-141">Wijs in CloudPassage, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="28d7b-141">In CloudPassage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="28d7b-142">tooconfigure en eenmalige aanmelding Azure AD-test met CloudPassage, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="28d7b-142">tooconfigure and test Azure AD single sign-on with CloudPassage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="28d7b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="28d7b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="28d7b-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28d7b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="28d7b-145">**[Maken van een testgebruiker CloudPassage](#creating-a-cloudpassage-test-user)**  -toohave een equivalent van Britta Simon in CloudPassage die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="28d7b-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - toohave a counterpart of Britta Simon in CloudPassage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="28d7b-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="28d7b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="28d7b-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="28d7b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="28d7b-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="28d7b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="28d7b-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing CloudPassage configureren.</span><span class="sxs-lookup"><span data-stu-id="28d7b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="28d7b-150">**Azure AD tooconfigure eenmalige aanmelding met CloudPassage, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="28d7b-150">**tooconfigure Azure AD single sign-on with CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="28d7b-151">In de Azure-portal op Hallo Hallo **CloudPassage** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-151">In hello Azure portal, on hello **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="28d7b-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="28d7b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="28d7b-155">Op Hallo **CloudPassage domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="28d7b-155">On hello **CloudPassage Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="28d7b-157">a.</span><span class="sxs-lookup"><span data-stu-id="28d7b-157">a.</span></span> <span data-ttu-id="28d7b-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="28d7b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="28d7b-159">b.</span><span class="sxs-lookup"><span data-stu-id="28d7b-159">b.</span></span> <span data-ttu-id="28d7b-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen: `https://portal.cloudpassage.com/saml/consume/accountid`.</span><span class="sxs-lookup"><span data-stu-id="28d7b-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="28d7b-161">U kunt de waarde voor dit kenmerk opvragen door te klikken op **SSO ondersteuningsdocumentatie** in Hallo **instellingen voor eenmalige aanmelding** gedeelte van uw CloudPassage-portal.</span><span class="sxs-lookup"><span data-stu-id="28d7b-161">You can get your value for this attribute by clicking **SSO Setup documentation** in hello **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="28d7b-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="28d7b-163">These values are not real.</span></span> <span data-ttu-id="28d7b-164">Deze waarden bijwerken met Hallo werkelijke antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="28d7b-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="28d7b-165">Neem contact op met [CloudPassage Client ondersteuningsteam](https://www.cloudpassage.com/company/contact/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="28d7b-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="28d7b-166">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="28d7b-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="28d7b-168">Uw toepassing CloudPassage verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="28d7b-168">Your CloudPassage application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span>   
<span data-ttu-id="28d7b-169">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="28d7b-169">hello following screenshot shows an example for this.</span></span>
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="28d7b-171">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in Hallo afbeelding hierboven en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="28d7b-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>

    | <span data-ttu-id="28d7b-172">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="28d7b-172">Attribute Name</span></span> | <span data-ttu-id="28d7b-173">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="28d7b-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="28d7b-174">Voornaam</span><span class="sxs-lookup"><span data-stu-id="28d7b-174">firstname</span></span> |<span data-ttu-id="28d7b-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="28d7b-175">user.givenname</span></span> |
    | <span data-ttu-id="28d7b-176">Achternaam</span><span class="sxs-lookup"><span data-stu-id="28d7b-176">lastname</span></span> |<span data-ttu-id="28d7b-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="28d7b-177">user.surname</span></span> |
    | <span data-ttu-id="28d7b-178">E-mail</span><span class="sxs-lookup"><span data-stu-id="28d7b-178">email</span></span> |<span data-ttu-id="28d7b-179">User.mail</span><span class="sxs-lookup"><span data-stu-id="28d7b-179">user.mail</span></span> |
    
    <span data-ttu-id="28d7b-180">a.</span><span class="sxs-lookup"><span data-stu-id="28d7b-180">a.</span></span> <span data-ttu-id="28d7b-181">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="28d7b-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="28d7b-184">b.</span><span class="sxs-lookup"><span data-stu-id="28d7b-184">b.</span></span> <span data-ttu-id="28d7b-185">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="28d7b-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="28d7b-186">c.</span><span class="sxs-lookup"><span data-stu-id="28d7b-186">c.</span></span> <span data-ttu-id="28d7b-187">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="28d7b-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="28d7b-188">d.</span><span class="sxs-lookup"><span data-stu-id="28d7b-188">d.</span></span> <span data-ttu-id="28d7b-189">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-189">Click **Ok**.</span></span>

7. <span data-ttu-id="28d7b-190">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="28d7b-190">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="28d7b-192">Op Hallo **CloudPassage configuratie** sectie, klikt u op **configureren CloudPassage** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="28d7b-192">On hello **CloudPassage Configuration** section, click **Configure CloudPassage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="28d7b-193">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="28d7b-193">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="28d7b-195">In een ander browservenster, aanmelding tooyour CloudPassage bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="28d7b-195">In a different browser window, sign-on tooyour CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="28d7b-196">Klik in het menu bovenaan Hallo Hallo **instellingen**, en klik vervolgens op **Sitebeheer**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-196">In hello menu on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Eenmalige aanmelding configureren][12]

11. <span data-ttu-id="28d7b-198">Klik op Hallo **verificatie-instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="28d7b-198">Click hello **Authentication Settings** tab.</span></span> 
   
    ![Eenmalige aanmelding configureren][13]

12. <span data-ttu-id="28d7b-200">In Hallo **instellingen voor eenmalige aanmelding** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="28d7b-200">In hello **Single Sign-on Settings** section, perform hello following steps:</span></span> 
   
    ![Eenmalige aanmelding configureren][14]

    <span data-ttu-id="28d7b-202">a.</span><span class="sxs-lookup"><span data-stu-id="28d7b-202">a.</span></span> <span data-ttu-id="28d7b-203">Selecteer **één inschakelen sign-on(SSO) (SSO Setup documentatie)** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="28d7b-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="28d7b-204">b.</span><span class="sxs-lookup"><span data-stu-id="28d7b-204">b.</span></span> <span data-ttu-id="28d7b-205">Plakken **SAML entiteit-ID** in Hallo **URL-verlener SAML** textbox.</span><span class="sxs-lookup"><span data-stu-id="28d7b-205">Paste **SAML Entity ID** into hello **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="28d7b-206">c.</span><span class="sxs-lookup"><span data-stu-id="28d7b-206">c.</span></span> <span data-ttu-id="28d7b-207">Plakken **SAML Single Sign-On Service-URL** in Hallo **eindpunt-URL van SAML** textbox.</span><span class="sxs-lookup"><span data-stu-id="28d7b-207">Paste **SAML Single Sign-On Service URL** into hello **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="28d7b-208">d.</span><span class="sxs-lookup"><span data-stu-id="28d7b-208">d.</span></span> <span data-ttu-id="28d7b-209">Plakken **Sign-Out URL** in Hallo **afmelding startpagina** textbox.</span><span class="sxs-lookup"><span data-stu-id="28d7b-209">Paste **Sign-Out URL** into hello **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="28d7b-210">e.</span><span class="sxs-lookup"><span data-stu-id="28d7b-210">e.</span></span> <span data-ttu-id="28d7b-211">Open uw gedownloade certificaat in Kladblok, kopieer Hallo inhoud van het gedownloade certificaat naar het Klembord en plak deze in Hallo **x 509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="28d7b-211">Open your downloaded certificate in notepad, copy hello content of downloaded certificate into your clipboard, and then paste it into hello **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="28d7b-212">f.</span><span class="sxs-lookup"><span data-stu-id="28d7b-212">f.</span></span> <span data-ttu-id="28d7b-213">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="28d7b-214">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="28d7b-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="28d7b-215">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="28d7b-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="28d7b-216">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="28d7b-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="28d7b-217">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="28d7b-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="28d7b-218">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="28d7b-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="28d7b-220">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="28d7b-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="28d7b-221">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="28d7b-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="28d7b-223">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="28d7b-225">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="28d7b-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="28d7b-227">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="28d7b-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="28d7b-229">a.</span><span class="sxs-lookup"><span data-stu-id="28d7b-229">a.</span></span> <span data-ttu-id="28d7b-230">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="28d7b-231">b.</span><span class="sxs-lookup"><span data-stu-id="28d7b-231">b.</span></span> <span data-ttu-id="28d7b-232">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="28d7b-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="28d7b-233">c.</span><span class="sxs-lookup"><span data-stu-id="28d7b-233">c.</span></span> <span data-ttu-id="28d7b-234">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="28d7b-235">d.</span><span class="sxs-lookup"><span data-stu-id="28d7b-235">d.</span></span> <span data-ttu-id="28d7b-236">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="28d7b-237">Een testgebruiker CloudPassage maken</span><span class="sxs-lookup"><span data-stu-id="28d7b-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="28d7b-238">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in CloudPassage van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="28d7b-238">hello objective of this section is toocreate a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="28d7b-239">**een gebruiker Britta Simon aangeroepen in CloudPassage, toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="28d7b-239">**toocreate a user called Britta Simon in CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="28d7b-240">Eenmalige aanmelding tooyour **CloudPassage** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="28d7b-240">Sign-on tooyour **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="28d7b-241">Klik in de werkbalk bovenaan Hallo Hallo op **instellingen**, en klik vervolgens op **Sitebeheer**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-241">In hello toolbar on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![Een testgebruiker CloudPassage maken][22] 

3. <span data-ttu-id="28d7b-243">Klik op Hallo **gebruikers** tabblad en klik vervolgens op **nieuwe gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-243">Click hello **Users** tab, and then click **Add New User**.</span></span> 
   
   ![Een testgebruiker CloudPassage maken][23]

4. <span data-ttu-id="28d7b-245">In Hallo **nieuwe gebruiker toevoegen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="28d7b-245">In hello **Add New User** section, perform hello following steps:</span></span> 
   
   ![Een testgebruiker CloudPassage maken][24]
    
    <span data-ttu-id="28d7b-247">a.</span><span class="sxs-lookup"><span data-stu-id="28d7b-247">a.</span></span> <span data-ttu-id="28d7b-248">In Hallo **voornaam** textbox Britta typt.</span><span class="sxs-lookup"><span data-stu-id="28d7b-248">In hello **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="28d7b-249">b.</span><span class="sxs-lookup"><span data-stu-id="28d7b-249">b.</span></span> <span data-ttu-id="28d7b-250">In Hallo **achternaam** textbox Simon typt.</span><span class="sxs-lookup"><span data-stu-id="28d7b-250">In hello **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="28d7b-251">c.</span><span class="sxs-lookup"><span data-stu-id="28d7b-251">c.</span></span> <span data-ttu-id="28d7b-252">In Hallo **gebruikersnaam** textbox Hallo **e** textbox en Hallo **e-mailbericht opnieuw** textbox, typ de gebruikersnaam van Britta in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28d7b-252">In hello **Username** textbox, hello **Email** textbox and hello **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="28d7b-253">d.</span><span class="sxs-lookup"><span data-stu-id="28d7b-253">d.</span></span> <span data-ttu-id="28d7b-254">Als **toegangstype**, selecteer **Halo Portal toegang inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="28d7b-255">e.</span><span class="sxs-lookup"><span data-stu-id="28d7b-255">e.</span></span> <span data-ttu-id="28d7b-256">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="28d7b-257">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="28d7b-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="28d7b-258">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooCloudPassage toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="28d7b-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloudPassage.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="28d7b-260">**tooassign Britta Simon tooCloudPassage, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="28d7b-260">**tooassign Britta Simon tooCloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="28d7b-261">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="28d7b-263">Selecteer in de lijst met de toepassingen van Hallo **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-263">In hello applications list, select **CloudPassage**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="28d7b-265">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="28d7b-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="28d7b-267">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="28d7b-267">Click **Add** button.</span></span> <span data-ttu-id="28d7b-268">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="28d7b-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="28d7b-270">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="28d7b-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="28d7b-271">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="28d7b-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="28d7b-272">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="28d7b-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="28d7b-273">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="28d7b-273">Testing single sign-on</span></span>

<span data-ttu-id="28d7b-274">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="28d7b-274">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="28d7b-275">Als u op Hallo CloudPassage tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour CloudPassage toepassing.</span><span class="sxs-lookup"><span data-stu-id="28d7b-275">When you click hello CloudPassage tile in hello Access Panel, you should get automatically signed-on tooyour CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="28d7b-276">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="28d7b-276">Additional resources</span></span>

* [<span data-ttu-id="28d7b-277">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28d7b-277">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="28d7b-278">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="28d7b-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

