---
title: 'Zelfstudie: Azure Active Directory-integratie met Bonusly | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Bonusly.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 60ad06c028463af81a7901ab321c4ae9346798ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="2b8fc-103">Zelfstudie: Azure Active Directory-integratie met Bonusly</span><span class="sxs-lookup"><span data-stu-id="2b8fc-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="2b8fc-104">In deze zelfstudie leert u hoe toointegrate Bonusly met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2b8fc-104">In this tutorial, you learn how toointegrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2b8fc-105">Bonusly integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2b8fc-105">Integrating Bonusly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2b8fc-106">U kunt beheren in Azure AD die tooBonusly toegang heeft</span><span class="sxs-lookup"><span data-stu-id="2b8fc-106">You can control in Azure AD who has access tooBonusly</span></span>
- <span data-ttu-id="2b8fc-107">U kunt uw gebruikers tooautomatically get aangemelde tooBonusly (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="2b8fc-107">You can enable your users tooautomatically get signed-on tooBonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2b8fc-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2b8fc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2b8fc-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2b8fc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b8fc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2b8fc-110">Prerequisites</span></span>

<span data-ttu-id="2b8fc-111">Azure AD-integratie met Bonusly tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="2b8fc-111">tooconfigure Azure AD integration with Bonusly, you need hello following items:</span></span>

- <span data-ttu-id="2b8fc-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2b8fc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2b8fc-113">Een Bonusly eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2b8fc-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2b8fc-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2b8fc-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2b8fc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2b8fc-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2b8fc-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b8fc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2b8fc-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2b8fc-118">Scenario description</span></span>
<span data-ttu-id="2b8fc-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2b8fc-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2b8fc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2b8fc-121">Het toevoegen van Bonusly van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2b8fc-121">Adding Bonusly from hello gallery</span></span>
2. <span data-ttu-id="2b8fc-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2b8fc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-hello-gallery"></a><span data-ttu-id="2b8fc-123">Het toevoegen van Bonusly van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2b8fc-123">Adding Bonusly from hello gallery</span></span>
<span data-ttu-id="2b8fc-124">tooconfigure hello integratie van Bonusly in Azure AD, moet u tooadd Bonusly uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-124">tooconfigure hello integration of Bonusly into Azure AD, you need tooadd Bonusly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2b8fc-125">**tooadd Bonusly via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2b8fc-125">**tooadd Bonusly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b8fc-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="2b8fc-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2b8fc-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="2b8fc-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="2b8fc-133">Typ in het zoekvak Hallo **Bonusly**, selecteer **Bonusly** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-133">In hello search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button tooadd hello application.</span></span>

    ![In de lijst met resultaten Hallo bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2b8fc-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b8fc-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="2b8fc-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Bonusly op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2b8fc-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Bonusly is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bonusly is tooa user in Azure AD.</span></span> <span data-ttu-id="2b8fc-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Bonusly toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-138">In other words, a link relationship between an Azure AD user and hello related user in Bonusly needs toobe established.</span></span>

<span data-ttu-id="2b8fc-139">Wijs in Bonusly, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-139">In Bonusly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2b8fc-140">tooconfigure en eenmalige aanmelding Azure AD-test met Bonusly, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2b8fc-140">tooconfigure and test Azure AD single sign-on with Bonusly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2b8fc-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2b8fc-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2b8fc-143">**[Maak een Bonusly testgebruiker](#create-a-bonusly-test-user)**  -toohave een equivalent van Britta Simon in Bonusly die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - toohave a counterpart of Britta Simon in Bonusly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2b8fc-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2b8fc-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2b8fc-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2b8fc-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2b8fc-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Bonusly configureren.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="2b8fc-148">**Azure AD tooconfigure eenmalige aanmelding met Bonusly, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2b8fc-148">**tooconfigure Azure AD single sign-on with Bonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b8fc-149">In de Azure-portal op Hallo Hallo **Bonusly** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-149">In hello Azure portal, on hello **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2b8fc-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="2b8fc-153">Op Hallo **Bonusly domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2b8fc-153">On hello **Bonusly Domain and URLs** section, perform hello following steps:</span></span>

    ![Bonusly domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="2b8fc-155">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="2b8fc-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2b8fc-156">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-156">hello value is not real.</span></span> <span data-ttu-id="2b8fc-157">Waarde van de update Hallo met Hallo werkelijke antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-157">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="2b8fc-158">Neem contact op met [Bonusly ondersteuningsteam](https://Bonusly/contact) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-158">Contact [Bonusly support team](https://Bonusly/contact) tooget hello value.</span></span>
 
4. <span data-ttu-id="2b8fc-159">Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van Hallo-certificaat.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="2b8fc-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-161">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2b8fc-163">Op Hallo **Bonusly configuratie** sectie, klikt u op **Bonusly configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-163">On hello **Bonusly Configuration** section, click **Configure Bonusly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2b8fc-164">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="2b8fc-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Bonusly configuratie](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="2b8fc-166">Aanmelden in een ander browservenster tooyour **Bonusly** tenant.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-166">In a different browser window, log in tooyour **Bonusly** tenant.</span></span>

8. <span data-ttu-id="2b8fc-167">Klik in de werkbalk bovenaan Hallo Hallo op **instellingen**, en selecteer vervolgens **integraties en apps**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-167">In hello toolbar on hello top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="2b8fc-168">![Bonusly sociale sectie](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="2b8fc-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="2b8fc-169">Onder **Single Sign-On**, selecteer **SAML**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="2b8fc-170">Op Hallo **SAML** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2b8fc-170">On hello **SAML** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="2b8fc-171">![Bonusly Saml dialoogvenster pagina](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="2b8fc-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="2b8fc-172">a.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-172">a.</span></span> <span data-ttu-id="2b8fc-173">In Hallo **doel-URL voor eenmalige aanmelding IdP** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-173">In hello **IdP SSO target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="2b8fc-174">b.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-174">b.</span></span> <span data-ttu-id="2b8fc-175">In Hallo **IdP verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-175">In hello **IdP Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="2b8fc-176">c.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-176">c.</span></span> <span data-ttu-id="2b8fc-177">In Hallo **IdP aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-177">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2b8fc-178">d.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-178">d.</span></span> <span data-ttu-id="2b8fc-179">Plak de **vingerafdruk** waarde gekopieerd vanuit Azure-portal naar Hallo **Cert vingerafdruk** textbox.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-179">Paste the **Thumbprint** value copied from Azure portal into hello **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="2b8fc-180">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2b8fc-181">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2b8fc-182">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2b8fc-183">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2b8fc-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2b8fc-184">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2b8fc-184">Create an Azure AD test user</span></span>
<span data-ttu-id="2b8fc-185">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="2b8fc-187">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2b8fc-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b8fc-188">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2b8fc-190">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2b8fc-192">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2b8fc-194">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2b8fc-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2b8fc-196">a.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-196">a.</span></span> <span data-ttu-id="2b8fc-197">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2b8fc-198">b.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-198">b.</span></span> <span data-ttu-id="2b8fc-199">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2b8fc-200">c.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-200">c.</span></span> <span data-ttu-id="2b8fc-201">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2b8fc-202">d.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-202">d.</span></span> <span data-ttu-id="2b8fc-203">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="2b8fc-204">Een Bonusly testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2b8fc-204">Create a Bonusly test user</span></span>

<span data-ttu-id="2b8fc-205">In de volgorde tooenable Azure AD gebruikers toolog in tooBonusly, moeten ze worden ingericht in Bonusly.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-205">In order tooenable Azure AD users toolog in tooBonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="2b8fc-206">In geval van Bonusly Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-206">In hello case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="2b8fc-207">U kunt een andere gebruiker Bonusly account hulpmiddelen voor het maken of API's die worden geleverd door Bonusly tooprovision AAD gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly tooprovision AAD user accounts.</span></span>
>  

<span data-ttu-id="2b8fc-208">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2b8fc-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b8fc-209">Aanmelden tooyour Bonusly tenant in een browservenster.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-209">In a web browser window, log in tooyour Bonusly tenant.</span></span>

2. <span data-ttu-id="2b8fc-210">Klik op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="2b8fc-211">![Instellingen](./media/active-directory-saas-bonus-tutorial/ic781041.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="2b8fc-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="2b8fc-212">Klik op Hallo **gebruikers en bonussen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-212">Click hello **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="2b8fc-213">![Gebruikers en bonussen](./media/active-directory-saas-bonus-tutorial/ic781042.png "gebruikers en bonussen")</span><span class="sxs-lookup"><span data-stu-id="2b8fc-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="2b8fc-214">Klik op **gebruikers beheren**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="2b8fc-215">![Gebruikers beheren](./media/active-directory-saas-bonus-tutorial/ic781043.png "gebruikers beheren")</span><span class="sxs-lookup"><span data-stu-id="2b8fc-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="2b8fc-216">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="2b8fc-217">![Gebruiker toevoegen](./media/active-directory-saas-bonus-tutorial/ic781044.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="2b8fc-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="2b8fc-218">Op Hallo **gebruiker toevoegen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="2b8fc-218">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="2b8fc-219">![Gebruiker toevoegen](./media/active-directory-saas-bonus-tutorial/ic781045.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="2b8fc-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="2b8fc-220">a.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-220">a.</span></span> <span data-ttu-id="2b8fc-221">In Hallo **voornaam** textbox Voer Hallo voornaam van de gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-221">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="2b8fc-222">b.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-222">b.</span></span> <span data-ttu-id="2b8fc-223">In Hallo **achternaam** textbox Voer Hallo achternaam van de gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-223">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="2b8fc-224">c.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-224">c.</span></span> <span data-ttu-id="2b8fc-225">In Hallo **e** textbox Voer Hallo e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="2b8fc-225">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="2b8fc-226">d.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-226">d.</span></span> <span data-ttu-id="2b8fc-227">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="2b8fc-228">Hello Azure AD-accounthouder ontvangt een e-mailbericht met een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-228">hello Azure AD account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span>
     >  

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2b8fc-229">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b8fc-229">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2b8fc-230">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooBonusly toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBonusly.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="2b8fc-232">**tooassign Britta Simon tooBonusly, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2b8fc-232">**tooassign Britta Simon tooBonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b8fc-233">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2b8fc-235">Selecteer in de lijst met de toepassingen van Hallo **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-235">In hello applications list, select **Bonusly**.</span></span>

    ![Hallo Bonusly koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="2b8fc-237">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. <span data-ttu-id="2b8fc-239">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-239">Click **Add** button.</span></span> <span data-ttu-id="2b8fc-240">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="2b8fc-242">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2b8fc-243">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2b8fc-244">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2b8fc-245">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2b8fc-245">Test single sign-on</span></span>

<span data-ttu-id="2b8fc-246">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2b8fc-247">Wanneer u klikt op Hallo Bonusly tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Bonusly toepassing.</span><span class="sxs-lookup"><span data-stu-id="2b8fc-247">When you click hello Bonusly tile in hello Access Panel, you should get automatically signed-on tooyour Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2b8fc-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2b8fc-248">Additional resources</span></span>

* [<span data-ttu-id="2b8fc-249">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b8fc-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2b8fc-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2b8fc-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

