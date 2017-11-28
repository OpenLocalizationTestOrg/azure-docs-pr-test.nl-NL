---
title: 'Zelfstudie: Azure Active Directory-integratie met Adobe Creative Cloud | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Adobe Creative Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="0dccc-103">Zelfstudie: Azure Active Directory-integratie met Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="0dccc-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="0dccc-104">In deze zelfstudie leert u hoe toointegrate Adobe advertentie Cloud met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0dccc-104">In this tutorial, you learn how toointegrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0dccc-105">Adobe Creative Cloud integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="0dccc-105">Integrating Adobe Creative Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0dccc-106">U kunt beheren in Azure AD wie toegang tot tooAdobe Creative Cloud heeft</span><span class="sxs-lookup"><span data-stu-id="0dccc-106">You can control in Azure AD who has access tooAdobe Creative Cloud</span></span>
- <span data-ttu-id="0dccc-107">U kunt uw gebruikers tooautomatically get aangemelde tooAdobe Creative Cloud (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="0dccc-107">You can enable your users tooautomatically get signed-on tooAdobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0dccc-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="0dccc-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="0dccc-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0dccc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dccc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0dccc-110">Prerequisites</span></span>

<span data-ttu-id="0dccc-111">Azure AD-integratie met Adobe Creative Cloud tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="0dccc-111">tooconfigure Azure AD integration with Adobe Creative Cloud, you need hello following items:</span></span>

- <span data-ttu-id="0dccc-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="0dccc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0dccc-113">Een Adobe Creative Cloud eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="0dccc-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0dccc-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="0dccc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0dccc-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="0dccc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0dccc-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="0dccc-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0dccc-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0dccc-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0dccc-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="0dccc-118">Scenario description</span></span>
<span data-ttu-id="0dccc-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0dccc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0dccc-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="0dccc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0dccc-121">Het toevoegen van Adobe Creative Cloud van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0dccc-121">Adding Adobe Creative Cloud from hello gallery</span></span>
2. <span data-ttu-id="0dccc-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0dccc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a><span data-ttu-id="0dccc-123">Het toevoegen van Adobe Creative Cloud van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0dccc-123">Adding Adobe Creative Cloud from hello gallery</span></span>
<span data-ttu-id="0dccc-124">tooconfigure hello integratie van Adobe Creative Cloud met Azure AD, moet u tooadd Adobe Creative Cloud uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="0dccc-124">tooconfigure hello integration of Adobe Creative Cloud into Azure AD, you need tooadd Adobe Creative Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0dccc-125">**tooadd Adobe Creative Cloud via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0dccc-125">**tooadd Adobe Creative Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dccc-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0dccc-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0dccc-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0dccc-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="0dccc-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="0dccc-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="0dccc-133">Typ in het zoekvak Hallo **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-133">In hello search box, type **Adobe Creative Cloud**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="0dccc-135">Selecteer in het deelvenster resultaten hello, **Adobe Creative Cloud**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0dccc-135">In hello results panel, select **Adobe Creative Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0dccc-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0dccc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0dccc-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Adobe Creative Cloud op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="0dccc-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0dccc-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Adobe Creative Cloud is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0dccc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Creative Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="0dccc-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Adobe Creative Cloud toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="0dccc-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Creative Cloud needs toobe established.</span></span>

<span data-ttu-id="0dccc-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="0dccc-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="0dccc-142">tooconfigure en eenmalige aanmelding Azure AD-test met Adobe Creative Cloud, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0dccc-142">tooconfigure and test Azure AD single sign-on with Adobe Creative Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0dccc-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="0dccc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0dccc-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0dccc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0dccc-145">**[Maken van een testgebruiker Adobe Creative Cloud](#creating-an-adobe-creative-cloud-test-user)**  -toohave een equivalent van Britta Simon in Adobe Creative Cloud die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="0dccc-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - toohave a counterpart of Britta Simon in Adobe Creative Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="0dccc-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0dccc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0dccc-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="0dccc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0dccc-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="0dccc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0dccc-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="0dccc-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="0dccc-150">**tooconfigure eenmalige aanmelding Azure AD met Adobe Creative Cloud, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0dccc-150">**tooconfigure Azure AD single sign-on with Adobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dccc-151">In hello Azure Management portal op Hallo **Adobe Creative Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-151">In hello Azure Management portal, on hello **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="0dccc-153">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0dccc-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="0dccc-155">Op Hallo **Adobe Creative Cloud-domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="0dccc-155">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="0dccc-157">a.</span><span class="sxs-lookup"><span data-stu-id="0dccc-157">a.</span></span> <span data-ttu-id="0dccc-158">In Hallo **id** textbox Hallo typewaarde als:`https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="0dccc-158">In hello **Identifier** textbox, type hello value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="0dccc-159">b.</span><span class="sxs-lookup"><span data-stu-id="0dccc-159">b.</span></span> <span data-ttu-id="0dccc-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="0dccc-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0dccc-161">Houd er rekening mee dat deze niet Hallo echte waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="0dccc-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="0dccc-162">U hebt deze waarden door de werkelijke id en de antwoord-URL Hallo tooupdate.</span><span class="sxs-lookup"><span data-stu-id="0dccc-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="0dccc-163">We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id.</span><span class="sxs-lookup"><span data-stu-id="0dccc-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="0dccc-164">Als u handmatig een gebruiker toocreate nodig, moet u toocontact Hallo Adobe Creative Cloud ondersteuningsteam.</span><span class="sxs-lookup"><span data-stu-id="0dccc-164">If you need toocreate an user manually, you need toocontact hello Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="0dccc-165">Op Hallo **Adobe Creative Cloud-domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="0dccc-165">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="0dccc-167">a.</span><span class="sxs-lookup"><span data-stu-id="0dccc-167">a.</span></span> <span data-ttu-id="0dccc-168">Klik op Hallo **weergeven geavanceerde instellingen voor URL** optie</span><span class="sxs-lookup"><span data-stu-id="0dccc-168">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="0dccc-169">b.</span><span class="sxs-lookup"><span data-stu-id="0dccc-169">b.</span></span> <span data-ttu-id="0dccc-170">In Hallo **aanmeldings-URL** textbox Hallo typewaarde als:`https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="0dccc-170">In hello **Sign-on URL** textbox, type hello value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="0dccc-171">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0dccc-171">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="0dccc-173">Op Hallo **Adobe Creative Cloudconfiguratie** sectie, klikt u op **Adobe Creative Cloud configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="0dccc-173">On hello **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0dccc-174">Kopieer Hallo **SAML entiteit-Id** en **SAML SSO Service URL** van naslag-sectie.</span><span class="sxs-lookup"><span data-stu-id="0dccc-174">Please copy hello **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="0dccc-176">In een ander browservenster, aanmelding tooyour Adobe Creative cloudtenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="0dccc-176">In a different web browser window, sign-on tooyour Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="0dccc-177">Ga te**identiteit** Hallo navigatiedeelvenster links en klikt u op uw domein.</span><span class="sxs-lookup"><span data-stu-id="0dccc-177">Go too**Identity** on hello left navigation pane and click your domain.</span></span> <span data-ttu-id="0dccc-178">Voert de volgende stappen uit op Hallo **eenmalige aanmelding op configuratie vereist** sectie.</span><span class="sxs-lookup"><span data-stu-id="0dccc-178">Then perform hello following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="0dccc-179">![Instellingen](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="0dccc-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="0dccc-180">Klik op **Bladeren** tooupload Hallo certificaat gedownload vanuit Azure AD te**IDP certificaat**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-180">Click **Browse** tooupload hello downloaded certificate from Azure AD too**IDP Certificate**.</span></span>

10. <span data-ttu-id="0dccc-181">In Hallo **IDP verlener** textbox Hallo-waarde van **SAML entiteit-Id** die u hebt gekopieerd uit **eenmalige aanmelding configureren** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0dccc-181">In hello **IDP issuer** textbox, put hello value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="0dccc-182">In Hallo **IDP aanmeldings-URL** textbox Hallo-waarde van **SAML SSO Service URL** die u hebt gekopieerd uit **eenmalige aanmelding configureren** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0dccc-182">In hello **IDP Login URL** textbox, put hello value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="0dccc-183">Selecteer **HTTP - omleiding** als **IDP Binding**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="0dccc-184">Selecteer **e-mailadres** als **aanmelding gebruikersinstelling**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="0dccc-185">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="0dccc-185">Click **Save** button.</span></span>

15. <span data-ttu-id="0dccc-186">Hallo dashboard biedt nu Hallo XML **'Metagegevens downloaden'** bestand.</span><span class="sxs-lookup"><span data-stu-id="0dccc-186">hello dashboard will now present hello XML **"Download Metadata"** file.</span></span> <span data-ttu-id="0dccc-187">Het bevat van Adobe EntityDescriptor URL's en AssertionConsumerService.</span><span class="sxs-lookup"><span data-stu-id="0dccc-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="0dccc-188">Hallo-bestand openen en deze configureren in Azure AD-toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="0dccc-188">Please open hello file and configure them in hello Azure AD application.</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="0dccc-191">a.</span><span class="sxs-lookup"><span data-stu-id="0dccc-191">a.</span></span> <span data-ttu-id="0dccc-192">Gebruik Hallo EntityDescriptor waarde Adobe geleverd, kunt u voor **id** op Hallo **App-instellingen configureren** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0dccc-192">Use hello EntityDescriptor value Adobe provided you for **Identifier** on hello **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="0dccc-193">b.</span><span class="sxs-lookup"><span data-stu-id="0dccc-193">b.</span></span> <span data-ttu-id="0dccc-194">Gebruik Hallo AssertionConsumerService waarde Adobe geleverd, kunt u voor **antwoord-URL** op Hallo **App-instellingen configureren** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0dccc-194">Use hello AssertionConsumerService value Adobe provided you for **Reply URL** on hello **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0dccc-195">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="0dccc-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="0dccc-196">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0dccc-196">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="0dccc-198">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0dccc-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dccc-199">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0dccc-199">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0dccc-201">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0dccc-201">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0dccc-203">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0dccc-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0dccc-205">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0dccc-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0dccc-207">a.</span><span class="sxs-lookup"><span data-stu-id="0dccc-207">a.</span></span> <span data-ttu-id="0dccc-208">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0dccc-209">b.</span><span class="sxs-lookup"><span data-stu-id="0dccc-209">b.</span></span> <span data-ttu-id="0dccc-210">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0dccc-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0dccc-211">c.</span><span class="sxs-lookup"><span data-stu-id="0dccc-211">c.</span></span> <span data-ttu-id="0dccc-212">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0dccc-213">d.</span><span class="sxs-lookup"><span data-stu-id="0dccc-213">d.</span></span> <span data-ttu-id="0dccc-214">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="0dccc-215">Een testgebruiker Adobe Creative Cloud maken</span><span class="sxs-lookup"><span data-stu-id="0dccc-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="0dccc-216">In de volgorde tooenable Azure AD gebruikers toolog in Adobe Creative Cloud, moeten ze worden ingericht in Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="0dccc-216">In order tooenable Azure AD users toolog into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="0dccc-217">In geval van Adobe Creative Cloud Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="0dccc-217">In hello case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="0dccc-218">**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**</span><span class="sxs-lookup"><span data-stu-id="0dccc-218">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dccc-219">Aanmelden tooyour Adobe Creative Cloud bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="0dccc-219">Log in tooyour Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="0dccc-220">Klik op **mensen**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-220">Click **People**.</span></span>

    <span data-ttu-id="0dccc-221">![Mensen](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "personen")</span><span class="sxs-lookup"><span data-stu-id="0dccc-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="0dccc-222">Klik op **gebruiker uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-222">Click **Invite User**.</span></span>

    <span data-ttu-id="0dccc-223">![Gebruikers uitnodigen](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "gebruikers uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="0dccc-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="0dccc-224">Op Hallo **personen uitnodigen** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0dccc-224">On hello **Invite People** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="0dccc-225">![Personen uitnodigen](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "personen uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="0dccc-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="0dccc-226">a.</span><span class="sxs-lookup"><span data-stu-id="0dccc-226">a.</span></span> <span data-ttu-id="0dccc-227">In Hallo **e** textbox type Hallo e-mailadres van Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="0dccc-227">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="0dccc-228">b.</span><span class="sxs-lookup"><span data-stu-id="0dccc-228">b.</span></span> <span data-ttu-id="0dccc-229">Klik op **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0dccc-230">Hello Azure Active Directory-accounthouder wordt een e-mailbericht ontvangen en volg een koppeling tooconfirm hun account maken voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="0dccc-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0dccc-231">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dccc-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0dccc-232">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar toegang tooAdobe Creative Cloud verlenen.</span><span class="sxs-lookup"><span data-stu-id="0dccc-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAdobe Creative Cloud.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="0dccc-234">**tooassign Britta Simon tooAdobe Creative Cloud Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0dccc-234">**tooassign Britta Simon tooAdobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dccc-235">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-235">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="0dccc-237">Selecteer in de lijst met de toepassingen van Hallo **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-237">In hello applications list, select **Adobe Creative Cloud**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="0dccc-239">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="0dccc-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="0dccc-241">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="0dccc-241">Click **Add** button.</span></span> <span data-ttu-id="0dccc-242">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0dccc-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="0dccc-244">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="0dccc-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0dccc-245">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0dccc-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0dccc-246">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0dccc-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0dccc-247">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0dccc-247">Testing single sign-on</span></span>

<span data-ttu-id="0dccc-248">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="0dccc-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0dccc-249">Als u op Hallo Adobe Creative Cloud-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Adobe Creative Cloud-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0dccc-249">When you click hello Adobe Creative Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0dccc-250">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="0dccc-250">Additional resources</span></span>

* [<span data-ttu-id="0dccc-251">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0dccc-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0dccc-252">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0dccc-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png