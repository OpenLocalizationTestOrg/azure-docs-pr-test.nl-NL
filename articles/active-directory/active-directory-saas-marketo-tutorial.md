---
title: 'Zelfstudie: Azure Active Directory-integratie met Marketo | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Marketo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="94331-103">Zelfstudie: Azure Active Directory-integratie met Marketo</span><span class="sxs-lookup"><span data-stu-id="94331-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="94331-104">In deze zelfstudie leert u hoe toointegrate Marketo met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94331-104">In this tutorial, you learn how toointegrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94331-105">Marketo integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="94331-105">Integrating Marketo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="94331-106">U kunt beheren in Azure AD die tooMarketo toegang heeft</span><span class="sxs-lookup"><span data-stu-id="94331-106">You can control in Azure AD who has access tooMarketo</span></span>
- <span data-ttu-id="94331-107">U kunt uw gebruikers tooautomatically get aangemelde tooMarketo (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="94331-107">You can enable your users tooautomatically get signed-on tooMarketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="94331-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="94331-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="94331-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="94331-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94331-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="94331-110">Prerequisites</span></span>

<span data-ttu-id="94331-111">Azure AD-integratie met Marketo tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="94331-111">tooconfigure Azure AD integration with Marketo, you need hello following items:</span></span>

- <span data-ttu-id="94331-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="94331-112">An Azure AD subscription</span></span>
- <span data-ttu-id="94331-113">Een Marketo-eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="94331-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="94331-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="94331-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="94331-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="94331-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94331-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="94331-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="94331-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94331-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="94331-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="94331-118">Scenario description</span></span>
<span data-ttu-id="94331-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="94331-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94331-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="94331-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94331-121">Het toevoegen van Marketo van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="94331-121">Adding Marketo from hello gallery</span></span>
2. <span data-ttu-id="94331-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="94331-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-hello-gallery"></a><span data-ttu-id="94331-123">Het toevoegen van Marketo van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="94331-123">Adding Marketo from hello gallery</span></span>
<span data-ttu-id="94331-124">tooconfigure hello integratie van Marketo in Azure AD, moet u tooadd Marketo uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="94331-124">tooconfigure hello integration of Marketo into Azure AD, you need tooadd Marketo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="94331-125">**tooadd Marketo via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="94331-125">**tooadd Marketo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="94331-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="94331-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="94331-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="94331-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="94331-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="94331-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="94331-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="94331-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="94331-133">Typ in het zoekvak Hallo **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="94331-133">In hello search box, type **Marketo**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="94331-135">Selecteer in het deelvenster resultaten hello, **Marketo**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="94331-135">In hello results panel, select **Marketo**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="94331-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="94331-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="94331-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Marketo op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="94331-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="94331-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Marketo is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94331-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Marketo is tooa user in Azure AD.</span></span> <span data-ttu-id="94331-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Marketo toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="94331-140">In other words, a link relationship between an Azure AD user and hello related user in Marketo needs toobe established.</span></span>

<span data-ttu-id="94331-141">Wijs in Marketo Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="94331-141">In Marketo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="94331-142">tooconfigure en eenmalige aanmelding Azure AD-test met Marketo, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="94331-142">tooconfigure and test Azure AD single sign-on with Marketo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="94331-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="94331-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="94331-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="94331-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="94331-145">**[Maken van een testgebruiker Marketo](#creating-a-marketo-test-user)**  -toohave een equivalent van Britta Simon in Marketo die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="94331-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - toohave a counterpart of Britta Simon in Marketo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="94331-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="94331-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="94331-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="94331-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="94331-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="94331-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="94331-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Marketo.</span><span class="sxs-lookup"><span data-stu-id="94331-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="94331-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Marketo Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="94331-150">**tooconfigure Azure AD single sign-on with Marketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="94331-151">In de Azure-portal op Hallo Hallo **Marketo** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="94331-151">In hello Azure portal, on hello **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="94331-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="94331-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="94331-155">Op Hallo **Marketo-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="94331-155">On hello **Marketo Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="94331-157">a.</span><span class="sxs-lookup"><span data-stu-id="94331-157">a.</span></span> <span data-ttu-id="94331-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="94331-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="94331-159">b.</span><span class="sxs-lookup"><span data-stu-id="94331-159">b.</span></span> <span data-ttu-id="94331-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="94331-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="94331-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="94331-161">These values are not real.</span></span> <span data-ttu-id="94331-162">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="94331-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="94331-163">Neem contact op met [Marketo-ondersteuningsteam](http://investors.marketo.com/contactus.cfm) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="94331-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) tooget these values.</span></span>
 
4. <span data-ttu-id="94331-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="94331-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="94331-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="94331-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="94331-168">Op Hallo **Marketo configuratie** sectie, klikt u op **configureren Marketo** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="94331-168">On hello **Marketo Configuration** section, click **Configure Marketo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="94331-169">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="94331-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="94331-171">tooget Munchkin-Id van uw toepassing met behulp van beheerdersreferenties tooMarketo aanmelden en volgende acties uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="94331-171">tooget Munchkin Id of your application, log in tooMarketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="94331-172">a.</span><span class="sxs-lookup"><span data-stu-id="94331-172">a.</span></span> <span data-ttu-id="94331-173">Meld u aan met beheerdersreferenties tooMarketo-app.</span><span class="sxs-lookup"><span data-stu-id="94331-173">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="94331-174">b.</span><span class="sxs-lookup"><span data-stu-id="94331-174">b.</span></span> <span data-ttu-id="94331-175">Klik op Hallo **Admin** knop op Hallo bovenste navigatiedeelvenster.</span><span class="sxs-lookup"><span data-stu-id="94331-175">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="94331-177">c.</span><span class="sxs-lookup"><span data-stu-id="94331-177">c.</span></span> <span data-ttu-id="94331-178">Toohello integratie menu Navigeren en klik op Hallo **Munchkin koppeling**.</span><span class="sxs-lookup"><span data-stu-id="94331-178">Navigate toohello Integration menu and click hello **Munchkin link**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="94331-180">d.</span><span class="sxs-lookup"><span data-stu-id="94331-180">d.</span></span> <span data-ttu-id="94331-181">Kopieer Hallo weergegeven op het welkomstscherm Munchkin-Id en uw antwoord-URL in de configuratiewizard hello Azure AD te voltooien.</span><span class="sxs-lookup"><span data-stu-id="94331-181">Copy hello Munchkin Id shown on hello screen and complete your Reply URL in hello Azure AD configuration wizard.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="94331-183">tooconfigure hello eenmalige aanmelding in de toepassing hello, volg Hallo onderstaande stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="94331-183">tooconfigure hello SSO in hello application, follow hello below steps:</span></span>
   
    <span data-ttu-id="94331-184">a.</span><span class="sxs-lookup"><span data-stu-id="94331-184">a.</span></span> <span data-ttu-id="94331-185">Meld u aan met beheerdersreferenties tooMarketo-app.</span><span class="sxs-lookup"><span data-stu-id="94331-185">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="94331-186">b.</span><span class="sxs-lookup"><span data-stu-id="94331-186">b.</span></span> <span data-ttu-id="94331-187">Klik op Hallo **Admin** knop op Hallo bovenste navigatiedeelvenster.</span><span class="sxs-lookup"><span data-stu-id="94331-187">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="94331-189">c.</span><span class="sxs-lookup"><span data-stu-id="94331-189">c.</span></span> <span data-ttu-id="94331-190">Navigeer toohello integratie menu en klik op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="94331-190">Navigate toohello Integration menu and click **Single Sign On**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="94331-192">d.</span><span class="sxs-lookup"><span data-stu-id="94331-192">d.</span></span> <span data-ttu-id="94331-193">tooenable hello SAML-instellingen, klikt u op **bewerken** knop.</span><span class="sxs-lookup"><span data-stu-id="94331-193">tooenable hello SAML Settings, click **Edit** button.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="94331-195">e.</span><span class="sxs-lookup"><span data-stu-id="94331-195">e.</span></span> <span data-ttu-id="94331-196">**Ingeschakeld** Single Sign-On-instellingen.</span><span class="sxs-lookup"><span data-stu-id="94331-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="94331-197">f.</span><span class="sxs-lookup"><span data-stu-id="94331-197">f.</span></span> <span data-ttu-id="94331-198">Plakken Hallo **SAML entiteit-ID**, in Hallo **uitgever-ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="94331-198">Paste hello **SAML Entity ID**, in hello **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="94331-199">g.</span><span class="sxs-lookup"><span data-stu-id="94331-199">g.</span></span> <span data-ttu-id="94331-200">In Hallo **entiteit-ID** textbox Voer Hallo-URL als `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="94331-200">In hello **Entity ID** textbox, enter hello URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="94331-201">h.</span><span class="sxs-lookup"><span data-stu-id="94331-201">h.</span></span> <span data-ttu-id="94331-202">Selecteer Hallo locatie van de ID van de gebruiker als **naam-ID-element**.</span><span class="sxs-lookup"><span data-stu-id="94331-202">Select hello User ID Location as **Name Identifier element**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="94331-204">Als uw gebruikers-id geen UPN-naam en waarde voor het Hallo Hallo kenmerk tabblad wijzigen is.</span><span class="sxs-lookup"><span data-stu-id="94331-204">If your User Identifier is not UPN value then change hello value in hello Attribute tab.</span></span>
   
    <span data-ttu-id="94331-205">ik.</span><span class="sxs-lookup"><span data-stu-id="94331-205">i.</span></span> <span data-ttu-id="94331-206">Hallo-certificaat dat u hebt gedownload van Azure AD-configuratiewizard uploaden.</span><span class="sxs-lookup"><span data-stu-id="94331-206">Upload hello certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="94331-207">**Sla** Hallo instellingen.</span><span class="sxs-lookup"><span data-stu-id="94331-207">**Save** hello settings.</span></span>
   
    <span data-ttu-id="94331-208">j.</span><span class="sxs-lookup"><span data-stu-id="94331-208">j.</span></span> <span data-ttu-id="94331-209">Hallo omleidingspagina's instellingen bewerken.</span><span class="sxs-lookup"><span data-stu-id="94331-209">Edit hello Redirect Pages settings.</span></span>
   
    <span data-ttu-id="94331-210">k.</span><span class="sxs-lookup"><span data-stu-id="94331-210">k.</span></span> <span data-ttu-id="94331-211">Plakken Hallo **SAML Single Sign-On Service-URL** in Hallo **aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="94331-211">Paste hello **SAML Single Sign-On Service URL** in hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="94331-212">l.</span><span class="sxs-lookup"><span data-stu-id="94331-212">l.</span></span> <span data-ttu-id="94331-213">Plakken Hallo **Sign-Out URL** in Hallo **afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="94331-213">Paste hello **Sign-Out URL** in hello **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="94331-214">m.</span><span class="sxs-lookup"><span data-stu-id="94331-214">m.</span></span> <span data-ttu-id="94331-215">In Hallo **Error URL**, kopie uw **Marketo exemplaar-URL** en klik op **opslaan** knop toosave instellingen.</span><span class="sxs-lookup"><span data-stu-id="94331-215">In hello **Error URL**, copy your **Marketo instance URL** and click **Save** button toosave settings.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="94331-217">tooenable hello eenmalige aanmelding voor gebruikers, volledige Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="94331-217">tooenable hello SSO for users, complete hello following actions:</span></span>
   
    <span data-ttu-id="94331-218">a.</span><span class="sxs-lookup"><span data-stu-id="94331-218">a.</span></span> <span data-ttu-id="94331-219">Meld u aan met beheerdersreferenties tooMarketo-app.</span><span class="sxs-lookup"><span data-stu-id="94331-219">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="94331-220">b.</span><span class="sxs-lookup"><span data-stu-id="94331-220">b.</span></span> <span data-ttu-id="94331-221">Klik op Hallo **Admin** knop op Hallo bovenste navigatiedeelvenster.</span><span class="sxs-lookup"><span data-stu-id="94331-221">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="94331-223">c.</span><span class="sxs-lookup"><span data-stu-id="94331-223">c.</span></span> <span data-ttu-id="94331-224">Navigeer toohello **beveiliging** en klik op **aanmeldingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="94331-224">Navigate toohello **Security** menu and click **Login Settings**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="94331-226">d.</span><span class="sxs-lookup"><span data-stu-id="94331-226">d.</span></span> <span data-ttu-id="94331-227">Controleer Hallo **vereisen SSO** optie en **opslaan** Hallo instellingen.</span><span class="sxs-lookup"><span data-stu-id="94331-227">Check hello **Require SSO** option and **Save** hello settings.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="94331-229">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="94331-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="94331-230">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="94331-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="94331-231">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="94331-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="94331-232">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="94331-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="94331-233">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="94331-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="94331-235">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="94331-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="94331-236">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="94331-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="94331-238">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="94331-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="94331-240">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="94331-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="94331-242">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="94331-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="94331-244">a.</span><span class="sxs-lookup"><span data-stu-id="94331-244">a.</span></span> <span data-ttu-id="94331-245">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="94331-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="94331-246">b.</span><span class="sxs-lookup"><span data-stu-id="94331-246">b.</span></span> <span data-ttu-id="94331-247">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="94331-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="94331-248">c.</span><span class="sxs-lookup"><span data-stu-id="94331-248">c.</span></span> <span data-ttu-id="94331-249">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="94331-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="94331-250">d.</span><span class="sxs-lookup"><span data-stu-id="94331-250">d.</span></span> <span data-ttu-id="94331-251">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="94331-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="94331-252">Een testgebruiker Marketo maken</span><span class="sxs-lookup"><span data-stu-id="94331-252">Creating a Marketo test user</span></span>

<span data-ttu-id="94331-253">In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in Marketo.</span><span class="sxs-lookup"><span data-stu-id="94331-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="94331-254">Volg deze stappen toocreate een gebruiker in Marketo-platform.</span><span class="sxs-lookup"><span data-stu-id="94331-254">follow these steps toocreate a user in Marketo platform.</span></span>

1. <span data-ttu-id="94331-255">Meld u aan met beheerdersreferenties tooMarketo-app.</span><span class="sxs-lookup"><span data-stu-id="94331-255">Log in tooMarketo app using admin credentials.</span></span>

2. <span data-ttu-id="94331-256">Klik op Hallo **Admin** knop op Hallo bovenste navigatiedeelvenster.</span><span class="sxs-lookup"><span data-stu-id="94331-256">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="94331-258">Navigeer toohello **beveiliging** en klik op **gebruikers en rollen**</span><span class="sxs-lookup"><span data-stu-id="94331-258">Navigate toohello **Security** menu and click **Users & Roles**</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="94331-260">Klik op Hallo **nieuwe gebruikers uitnodigen** koppeling op een tabblad Hallo-gebruikers</span><span class="sxs-lookup"><span data-stu-id="94331-260">Click hello **Invite New User** link on hello Users tab</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="94331-262">In Hallo nieuwe gebruikers uitnodigen wizard opvulling Hallo volgende informatie</span><span class="sxs-lookup"><span data-stu-id="94331-262">In hello Invite New User wizard fill hello following information</span></span>
   
    <span data-ttu-id="94331-263">a.</span><span class="sxs-lookup"><span data-stu-id="94331-263">a.</span></span> <span data-ttu-id="94331-264">Voer Hallo gebruiker **e** adres in het tekstvak Hallo</span><span class="sxs-lookup"><span data-stu-id="94331-264">Enter hello user **Email** address in hello textbox</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="94331-266">b.</span><span class="sxs-lookup"><span data-stu-id="94331-266">b.</span></span> <span data-ttu-id="94331-267">Voer Hallo **voornaam** in Hallo tekstvak</span><span class="sxs-lookup"><span data-stu-id="94331-267">Enter hello **First Name** in hello textbox</span></span>
   
    <span data-ttu-id="94331-268">c.</span><span class="sxs-lookup"><span data-stu-id="94331-268">c.</span></span> <span data-ttu-id="94331-269">Voer Hallo **achternaam** in Hallo tekstvak</span><span class="sxs-lookup"><span data-stu-id="94331-269">Enter hello **Last Name**  in hello textbox</span></span>
   
    <span data-ttu-id="94331-270">d.</span><span class="sxs-lookup"><span data-stu-id="94331-270">d.</span></span> <span data-ttu-id="94331-271">Klik op **Volgende**</span><span class="sxs-lookup"><span data-stu-id="94331-271">Click **Next**</span></span>

6. <span data-ttu-id="94331-272">In Hallo **machtigingen** tabblad, selecteer Hallo **userRoles** en klik op **volgende**</span><span class="sxs-lookup"><span data-stu-id="94331-272">In hello **Permissions** tab, select hello **userRoles** and click **Next**</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="94331-274">Klik op Hallo **verzenden** knop toosend Hallo gebruiker uitnodiging</span><span class="sxs-lookup"><span data-stu-id="94331-274">Click hello **Send** button toosend hello user invitation</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="94331-276">Gebruiker Hallo e-mailmelding ontvangt en tooclick Hallo koppelen en Hallo wachtwoord tooactivate Hallo account wijzigen.</span><span class="sxs-lookup"><span data-stu-id="94331-276">User receives hello email notification and has tooclick hello link and change hello password tooactivate hello account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="94331-277">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="94331-277">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="94331-278">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooMarketo toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="94331-278">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMarketo.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="94331-280">**tooassign Britta Simon tooMarketo, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="94331-280">**tooassign Britta Simon tooMarketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="94331-281">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="94331-281">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="94331-283">Selecteer in de lijst met de toepassingen van Hallo **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="94331-283">In hello applications list, select **Marketo**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="94331-285">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="94331-285">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="94331-287">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="94331-287">Click **Add** button.</span></span> <span data-ttu-id="94331-288">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="94331-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="94331-290">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="94331-290">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="94331-291">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="94331-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="94331-292">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="94331-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="94331-293">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="94331-293">Testing single sign-on</span></span>

<span data-ttu-id="94331-294">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="94331-294">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="94331-295">Als u op Hallo Marketo-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Marketo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="94331-295">When you click hello Marketo tile in hello Access Panel, you should get automatically signed-on tooyour Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="94331-296">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="94331-296">Additional resources</span></span>

* [<span data-ttu-id="94331-297">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94331-297">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="94331-298">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="94331-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

