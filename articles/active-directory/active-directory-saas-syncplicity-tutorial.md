---
title: 'Zelfstudie: Azure Active Directory-integratie met Syncplicity | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Syncplicity.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="35e3a-103">Zelfstudie: Azure Active Directory-integratie met Syncplicity</span><span class="sxs-lookup"><span data-stu-id="35e3a-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="35e3a-104">In deze zelfstudie leert u hoe toointegrate Syncplicity met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="35e3a-104">In this tutorial, you learn how toointegrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35e3a-105">Syncplicity integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="35e3a-105">Integrating Syncplicity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="35e3a-106">U kunt beheren in Azure AD die tooSyncplicity toegang heeft</span><span class="sxs-lookup"><span data-stu-id="35e3a-106">You can control in Azure AD who has access tooSyncplicity</span></span>
- <span data-ttu-id="35e3a-107">U kunt uw gebruikers tooautomatically get aangemelde tooSyncplicity (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="35e3a-107">You can enable your users tooautomatically get signed-on tooSyncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="35e3a-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="35e3a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="35e3a-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35e3a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35e3a-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="35e3a-110">Prerequisites</span></span>

<span data-ttu-id="35e3a-111">Azure AD-integratie met Syncplicity tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="35e3a-111">tooconfigure Azure AD integration with Syncplicity, you need hello following items:</span></span>

- <span data-ttu-id="35e3a-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="35e3a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="35e3a-113">Een Syncplicity eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="35e3a-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="35e3a-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="35e3a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="35e3a-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="35e3a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="35e3a-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="35e3a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="35e3a-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35e3a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="35e3a-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="35e3a-118">Scenario description</span></span>
<span data-ttu-id="35e3a-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="35e3a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="35e3a-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="35e3a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35e3a-121">Het toevoegen van Syncplicity van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="35e3a-121">Adding Syncplicity from hello gallery</span></span>
2. <span data-ttu-id="35e3a-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="35e3a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-hello-gallery"></a><span data-ttu-id="35e3a-123">Het toevoegen van Syncplicity van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="35e3a-123">Adding Syncplicity from hello gallery</span></span>
<span data-ttu-id="35e3a-124">tooconfigure hello integratie van Syncplicity in Azure AD, moet u tooadd Syncplicity uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="35e3a-124">tooconfigure hello integration of Syncplicity into Azure AD, you need tooadd Syncplicity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="35e3a-125">**tooadd Syncplicity via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="35e3a-125">**tooadd Syncplicity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="35e3a-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="35e3a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="35e3a-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="35e3a-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="35e3a-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="35e3a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="35e3a-133">Typ in het zoekvak Hallo **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-133">In hello search box, type **Syncplicity**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="35e3a-135">Selecteer in het deelvenster resultaten hello, **Syncplicity**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="35e3a-135">In hello results panel, select **Syncplicity**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="35e3a-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="35e3a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="35e3a-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Syncplicity op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="35e3a-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="35e3a-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Syncplicity is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35e3a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Syncplicity is tooa user in Azure AD.</span></span> <span data-ttu-id="35e3a-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Syncplicity toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="35e3a-140">In other words, a link relationship between an Azure AD user and hello related user in Syncplicity needs toobe established.</span></span>

<span data-ttu-id="35e3a-141">Wijs in Syncplicity, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="35e3a-141">In Syncplicity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="35e3a-142">tooconfigure en eenmalige aanmelding Azure AD-test met Syncplicity, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="35e3a-142">tooconfigure and test Azure AD single sign-on with Syncplicity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="35e3a-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="35e3a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="35e3a-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="35e3a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="35e3a-145">**[Maken van een testgebruiker Syncplicity](#creating-a-syncplicity-test-user)**  -toohave een equivalent van Britta Simon in Syncplicity die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="35e3a-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - toohave a counterpart of Britta Simon in Syncplicity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="35e3a-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="35e3a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="35e3a-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="35e3a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="35e3a-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="35e3a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="35e3a-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Syncplicity configureren.</span><span class="sxs-lookup"><span data-stu-id="35e3a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="35e3a-150">**Azure AD tooconfigure eenmalige aanmelding met Syncplicity, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="35e3a-150">**tooconfigure Azure AD single sign-on with Syncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="35e3a-151">In de Azure-portal op Hallo Hallo **Syncplicity** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-151">In hello Azure portal, on hello **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="35e3a-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="35e3a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="35e3a-155">Op Hallo **Syncplicity domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="35e3a-155">On hello **Syncplicity Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="35e3a-157">a.</span><span class="sxs-lookup"><span data-stu-id="35e3a-157">a.</span></span> <span data-ttu-id="35e3a-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="35e3a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="35e3a-159">b.</span><span class="sxs-lookup"><span data-stu-id="35e3a-159">b.</span></span> <span data-ttu-id="35e3a-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="35e3a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="35e3a-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="35e3a-161">These values are not real.</span></span> <span data-ttu-id="35e3a-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="35e3a-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="35e3a-163">Neem contact op met [Syncplicity Client ondersteuningsteam](https://www.syncplicity.com/contact-us) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="35e3a-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) tooget these values.</span></span> 
 

4. <span data-ttu-id="35e3a-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="35e3a-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="35e3a-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="35e3a-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="35e3a-168">Op Hallo **Syncplicity configuratie** sectie, klikt u op **configureren Syncplicity** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="35e3a-168">On hello **Syncplicity Configuration** section, click **Configure Syncplicity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="35e3a-169">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="35e3a-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="35e3a-171">Meld u aan tooyour **Syncplicity** tenant.</span><span class="sxs-lookup"><span data-stu-id="35e3a-171">Sign in tooyour **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="35e3a-172">Klik in het menu bovenaan Hallo Hallo **admin**, selecteer **instellingen**, en klik vervolgens op **aangepaste domeinen en eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-172">In hello menu on hello top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="35e3a-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="35e3a-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="35e3a-174">Op Hallo **eenmalige aanmelding (SSO)** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="35e3a-174">On hello **Single Sign-On (SSO)** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="35e3a-175">![Eenmalige aanmelding \(eenmalige aanmelding\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="35e3a-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="35e3a-176">a.</span><span class="sxs-lookup"><span data-stu-id="35e3a-176">a.</span></span> <span data-ttu-id="35e3a-177">In Hallo **aangepaste domeinen** textbox Hallo-typenaam van uw domein.</span><span class="sxs-lookup"><span data-stu-id="35e3a-177">In hello **Custom Domain** textbox, type hello name of your domain.</span></span>
  
    <span data-ttu-id="35e3a-178">b.</span><span class="sxs-lookup"><span data-stu-id="35e3a-178">b.</span></span> <span data-ttu-id="35e3a-179">Selecteer **ingeschakeld** als **Single Sign-On Status**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="35e3a-180">c.</span><span class="sxs-lookup"><span data-stu-id="35e3a-180">c.</span></span> <span data-ttu-id="35e3a-181">In Hallo **entiteit-Id** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="35e3a-181">In hello **Entity Id** textbox, Paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="35e3a-182">d.</span><span class="sxs-lookup"><span data-stu-id="35e3a-182">d.</span></span> <span data-ttu-id="35e3a-183">In Hallo **aanmelden pagina-URL** textbox plakken Hallo **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="35e3a-183">In hello **Sign-in page URL** textbox, Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="35e3a-184">e.</span><span class="sxs-lookup"><span data-stu-id="35e3a-184">e.</span></span> <span data-ttu-id="35e3a-185">In Hallo **pagina-URL voor afmelden** textbox plakken Hallo **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="35e3a-185">In hello **Logout page URL** textbox, Paste hello **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="35e3a-186">f.</span><span class="sxs-lookup"><span data-stu-id="35e3a-186">f.</span></span> <span data-ttu-id="35e3a-187">In **Provider identiteitscertificaat**, klikt u op **bestand kiezen**, en vervolgens uploaden Hallo-certificaat dat u hebt gedownload van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="35e3a-187">In **Identity Provider Certificate**, click **Choose file**, and then upload hello certificate which you have downloaded from hello Azure portal.</span></span> 

    <span data-ttu-id="35e3a-188">g.</span><span class="sxs-lookup"><span data-stu-id="35e3a-188">g.</span></span> <span data-ttu-id="35e3a-189">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="35e3a-190">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="35e3a-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="35e3a-191">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="35e3a-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="35e3a-192">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="35e3a-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="35e3a-193">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="35e3a-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="35e3a-194">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="35e3a-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="35e3a-196">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="35e3a-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="35e3a-197">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="35e3a-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="35e3a-199">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="35e3a-201">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="35e3a-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="35e3a-203">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="35e3a-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="35e3a-205">a.</span><span class="sxs-lookup"><span data-stu-id="35e3a-205">a.</span></span> <span data-ttu-id="35e3a-206">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="35e3a-207">b.</span><span class="sxs-lookup"><span data-stu-id="35e3a-207">b.</span></span> <span data-ttu-id="35e3a-208">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="35e3a-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="35e3a-209">c.</span><span class="sxs-lookup"><span data-stu-id="35e3a-209">c.</span></span> <span data-ttu-id="35e3a-210">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="35e3a-211">d.</span><span class="sxs-lookup"><span data-stu-id="35e3a-211">d.</span></span> <span data-ttu-id="35e3a-212">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="35e3a-213">Een testgebruiker Syncplicity maken</span><span class="sxs-lookup"><span data-stu-id="35e3a-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="35e3a-214">Voor AAD gebruikers toobe kunnen toosign in, moeten ze ingerichte tooSyncplicity toepassing zijn.</span><span class="sxs-lookup"><span data-stu-id="35e3a-214">For AAD users toobe able toosign in, they must be provisioned tooSyncplicity application.</span></span> <span data-ttu-id="35e3a-215">Deze sectie beschrijft hoe toocreate AAD gebruikersaccounts in Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="35e3a-215">This section describes how toocreate AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="35e3a-216">**een gebruiker account-tooSyncplicity tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="35e3a-216">**tooprovision a user account tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="35e3a-217">Meld u bij tooyour **Syncplicity** tenant (bijvoorbeeld: `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="35e3a-217">Log in tooyour **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="35e3a-218">Klik op **admin** en selecteer **gebruikersaccounts**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="35e3a-219">Klik op **toevoegen van een gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="35e3a-220">![Gebruikers beheren](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "gebruikers beheren")</span><span class="sxs-lookup"><span data-stu-id="35e3a-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="35e3a-221">Type Hallo **e adressen** van een AAD-account dat u wilt dat tooprovision, selecteer **gebruiker** als **rol**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-221">Type hello **Email addressess** of an AAD account you want tooprovision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="35e3a-222">![Accountgegevens](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "accountgegevens")</span><span class="sxs-lookup"><span data-stu-id="35e3a-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="35e3a-223">Hallo AAD accounthouder opgehaald van een e-mailbericht met inbegrip van een koppeling tooconfirm en Hallo account activeren.</span><span class="sxs-lookup"><span data-stu-id="35e3a-223">hello AAD account holder  gets an email including a link tooconfirm and activate hello account.</span></span> 
    > 

5. <span data-ttu-id="35e3a-224">Selecteer een groep in uw bedrijf dat de nieuwe gebruiker moet lid van en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="35e3a-225">![Groepslidmaatschap](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "groepslidmaatschap")</span><span class="sxs-lookup"><span data-stu-id="35e3a-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="35e3a-226">Als er geen groepen die zijn vermeld zijn, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="35e3a-227">Selecteer Hallo mappen u wilt tooplace onder het beheer van Syncplicity op Hallo van de gebruiker, computer, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-227">Select hello folders you would like tooplace under Syncplicity’s control on hello user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="35e3a-228">![Syncplicity mappen](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity mappen")</span><span class="sxs-lookup"><span data-stu-id="35e3a-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="35e3a-229">U kunt andere Syncplicity gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Syncplicity tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="35e3a-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="35e3a-230">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="35e3a-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="35e3a-231">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSyncplicity toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="35e3a-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSyncplicity.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="35e3a-233">**tooassign Britta Simon tooSyncplicity, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="35e3a-233">**tooassign Britta Simon tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="35e3a-234">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="35e3a-236">Selecteer in de lijst met de toepassingen van Hallo **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-236">In hello applications list, select **Syncplicity**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="35e3a-238">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="35e3a-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="35e3a-240">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="35e3a-240">Click **Add** button.</span></span> <span data-ttu-id="35e3a-241">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="35e3a-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="35e3a-243">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="35e3a-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="35e3a-244">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="35e3a-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="35e3a-245">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="35e3a-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="35e3a-246">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="35e3a-246">Testing single sign-on</span></span>

<span data-ttu-id="35e3a-247">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="35e3a-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="35e3a-248">Als u op Hallo Syncplicity tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Syncplicity toepassing.</span><span class="sxs-lookup"><span data-stu-id="35e3a-248">When you click hello Syncplicity tile in hello Access Panel, you should get automatically signed-on tooyour Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="35e3a-249">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="35e3a-249">Additional resources</span></span>

* [<span data-ttu-id="35e3a-250">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35e3a-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35e3a-251">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="35e3a-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

