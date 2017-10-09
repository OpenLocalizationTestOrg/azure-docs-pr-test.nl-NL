---
title: 'Zelfstudie: Azure Active Directory-integratie met Sprinklr | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Sprinklr.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="ee2f3-103">Zelfstudie: Azure Active Directory-integratie met Sprinklr</span><span class="sxs-lookup"><span data-stu-id="ee2f3-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="ee2f3-104">In deze zelfstudie leert u hoe toointegrate Sprinklr met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ee2f3-104">In this tutorial, you learn how toointegrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ee2f3-105">Sprinklr integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ee2f3-105">Integrating Sprinklr with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ee2f3-106">U kunt beheren in Azure AD die tooSprinklr toegang heeft</span><span class="sxs-lookup"><span data-stu-id="ee2f3-106">You can control in Azure AD who has access tooSprinklr</span></span>
- <span data-ttu-id="ee2f3-107">U kunt uw gebruikers tooautomatically get aangemelde tooSprinklr (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ee2f3-107">You can enable your users tooautomatically get signed-on tooSprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ee2f3-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ee2f3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ee2f3-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ee2f3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee2f3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ee2f3-110">Prerequisites</span></span>

<span data-ttu-id="ee2f3-111">Azure AD-integratie met Sprinklr tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ee2f3-111">tooconfigure Azure AD integration with Sprinklr, you need hello following items:</span></span>

- <span data-ttu-id="ee2f3-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ee2f3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ee2f3-113">Een Sprinklr eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ee2f3-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ee2f3-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ee2f3-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ee2f3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ee2f3-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ee2f3-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ee2f3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ee2f3-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ee2f3-118">Scenario description</span></span>
<span data-ttu-id="ee2f3-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ee2f3-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ee2f3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ee2f3-121">Het toevoegen van Sprinklr van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ee2f3-121">Adding Sprinklr from hello gallery</span></span>
2. <span data-ttu-id="ee2f3-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ee2f3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-hello-gallery"></a><span data-ttu-id="ee2f3-123">Het toevoegen van Sprinklr van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ee2f3-123">Adding Sprinklr from hello gallery</span></span>
<span data-ttu-id="ee2f3-124">tooconfigure hello integratie van Sprinklr in Azure AD, moet u tooadd Sprinklr uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-124">tooconfigure hello integration of Sprinklr into Azure AD, you need tooadd Sprinklr from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ee2f3-125">**tooadd Sprinklr via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ee2f3-125">**tooadd Sprinklr from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee2f3-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ee2f3-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ee2f3-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ee2f3-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ee2f3-133">Typ in het zoekvak Hallo **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-133">In hello search box, type **Sprinklr**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="ee2f3-135">Selecteer in het deelvenster resultaten hello, **Sprinklr**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-135">In hello results panel, select **Sprinklr**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ee2f3-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ee2f3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ee2f3-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Sprinklr op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="ee2f3-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ee2f3-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Sprinklr is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sprinklr is tooa user in Azure AD.</span></span> <span data-ttu-id="ee2f3-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Sprinklr toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-140">In other words, a link relationship between an Azure AD user and hello related user in Sprinklr needs toobe established.</span></span>

<span data-ttu-id="ee2f3-141">Wijs in Sprinklr, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-141">In Sprinklr, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ee2f3-142">tooconfigure en eenmalige aanmelding Azure AD-test met Sprinklr, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ee2f3-142">tooconfigure and test Azure AD single sign-on with Sprinklr, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ee2f3-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ee2f3-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ee2f3-145">**[Maken van een testgebruiker Sprinklr](#creating-a-sprinklr-test-user)**  -toohave een equivalent van Britta Simon in Sprinklr die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - toohave a counterpart of Britta Simon in Sprinklr that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ee2f3-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ee2f3-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ee2f3-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ee2f3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ee2f3-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Sprinklr configureren.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="ee2f3-150">**Azure AD tooconfigure eenmalige aanmelding met Sprinklr, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ee2f3-150">**tooconfigure Azure AD single sign-on with Sprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee2f3-151">In de Azure-portal op Hallo Hallo **Sprinklr** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-151">In hello Azure portal, on hello **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ee2f3-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="ee2f3-155">Op Hallo **Sprinklr domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ee2f3-155">On hello **Sprinklr Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="ee2f3-157">a.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-157">a.</span></span> <span data-ttu-id="ee2f3-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="ee2f3-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="ee2f3-159">b.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-159">b.</span></span> <span data-ttu-id="ee2f3-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="ee2f3-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ee2f3-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-161">These values are not real.</span></span> <span data-ttu-id="ee2f3-162">Hallo-waarde met de Hallo bijwerken werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-162">Update hello value with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ee2f3-163">Neem contact op met [Sprinklr Client ondersteuningsteam](https://www.sprinklr.com/contact-us/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="ee2f3-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="ee2f3-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ee2f3-168">Op Hallo **Sprinklr configuratie** sectie, klikt u op **configureren Sprinklr** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-168">On hello **Sprinklr Configuration** section, click **Configure Sprinklr** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ee2f3-169">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="ee2f3-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

7. <span data-ttu-id="ee2f3-170">In een ander browservenster, meld u aan tooyour Sprinklr bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-170">In a different web browser window, log in tooyour Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="ee2f3-171">Ga te**beheer \> instellingen**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-171">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="ee2f3-172">![Beheer](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="ee2f3-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="ee2f3-173">Ga te**beheren Partner \> eenmalige** op in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-173">Go too**Manage Partner \> Single Sign** on from hello left pane.</span></span>
   
    <span data-ttu-id="ee2f3-174">![Partner beheren](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Partner beheren")</span><span class="sxs-lookup"><span data-stu-id="ee2f3-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="ee2f3-175">Klik op **+ toevoegen voor eenmalige aanmeldingen**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="ee2f3-176">![Eenmalige aanmeldingen](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "eenmalige aanmeldingen")</span><span class="sxs-lookup"><span data-stu-id="ee2f3-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="ee2f3-177">Op Hallo **voor eenmalige aanmelding** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ee2f3-177">On hello **Single Sign on** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="ee2f3-178">![Eenmalige aanmeldingen](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "eenmalige aanmeldingen")</span><span class="sxs-lookup"><span data-stu-id="ee2f3-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="ee2f3-179">a.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-179">a.</span></span> <span data-ttu-id="ee2f3-180">In Hallo **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="ee2f3-180">In hello **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="ee2f3-181">b.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-181">b.</span></span> <span data-ttu-id="ee2f3-182">Selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-182">Select **Enabled**.</span></span>

    <span data-ttu-id="ee2f3-183">c.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-183">c.</span></span> <span data-ttu-id="ee2f3-184">Selecteer **nieuw certificaat voor eenmalige aanmelding gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="ee2f3-185">e.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-185">e.</span></span> <span data-ttu-id="ee2f3-186">De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **Provider identiteitscertificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-186">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="ee2f3-187">f.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-187">f.</span></span> <span data-ttu-id="ee2f3-188">Plakken Hallo **SAML entiteit-ID** waarde die u vanuit Azure Portal hebt gekopieerd in Hallo **entiteit-Id** textbox.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-188">Paste hello **SAML Entity ID** value which you have copied from Azure Portal into hello **Entity Id** textbox.</span></span>

    <span data-ttu-id="ee2f3-189">g.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-189">g.</span></span> <span data-ttu-id="ee2f3-190">Plakken Hallo **SAML Single Sign-On Service-URL** waarde die u vanuit Azure Portal hebt gekopieerd in Hallo **identiteit Provider aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="ee2f3-191">h.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-191">h.</span></span> <span data-ttu-id="ee2f3-192">Plakken Hallo **Sign-Out URL** waarde die u vanuit Azure Portal hebt gekopieerd in Hallo **identiteit Provider afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-192">Paste hello **Sign-Out URL** value which you have copied from Azure Portal into hello **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="ee2f3-193">ik.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-193">i.</span></span> <span data-ttu-id="ee2f3-194">Als **SAML-ID gebruikerstype**, selecteer **Assertion gebruiker bevat ' s sprinklr.com gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="ee2f3-195">j.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-195">j.</span></span> <span data-ttu-id="ee2f3-196">Als **SAML-ID gebruikerslocatie**, selecteer **gebruikersnaam wordt Hallo-naam-ID-element van Hallo onderwerp instructie**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-196">As **SAML User ID Location**, select **User ID is in hello Name Identifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="ee2f3-197">k.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-197">k.</span></span> <span data-ttu-id="ee2f3-198">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-198">Click **Save**.</span></span>
       
    <span data-ttu-id="ee2f3-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="ee2f3-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="ee2f3-200">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ee2f3-201">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ee2f3-202">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ee2f3-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ee2f3-203">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ee2f3-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="ee2f3-204">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ee2f3-206">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ee2f3-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee2f3-207">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ee2f3-209">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ee2f3-211">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ee2f3-213">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ee2f3-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ee2f3-215">a.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-215">a.</span></span> <span data-ttu-id="ee2f3-216">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ee2f3-217">b.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-217">b.</span></span> <span data-ttu-id="ee2f3-218">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ee2f3-219">c.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-219">c.</span></span> <span data-ttu-id="ee2f3-220">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ee2f3-221">d.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-221">d.</span></span> <span data-ttu-id="ee2f3-222">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="ee2f3-223">Een testgebruiker Sprinklr maken</span><span class="sxs-lookup"><span data-stu-id="ee2f3-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="ee2f3-224">Aanmelden tooyour Sprinklr bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-224">Log in tooyour Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="ee2f3-225">Ga te**beheer \> instellingen**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-225">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="ee2f3-226">![Beheer](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="ee2f3-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="ee2f3-227">Ga te**Client beheren \> gebruikers** in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-227">Go too**Manage Client \> Users** from hello left pane.</span></span>
   
    <span data-ttu-id="ee2f3-228">![Instellingen](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="ee2f3-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="ee2f3-229">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="ee2f3-230">![Instellingen](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="ee2f3-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="ee2f3-231">Op Hallo **bewerken gebruiker** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="ee2f3-231">On hello **Edit user** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="ee2f3-232">![Gebruiker bewerken](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "gebruiker bewerken")</span><span class="sxs-lookup"><span data-stu-id="ee2f3-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="ee2f3-233">a.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-233">a.</span></span> <span data-ttu-id="ee2f3-234">In Hallo **e**, **voornaam** en **achternaam** tekstvakken, Hallo-informatie van een Azure AD-gebruikersaccount dat u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-234">In hello **Email**, **First Name** and **Last Name** textboxes, type hello information of an Azure AD user account you want tooprovision.</span></span>

    <span data-ttu-id="ee2f3-235">b.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-235">b.</span></span> <span data-ttu-id="ee2f3-236">Selecteer **wachtwoord uitgeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="ee2f3-237">c.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-237">c.</span></span> <span data-ttu-id="ee2f3-238">Selecteer **taal**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-238">Select **Language**.</span></span>

    <span data-ttu-id="ee2f3-239">d.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-239">d.</span></span> <span data-ttu-id="ee2f3-240">Selecteer **gebruikerstype**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-240">Select **User Type**.</span></span>

    <span data-ttu-id="ee2f3-241">e.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-241">e.</span></span> <span data-ttu-id="ee2f3-242">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="ee2f3-243">**Wachtwoord uitgeschakeld** moet geselecteerde tooenable een toolog gebruiker in via een id-provider.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-243">**Password Disabled** must be selected tooenable a user toolog in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="ee2f3-244">Ga te**rol**, en klik vervolgens op Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ee2f3-244">Go too**Role**, and then perform hello following steps:</span></span>
   
    <span data-ttu-id="ee2f3-245">![Rollen partner](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner rollen")</span><span class="sxs-lookup"><span data-stu-id="ee2f3-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="ee2f3-246">a.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-246">a.</span></span> <span data-ttu-id="ee2f3-247">Van Hallo **Global** selecteert **alle\_machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-247">From hello **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="ee2f3-248">b.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-248">b.</span></span> <span data-ttu-id="ee2f3-249">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="ee2f3-250">U kunt andere Sprinklr gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Sprinklr tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ee2f3-251">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee2f3-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ee2f3-252">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSprinklr toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSprinklr.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ee2f3-254">**tooassign Britta Simon tooSprinklr, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ee2f3-254">**tooassign Britta Simon tooSprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee2f3-255">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ee2f3-257">Selecteer in de lijst met de toepassingen van Hallo **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-257">In hello applications list, select **Sprinklr**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="ee2f3-259">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ee2f3-261">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-261">Click **Add** button.</span></span> <span data-ttu-id="ee2f3-262">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ee2f3-264">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ee2f3-265">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ee2f3-266">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ee2f3-267">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ee2f3-267">Testing single sign-on</span></span>

<span data-ttu-id="ee2f3-268">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ee2f3-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ee2f3-269">Wanneer u Hallo Sprinklr tegel in Hallo toegangsvenster klikt, moet u automatisch aangemelde tooyour Sprinklr-toepassing voor meer informatie over Hallo Toegangsvenster ophalen, Zie [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ee2f3-269">When you click hello Sprinklr tile in hello Access Panel, you should get automatically signed-on tooyour Sprinklr application For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ee2f3-270">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ee2f3-270">Additional resources</span></span>

* [<span data-ttu-id="ee2f3-271">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee2f3-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ee2f3-272">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ee2f3-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

