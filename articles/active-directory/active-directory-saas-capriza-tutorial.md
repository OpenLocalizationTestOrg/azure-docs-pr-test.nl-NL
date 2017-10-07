---
title: 'Zelfstudie: Azure Active Directory-integratie met Capriza Platform | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Capriza Platform.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48d92247-f00a-47b9-8d4e-137028d9e200
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 1c4adb737bb5ba4690bbf74688010238c5c83f3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-capriza-platform"></a><span data-ttu-id="4fc75-103">Zelfstudie: Azure Active Directory-integratie met Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="4fc75-103">Tutorial: Azure Active Directory integration with Capriza Platform</span></span>

<span data-ttu-id="4fc75-104">In deze zelfstudie leert u hoe toointegrate Capriza Platform met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4fc75-104">In this tutorial, you learn how toointegrate Capriza Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4fc75-105">Capriza Platform integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4fc75-105">Integrating Capriza Platform with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4fc75-106">U kunt beheren in Azure AD wie toegang tot tooCapriza Platform heeft</span><span class="sxs-lookup"><span data-stu-id="4fc75-106">You can control in Azure AD who has access tooCapriza Platform</span></span>
- <span data-ttu-id="4fc75-107">U kunt uw gebruikers tooautomatically get aangemelde tooCapriza Platform (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="4fc75-107">You can enable your users tooautomatically get signed-on tooCapriza Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4fc75-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="4fc75-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4fc75-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4fc75-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fc75-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4fc75-110">Prerequisites</span></span>

<span data-ttu-id="4fc75-111">Azure AD-integratie met Capriza Platform tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="4fc75-111">tooconfigure Azure AD integration with Capriza Platform, you need hello following items:</span></span>

- <span data-ttu-id="4fc75-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4fc75-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4fc75-113">Een Capriza Platform eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="4fc75-113">A Capriza Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4fc75-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4fc75-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4fc75-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4fc75-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4fc75-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4fc75-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4fc75-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4fc75-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4fc75-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="4fc75-118">Scenario description</span></span>
<span data-ttu-id="4fc75-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4fc75-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4fc75-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="4fc75-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4fc75-121">Het toevoegen van Capriza Platform van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4fc75-121">Adding Capriza Platform from hello gallery</span></span>
2. <span data-ttu-id="4fc75-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4fc75-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-capriza-platform-from-hello-gallery"></a><span data-ttu-id="4fc75-123">Het toevoegen van Capriza Platform van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4fc75-123">Adding Capriza Platform from hello gallery</span></span>
<span data-ttu-id="4fc75-124">tooconfigure hello integratie van Capriza Platform in Azure AD, moet u tooadd Capriza Platform uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="4fc75-124">tooconfigure hello integration of Capriza Platform into Azure AD, you need tooadd Capriza Platform from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4fc75-125">**tooadd Capriza Platform via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4fc75-125">**tooadd Capriza Platform from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fc75-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4fc75-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4fc75-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4fc75-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4fc75-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4fc75-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="4fc75-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4fc75-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="4fc75-133">Typ in het zoekvak Hallo **Capriza Platform**.</span><span class="sxs-lookup"><span data-stu-id="4fc75-133">In hello search box, type **Capriza Platform**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_search.png)

5. <span data-ttu-id="4fc75-135">Selecteer in het deelvenster resultaten hello, **Capriza Platform**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4fc75-135">In hello results panel, select **Capriza Platform**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4fc75-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4fc75-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4fc75-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Capriza Platform op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4fc75-138">In this section, you configure and test Azure AD single sign-on with Capriza Platform based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4fc75-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Capriza Platform is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fc75-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Capriza Platform is tooa user in Azure AD.</span></span> <span data-ttu-id="4fc75-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Capriza Platform toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="4fc75-140">In other words, a link relationship between an Azure AD user and hello related user in Capriza Platform needs toobe established.</span></span>

<span data-ttu-id="4fc75-141">In Capriza Platform, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="4fc75-141">In Capriza Platform, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4fc75-142">tooconfigure en test eenmalige aanmelding Azure AD met Capriza Platform, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4fc75-142">tooconfigure and test Azure AD single sign-on with Capriza Platform, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4fc75-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="4fc75-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4fc75-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fc75-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4fc75-145">**[Maken van een testgebruiker Capriza Platform](#creating-a-capriza-platform-test-user)**  -toohave een equivalent van Britta Simon in Capriza Platform dat is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4fc75-145">**[Creating a Capriza Platform test user](#creating-a-capriza-platform-test-user)** - toohave a counterpart of Britta Simon in Capriza Platform that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4fc75-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4fc75-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4fc75-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="4fc75-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4fc75-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="4fc75-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4fc75-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Capriza Platform configureren.</span><span class="sxs-lookup"><span data-stu-id="4fc75-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Capriza Platform application.</span></span>

<span data-ttu-id="4fc75-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Capriza Platform Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4fc75-150">**tooconfigure Azure AD single sign-on with Capriza Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fc75-151">In de Azure-portal op Hallo Hallo **Capriza Platform** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4fc75-151">In hello Azure portal, on hello **Capriza Platform** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="4fc75-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4fc75-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_samlbase.png)

3. <span data-ttu-id="4fc75-155">Op Hallo **Capriza Platform domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4fc75-155">On hello **Capriza Platform Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_url.png)

    <span data-ttu-id="4fc75-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.capriza.com/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="4fc75-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.capriza.com/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4fc75-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="4fc75-158">This value is not real.</span></span> <span data-ttu-id="4fc75-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="4fc75-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="4fc75-160">Neem contact op met [Capriza Platform Client ondersteuningsteam](mailTo:support@capriza.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="4fc75-160">Contact [Capriza Platform Client support team](mailTo:support@capriza.com) tooget this value.</span></span> 

4. <span data-ttu-id="4fc75-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4fc75-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_certificate.png) 

5. <span data-ttu-id="4fc75-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4fc75-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-capriza-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4fc75-165">Op Hallo **Capriza platformconfiguratie** sectie, klikt u op **Capriza Platform configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="4fc75-165">On hello **Capriza Platform Configuration** section, click **Configure Capriza Platform** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4fc75-166">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="4fc75-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_configure.png) 

7. <span data-ttu-id="4fc75-168">tooconfigure eenmalige aanmelding op **Capriza Platform** zijde, moet u toosend Hallo gedownload **certificaat**, **Sign-Out URL**, **SAML entiteit-ID** en **SAML Single Sign-On Service-URL** te[Capriza Platform ondersteuningsteam](mailTo:support@capriza.com).</span><span class="sxs-lookup"><span data-stu-id="4fc75-168">tooconfigure single sign-on on **Capriza Platform** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[Capriza Platform support team](mailTo:support@capriza.com).</span></span> <span data-ttu-id="4fc75-169">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4fc75-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="4fc75-170">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="4fc75-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4fc75-171">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="4fc75-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4fc75-172">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4fc75-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4fc75-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4fc75-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="4fc75-174">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4fc75-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="4fc75-176">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4fc75-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fc75-177">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4fc75-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-capriza-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4fc75-179">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4fc75-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-capriza-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4fc75-181">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="4fc75-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-capriza-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4fc75-183">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4fc75-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-capriza-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4fc75-185">a.</span><span class="sxs-lookup"><span data-stu-id="4fc75-185">a.</span></span> <span data-ttu-id="4fc75-186">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4fc75-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4fc75-187">b.</span><span class="sxs-lookup"><span data-stu-id="4fc75-187">b.</span></span> <span data-ttu-id="4fc75-188">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4fc75-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4fc75-189">c.</span><span class="sxs-lookup"><span data-stu-id="4fc75-189">c.</span></span> <span data-ttu-id="4fc75-190">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="4fc75-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4fc75-191">d.</span><span class="sxs-lookup"><span data-stu-id="4fc75-191">d.</span></span> <span data-ttu-id="4fc75-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4fc75-192">Click **Create**.</span></span>
 
### <a name="creating-a-capriza-platform-test-user"></a><span data-ttu-id="4fc75-193">Maken van een testgebruiker Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="4fc75-193">Creating a Capriza Platform test user</span></span>

<span data-ttu-id="4fc75-194">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Capriza van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4fc75-194">hello objective of this section is toocreate a user called Britta Simon in Capriza.</span></span> <span data-ttu-id="4fc75-195">Capriza ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4fc75-195">Capriza supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="4fc75-196">**Zorg dat de domeinnaam van uw is geconfigureerd met Capriza voor gebruikers inrichten. Na die alleen Hallo werkt just in time gebruikersaanvragen.**</span><span class="sxs-lookup"><span data-stu-id="4fc75-196">**Please make sure that your domain name is configured with Capriza for user provisioning. After that only hello just-in-time user provisioning will work.**</span></span>

<span data-ttu-id="4fc75-197">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="4fc75-197">There is no action item for you in this section.</span></span> <span data-ttu-id="4fc75-198">Een nieuwe gebruiker wordt tijdens een poging tooaccess Capriza gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="4fc75-198">A new user will be created during an attempt tooaccess Capriza if it doesn't exist yet.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4fc75-199">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fc75-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4fc75-200">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooCapriza Platform.</span><span class="sxs-lookup"><span data-stu-id="4fc75-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCapriza Platform.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="4fc75-202">**tooassign Britta Simon tooCapriza Platform, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4fc75-202">**tooassign Britta Simon tooCapriza Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fc75-203">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4fc75-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="4fc75-205">Selecteer in de lijst met de toepassingen van Hallo **Capriza Platform**.</span><span class="sxs-lookup"><span data-stu-id="4fc75-205">In hello applications list, select **Capriza Platform**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_app.png) 

3. <span data-ttu-id="4fc75-207">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="4fc75-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="4fc75-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4fc75-209">Click **Add** button.</span></span> <span data-ttu-id="4fc75-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4fc75-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="4fc75-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="4fc75-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4fc75-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4fc75-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4fc75-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4fc75-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4fc75-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4fc75-215">Testing single sign-on</span></span>

<span data-ttu-id="4fc75-216">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="4fc75-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4fc75-217">Als u op Hallo Capriza Platform-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Capriza toepassing.</span><span class="sxs-lookup"><span data-stu-id="4fc75-217">When you click hello Capriza Platform tile in hello Access Panel, you should get automatically signed-on tooyour Capriza application.</span></span> <span data-ttu-id="4fc75-218">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4fc75-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4fc75-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4fc75-219">Additional resources</span></span>

* [<span data-ttu-id="4fc75-220">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4fc75-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4fc75-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4fc75-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_203.png

