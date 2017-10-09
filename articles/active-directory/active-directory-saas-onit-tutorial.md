---
title: 'Zelfstudie: Azure Active Directory-integratie met Onit | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Onit.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 9e12449e5bf7f169b3cadfaa12438ac5d52ed8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="e58c8-103">Zelfstudie: Azure Active Directory-integratie met Onit</span><span class="sxs-lookup"><span data-stu-id="e58c8-103">Tutorial: Azure Active Directory integration with Onit</span></span>

<span data-ttu-id="e58c8-104">In deze zelfstudie leert u hoe toointegrate Onit met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e58c8-104">In this tutorial, you learn how toointegrate Onit with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e58c8-105">Onit integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e58c8-105">Integrating Onit with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e58c8-106">U kunt beheren in Azure AD die tooOnit toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="e58c8-106">You can control in Azure AD who has access tooOnit.</span></span>
- <span data-ttu-id="e58c8-107">U kunt uw gebruikers tooautomatically get aangemelde tooOnit (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e58c8-107">You can enable your users tooautomatically get signed-on tooOnit (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e58c8-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="e58c8-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e58c8-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e58c8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e58c8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e58c8-110">Prerequisites</span></span>

<span data-ttu-id="e58c8-111">Azure AD-integratie met Onit tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="e58c8-111">tooconfigure Azure AD integration with Onit, you need hello following items:</span></span>

- <span data-ttu-id="e58c8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e58c8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e58c8-113">Een Onit eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e58c8-113">An Onit single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e58c8-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e58c8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e58c8-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e58c8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e58c8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e58c8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e58c8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e58c8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e58c8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e58c8-118">Scenario description</span></span>

<span data-ttu-id="e58c8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e58c8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e58c8-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e58c8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e58c8-121">Het toevoegen van Onit van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e58c8-121">Adding Onit from hello gallery</span></span>
2. <span data-ttu-id="e58c8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e58c8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onit-from-hello-gallery"></a><span data-ttu-id="e58c8-123">Het toevoegen van Onit van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e58c8-123">Adding Onit from hello gallery</span></span>
<span data-ttu-id="e58c8-124">tooconfigure hello integratie van Onit in Azure AD, moet u tooadd Onit uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e58c8-124">tooconfigure hello integration of Onit into Azure AD, you need tooadd Onit from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e58c8-125">**tooadd Onit via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e58c8-125">**tooadd Onit from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e58c8-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e58c8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="e58c8-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e58c8-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="e58c8-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e58c8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="e58c8-133">Typ in het zoekvak Hallo **Onit**, selecteer **Onit** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e58c8-133">In hello search box, type **Onit**, select **Onit** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Onit in de lijst met resultaten Hallo](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e58c8-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58c8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e58c8-136">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Onit op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="e58c8-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e58c8-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Onit is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e58c8-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Onit is tooa user in Azure AD.</span></span> <span data-ttu-id="e58c8-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Onit toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="e58c8-138">In other words, a link relationship between an Azure AD user and hello related user in Onit needs toobe established.</span></span>

<span data-ttu-id="e58c8-139">Wijs in Onit, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="e58c8-139">In Onit, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e58c8-140">tooconfigure en eenmalige aanmelding Azure AD-test met Onit, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e58c8-140">tooconfigure and test Azure AD single sign-on with Onit, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e58c8-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="e58c8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e58c8-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e58c8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e58c8-143">**[Maken van een testgebruiker Onit](#create-an-onit-test-user)**  -toohave een equivalent van Britta Simon in Onit die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e58c8-143">**[Create an Onit test user](#create-an-onit-test-user)** - toohave a counterpart of Britta Simon in Onit that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e58c8-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e58c8-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e58c8-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e58c8-145">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e58c8-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e58c8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e58c8-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Onit configureren.</span><span class="sxs-lookup"><span data-stu-id="e58c8-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Onit application.</span></span>

<span data-ttu-id="e58c8-148">**Azure AD tooconfigure eenmalige aanmelding met Onit, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e58c8-148">**tooconfigure Azure AD single sign-on with Onit, perform hello following steps:**</span></span>

1. <span data-ttu-id="e58c8-149">In de Azure-portal op Hallo Hallo **Onit** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-149">In hello Azure portal, on hello **Onit** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e58c8-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e58c8-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. <span data-ttu-id="e58c8-153">Op Hallo **Onit domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e58c8-153">On hello **Onit Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en Onit domein eenmalige aanmelding informatie](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    <span data-ttu-id="e58c8-155">a.</span><span class="sxs-lookup"><span data-stu-id="e58c8-155">a.</span></span> <span data-ttu-id="e58c8-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="e58c8-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    <span data-ttu-id="e58c8-157">b.</span><span class="sxs-lookup"><span data-stu-id="e58c8-157">b.</span></span> <span data-ttu-id="e58c8-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="e58c8-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e58c8-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="e58c8-159">These values are not real.</span></span> <span data-ttu-id="e58c8-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="e58c8-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e58c8-161">Neem contact op met [Onit Client ondersteuningsteam](https://www.onit.com/support) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="e58c8-161">Contact [Onit Client support team](https://www.onit.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="e58c8-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="e58c8-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. <span data-ttu-id="e58c8-164">Hallo SAML asserties verwacht Onit toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="e58c8-164">Onit application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="e58c8-165">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="e58c8-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="e58c8-166">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **'Atrribute'** tabblad van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="e58c8-166">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="e58c8-167">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="e58c8-167">hello following screenshot shows an example for this.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. <span data-ttu-id="e58c8-169">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e58c8-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="e58c8-170">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="e58c8-170">Attribute Name</span></span> | <span data-ttu-id="e58c8-171">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="e58c8-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="e58c8-172">E-mail</span><span class="sxs-lookup"><span data-stu-id="e58c8-172">email</span></span> | <span data-ttu-id="e58c8-173">User.mail</span><span class="sxs-lookup"><span data-stu-id="e58c8-173">user.mail</span></span> |
    
    <span data-ttu-id="e58c8-174">a.</span><span class="sxs-lookup"><span data-stu-id="e58c8-174">a.</span></span> <span data-ttu-id="e58c8-175">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e58c8-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="e58c8-178">b.</span><span class="sxs-lookup"><span data-stu-id="e58c8-178">b.</span></span> <span data-ttu-id="e58c8-179">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="e58c8-179">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="e58c8-180">c.</span><span class="sxs-lookup"><span data-stu-id="e58c8-180">c.</span></span> <span data-ttu-id="e58c8-181">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="e58c8-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="e58c8-182">d.</span><span class="sxs-lookup"><span data-stu-id="e58c8-182">d.</span></span> <span data-ttu-id="e58c8-183">Hallo laat **Namespace** leeg.</span><span class="sxs-lookup"><span data-stu-id="e58c8-183">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="e58c8-184">e.</span><span class="sxs-lookup"><span data-stu-id="e58c8-184">e.</span></span> <span data-ttu-id="e58c8-185">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-185">Click **Ok**.</span></span>

7. <span data-ttu-id="e58c8-186">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e58c8-186">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e58c8-188">Op Hallo **Onit configuratie** sectie, klikt u op **configureren Onit** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="e58c8-188">On hello **Onit Configuration** section, click **Configure Onit** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e58c8-189">Kopiëren Hallo **Sign-Out-URL, SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="e58c8-189">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Onit configuratie](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. <span data-ttu-id="e58c8-191">In een ander browservenster, meld u bij uw bedrijf Onit site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e58c8-191">In a different web browser window, log into your Onit company site as an administrator.</span></span>

10. <span data-ttu-id="e58c8-192">Klik in het menu bovenaan Hallo Hallo **beheer**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-192">In hello menu on hello top, click **Administration**.</span></span>
   
   <span data-ttu-id="e58c8-193">![Beheer](./media/active-directory-saas-onit-tutorial/IC791174.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="e58c8-193">![Administration](./media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span></span>
11. <span data-ttu-id="e58c8-194">Klik op **bewerken Corporation**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-194">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="e58c8-195">![Bewerken Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Corporation bewerken")</span><span class="sxs-lookup"><span data-stu-id="e58c8-195">![Edit Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span></span>
   
12. <span data-ttu-id="e58c8-196">Klik op Hallo **beveiliging** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e58c8-196">Click hello **Security** tab.</span></span>
    
    <span data-ttu-id="e58c8-197">![Bedrijfsgegevens bewerken](./media/active-directory-saas-onit-tutorial/IC791176.png "bedrijfsgegevens bewerken")</span><span class="sxs-lookup"><span data-stu-id="e58c8-197">![Edit Company Information](./media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span></span>

13. <span data-ttu-id="e58c8-198">Op Hallo **beveiliging** tabblad, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e58c8-198">On hello **Security** tab, perform hello following steps:</span></span>

    <span data-ttu-id="e58c8-199">![Eenmalige aanmelding](./media/active-directory-saas-onit-tutorial/IC791177.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="e58c8-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span></span>

    <span data-ttu-id="e58c8-200">a.</span><span class="sxs-lookup"><span data-stu-id="e58c8-200">a.</span></span> <span data-ttu-id="e58c8-201">Als **Verificatiestrategie**, selecteer **eenmalige aanmelding en het wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
    
    <span data-ttu-id="e58c8-202">b.</span><span class="sxs-lookup"><span data-stu-id="e58c8-202">b.</span></span> <span data-ttu-id="e58c8-203">In **Idp doel-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e58c8-203">In **Idp Target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e58c8-204">c.</span><span class="sxs-lookup"><span data-stu-id="e58c8-204">c.</span></span> <span data-ttu-id="e58c8-205">In **Idp afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e58c8-205">In **Idp logout URL** textbox, paste hello value of  **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e58c8-206">d.</span><span class="sxs-lookup"><span data-stu-id="e58c8-206">d.</span></span> <span data-ttu-id="e58c8-207">In **Idp Cert vingerafdruk (SHA1)** textbox plakken Hallo **vingerafdruk** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e58c8-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste hello  **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="e58c8-208">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="e58c8-208">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e58c8-209">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="e58c8-209">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e58c8-210">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e58c8-210">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e58c8-211">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e58c8-211">Create an Azure AD test user</span></span>

<span data-ttu-id="e58c8-212">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e58c8-212">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="e58c8-214">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e58c8-214">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e58c8-215">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="e58c8-215">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e58c8-217">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-217">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e58c8-219">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e58c8-219">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e58c8-221">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e58c8-221">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e58c8-223">a.</span><span class="sxs-lookup"><span data-stu-id="e58c8-223">a.</span></span> <span data-ttu-id="e58c8-224">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-224">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e58c8-225">b.</span><span class="sxs-lookup"><span data-stu-id="e58c8-225">b.</span></span> <span data-ttu-id="e58c8-226">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="e58c8-226">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e58c8-227">c.</span><span class="sxs-lookup"><span data-stu-id="e58c8-227">c.</span></span> <span data-ttu-id="e58c8-228">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="e58c8-228">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e58c8-229">d.</span><span class="sxs-lookup"><span data-stu-id="e58c8-229">d.</span></span> <span data-ttu-id="e58c8-230">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-230">Click **Create**.</span></span>
 
### <a name="create-an-onit-test-user"></a><span data-ttu-id="e58c8-231">Een testgebruiker Onit maken</span><span class="sxs-lookup"><span data-stu-id="e58c8-231">Create an Onit test user</span></span>

<span data-ttu-id="e58c8-232">In de volgorde tooenable Azure AD gebruikers toolog in Onit, moeten ze worden ingericht in Onit.</span><span class="sxs-lookup"><span data-stu-id="e58c8-232">In order tooenable Azure AD users toolog into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="e58c8-233">In geval van Onit Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="e58c8-233">In hello case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="e58c8-234">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e58c8-234">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="e58c8-235">Meld u aan bij tooyour **Onit** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e58c8-235">Sign on tooyour **Onit** company site as an administrator.</span></span>
2. <span data-ttu-id="e58c8-236">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-236">Click **Add User**.</span></span>
   
   <span data-ttu-id="e58c8-237">![Beheer](./media/active-directory-saas-onit-tutorial/IC791180.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="e58c8-237">![Administration](./media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span></span>
3. <span data-ttu-id="e58c8-238">Op Hallo **gebruiker toevoegen** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e58c8-238">On hello **Add User** dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="e58c8-239">![Gebruiker toevoegen](./media/active-directory-saas-onit-tutorial/IC791181.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="e58c8-239">![Add User](./media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="e58c8-240">Type Hallo **naam** en Hallo **e-mailadres** van een geldig Azure tekstvakken met betrekking tot AD-account u wilt dat tooprovision in Hallo.</span><span class="sxs-lookup"><span data-stu-id="e58c8-240">Type hello **Name** and hello **Email Address** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>
  2. <span data-ttu-id="e58c8-241">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-241">Click **Create**.</span></span>    
   
 > [!NOTE]
 > <span data-ttu-id="e58c8-242">Hello Azure Active Directory-accounthouder ontvangt een e-mailbericht en een koppeling tooconfirm volgt hun account voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="e58c8-242">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e58c8-243">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e58c8-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e58c8-244">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooOnit toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="e58c8-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOnit.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="e58c8-246">**tooassign Britta Simon tooOnit, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e58c8-246">**tooassign Britta Simon tooOnit, perform hello following steps:**</span></span>

1. <span data-ttu-id="e58c8-247">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e58c8-249">Selecteer in de lijst met de toepassingen van Hallo **Onit**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-249">In hello applications list, select **Onit**.</span></span>

    ![Hallo Onit koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. <span data-ttu-id="e58c8-251">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="e58c8-253">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e58c8-253">Click **Add** button.</span></span> <span data-ttu-id="e58c8-254">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e58c8-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="e58c8-256">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="e58c8-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e58c8-257">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e58c8-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e58c8-258">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e58c8-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e58c8-259">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e58c8-259">Test single sign-on</span></span>

<span data-ttu-id="e58c8-260">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e58c8-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e58c8-261">Als u op Hallo Onit tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Onit toepassing.</span><span class="sxs-lookup"><span data-stu-id="e58c8-261">When you click hello Onit tile in hello Access Panel, you should get automatically signed-on tooyour Onit application.</span></span>
<span data-ttu-id="e58c8-262">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e58c8-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e58c8-263">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e58c8-263">Additional resources</span></span>

* [<span data-ttu-id="e58c8-264">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e58c8-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e58c8-265">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e58c8-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png

