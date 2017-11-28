---
title: 'Zelfstudie: Azure Active Directory-integratie met Lifesize Cloud | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Lifesize Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ae599907e872571b3220de7122006c7db8db4a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="d55a9-103">Zelfstudie: Azure Active Directory-integratie met Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="d55a9-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="d55a9-104">In deze zelfstudie leert u hoe toointegrate Lifesize Cloud met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d55a9-104">In this tutorial, you learn how toointegrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d55a9-105">Lifesize Cloud integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d55a9-105">Integrating Lifesize Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d55a9-106">U kunt beheren in Azure AD wie toegang tot tooLifesize Cloud heeft</span><span class="sxs-lookup"><span data-stu-id="d55a9-106">You can control in Azure AD who has access tooLifesize Cloud</span></span>
- <span data-ttu-id="d55a9-107">U kunt uw gebruikers tooautomatically get aangemelde tooLifesize Cloud (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="d55a9-107">You can enable your users tooautomatically get signed-on tooLifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d55a9-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d55a9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d55a9-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d55a9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d55a9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d55a9-110">Prerequisites</span></span>

<span data-ttu-id="d55a9-111">Azure AD-integratie met Lifesize Cloud tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="d55a9-111">tooconfigure Azure AD integration with Lifesize Cloud, you need hello following items:</span></span>

- <span data-ttu-id="d55a9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d55a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d55a9-113">Een Lifesize Cloud eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d55a9-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d55a9-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d55a9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d55a9-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d55a9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d55a9-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d55a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d55a9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d55a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d55a9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d55a9-118">Scenario description</span></span>
<span data-ttu-id="d55a9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d55a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d55a9-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d55a9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d55a9-121">Het toevoegen van Lifesize Cloud van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d55a9-121">Adding Lifesize Cloud from hello gallery</span></span>
2. <span data-ttu-id="d55a9-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d55a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-hello-gallery"></a><span data-ttu-id="d55a9-123">Het toevoegen van Lifesize Cloud van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d55a9-123">Adding Lifesize Cloud from hello gallery</span></span>
<span data-ttu-id="d55a9-124">tooconfigure hello integratie van Lifesize Cloud met Azure AD, moet u tooadd Lifesize Cloud uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d55a9-124">tooconfigure hello integration of Lifesize Cloud into Azure AD, you need tooadd Lifesize Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d55a9-125">**tooadd Lifesize Cloud via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d55a9-125">**tooadd Lifesize Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d55a9-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d55a9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d55a9-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d55a9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d55a9-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d55a9-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d55a9-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d55a9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d55a9-133">Typ in het zoekvak Hallo **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="d55a9-133">In hello search box, type **Lifesize Cloud**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="d55a9-135">Selecteer in het deelvenster resultaten hello, **Lifesize Cloud**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d55a9-135">In hello results panel, select **Lifesize Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d55a9-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d55a9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d55a9-138">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Lifesize Cloud op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="d55a9-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d55a9-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de Lifesize Cloud is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d55a9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lifesize Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="d55a9-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in de Lifesize Cloud hello toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="d55a9-140">In other words, a link relationship between an Azure AD user and hello related user in Lifesize Cloud needs toobe established.</span></span>

<span data-ttu-id="d55a9-141">In de Lifesize Cloud, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="d55a9-141">In Lifesize Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d55a9-142">tooconfigure en eenmalige aanmelding Azure AD-test met Lifesize Cloud, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d55a9-142">tooconfigure and test Azure AD single sign-on with Lifesize Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d55a9-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="d55a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d55a9-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d55a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d55a9-145">**[Maken van een testgebruiker Lifesize Cloud](#creating-a-lifesize-cloud-test-user)**  -toohave een equivalent van Britta Simon in Lifesize Cloud die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d55a9-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - toohave a counterpart of Britta Simon in Lifesize Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d55a9-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d55a9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d55a9-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d55a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d55a9-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d55a9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d55a9-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="d55a9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="d55a9-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Lifesize Cloud, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d55a9-150">**tooconfigure Azure AD single sign-on with Lifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="d55a9-151">In de Azure-portal op Hallo Hallo **Lifesize Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d55a9-151">In hello Azure portal, on hello **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d55a9-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d55a9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="d55a9-155">Op Hallo **Lifesize Cloud-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d55a9-155">On hello **Lifesize Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="d55a9-157">a.</span><span class="sxs-lookup"><span data-stu-id="d55a9-157">a.</span></span> <span data-ttu-id="d55a9-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="d55a9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="d55a9-159">b.</span><span class="sxs-lookup"><span data-stu-id="d55a9-159">b.</span></span> <span data-ttu-id="d55a9-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="d55a9-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="d55a9-161">Controleer **weergeven geavanceerde instellingen voor URL**, Hallo stap uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d55a9-161">Check **Show advanced URL settings**, perform hello following step:</span></span>  
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="d55a9-163">In Hallo **Relay-status** textbox, typ een URL met Hallo patroon volgen:`https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="d55a9-163">In hello **Relay state** textbox, type a URL using hello following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="d55a9-164">Houd er rekening mee dat deze niet Hallo echte waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="d55a9-164">Please note that these are not hello real values.</span></span> <span data-ttu-id="d55a9-165">u hebt tooupdate deze waarden Hello werkelijke aanmeldings-URL, de Relay-status en -id.</span><span class="sxs-lookup"><span data-stu-id="d55a9-165">you have tooupdate these values with hello actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="d55a9-166">Neem contact op met [Lifesize Cloud Client ondersteuningsteam](https://www.lifesize.com/support) tooget aanmeldings-URL, en id-waarden en u kunt benutten Relay status SSO-configuratie die later in Hallo zelfstudie wordt uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="d55a9-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) tooget Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in hello tutorial.</span></span>

4. <span data-ttu-id="d55a9-167">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d55a9-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="d55a9-169">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d55a9-169">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d55a9-171">Op Hallo **Lifesize Cloudconfiguratie** sectie, klikt u op **Lifesize Cloud configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="d55a9-171">On hello **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d55a9-172">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="d55a9-172">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="d55a9-174">tooget SSO is geconfigureerd voor uw toepassing, aanmelding bij Hallo Lifesize cloudtoepassing met beheerdersbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="d55a9-174">tooget SSO configured for your application, login into hello Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="d55a9-175">Klik op de naam van uw in Hallo rechterbovenhoek en klik vervolgens op Hallo **geavanceerde instellingen**.</span><span class="sxs-lookup"><span data-stu-id="d55a9-175">In hello top right corner click on your name and then click on hello **Advance Settings**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="d55a9-177">In de geavanceerde instellingen Klik nu op Hallo Hallo **SSO configuratie** koppeling.</span><span class="sxs-lookup"><span data-stu-id="d55a9-177">In hello Advance Settings now click on hello **SSO Configuration** link.</span></span> <span data-ttu-id="d55a9-178">Hallo SSO-configuratiepagina voor uw exemplaar wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="d55a9-178">It will open hello SSO Configuration page for your instance.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="d55a9-180">Nu configureren Hallo volgende waarden in de gebruikersinterface voor Hallo SSO-configuratie.</span><span class="sxs-lookup"><span data-stu-id="d55a9-180">Now configure hello following values in hello SSO configuration UI.</span></span>    
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="d55a9-182">a.</span><span class="sxs-lookup"><span data-stu-id="d55a9-182">a.</span></span> <span data-ttu-id="d55a9-183">In **identiteit Provider verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d55a9-183">In **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d55a9-184">b.</span><span class="sxs-lookup"><span data-stu-id="d55a9-184">b.</span></span>  <span data-ttu-id="d55a9-185">In **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d55a9-185">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d55a9-186">c.</span><span class="sxs-lookup"><span data-stu-id="d55a9-186">c.</span></span> <span data-ttu-id="d55a9-187">De base-64 gecodeerde certificaat openen in Kladblok gedownload vanuit Azure-portal kopie Hallo inhoud ervan naar het Klembord en plak deze toohello **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="d55a9-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="d55a9-188">d.</span><span class="sxs-lookup"><span data-stu-id="d55a9-188">d.</span></span> <span data-ttu-id="d55a9-189">Toewijzingen voor Hallo voornaam tekstvak Voer Hallo-waarde als in Hallo SAML-kenmerk **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="d55a9-189">In hello SAML Attribute mappings for hello First Name text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="d55a9-190">e.</span><span class="sxs-lookup"><span data-stu-id="d55a9-190">e.</span></span> <span data-ttu-id="d55a9-191">In de toewijzing van de Hallo SAML-kenmerk voor Hallo **achternaam** tekstvak Voer Hallo-waarde als **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="d55a9-191">In hello SAML Attribute mapping for hello **Last Name** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="d55a9-192">f.</span><span class="sxs-lookup"><span data-stu-id="d55a9-192">f.</span></span> <span data-ttu-id="d55a9-193">In de toewijzing van de Hallo SAML-kenmerk voor Hallo **e** tekstvak Voer Hallo-waarde als **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="d55a9-193">In hello SAML Attribute mapping for hello **Email** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="d55a9-194">toocheck hello configuratie kunt u Hallo op **Test** knop.</span><span class="sxs-lookup"><span data-stu-id="d55a9-194">toocheck hello configuration you can click on hello **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="d55a9-195">Voor het testen van geslaagde toocomplete Hallo-configuratiewizard moet in Azure AD en bieden ook toegang toousers of -groepen die Hallo test kunnen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d55a9-195">For successful testing you need toocomplete hello configuration wizard in Azure AD and also provide access toousers or groups who can perform hello test.</span></span>

12. <span data-ttu-id="d55a9-196">Hallo eenmalige aanmelding inschakelen door te controleren op Hallo **eenmalige aanmelding inschakelen** knop.</span><span class="sxs-lookup"><span data-stu-id="d55a9-196">Enable hello SSO by checking on hello **Enable SSO** button.</span></span>

13. <span data-ttu-id="d55a9-197">Klik nu op Hallo **Update** knop zodat alle Hallo-instellingen worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d55a9-197">Now click on hello **Update** button so that all hello settings are saved.</span></span> <span data-ttu-id="d55a9-198">Hierdoor wordt Hallo RelayState waarde gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d55a9-198">This will generate hello RelayState value.</span></span> <span data-ttu-id="d55a9-199">Kopiëren Hallo RelayState waarde, die wordt gegenereerd in het tekstvak hello, plak deze in Hallo **Relay status** textbox onder **Lifesize Cloud-domein en de URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="d55a9-199">Copy hello RelayState value, which is generated in hello text box, paste it in hello **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="d55a9-200">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="d55a9-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d55a9-201">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="d55a9-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d55a9-202">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d55a9-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d55a9-203">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d55a9-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="d55a9-204">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d55a9-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d55a9-206">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d55a9-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d55a9-207">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d55a9-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d55a9-209">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d55a9-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d55a9-211">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="d55a9-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d55a9-213">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d55a9-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d55a9-215">a.</span><span class="sxs-lookup"><span data-stu-id="d55a9-215">a.</span></span> <span data-ttu-id="d55a9-216">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d55a9-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d55a9-217">b.</span><span class="sxs-lookup"><span data-stu-id="d55a9-217">b.</span></span> <span data-ttu-id="d55a9-218">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d55a9-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d55a9-219">c.</span><span class="sxs-lookup"><span data-stu-id="d55a9-219">c.</span></span> <span data-ttu-id="d55a9-220">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d55a9-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d55a9-221">d.</span><span class="sxs-lookup"><span data-stu-id="d55a9-221">d.</span></span> <span data-ttu-id="d55a9-222">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d55a9-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="d55a9-223">Een testgebruiker Lifesize Cloud maken</span><span class="sxs-lookup"><span data-stu-id="d55a9-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="d55a9-224">In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in de Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="d55a9-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="d55a9-225">Lifesize cloud biedt ondersteuning voor automatisch gebruikers inrichten.</span><span class="sxs-lookup"><span data-stu-id="d55a9-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="d55a9-226">Na de geslaagde verificatie op Azure AD worden Hallo gebruiker automatisch ingericht in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d55a9-226">After successful authentication at Azure AD, hello user will be automatically provisioned in hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d55a9-227">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d55a9-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d55a9-228">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooLifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="d55a9-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLifesize Cloud.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d55a9-230">**tooassign Britta Simon tooLifesize Cloud, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d55a9-230">**tooassign Britta Simon tooLifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="d55a9-231">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d55a9-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d55a9-233">Selecteer in de lijst met de toepassingen van Hallo **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="d55a9-233">In hello applications list, select **Lifesize Cloud**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="d55a9-235">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d55a9-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d55a9-237">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d55a9-237">Click **Add** button.</span></span> <span data-ttu-id="d55a9-238">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d55a9-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d55a9-240">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="d55a9-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d55a9-241">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d55a9-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d55a9-242">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d55a9-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d55a9-243">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d55a9-243">Testing single sign-on</span></span>

<span data-ttu-id="d55a9-244">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d55a9-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d55a9-245">Als u op Hallo Lifesize Cloud-tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina van Lifesize Cloud-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d55a9-245">When you click hello Lifesize Cloud tile in hello Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="d55a9-246">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d55a9-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d55a9-247">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d55a9-247">Additional resources</span></span>

* [<span data-ttu-id="d55a9-248">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d55a9-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d55a9-249">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d55a9-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

