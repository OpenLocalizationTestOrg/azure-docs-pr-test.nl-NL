---
title: 'Zelfstudie: Azure Active Directory-integratie met kleine verbeteringen | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory- en kleine verbeteringen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33213fe4b61f5005cf78bee2c05b2b1e5e71ae8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a><span data-ttu-id="78f39-103">Zelfstudie: Azure Active Directory-integratie met kleine verbeteringen</span><span class="sxs-lookup"><span data-stu-id="78f39-103">Tutorial: Azure Active Directory integration with Small Improvements</span></span>

<span data-ttu-id="78f39-104">In deze zelfstudie leert u hoe toointegrate kleine verbeteringen met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="78f39-104">In this tutorial, you learn how toointegrate Small Improvements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="78f39-105">Kleine verbeteringen integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="78f39-105">Integrating Small Improvements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="78f39-106">U kunt beheren in Azure AD wie toegang tot tooSmall verbeteringen heeft</span><span class="sxs-lookup"><span data-stu-id="78f39-106">You can control in Azure AD who has access tooSmall Improvements</span></span>
- <span data-ttu-id="78f39-107">U kunt uw gebruikers tooautomatically get aangemelde tooSmall verbeteringen (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="78f39-107">You can enable your users tooautomatically get signed-on tooSmall Improvements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="78f39-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="78f39-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="78f39-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="78f39-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78f39-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="78f39-110">Prerequisites</span></span>

<span data-ttu-id="78f39-111">Azure AD-integratie met kleine verbeteringen tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="78f39-111">tooconfigure Azure AD integration with Small Improvements, you need hello following items:</span></span>

- <span data-ttu-id="78f39-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="78f39-112">An Azure AD subscription</span></span>
- <span data-ttu-id="78f39-113">Een kleine verbeteringen eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="78f39-113">A Small Improvements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="78f39-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="78f39-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="78f39-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="78f39-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="78f39-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="78f39-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="78f39-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u hier een proefversie van één maand krijgen [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78f39-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="78f39-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="78f39-118">Scenario description</span></span>
<span data-ttu-id="78f39-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="78f39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="78f39-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="78f39-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78f39-121">Het toevoegen van kleine verbeteringen van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="78f39-121">Adding Small Improvements from hello gallery</span></span>
2. <span data-ttu-id="78f39-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="78f39-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-small-improvements-from-hello-gallery"></a><span data-ttu-id="78f39-123">Het toevoegen van kleine verbeteringen van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="78f39-123">Adding Small Improvements from hello gallery</span></span>
<span data-ttu-id="78f39-124">tooconfigure hello integratie van kleine verbeteringen in Azure AD, moet u tooadd kleine verbeteringen in Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="78f39-124">tooconfigure hello integration of Small Improvements into Azure AD, you need tooadd Small Improvements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="78f39-125">**tooadd kleine verbeteringen via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="78f39-125">**tooadd Small Improvements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="78f39-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="78f39-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="78f39-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="78f39-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="78f39-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="78f39-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="78f39-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="78f39-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="78f39-133">Typ in het zoekvak Hallo **kleine verbeteringen**.</span><span class="sxs-lookup"><span data-stu-id="78f39-133">In hello search box, type **Small Improvements**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_search.png)

5. <span data-ttu-id="78f39-135">Selecteer in het deelvenster resultaten hello, **kleine verbeteringen**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="78f39-135">In hello results panel, select **Small Improvements**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="78f39-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="78f39-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="78f39-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met kleine verbeteringen op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="78f39-138">In this section, you configure and test Azure AD single sign-on with Small Improvements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="78f39-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in kleine verbeteringen is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78f39-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Small Improvements is tooa user in Azure AD.</span></span> <span data-ttu-id="78f39-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in kleine verbeteringen toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="78f39-140">In other words, a link relationship between an Azure AD user and hello related user in Small Improvements needs toobe established.</span></span>

<span data-ttu-id="78f39-141">Wijs in kleine verbeteringen Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="78f39-141">In Small Improvements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="78f39-142">tooconfigure en eenmalige aanmelding Azure AD-test met kleine verbeteringen, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="78f39-142">tooconfigure and test Azure AD single sign-on with Small Improvements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="78f39-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="78f39-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="78f39-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="78f39-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="78f39-145">**[Maken van een testgebruiker kleine verbeteringen](#creating-a-small-improvements-test-user)**  -toohave een equivalent van Britta Simon in kleine verbeteringen die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="78f39-145">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - toohave a counterpart of Britta Simon in Small Improvements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="78f39-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="78f39-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="78f39-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="78f39-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="78f39-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="78f39-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="78f39-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing kleine verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="78f39-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Small Improvements application.</span></span>

<span data-ttu-id="78f39-150">**Voer tooconfigure Azure AD eenmalige aanmelding met kleine verbeteringen Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="78f39-150">**tooconfigure Azure AD single sign-on with Small Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="78f39-151">In de Azure-portal op Hallo Hallo **kleine verbeteringen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="78f39-151">In hello Azure portal, on hello **Small Improvements** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="78f39-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="78f39-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_samlbase.png)

3. <span data-ttu-id="78f39-155">Op Hallo **kleine verbeteringen domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="78f39-155">On hello **Small Improvements Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_url.png)

    <span data-ttu-id="78f39-157">a.</span><span class="sxs-lookup"><span data-stu-id="78f39-157">a.</span></span> <span data-ttu-id="78f39-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="78f39-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    <span data-ttu-id="78f39-159">b.</span><span class="sxs-lookup"><span data-stu-id="78f39-159">b.</span></span> <span data-ttu-id="78f39-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="78f39-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="78f39-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="78f39-161">These values are not real.</span></span> <span data-ttu-id="78f39-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="78f39-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="78f39-163">Neem contact op met [kleine verbeteringen Client ondersteuningsteam](mailto:support@small-improvements.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="78f39-163">Contact [Small Improvements Client support team](mailto:support@small-improvements.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="78f39-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="78f39-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_certificate.png) 

5. <span data-ttu-id="78f39-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="78f39-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="78f39-168">Op Hallo **kleine verbeteringen configuratie** sectie, klikt u op **kleine verbeteringen configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="78f39-168">On hello **Small Improvements Configuration** section, click **Configure Small Improvements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="78f39-169">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="78f39-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_configure.png) 

7. <span data-ttu-id="78f39-171">Een ander browservenster geopend Meld u aan bij tooyour kleine verbeteringen bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="78f39-171">In another browser window, sign on tooyour Small Improvements company site as an administrator.</span></span>

8. <span data-ttu-id="78f39-172">Klik op de pagina Hallo hoofddashboard **beheer** knop aan de linkerkant Hallo.</span><span class="sxs-lookup"><span data-stu-id="78f39-172">From hello main dashboard page, click **Administration** button on hello left.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_06.png) 

9. <span data-ttu-id="78f39-174">Klik op Hallo **SAML SSO** knop van **integraties** sectie.</span><span class="sxs-lookup"><span data-stu-id="78f39-174">Click hello **SAML SSO** button from **Integrations** section.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_07.png) 

10. <span data-ttu-id="78f39-176">Op Hallo SSO-installatiepagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="78f39-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_08.png)  

    <span data-ttu-id="78f39-178">a.</span><span class="sxs-lookup"><span data-stu-id="78f39-178">a.</span></span> <span data-ttu-id="78f39-179">In Hallo **HTTP-eindpunt** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="78f39-179">In hello **HTTP Endpoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="78f39-180">b.</span><span class="sxs-lookup"><span data-stu-id="78f39-180">b.</span></span> <span data-ttu-id="78f39-181">Open uw gedownloade certificaat in Kladblok, kopieer Hallo inhoud, en plak deze in Hallo **x509 certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="78f39-181">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="78f39-182">c.</span><span class="sxs-lookup"><span data-stu-id="78f39-182">c.</span></span> <span data-ttu-id="78f39-183">Als u toohave eenmalige aanmelding en aanmelding formulier verificatieoptie beschikbaar voor gebruikers wenst, controleert u Hallo **toegang via aanmelding en wachtwoord te inschakelen** optie.</span><span class="sxs-lookup"><span data-stu-id="78f39-183">If you wish toohave SSO and Login form authentication option available for users, then check hello **Enable access via login/password too** option.</span></span>  

    <span data-ttu-id="78f39-184">d.</span><span class="sxs-lookup"><span data-stu-id="78f39-184">d.</span></span> <span data-ttu-id="78f39-185">Voer Hallo geschikte waarde tooName Hallo SSO aanmelding knop in Hallo **SAML vragen** textbox.</span><span class="sxs-lookup"><span data-stu-id="78f39-185">Enter hello appropriate value tooName hello SSO Login button in hello **SAML Prompt** textbox.</span></span>  

    <span data-ttu-id="78f39-186">e.</span><span class="sxs-lookup"><span data-stu-id="78f39-186">e.</span></span> <span data-ttu-id="78f39-187">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="78f39-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="78f39-188">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="78f39-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="78f39-189">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="78f39-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="78f39-190">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="78f39-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="78f39-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="78f39-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="78f39-192">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="78f39-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="78f39-194">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="78f39-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="78f39-195">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="78f39-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="78f39-197">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="78f39-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="78f39-199">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="78f39-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="78f39-201">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="78f39-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="78f39-203">a.</span><span class="sxs-lookup"><span data-stu-id="78f39-203">a.</span></span> <span data-ttu-id="78f39-204">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="78f39-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="78f39-205">b.</span><span class="sxs-lookup"><span data-stu-id="78f39-205">b.</span></span> <span data-ttu-id="78f39-206">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="78f39-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="78f39-207">c.</span><span class="sxs-lookup"><span data-stu-id="78f39-207">c.</span></span> <span data-ttu-id="78f39-208">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="78f39-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="78f39-209">d.</span><span class="sxs-lookup"><span data-stu-id="78f39-209">d.</span></span> <span data-ttu-id="78f39-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="78f39-210">Click **Create**.</span></span>
 
### <a name="creating-a-small-improvements-test-user"></a><span data-ttu-id="78f39-211">Een kleine verbeteringen testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="78f39-211">Creating a Small Improvements test user</span></span>

<span data-ttu-id="78f39-212">Azure AD tooenable gebruikers toolog in tooSmall verbeteringen, moeten ze worden ingericht in kleine verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="78f39-212">tooenable Azure AD users toolog in tooSmall Improvements, they must be provisioned into Small Improvements.</span></span> <span data-ttu-id="78f39-213">In geval van kleine verbeteringen Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="78f39-213">In hello case of Small Improvements, provisioning is a manual task.</span></span>

<span data-ttu-id="78f39-214">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="78f39-214">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="78f39-215">Eenmalige aanmelding tooyour kleine verbeteringen bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="78f39-215">Sign-on tooyour Small Improvements company site as an administrator.</span></span>

2. <span data-ttu-id="78f39-216">Ga op de introductiepagina Hallo toohello menu op Hallo van links, klikt u op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="78f39-216">From hello Home page, go toohello menu on hello left, click **Administration**.</span></span>

3. <span data-ttu-id="78f39-217">Klik op Hallo **gebruikerslijst** knop uit de sectie beheer van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="78f39-217">Click hello **User Directory** button from User Management section.</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_10.png) 

4. <span data-ttu-id="78f39-219">Klik op **gebruikers toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="78f39-219">Click **Add users**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png) 

5. <span data-ttu-id="78f39-221">Op Hallo **gebruikers toevoegen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="78f39-221">On hello **Add Users** dialog, perform hello following steps:</span></span> 

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)
    
    <span data-ttu-id="78f39-223">a.</span><span class="sxs-lookup"><span data-stu-id="78f39-223">a.</span></span> <span data-ttu-id="78f39-224">Voer Hallo **voornaam** van gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="78f39-224">Enter hello **first name** of user like **Britta**.</span></span>

    <span data-ttu-id="78f39-225">b.</span><span class="sxs-lookup"><span data-stu-id="78f39-225">b.</span></span> <span data-ttu-id="78f39-226">Voer Hallo **achternaam** van gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="78f39-226">Enter hello **Last name** of user like **Simon**.</span></span>

    <span data-ttu-id="78f39-227">c.</span><span class="sxs-lookup"><span data-stu-id="78f39-227">c.</span></span> <span data-ttu-id="78f39-228">Voer Hallo **e** van gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="78f39-228">Enter hello **Email** of user like **brittasimon@contoso.com**.</span></span> 

    <span data-ttu-id="78f39-229">d.</span><span class="sxs-lookup"><span data-stu-id="78f39-229">d.</span></span> <span data-ttu-id="78f39-230">U kunt ook persoonlijke tooenter Hallo-bericht in Hallo **e-mailmelding verzenden** vak.</span><span class="sxs-lookup"><span data-stu-id="78f39-230">You can also choose tooenter hello personal message in hello **Send notification email** box.</span></span> <span data-ttu-id="78f39-231">Als u niet dat toosend Hallo melding wenst, schakelt u dit selectievakje in.</span><span class="sxs-lookup"><span data-stu-id="78f39-231">If you do not wish toosend hello notification, then uncheck this checkbox.</span></span>

    <span data-ttu-id="78f39-232">e.</span><span class="sxs-lookup"><span data-stu-id="78f39-232">e.</span></span> <span data-ttu-id="78f39-233">Klik op **gebruikers maken**.</span><span class="sxs-lookup"><span data-stu-id="78f39-233">Click **Create Users**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="78f39-234">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="78f39-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="78f39-235">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSmall verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="78f39-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmall Improvements.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="78f39-237">**tooassign Britta Simon tooSmall verbeteringen, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="78f39-237">**tooassign Britta Simon tooSmall Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="78f39-238">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="78f39-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="78f39-240">Selecteer in de lijst met de toepassingen van Hallo **kleine verbeteringen**.</span><span class="sxs-lookup"><span data-stu-id="78f39-240">In hello applications list, select **Small Improvements**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_app.png) 

3. <span data-ttu-id="78f39-242">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="78f39-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="78f39-244">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="78f39-244">Click **Add** button.</span></span> <span data-ttu-id="78f39-245">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="78f39-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="78f39-247">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="78f39-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="78f39-248">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="78f39-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="78f39-249">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="78f39-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="78f39-250">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="78f39-250">Testing single sign-on</span></span>

<span data-ttu-id="78f39-251">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="78f39-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="78f39-252">Wanneer u Hallo kleine verbeteringen in Hallo Toegangsvenster tegel klikt, krijgt u automatisch aangemelde tooyour kleine verbeteringen toepassing.</span><span class="sxs-lookup"><span data-stu-id="78f39-252">When you click hello Small Improvements tile in hello Access Panel, you should get automatically signed-on tooyour Small Improvements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78f39-253">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="78f39-253">Additional resources</span></span>

* [<span data-ttu-id="78f39-254">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78f39-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78f39-255">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="78f39-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_203.png

