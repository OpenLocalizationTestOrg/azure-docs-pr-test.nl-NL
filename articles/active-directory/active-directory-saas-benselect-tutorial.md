---
title: 'Zelfstudie: Azure Active Directory-integratie met BenSelect | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en BenSelect.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c3705da337bf8f6e76de58cd21c5b047c8f5e12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="ac62d-103">Zelfstudie: Azure Active Directory-integratie met BenSelect</span><span class="sxs-lookup"><span data-stu-id="ac62d-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="ac62d-104">In deze zelfstudie leert u hoe toointegrate BenSelect met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ac62d-104">In this tutorial, you learn how toointegrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ac62d-105">BenSelect integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ac62d-105">Integrating BenSelect with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ac62d-106">U kunt beheren in Azure AD die tooBenSelect toegang heeft</span><span class="sxs-lookup"><span data-stu-id="ac62d-106">You can control in Azure AD who has access tooBenSelect</span></span>
- <span data-ttu-id="ac62d-107">U kunt uw gebruikers tooautomatically get aangemelde tooBenSelect (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ac62d-107">You can enable your users tooautomatically get signed-on tooBenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ac62d-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ac62d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ac62d-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ac62d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac62d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ac62d-110">Prerequisites</span></span>

<span data-ttu-id="ac62d-111">Azure AD-integratie met BenSelect tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ac62d-111">tooconfigure Azure AD integration with BenSelect, you need hello following items:</span></span>

- <span data-ttu-id="ac62d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ac62d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ac62d-113">Een BenSelect eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ac62d-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ac62d-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ac62d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ac62d-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ac62d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ac62d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ac62d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ac62d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ac62d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ac62d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ac62d-118">Scenario description</span></span>
<span data-ttu-id="ac62d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ac62d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ac62d-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ac62d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ac62d-121">Het toevoegen van BenSelect van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ac62d-121">Adding BenSelect from hello gallery</span></span>
2. <span data-ttu-id="ac62d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ac62d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-hello-gallery"></a><span data-ttu-id="ac62d-123">Het toevoegen van BenSelect van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ac62d-123">Adding BenSelect from hello gallery</span></span>
<span data-ttu-id="ac62d-124">tooconfigure hello integratie van BenSelect in Azure AD, moet u tooadd BenSelect uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ac62d-124">tooconfigure hello integration of BenSelect into Azure AD, you need tooadd BenSelect from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ac62d-125">**tooadd BenSelect via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ac62d-125">**tooadd BenSelect from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac62d-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ac62d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ac62d-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ac62d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ac62d-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ac62d-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ac62d-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac62d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ac62d-133">Typ in het zoekvak Hallo **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="ac62d-133">In hello search box, type **BenSelect**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="ac62d-135">Selecteer in het deelvenster resultaten hello, **BenSelect**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ac62d-135">In hello results panel, select **BenSelect**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ac62d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ac62d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ac62d-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met BenSelect op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="ac62d-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ac62d-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in BenSelect is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac62d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenSelect is tooa user in Azure AD.</span></span> <span data-ttu-id="ac62d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in BenSelect toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="ac62d-140">In other words, a link relationship between an Azure AD user and hello related user in BenSelect needs toobe established.</span></span>

<span data-ttu-id="ac62d-141">Wijs in BenSelect, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="ac62d-141">In BenSelect, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ac62d-142">tooconfigure en eenmalige aanmelding Azure AD-test met BenSelect, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ac62d-142">tooconfigure and test Azure AD single sign-on with BenSelect, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ac62d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="ac62d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ac62d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ac62d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ac62d-145">**[Maken van een testgebruiker BenSelect](#creating-a-benselect-test-user)**  -toohave een equivalent van Britta Simon in BenSelect die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ac62d-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - toohave a counterpart of Britta Simon in BenSelect that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ac62d-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ac62d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ac62d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ac62d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ac62d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ac62d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ac62d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing BenSelect configureren.</span><span class="sxs-lookup"><span data-stu-id="ac62d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="ac62d-150">**Azure AD tooconfigure eenmalige aanmelding met BenSelect, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ac62d-150">**tooconfigure Azure AD single sign-on with BenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac62d-151">In de Azure-portal op Hallo Hallo **BenSelect** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ac62d-151">In hello Azure portal, on hello **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ac62d-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ac62d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="ac62d-155">Op Hallo **BenSelect domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ac62d-155">On hello **BenSelect Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="ac62d-157">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="ac62d-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ac62d-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="ac62d-158">This value is not real.</span></span> <span data-ttu-id="ac62d-159">Deze waarde met de werkelijke antwoord-URL Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="ac62d-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="ac62d-160">Neem contact op met [BenSelect ondersteuningsteam](mailto:support@selerix.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="ac62d-160">Contact [BenSelect support team](mailto:support@selerix.com) tooget this value.</span></span>
 
4. <span data-ttu-id="ac62d-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Raw)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ac62d-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="ac62d-163">Hallo SAML asserties verwacht BenSelect toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="ac62d-163">BenSelect application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="ac62d-164">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="ac62d-164">Configure hello following claims for this application.</span></span> <span data-ttu-id="ac62d-165">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **gebruikerskenmerken** sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="ac62d-165">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="ac62d-166">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="ac62d-166">hello following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="ac62d-168">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="ac62d-168">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="ac62d-169">a.</span><span class="sxs-lookup"><span data-stu-id="ac62d-169">a.</span></span> <span data-ttu-id="ac62d-170">In Hallo **gebruikers-id** vervolgkeuzelijst, selecteer **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="ac62d-170">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="ac62d-171">b.</span><span class="sxs-lookup"><span data-stu-id="ac62d-171">b.</span></span> <span data-ttu-id="ac62d-172">In Hallo **Mail** vervolgkeuzelijst, selecteer **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="ac62d-172">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="ac62d-173">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ac62d-173">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ac62d-175">Op Hallo **BenSelect configuratie** sectie, klikt u op **configureren BenSelect** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="ac62d-175">On hello **BenSelect Configuration** section, click **Configure BenSelect** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ac62d-176">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="ac62d-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="ac62d-178">tooconfigure eenmalige aanmelding op **BenSelect** zijde, moet u toosend Hallo gedownload **Certificate(Raw)** en **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL**te[BenSelect ondersteuningsteam](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="ac62d-178">tooconfigure single sign-on on **BenSelect** side, you need toosend hello downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="ac62d-179">U moet toomention die deze integratie Hallo SHA256-algoritme vereist (SHA1 wordt niet ondersteund) tooset Hallo eenmalige aanmelding op de juiste server Hallo zoals app2101 enzovoort.</span><span class="sxs-lookup"><span data-stu-id="ac62d-179">You need toomention that this integration requires hello SHA256 algorithm (SHA1 is not supported) tooset hello SSO on hello appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="ac62d-180">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="ac62d-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ac62d-181">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="ac62d-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ac62d-182">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ac62d-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ac62d-183">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ac62d-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="ac62d-184">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ac62d-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ac62d-186">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ac62d-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac62d-187">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ac62d-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ac62d-189">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ac62d-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ac62d-191">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="ac62d-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ac62d-193">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ac62d-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ac62d-195">a.</span><span class="sxs-lookup"><span data-stu-id="ac62d-195">a.</span></span> <span data-ttu-id="ac62d-196">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ac62d-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ac62d-197">b.</span><span class="sxs-lookup"><span data-stu-id="ac62d-197">b.</span></span> <span data-ttu-id="ac62d-198">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ac62d-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ac62d-199">c.</span><span class="sxs-lookup"><span data-stu-id="ac62d-199">c.</span></span> <span data-ttu-id="ac62d-200">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ac62d-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ac62d-201">d.</span><span class="sxs-lookup"><span data-stu-id="ac62d-201">d.</span></span> <span data-ttu-id="ac62d-202">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ac62d-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="ac62d-203">Een testgebruiker BenSelect maken</span><span class="sxs-lookup"><span data-stu-id="ac62d-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="ac62d-204">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in BenSelect van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ac62d-204">hello objective of this section is toocreate a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="ac62d-205">Werken met [BenSelect ondersteuningsteam](mailto:support@selerix.com) tooadd Hallo gebruikers in Hallo BenSelect-account.</span><span class="sxs-lookup"><span data-stu-id="ac62d-205">Work with [BenSelect support team](mailto:support@selerix.com) tooadd hello users in hello BenSelect account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ac62d-206">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac62d-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ac62d-207">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooBenSelect toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="ac62d-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenSelect.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ac62d-209">**tooassign Britta Simon tooBenSelect, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ac62d-209">**tooassign Britta Simon tooBenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac62d-210">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ac62d-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ac62d-212">Selecteer in de lijst met de toepassingen van Hallo **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="ac62d-212">In hello applications list, select **BenSelect**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="ac62d-214">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ac62d-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ac62d-216">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ac62d-216">Click **Add** button.</span></span> <span data-ttu-id="ac62d-217">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac62d-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ac62d-219">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac62d-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ac62d-220">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac62d-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ac62d-221">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac62d-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ac62d-222">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ac62d-222">Testing single sign-on</span></span>

<span data-ttu-id="ac62d-223">In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ac62d-223">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ac62d-224">Als u op Hallo BenSelect tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour BenSelect toepassing.</span><span class="sxs-lookup"><span data-stu-id="ac62d-224">When you click hello BenSelect tile in hello Access Panel, you should get automatically signed-on tooyour BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ac62d-225">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ac62d-225">Additional resources</span></span>

* [<span data-ttu-id="ac62d-226">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac62d-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ac62d-227">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ac62d-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png

