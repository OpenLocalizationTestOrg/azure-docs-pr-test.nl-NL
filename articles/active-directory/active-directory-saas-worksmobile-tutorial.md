---
title: 'Zelfstudie: Azure Active Directory-integratie met WORKS MOBILE | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en werkt MOBILE.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 80192218a2e99a921834bb53e708d5e4fab413f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="70ad3-103">Zelfstudie: Azure Active Directory-integratie met WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="70ad3-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="70ad3-104">In deze zelfstudie leert u hoe toointegrate werkt MOBIEL met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70ad3-104">In this tutorial, you learn how toointegrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70ad3-105">WERKT MOBILE integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="70ad3-105">Integrating WORKS MOBILE with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="70ad3-106">U kunt beheren in Azure AD wie toegang tot tooWORKS MOBILE heeft</span><span class="sxs-lookup"><span data-stu-id="70ad3-106">You can control in Azure AD who has access tooWORKS MOBILE</span></span>
- <span data-ttu-id="70ad3-107">U kunt uw gebruikers tooautomatically get aangemelde tooWORKS MOBILE (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="70ad3-107">You can enable your users tooautomatically get signed-on tooWORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70ad3-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="70ad3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="70ad3-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="70ad3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70ad3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="70ad3-110">Prerequisites</span></span>

<span data-ttu-id="70ad3-111">Azure AD-integratie met WORKS MOBILE tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="70ad3-111">tooconfigure Azure AD integration with WORKS MOBILE, you need hello following items:</span></span>

- <span data-ttu-id="70ad3-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="70ad3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70ad3-113">Een mobiele werkt eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="70ad3-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70ad3-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="70ad3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70ad3-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="70ad3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70ad3-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="70ad3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70ad3-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70ad3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70ad3-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="70ad3-118">Scenario description</span></span>
<span data-ttu-id="70ad3-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="70ad3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70ad3-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="70ad3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70ad3-121">Het toevoegen van WORKS MOBILE van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="70ad3-121">Adding WORKS MOBILE from hello gallery</span></span>
2. <span data-ttu-id="70ad3-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="70ad3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-hello-gallery"></a><span data-ttu-id="70ad3-123">Het toevoegen van WORKS MOBILE van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="70ad3-123">Adding WORKS MOBILE from hello gallery</span></span>
<span data-ttu-id="70ad3-124">tooconfigure hello integratie van MOBILE werkt met Azure AD, moet u tooadd WORKS MOBILE uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="70ad3-124">tooconfigure hello integration of WORKS MOBILE into Azure AD, you need tooadd WORKS MOBILE from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="70ad3-125">**tooadd WORKS MOBILE via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="70ad3-125">**tooadd WORKS MOBILE from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="70ad3-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="70ad3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70ad3-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="70ad3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="70ad3-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="70ad3-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="70ad3-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="70ad3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="70ad3-133">Typ in het zoekvak Hallo **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="70ad3-133">In hello search box, type **WORKS MOBILE**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="70ad3-135">Selecteer in het deelvenster resultaten hello, **WORKS MOBILE**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="70ad3-135">In hello results panel, select **WORKS MOBILE**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70ad3-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="70ad3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="70ad3-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met WORKS MOBILE op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="70ad3-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="70ad3-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in WORKS MOBILE is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70ad3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in WORKS MOBILE is tooa user in Azure AD.</span></span> <span data-ttu-id="70ad3-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in WORKS MOBILE toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="70ad3-140">In other words, a link relationship between an Azure AD user and hello related user in WORKS MOBILE needs toobe established.</span></span>

<span data-ttu-id="70ad3-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in MOBILE werkt.</span><span class="sxs-lookup"><span data-stu-id="70ad3-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="70ad3-142">tooconfigure en test eenmalige aanmelding Azure AD met MOBILE werkt, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="70ad3-142">tooconfigure and test Azure AD single sign-on with WORKS MOBILE, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="70ad3-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="70ad3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="70ad3-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70ad3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70ad3-145">**[Maken van een gebruiker van de test werkt MOBILE](#creating-a-works-mobile-test-user)**  -toohave een equivalent van Britta Simon in MOBILE werkt die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="70ad3-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - toohave a counterpart of Britta Simon in WORKS MOBILE that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="70ad3-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="70ad3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70ad3-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="70ad3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70ad3-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="70ad3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70ad3-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing werkt MOBILE.</span><span class="sxs-lookup"><span data-stu-id="70ad3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="70ad3-150">**Voer tooconfigure Azure AD eenmalige aanmelding met MOBILE werkt, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="70ad3-150">**tooconfigure Azure AD single sign-on with WORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="70ad3-151">In Azure-portal op Hallo Hallo **WORKS MOBILE** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="70ad3-151">In hello Azure portal, on hello **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="70ad3-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="70ad3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="70ad3-155">Op Hallo **WORKS MOBILE domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="70ad3-155">On hello **WORKS MOBILE Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="70ad3-157">a.</span><span class="sxs-lookup"><span data-stu-id="70ad3-157">a.</span></span> <span data-ttu-id="70ad3-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="70ad3-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="70ad3-159">b.</span><span class="sxs-lookup"><span data-stu-id="70ad3-159">b.</span></span> <span data-ttu-id="70ad3-160">In Hallo **id** textbox Hallo typewaarde als`worksmobile.com`</span><span class="sxs-lookup"><span data-stu-id="70ad3-160">In hello **Identifier** textbox, type hello value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="70ad3-161">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="70ad3-161">This value is not real.</span></span> <span data-ttu-id="70ad3-162">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="70ad3-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="70ad3-163">Neem contact op met [MOBILE-Client werkt ondersteuningsteam](mailto:dl_ssoinfo@worksmobile.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="70ad3-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="70ad3-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Raw)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="70ad3-164">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="70ad3-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="70ad3-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="70ad3-168">Op Hallo **configuratie van de mobiele WORKS** sectie, klikt u op **configureren WORKS MOBILE** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="70ad3-168">On hello **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="70ad3-169">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="70ad3-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="70ad3-171">tooget SSO geconfigureerd voor uw toepassing, neem contact op met [WORKS MOBILE ondersteuningsteam](mailto:dl_ssoinfo@worksmobile.com) en voorzien Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="70ad3-171">tooget SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with hello following information:</span></span> 

    <span data-ttu-id="70ad3-172">• Hallo gedownload **certificaatbestand**</span><span class="sxs-lookup"><span data-stu-id="70ad3-172">• hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="70ad3-173">• Hallo **SAML Single Sign-On Service-URL**</span><span class="sxs-lookup"><span data-stu-id="70ad3-173">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="70ad3-174">• Hallo **SAML entiteit-ID**</span><span class="sxs-lookup"><span data-stu-id="70ad3-174">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="70ad3-175">• Hallo **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="70ad3-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="70ad3-176">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="70ad3-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="70ad3-177">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="70ad3-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="70ad3-178">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="70ad3-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70ad3-179">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="70ad3-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="70ad3-180">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="70ad3-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="70ad3-182">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="70ad3-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="70ad3-183">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="70ad3-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70ad3-185">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="70ad3-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70ad3-187">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="70ad3-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70ad3-189">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="70ad3-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70ad3-191">a.</span><span class="sxs-lookup"><span data-stu-id="70ad3-191">a.</span></span> <span data-ttu-id="70ad3-192">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="70ad3-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70ad3-193">b.</span><span class="sxs-lookup"><span data-stu-id="70ad3-193">b.</span></span> <span data-ttu-id="70ad3-194">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="70ad3-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70ad3-195">c.</span><span class="sxs-lookup"><span data-stu-id="70ad3-195">c.</span></span> <span data-ttu-id="70ad3-196">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="70ad3-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="70ad3-197">d.</span><span class="sxs-lookup"><span data-stu-id="70ad3-197">d.</span></span> <span data-ttu-id="70ad3-198">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="70ad3-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="70ad3-199">Maken van een gebruiker van de test werkt MOBILE</span><span class="sxs-lookup"><span data-stu-id="70ad3-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="70ad3-200">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in WORKS MOBILE maken.</span><span class="sxs-lookup"><span data-stu-id="70ad3-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="70ad3-201">Neem contact op met [WORKS MOBILE ondersteuningsteam](mailto:dl_ssoinfo@worksmobile.com) tooadd Hallo gebruikers in Hallo WORKS MOBIEL platform.</span><span class="sxs-lookup"><span data-stu-id="70ad3-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) tooadd hello users in hello WORKS MOBILE platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="70ad3-202">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="70ad3-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="70ad3-203">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooWORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="70ad3-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWORKS MOBILE.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="70ad3-205">**tooassign Britta Simon tooWORKS MOBILE, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="70ad3-205">**tooassign Britta Simon tooWORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="70ad3-206">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="70ad3-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="70ad3-208">Selecteer in de lijst met de toepassingen van Hallo **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="70ad3-208">In hello applications list, select **WORKS MOBILE**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="70ad3-210">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="70ad3-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="70ad3-212">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="70ad3-212">Click **Add** button.</span></span> <span data-ttu-id="70ad3-213">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="70ad3-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="70ad3-215">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="70ad3-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="70ad3-216">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="70ad3-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70ad3-217">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="70ad3-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="70ad3-218">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="70ad3-218">Testing single sign-on</span></span>

<span data-ttu-id="70ad3-219">In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="70ad3-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="70ad3-220">Als u op Hallo WORKS MOBILE tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour WORKS mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="70ad3-220">When you click hello WORKS MOBILE tile in hello Access Panel, you should get automatically signed-on tooyour WORKS MOBILE application.</span></span>
<span data-ttu-id="70ad3-221">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="70ad3-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="70ad3-222">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="70ad3-222">Additional resources</span></span>

* [<span data-ttu-id="70ad3-223">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70ad3-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70ad3-224">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="70ad3-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

