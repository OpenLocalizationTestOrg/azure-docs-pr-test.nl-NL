---
title: 'Zelfstudie: Azure Active Directory-integratie met Igloo Software | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Igloo Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="29fa6-103">Zelfstudie: Azure Active Directory-integratie met Igloo Software</span><span class="sxs-lookup"><span data-stu-id="29fa6-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="29fa6-104">In deze zelfstudie leert u hoe toointegrate Igloo Software met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="29fa6-104">In this tutorial, you learn how toointegrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29fa6-105">Igloo Software integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="29fa6-105">Integrating Igloo Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="29fa6-106">U kunt beheren in Azure AD wie toegang tot tooIgloo Software heeft</span><span class="sxs-lookup"><span data-stu-id="29fa6-106">You can control in Azure AD who has access tooIgloo Software</span></span>
- <span data-ttu-id="29fa6-107">U kunt uw gebruikers tooautomatically get aangemelde tooIgloo Software (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="29fa6-107">You can enable your users tooautomatically get signed-on tooIgloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="29fa6-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="29fa6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="29fa6-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29fa6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29fa6-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="29fa6-110">Prerequisites</span></span>

<span data-ttu-id="29fa6-111">Azure AD-integratie met Igloo Software tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="29fa6-111">tooconfigure Azure AD integration with Igloo Software, you need hello following items:</span></span>

- <span data-ttu-id="29fa6-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="29fa6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="29fa6-113">Een Igloo Software eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="29fa6-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29fa6-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="29fa6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="29fa6-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="29fa6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="29fa6-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="29fa6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="29fa6-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29fa6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29fa6-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="29fa6-118">Scenario description</span></span>
<span data-ttu-id="29fa6-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="29fa6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29fa6-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="29fa6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29fa6-121">Het toevoegen van Igloo Software van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="29fa6-121">Adding Igloo Software from hello gallery</span></span>
2. <span data-ttu-id="29fa6-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="29fa6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-hello-gallery"></a><span data-ttu-id="29fa6-123">Het toevoegen van Igloo Software van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="29fa6-123">Adding Igloo Software from hello gallery</span></span>
<span data-ttu-id="29fa6-124">tooconfigure hello integratie van Igloo Software in Azure AD, moet u tooadd Igloo Software uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="29fa6-124">tooconfigure hello integration of Igloo Software into Azure AD, you need tooadd Igloo Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="29fa6-125">**tooadd Igloo Software uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="29fa6-125">**tooadd Igloo Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="29fa6-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="29fa6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="29fa6-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="29fa6-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="29fa6-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="29fa6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="29fa6-133">Typ in het zoekvak Hallo **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-133">In hello search box, type **Igloo Software**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="29fa6-135">Selecteer in het deelvenster resultaten hello, **Igloo Software**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="29fa6-135">In hello results panel, select **Igloo Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="29fa6-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="29fa6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="29fa6-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Igloo Software op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="29fa6-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="29fa6-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Igloo Software is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29fa6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Igloo Software is tooa user in Azure AD.</span></span> <span data-ttu-id="29fa6-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en het Hallo gerelateerde gebruiker in Software Igloo toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="29fa6-140">In other words, a link relationship between an Azure AD user and hello related user in Igloo Software needs toobe established.</span></span>

<span data-ttu-id="29fa6-141">In Igloo Software, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="29fa6-141">In Igloo Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="29fa6-142">tooconfigure en test eenmalige aanmelding Azure AD met Igloo Software, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="29fa6-142">tooconfigure and test Azure AD single sign-on with Igloo Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="29fa6-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="29fa6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="29fa6-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29fa6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29fa6-145">**[Maken van een testgebruiker Igloo Software](#creating-an-igloo-software-test-user)**  -toohave een equivalent van Britta Simon in Igloo-Software die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="29fa6-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - toohave a counterpart of Britta Simon in Igloo Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="29fa6-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="29fa6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29fa6-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="29fa6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="29fa6-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="29fa6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="29fa6-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="29fa6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="29fa6-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Igloo Software Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="29fa6-150">**tooconfigure Azure AD single sign-on with Igloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="29fa6-151">In de Azure-portal op Hallo Hallo **Igloo Software** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-151">In hello Azure portal, on hello **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="29fa6-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="29fa6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="29fa6-155">Op Hallo **Igloo Software domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="29fa6-155">On hello **Igloo Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="29fa6-157">a.</span><span class="sxs-lookup"><span data-stu-id="29fa6-157">a.</span></span> <span data-ttu-id="29fa6-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="29fa6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="29fa6-159">b.</span><span class="sxs-lookup"><span data-stu-id="29fa6-159">b.</span></span> <span data-ttu-id="29fa6-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="29fa6-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="29fa6-161">c.</span><span class="sxs-lookup"><span data-stu-id="29fa6-161">c.</span></span> <span data-ttu-id="29fa6-162">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="29fa6-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="29fa6-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="29fa6-163">These values are not real.</span></span> <span data-ttu-id="29fa6-164">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="29fa6-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="29fa6-165">Neem contact op met [Igloo Software Client ondersteuningsteam](https://www.igloosoftware.com/services/support) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="29fa6-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="29fa6-166">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="29fa6-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="29fa6-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="29fa6-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="29fa6-170">Op Hallo **Igloo softwareconfiguratie** sectie, klikt u op **Igloo Software configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="29fa6-170">On hello **Igloo Software Configuration** section, click **Configure Igloo Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="29fa6-171">Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="29fa6-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="29fa6-173">In een ander browservenster, meld u aan tooyour Igloo Software bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="29fa6-173">In a different web browser window, log in tooyour Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="29fa6-174">Ga toohello **Configuratiescherm**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-174">Go toohello **Control Panel**.</span></span>
   
     <span data-ttu-id="29fa6-175">![Het Configuratiescherm](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Configuratiescherm")</span><span class="sxs-lookup"><span data-stu-id="29fa6-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="29fa6-176">In Hallo **lidmaatschap** tabblad **aanmelding In instellingen**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-176">In hello **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="29fa6-177">![Meld u aan instellingen](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "instellingen aanmelden")</span><span class="sxs-lookup"><span data-stu-id="29fa6-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="29fa6-178">Klik in de configuratiesectie SAML hello, op **SAML-verificatie configureren**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-178">In hello SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="29fa6-179">![De SAML-configuratie](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML-configuratie")</span><span class="sxs-lookup"><span data-stu-id="29fa6-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="29fa6-180">In Hallo **algemene configuratie** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="29fa6-180">In hello **General Configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="29fa6-181">![Algemene configuratie](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "algemene configuratie")</span><span class="sxs-lookup"><span data-stu-id="29fa6-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="29fa6-182">a.</span><span class="sxs-lookup"><span data-stu-id="29fa6-182">a.</span></span> <span data-ttu-id="29fa6-183">In Hallo **verbindingsnaam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="29fa6-183">In hello **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="29fa6-184">b.</span><span class="sxs-lookup"><span data-stu-id="29fa6-184">b.</span></span> <span data-ttu-id="29fa6-185">In Hallo **IdP aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="29fa6-185">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="29fa6-186">c.</span><span class="sxs-lookup"><span data-stu-id="29fa6-186">c.</span></span> <span data-ttu-id="29fa6-187">In Hallo **IdP afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="29fa6-187">In hello **IdP Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="29fa6-188">d.</span><span class="sxs-lookup"><span data-stu-id="29fa6-188">d.</span></span> <span data-ttu-id="29fa6-189">Selecteer **afmelding antwoord en Type van de HTTP-aanvraag** als **POST**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="29fa6-190">e.</span><span class="sxs-lookup"><span data-stu-id="29fa6-190">e.</span></span> <span data-ttu-id="29fa6-191">Open uw **base 64-** gecodeerd certificaat in Kladblok gedownload vanuit Azure-portal kopie Hallo inhoud ervan naar het Klembord en plak deze toohello **openbaar certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="29fa6-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="29fa6-192">In Hallo **respons en de configuratie van verificatie**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="29fa6-192">In hello **Response and Authentication Configuration**, perform hello following steps:</span></span>
    
    <span data-ttu-id="29fa6-193">![Respons en de configuratie van verificatie](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "respons en de configuratie van verificatie")</span><span class="sxs-lookup"><span data-stu-id="29fa6-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="29fa6-194">a.</span><span class="sxs-lookup"><span data-stu-id="29fa6-194">a.</span></span> <span data-ttu-id="29fa6-195">Als **identiteitsprovider**, selecteer **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="29fa6-196">b.</span><span class="sxs-lookup"><span data-stu-id="29fa6-196">b.</span></span> <span data-ttu-id="29fa6-197">Als **id van het Type**, selecteer **e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="29fa6-198">c.</span><span class="sxs-lookup"><span data-stu-id="29fa6-198">c.</span></span> <span data-ttu-id="29fa6-199">In Hallo **e kenmerk** textbox type **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-199">In hello **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="29fa6-200">d.</span><span class="sxs-lookup"><span data-stu-id="29fa6-200">d.</span></span> <span data-ttu-id="29fa6-201">In Hallo **voornaam kenmerk** textbox type **givenname**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-201">In hello **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="29fa6-202">e.</span><span class="sxs-lookup"><span data-stu-id="29fa6-202">e.</span></span> <span data-ttu-id="29fa6-203">In Hallo **laatste naamkenmerk** textbox type **achternaam**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-203">In hello **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="29fa6-204">Hallo te volgen stappen toocomplete Hallo configuratie uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="29fa6-204">Perform hello following steps toocomplete hello configuration:</span></span>
    
    <span data-ttu-id="29fa6-205">![Het maken van de gebruiker op aanmelden](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "aanmaken op aanmelding gebruiker")</span><span class="sxs-lookup"><span data-stu-id="29fa6-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="29fa6-206">a.</span><span class="sxs-lookup"><span data-stu-id="29fa6-206">a.</span></span> <span data-ttu-id="29fa6-207">Als **aanmaken op aanmelding gebruiker**, selecteer **Maak een nieuwe gebruiker in uw site wanneer ze zich aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="29fa6-208">b.</span><span class="sxs-lookup"><span data-stu-id="29fa6-208">b.</span></span> <span data-ttu-id="29fa6-209">Als **aanmelden instellingen**, selecteer **gebruik SAML-knop op het scherm 'Aanmelden'**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="29fa6-210">c.</span><span class="sxs-lookup"><span data-stu-id="29fa6-210">c.</span></span> <span data-ttu-id="29fa6-211">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="29fa6-212">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="29fa6-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="29fa6-213">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="29fa6-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="29fa6-214">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="29fa6-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="29fa6-215">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="29fa6-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="29fa6-216">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="29fa6-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="29fa6-218">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="29fa6-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="29fa6-219">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="29fa6-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="29fa6-221">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="29fa6-223">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="29fa6-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="29fa6-225">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="29fa6-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="29fa6-227">a.</span><span class="sxs-lookup"><span data-stu-id="29fa6-227">a.</span></span> <span data-ttu-id="29fa6-228">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29fa6-229">b.</span><span class="sxs-lookup"><span data-stu-id="29fa6-229">b.</span></span> <span data-ttu-id="29fa6-230">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="29fa6-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="29fa6-231">c.</span><span class="sxs-lookup"><span data-stu-id="29fa6-231">c.</span></span> <span data-ttu-id="29fa6-232">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="29fa6-233">d.</span><span class="sxs-lookup"><span data-stu-id="29fa6-233">d.</span></span> <span data-ttu-id="29fa6-234">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="29fa6-235">Een testgebruiker Igloo Software maken</span><span class="sxs-lookup"><span data-stu-id="29fa6-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="29fa6-236">Er is geen actie-item voor u tooconfigure gebruikers inrichten tooIgloo Software.</span><span class="sxs-lookup"><span data-stu-id="29fa6-236">There is no action item for you tooconfigure user provisioning tooIgloo Software.</span></span>  

<span data-ttu-id="29fa6-237">Wanneer een toegewezen gebruiker probeert toolog in tooIgloo Hallo-paneel voor apptoegang, Igloo Software met Software controleert of de gebruiker Hallo bestaat.</span><span class="sxs-lookup"><span data-stu-id="29fa6-237">When an assigned user tries toolog in tooIgloo Software using hello access panel, Igloo Software checks whether hello user exists.</span></span>  <span data-ttu-id="29fa6-238">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="29fa6-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="29fa6-239">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="29fa6-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="29fa6-240">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooIgloo Software.</span><span class="sxs-lookup"><span data-stu-id="29fa6-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIgloo Software.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="29fa6-242">**tooassign Britta Simon tooIgloo Software, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="29fa6-242">**tooassign Britta Simon tooIgloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="29fa6-243">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="29fa6-245">Selecteer in de lijst met de toepassingen van Hallo **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-245">In hello applications list, select **Igloo Software**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="29fa6-247">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="29fa6-249">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="29fa6-249">Click **Add** button.</span></span> <span data-ttu-id="29fa6-250">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="29fa6-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="29fa6-252">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="29fa6-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="29fa6-253">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="29fa6-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="29fa6-254">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="29fa6-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="29fa6-255">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="29fa6-255">Testing single sign-on</span></span>

<span data-ttu-id="29fa6-256">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="29fa6-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="29fa6-257">Als u op Hallo Igloo Software tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Igloo softwaretoepassing.</span><span class="sxs-lookup"><span data-stu-id="29fa6-257">When you click hello Igloo Software tile in hello Access Panel, you should get automatically signed-on tooyour Igloo Software application.</span></span>
<span data-ttu-id="29fa6-258">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="29fa6-258">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="29fa6-259">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="29fa6-259">Additional resources</span></span>

* [<span data-ttu-id="29fa6-260">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29fa6-260">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29fa6-261">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="29fa6-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

