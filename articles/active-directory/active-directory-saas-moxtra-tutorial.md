---
title: 'Zelfstudie: Azure Active Directory-integratie met Moxtra | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Moxtra.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="0cb1e-103">Zelfstudie: Azure Active Directory-integratie met Moxtra</span><span class="sxs-lookup"><span data-stu-id="0cb1e-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="0cb1e-104">In deze zelfstudie leert u hoe toointegrate Moxtra met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0cb1e-104">In this tutorial, you learn how toointegrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0cb1e-105">Moxtra integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="0cb1e-105">Integrating Moxtra with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0cb1e-106">U kunt beheren in Azure AD die tooMoxtra toegang heeft</span><span class="sxs-lookup"><span data-stu-id="0cb1e-106">You can control in Azure AD who has access tooMoxtra</span></span>
- <span data-ttu-id="0cb1e-107">U kunt uw gebruikers tooautomatically get aangemelde tooMoxtra (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="0cb1e-107">You can enable your users tooautomatically get signed-on tooMoxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0cb1e-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="0cb1e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0cb1e-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0cb1e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cb1e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0cb1e-110">Prerequisites</span></span>

<span data-ttu-id="0cb1e-111">Azure AD-integratie met Moxtra tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="0cb1e-111">tooconfigure Azure AD integration with Moxtra, you need hello following items:</span></span>

- <span data-ttu-id="0cb1e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="0cb1e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0cb1e-113">Een Moxtra eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="0cb1e-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0cb1e-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0cb1e-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="0cb1e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0cb1e-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0cb1e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0cb1e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0cb1e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="0cb1e-118">Scenario description</span></span>
<span data-ttu-id="0cb1e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0cb1e-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="0cb1e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0cb1e-121">Het toevoegen van Moxtra van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0cb1e-121">Adding Moxtra from hello gallery</span></span>
2. <span data-ttu-id="0cb1e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0cb1e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-hello-gallery"></a><span data-ttu-id="0cb1e-123">Het toevoegen van Moxtra van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0cb1e-123">Adding Moxtra from hello gallery</span></span>
<span data-ttu-id="0cb1e-124">tooconfigure hello integratie van Moxtra in Azure AD, moet u tooadd Moxtra uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-124">tooconfigure hello integration of Moxtra into Azure AD, you need tooadd Moxtra from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0cb1e-125">**tooadd Moxtra via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0cb1e-125">**tooadd Moxtra from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cb1e-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0cb1e-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0cb1e-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="0cb1e-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="0cb1e-133">Typ in het zoekvak Hallo **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-133">In hello search box, type **Moxtra**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="0cb1e-135">Selecteer in het deelvenster resultaten hello, **Moxtra**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-135">In hello results panel, select **Moxtra**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0cb1e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0cb1e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0cb1e-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Moxtra op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0cb1e-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Moxtra is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Moxtra is tooa user in Azure AD.</span></span> <span data-ttu-id="0cb1e-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Moxtra toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-140">In other words, a link relationship between an Azure AD user and hello related user in Moxtra needs toobe established.</span></span>

<span data-ttu-id="0cb1e-141">Wijs in Moxtra, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-141">In Moxtra, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0cb1e-142">tooconfigure en eenmalige aanmelding Azure AD-test met Moxtra, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0cb1e-142">tooconfigure and test Azure AD single sign-on with Moxtra, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0cb1e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0cb1e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0cb1e-145">**[Maken van een testgebruiker Moxtra](#creating-a-moxtra-test-user)**  -toohave een equivalent van Britta Simon in Moxtra die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - toohave a counterpart of Britta Simon in Moxtra that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0cb1e-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0cb1e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0cb1e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="0cb1e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0cb1e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Moxtra configureren.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="0cb1e-150">**Azure AD tooconfigure eenmalige aanmelding met Moxtra, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0cb1e-150">**tooconfigure Azure AD single sign-on with Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cb1e-151">In de Azure-portal op Hallo Hallo **Moxtra** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-151">In hello Azure portal, on hello **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="0cb1e-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="0cb1e-155">Op Hallo **Moxtra domein en de URL's** sectie, voert u Hallo stap:</span><span class="sxs-lookup"><span data-stu-id="0cb1e-155">On hello **Moxtra Domain and URLs** section, perform hello following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="0cb1e-157">In Hallo **aanmeldings-URL** textbox, typ een URL als:`https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="0cb1e-157">In hello **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="0cb1e-158">Hallo SAML asserties verwacht Moxtra toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-158">Moxtra application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="0cb1e-159">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-159">Configure hello following claims for this application.</span></span> <span data-ttu-id="0cb1e-160">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-160">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="0cb1e-161">Hallo volgende Schermafbeelding toont een voorbeeld voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-161">hello following screenshot shows an example for this configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="0cb1e-163">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0cb1e-163">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="0cb1e-164">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="0cb1e-164">Attribute Name</span></span> | <span data-ttu-id="0cb1e-165">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="0cb1e-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="0cb1e-166">Voornaam</span><span class="sxs-lookup"><span data-stu-id="0cb1e-166">firstname</span></span> | <span data-ttu-id="0cb1e-167">User.givenName</span><span class="sxs-lookup"><span data-stu-id="0cb1e-167">user.givenname</span></span> |
    | <span data-ttu-id="0cb1e-168">Achternaam</span><span class="sxs-lookup"><span data-stu-id="0cb1e-168">lastname</span></span> | <span data-ttu-id="0cb1e-169">User.surname</span><span class="sxs-lookup"><span data-stu-id="0cb1e-169">user.surname</span></span> |
    | <span data-ttu-id="0cb1e-170">idpid</span><span class="sxs-lookup"><span data-stu-id="0cb1e-170">idpid</span></span>    | <span data-ttu-id="0cb1e-171">< SAML entiteit-ID ></span><span class="sxs-lookup"><span data-stu-id="0cb1e-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="0cb1e-172">waarde van Hallo **idpid** -kenmerk is niet echt.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-172">hello value of **idpid** attribute is not real.</span></span> <span data-ttu-id="0cb1e-173">U kunt de werkelijke waarde Hallo van opvragen **Naslaggids** onder sectie **Moxtra configuratie**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-173">You can get hello actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="0cb1e-174">a.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-174">a.</span></span> <span data-ttu-id="0cb1e-175">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="0cb1e-177">b.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-177">b.</span></span> <span data-ttu-id="0cb1e-178">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="0cb1e-180">c.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-180">c.</span></span> <span data-ttu-id="0cb1e-181">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="0cb1e-182">d.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-182">d.</span></span> <span data-ttu-id="0cb1e-183">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="0cb1e-184">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-184">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="0cb1e-186">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-186">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0cb1e-188">Op Hallo **Moxtra configuratie** sectie, klikt u op **configureren Moxtra** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-188">On hello **Moxtra Configuration** section, click **Configure Moxtra** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0cb1e-189">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="0cb1e-189">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="0cb1e-191">Een ander browservenster geopend Meld u aan bij tooyour Moxtra bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-191">In another browser window, sign on tooyour Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="0cb1e-192">Klik in de werkbalk aan de linkerkant Hallo Hallo op **-beheerconsole > SAML Single Sign-on**, en klik vervolgens op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-192">In hello toolbar on hello left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="0cb1e-194">Op Hallo **SAML** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0cb1e-194">On hello **SAML** page, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="0cb1e-196">a.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-196">a.</span></span> <span data-ttu-id="0cb1e-197">In Hallo **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: *SAML*).</span><span class="sxs-lookup"><span data-stu-id="0cb1e-197">In hello **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="0cb1e-198">b.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-198">b.</span></span> <span data-ttu-id="0cb1e-199">In Hallo **IdP entiteit-ID** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-199">In hello **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="0cb1e-200">c.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-200">c.</span></span> <span data-ttu-id="0cb1e-201">In **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-201">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="0cb1e-202">d.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-202">d.</span></span> <span data-ttu-id="0cb1e-203">In Hallo **AuthnContextClassRef** textbox type **urn: oasis: namen: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-203">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="0cb1e-204">e.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-204">e.</span></span> <span data-ttu-id="0cb1e-205">In Hallo **NameID indeling** textbox type **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-205">In hello **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="0cb1e-206">f.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-206">f.</span></span> <span data-ttu-id="0cb1e-207">Open certificaat dat u hebt gedownload vanuit Azure-portal in Kladblok Hallo inhoud kopieert en plakt u deze in Hallo **certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-207">Open certificate which you have downloaded from Azure portal in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="0cb1e-208">g.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-208">g.</span></span> <span data-ttu-id="0cb1e-209">Typ uw e-maildomein SAML in Hallo SAML e domein textbox.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-209">In hello SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="0cb1e-210">toosee hello stappen tooverify Hallo domein, klikt u op Hallo '**ik**' hieronder.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-210">toosee hello steps tooverify hello domain, click hello "**i**" below.</span></span>

    <span data-ttu-id="0cb1e-211">h.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-211">h.</span></span> <span data-ttu-id="0cb1e-212">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="0cb1e-213">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0cb1e-214">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0cb1e-215">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0cb1e-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0cb1e-216">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="0cb1e-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="0cb1e-217">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="0cb1e-219">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0cb1e-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cb1e-220">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0cb1e-222">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0cb1e-224">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0cb1e-226">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0cb1e-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0cb1e-228">a.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-228">a.</span></span> <span data-ttu-id="0cb1e-229">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0cb1e-230">b.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-230">b.</span></span> <span data-ttu-id="0cb1e-231">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0cb1e-232">c.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-232">c.</span></span> <span data-ttu-id="0cb1e-233">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0cb1e-234">d.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-234">d.</span></span> <span data-ttu-id="0cb1e-235">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="0cb1e-236">Een testgebruiker Moxtra maken</span><span class="sxs-lookup"><span data-stu-id="0cb1e-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="0cb1e-237">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Moxtra van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-237">hello objective of this section is toocreate a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="0cb1e-238">**een gebruiker Britta Simon aangeroepen in Moxtra, toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0cb1e-238">**toocreate a user called Britta Simon in Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cb1e-239">Meld u op tooyour Moxtra bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-239">Sign on tooyour Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="0cb1e-240">Klik in de werkbalk aan de linkerkant Hallo Hallo op **-beheerconsole > Gebruikersbeheer**, en vervolgens **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-240">In hello toolbar on hello left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="0cb1e-242">Op Hallo **gebruiker toevoegen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="0cb1e-242">On hello **Add User** dialog, perform hello following steps:</span></span>
  
    <span data-ttu-id="0cb1e-243">a.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-243">a.</span></span> <span data-ttu-id="0cb1e-244">In Hallo **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-244">In hello **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="0cb1e-245">b.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-245">b.</span></span> <span data-ttu-id="0cb1e-246">In Hallo **achternaam** textbox type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-246">In hello **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="0cb1e-247">c.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-247">c.</span></span> <span data-ttu-id="0cb1e-248">In Hallo **e** textbox type Britta van e-mailadres dezelfde als voor de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-248">In hello **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="0cb1e-249">d.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-249">d.</span></span> <span data-ttu-id="0cb1e-250">In Hallo **deling** textbox type **Dev**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-250">In hello **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="0cb1e-251">e.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-251">e.</span></span> <span data-ttu-id="0cb1e-252">In Hallo **afdeling** textbox type **IT**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-252">In hello **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="0cb1e-253">f.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-253">f.</span></span> <span data-ttu-id="0cb1e-254">Selecteer **beheerder**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="0cb1e-255">g.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-255">g.</span></span> <span data-ttu-id="0cb1e-256">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0cb1e-257">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cb1e-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0cb1e-258">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooMoxtra toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMoxtra.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="0cb1e-260">**tooassign Britta Simon tooMoxtra, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0cb1e-260">**tooassign Britta Simon tooMoxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cb1e-261">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="0cb1e-263">Selecteer in de lijst met de toepassingen van Hallo **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-263">In hello applications list, select **Moxtra**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="0cb1e-265">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="0cb1e-267">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-267">Click **Add** button.</span></span> <span data-ttu-id="0cb1e-268">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="0cb1e-270">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0cb1e-271">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0cb1e-272">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0cb1e-273">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0cb1e-273">Testing single sign-on</span></span>

<span data-ttu-id="0cb1e-274">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0cb1e-275">Als u op Hallo Moxtra tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Moxtra toepassing.</span><span class="sxs-lookup"><span data-stu-id="0cb1e-275">When you click hello Moxtra tile in hello Access Panel, you should get automatically signed-on tooyour Moxtra application.</span></span>
<span data-ttu-id="0cb1e-276">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0cb1e-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0cb1e-277">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="0cb1e-277">Additional resources</span></span>

* [<span data-ttu-id="0cb1e-278">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0cb1e-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0cb1e-279">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0cb1e-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

