---
title: 'Zelfstudie: Azure Active Directory-integratie met Samanage | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Samanage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="e8353-103">Zelfstudie: Azure Active Directory-integratie met Samanage</span><span class="sxs-lookup"><span data-stu-id="e8353-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="e8353-104">In deze zelfstudie leert u hoe toointegrate Samanage met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e8353-104">In this tutorial, you learn how toointegrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e8353-105">Samanage integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e8353-105">Integrating Samanage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e8353-106">U kunt beheren in Azure AD die tooSamanage toegang heeft</span><span class="sxs-lookup"><span data-stu-id="e8353-106">You can control in Azure AD who has access tooSamanage</span></span>
- <span data-ttu-id="e8353-107">U kunt uw gebruikers tooautomatically get aangemelde tooSamanage (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="e8353-107">You can enable your users tooautomatically get signed-on tooSamanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e8353-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e8353-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e8353-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e8353-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8353-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e8353-110">Prerequisites</span></span>

<span data-ttu-id="e8353-111">Azure AD-integratie met Samanage tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="e8353-111">tooconfigure Azure AD integration with Samanage, you need hello following items:</span></span>

- <span data-ttu-id="e8353-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e8353-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e8353-113">Een Samanage eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e8353-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e8353-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e8353-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e8353-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e8353-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e8353-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e8353-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e8353-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e8353-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e8353-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e8353-118">Scenario description</span></span>
<span data-ttu-id="e8353-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e8353-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e8353-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e8353-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e8353-121">Het toevoegen van Samanage van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e8353-121">Adding Samanage from hello gallery</span></span>
2. <span data-ttu-id="e8353-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e8353-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-hello-gallery"></a><span data-ttu-id="e8353-123">Het toevoegen van Samanage van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e8353-123">Adding Samanage from hello gallery</span></span>
<span data-ttu-id="e8353-124">tooconfigure hello integratie van Samanage in Azure AD, moet u tooadd Samanage uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e8353-124">tooconfigure hello integration of Samanage into Azure AD, you need tooadd Samanage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e8353-125">**tooadd Samanage via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e8353-125">**tooadd Samanage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8353-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e8353-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e8353-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e8353-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e8353-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e8353-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e8353-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e8353-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e8353-133">Typ in het zoekvak Hallo **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="e8353-133">In hello search box, type **Samanage**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="e8353-135">Selecteer in het deelvenster resultaten hello, **Samanage**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e8353-135">In hello results panel, select **Samanage**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e8353-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e8353-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e8353-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Samanage op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="e8353-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e8353-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Samanage is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8353-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Samanage is tooa user in Azure AD.</span></span> <span data-ttu-id="e8353-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Samanage toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="e8353-140">In other words, a link relationship between an Azure AD user and hello related user in Samanage needs toobe established.</span></span>

<span data-ttu-id="e8353-141">Wijs in Samanage, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="e8353-141">In Samanage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e8353-142">tooconfigure en eenmalige aanmelding Azure AD-test met Samanage, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e8353-142">tooconfigure and test Azure AD single sign-on with Samanage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e8353-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="e8353-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e8353-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e8353-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e8353-145">**[Maken van een testgebruiker Samanage](#creating-a-samanage-test-user)**  -toohave een equivalent van Britta Simon in Samanage die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e8353-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - toohave a counterpart of Britta Simon in Samanage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e8353-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e8353-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e8353-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e8353-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e8353-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e8353-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e8353-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Samanage configureren.</span><span class="sxs-lookup"><span data-stu-id="e8353-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="e8353-150">**Azure AD tooconfigure eenmalige aanmelding met Samanage, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e8353-150">**tooconfigure Azure AD single sign-on with Samanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8353-151">In de Azure-portal op Hallo Hallo **Samanage** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e8353-151">In hello Azure portal, on hello **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e8353-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e8353-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="e8353-155">Op Hallo **Samanage domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e8353-155">On hello **Samanage Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="e8353-157">a.</span><span class="sxs-lookup"><span data-stu-id="e8353-157">a.</span></span> <span data-ttu-id="e8353-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<Company Name>.samanage.com/saml_login/<Company Name>`</span><span class="sxs-lookup"><span data-stu-id="e8353-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="e8353-159">b.</span><span class="sxs-lookup"><span data-stu-id="e8353-159">b.</span></span> <span data-ttu-id="e8353-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="e8353-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e8353-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="e8353-161">These values are not real.</span></span> <span data-ttu-id="e8353-162">Deze waarden bijwerken met Hallo werkelijke aanmeldings-URL en de id, die verderop in Hallo zelfstudie wordt uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="e8353-162">Update these values with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> <span data-ttu-id="e8353-163">Voor meer informatie contact op met [Samanage Client ondersteuningsteam](https://www.samanage.com/support).</span><span class="sxs-lookup"><span data-stu-id="e8353-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="e8353-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e8353-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="e8353-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e8353-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e8353-168">Op Hallo **Samanage configuratie** sectie, klikt u op **configureren Samanage** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="e8353-168">On hello **Samanage Configuration** section, click **Configure Samanage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e8353-169">Kopiëren Hallo **Sign-Out-URL en de entiteit-ID SAML** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="e8353-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="e8353-171">In een ander browservenster, meld u bij uw bedrijf Samanage site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e8353-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="e8353-172">Klik op **Dashboard** en selecteer **Setup** in het navigatiedeelvenster links.</span><span class="sxs-lookup"><span data-stu-id="e8353-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="e8353-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span><span class="sxs-lookup"><span data-stu-id="e8353-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="e8353-174">Klik op **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="e8353-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="e8353-175">![Eenmalige aanmelding](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="e8353-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="e8353-176">Navigeer te**aanmelding via SAML** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e8353-176">Navigate too**Login using SAML** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e8353-177">![Aanmelding via SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "aanmelding via SAML")</span><span class="sxs-lookup"><span data-stu-id="e8353-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="e8353-178">a.</span><span class="sxs-lookup"><span data-stu-id="e8353-178">a.</span></span> <span data-ttu-id="e8353-179">Klik op **eenmalige aanmelding met SAML inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="e8353-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="e8353-180">b.</span><span class="sxs-lookup"><span data-stu-id="e8353-180">b.</span></span> <span data-ttu-id="e8353-181">In Hallo **identiteit Provider URL** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e8353-181">In hello **Identity Provider URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="e8353-182">c.</span><span class="sxs-lookup"><span data-stu-id="e8353-182">c.</span></span> <span data-ttu-id="e8353-183">Hallo bevestigen **aanmeldings-URL** komt overeen met Hallo **aanmelding op URL** van **Samanage domein en de URL's** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e8353-183">Confirm hello **Login URL** matches hello **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="e8353-184">d.</span><span class="sxs-lookup"><span data-stu-id="e8353-184">d.</span></span> <span data-ttu-id="e8353-185">In Hallo **afmelding URL** textbox Hallo waarde **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e8353-185">In hello **Logout URL** textbox, enter hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="e8353-186">e.</span><span class="sxs-lookup"><span data-stu-id="e8353-186">e.</span></span> <span data-ttu-id="e8353-187">In Hallo **SAML verlener** textbox type Hallo app id URI instellen in de id-provider.</span><span class="sxs-lookup"><span data-stu-id="e8353-187">In hello **SAML Issuer** textbox, type hello app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="e8353-188">f.</span><span class="sxs-lookup"><span data-stu-id="e8353-188">f.</span></span> <span data-ttu-id="e8353-189">Open uw base-64 gecodeerde certificaat gedownload vanuit Azure-portal in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **plak uw id-Provider-x.509-certificaat onderstaande** textbox.</span><span class="sxs-lookup"><span data-stu-id="e8353-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="e8353-190">g.</span><span class="sxs-lookup"><span data-stu-id="e8353-190">g.</span></span> <span data-ttu-id="e8353-191">Klik op **gebruikers maken als ze bestaan niet in Samanage**.</span><span class="sxs-lookup"><span data-stu-id="e8353-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="e8353-192">h.</span><span class="sxs-lookup"><span data-stu-id="e8353-192">h.</span></span> <span data-ttu-id="e8353-193">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="e8353-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="e8353-194">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="e8353-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e8353-195">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="e8353-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e8353-196">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e8353-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e8353-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e8353-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="e8353-198">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e8353-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e8353-200">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e8353-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8353-201">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e8353-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e8353-203">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e8353-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e8353-205">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="e8353-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e8353-207">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e8353-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e8353-209">a.</span><span class="sxs-lookup"><span data-stu-id="e8353-209">a.</span></span> <span data-ttu-id="e8353-210">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e8353-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e8353-211">b.</span><span class="sxs-lookup"><span data-stu-id="e8353-211">b.</span></span> <span data-ttu-id="e8353-212">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e8353-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e8353-213">c.</span><span class="sxs-lookup"><span data-stu-id="e8353-213">c.</span></span> <span data-ttu-id="e8353-214">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e8353-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e8353-215">d.</span><span class="sxs-lookup"><span data-stu-id="e8353-215">d.</span></span> <span data-ttu-id="e8353-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e8353-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="e8353-217">Een testgebruiker Samanage maken</span><span class="sxs-lookup"><span data-stu-id="e8353-217">Creating a Samanage test user</span></span>

<span data-ttu-id="e8353-218">Azure AD tooenable gebruikers toolog in tooSamanage, ze in Samanage moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="e8353-218">tooenable Azure AD users toolog in tooSamanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="e8353-219">In geval van Samanage Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="e8353-219">In hello case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="e8353-220">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e8353-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8353-221">Meld u aan bij uw bedrijf Samanage site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e8353-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="e8353-222">Klik op **Dashboard** en selecteer **Setup** in het linkernavigatievenster pan.</span><span class="sxs-lookup"><span data-stu-id="e8353-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="e8353-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="e8353-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="e8353-224">Klik op Hallo **gebruikers** tabblad</span><span class="sxs-lookup"><span data-stu-id="e8353-224">Click hello **Users** tab</span></span>
   
    <span data-ttu-id="e8353-225">![Gebruikers](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="e8353-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="e8353-226">Klik op **nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="e8353-226">Click **New User**.</span></span>
   
    <span data-ttu-id="e8353-227">![Nieuwe gebruiker](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="e8353-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="e8353-228">Type Hallo **naam** en Hallo **e-mailadres** van een Azure Active Directory-account u wilt tooprovision en op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="e8353-228">Type hello **Name** and hello **Email Address** of an Azure Active Directory account you want tooprovision and click **Create user**.</span></span>
   
    <span data-ttu-id="e8353-229">![Gebruiker maken](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="e8353-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="e8353-230">Hello Azure Active Directory-accounthouder wordt een e-mailbericht ontvangen en volg een koppeling tooconfirm hun account maken voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="e8353-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="e8353-231">U kunt andere Samanage gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Samanage tooprovision Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="e8353-231">You can use any other Samanage user account creation tools or APIs provided by Samanage tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e8353-232">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8353-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e8353-233">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSamanage toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="e8353-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSamanage.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e8353-235">**tooassign Britta Simon tooSamanage, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e8353-235">**tooassign Britta Simon tooSamanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8353-236">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e8353-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e8353-238">Selecteer in de lijst met de toepassingen van Hallo **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="e8353-238">In hello applications list, select **Samanage**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="e8353-240">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e8353-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e8353-242">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e8353-242">Click **Add** button.</span></span> <span data-ttu-id="e8353-243">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e8353-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e8353-245">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="e8353-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e8353-246">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e8353-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e8353-247">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e8353-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e8353-248">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e8353-248">Testing single sign-on</span></span>

<span data-ttu-id="e8353-249">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e8353-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e8353-250">Als u op Hallo Samanage tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Samanage toepassing.</span><span class="sxs-lookup"><span data-stu-id="e8353-250">When you click hello Samanage tile in hello Access Panel, you should get automatically signed-on tooyour Samanage application.</span></span>
<span data-ttu-id="e8353-251">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e8353-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e8353-252">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e8353-252">Additional resources</span></span>

* [<span data-ttu-id="e8353-253">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e8353-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e8353-254">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e8353-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

