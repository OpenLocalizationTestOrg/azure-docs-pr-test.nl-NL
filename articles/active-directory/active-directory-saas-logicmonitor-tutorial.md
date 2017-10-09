---
title: 'Zelfstudie: Azure Active Directory-integratie met LogicMonitor | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en LogicMonitor.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: ea5cb8b574d763cb114286e3b2a5c94ab5546756
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="57e86-103">Zelfstudie: Azure Active Directory-integratie met LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="57e86-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="57e86-104">In deze zelfstudie leert u hoe toointegrate LogicMonitor met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57e86-104">In this tutorial, you learn how toointegrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57e86-105">LogicMonitor integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="57e86-105">Integrating LogicMonitor with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="57e86-106">U kunt beheren in Azure AD die tooLogicMonitor toegang heeft</span><span class="sxs-lookup"><span data-stu-id="57e86-106">You can control in Azure AD who has access tooLogicMonitor</span></span>
- <span data-ttu-id="57e86-107">U kunt uw gebruikers tooautomatically get aangemelde tooLogicMonitor (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="57e86-107">You can enable your users tooautomatically get signed-on tooLogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57e86-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="57e86-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="57e86-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57e86-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57e86-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="57e86-110">Prerequisites</span></span>

<span data-ttu-id="57e86-111">Azure AD-integratie met LogicMonitor tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="57e86-111">tooconfigure Azure AD integration with LogicMonitor, you need hello following items:</span></span>

- <span data-ttu-id="57e86-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="57e86-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57e86-113">Een LogicMonitor eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="57e86-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57e86-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="57e86-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57e86-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="57e86-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57e86-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="57e86-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57e86-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57e86-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57e86-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="57e86-118">Scenario description</span></span>
<span data-ttu-id="57e86-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="57e86-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57e86-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="57e86-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57e86-121">Het toevoegen van LogicMonitor van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="57e86-121">Adding LogicMonitor from hello gallery</span></span>
2. <span data-ttu-id="57e86-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="57e86-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-hello-gallery"></a><span data-ttu-id="57e86-123">Het toevoegen van LogicMonitor van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="57e86-123">Adding LogicMonitor from hello gallery</span></span>
<span data-ttu-id="57e86-124">tooconfigure hello integratie van LogicMonitor in Azure AD, moet u tooadd LogicMonitor uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="57e86-124">tooconfigure hello integration of LogicMonitor into Azure AD, you need tooadd LogicMonitor from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="57e86-125">**tooadd LogicMonitor via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="57e86-125">**tooadd LogicMonitor from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="57e86-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="57e86-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="57e86-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="57e86-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="57e86-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="57e86-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="57e86-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57e86-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="57e86-133">Typ in het zoekvak Hallo **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="57e86-133">In hello search box, type **LogicMonitor**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="57e86-135">Selecteer in het deelvenster resultaten hello, **LogicMonitor**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="57e86-135">In hello results panel, select **LogicMonitor**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="57e86-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="57e86-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="57e86-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met LogicMonitor op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="57e86-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="57e86-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in LogicMonitor is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57e86-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LogicMonitor is tooa user in Azure AD.</span></span> <span data-ttu-id="57e86-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in LogicMonitor toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="57e86-140">In other words, a link relationship between an Azure AD user and hello related user in LogicMonitor needs toobe established.</span></span>

<span data-ttu-id="57e86-141">Wijs in LogicMonitor, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="57e86-141">In LogicMonitor, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="57e86-142">tooconfigure en eenmalige aanmelding Azure AD-test met LogicMonitor, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="57e86-142">tooconfigure and test Azure AD single sign-on with LogicMonitor, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="57e86-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="57e86-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="57e86-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57e86-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57e86-145">**[Maken van een testgebruiker LogicMonitor](#creating-a-logicmonitor-test-user)**  -toohave een equivalent van Britta Simon in LogicMonitor die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="57e86-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - toohave a counterpart of Britta Simon in LogicMonitor that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="57e86-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="57e86-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57e86-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="57e86-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="57e86-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="57e86-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="57e86-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing LogicMonitor configureren.</span><span class="sxs-lookup"><span data-stu-id="57e86-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="57e86-150">**Azure AD tooconfigure eenmalige aanmelding met LogicMonitor, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="57e86-150">**tooconfigure Azure AD single sign-on with LogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="57e86-151">In de Azure-portal op Hallo Hallo **LogicMonitor** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="57e86-151">In hello Azure portal, on hello **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="57e86-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="57e86-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="57e86-155">Op Hallo **LogicMonitor domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="57e86-155">On hello **LogicMonitor Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="57e86-157">a.</span><span class="sxs-lookup"><span data-stu-id="57e86-157">a.</span></span> <span data-ttu-id="57e86-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="57e86-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="57e86-159">b.</span><span class="sxs-lookup"><span data-stu-id="57e86-159">b.</span></span> <span data-ttu-id="57e86-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="57e86-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="57e86-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="57e86-161">These values are not real.</span></span> <span data-ttu-id="57e86-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="57e86-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="57e86-163">Neem contact op met [LogicMonitor Client ondersteuningsteam](https://www.logicmonitor.com/contact/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="57e86-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) tooget these values.</span></span> 
 


4. <span data-ttu-id="57e86-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="57e86-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="57e86-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="57e86-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="57e86-168">Meld u bij tooyour **LogicMonitor** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="57e86-168">Log in tooyour **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="57e86-169">Klik in het menu bovenaan Hallo Hallo **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="57e86-169">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="57e86-170">![Instellingen](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="57e86-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="57e86-171">Klik in de navigatie-bat Hallo aan de linkerkant hello, op **eenmalige aanmelding**</span><span class="sxs-lookup"><span data-stu-id="57e86-171">In hello navigation bat on hello left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="57e86-172">![Eenmalige aanmelding](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="57e86-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="57e86-173">In Hallo **instellingen voor eenmalige aanmelding (SSO)** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="57e86-173">In hello **Single Sign-on (SSO) settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="57e86-174">![Eenmalige aanmelding instellingen](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="57e86-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="57e86-175">a.</span><span class="sxs-lookup"><span data-stu-id="57e86-175">a.</span></span> <span data-ttu-id="57e86-176">Selecteer **eenmalige aanmelding inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="57e86-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="57e86-177">b.</span><span class="sxs-lookup"><span data-stu-id="57e86-177">b.</span></span> <span data-ttu-id="57e86-178">Als **roltoewijzing standaard**, selecteer **readonly**.</span><span class="sxs-lookup"><span data-stu-id="57e86-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="57e86-179">c.</span><span class="sxs-lookup"><span data-stu-id="57e86-179">c.</span></span> <span data-ttu-id="57e86-180">Open Hallo gedownload metagegevensbestand in Kladblok en plak de inhoud van Hallo-bestand in Hallo **identiteit Provider metagegevens** textbox.</span><span class="sxs-lookup"><span data-stu-id="57e86-180">Open hello downloaded metadata file in notepad, and then paste content of hello file into hello **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="57e86-181">d.</span><span class="sxs-lookup"><span data-stu-id="57e86-181">d.</span></span> <span data-ttu-id="57e86-182">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="57e86-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="57e86-183">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="57e86-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="57e86-184">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="57e86-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="57e86-185">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="57e86-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="57e86-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="57e86-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="57e86-187">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="57e86-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="57e86-189">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="57e86-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="57e86-190">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="57e86-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57e86-192">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="57e86-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57e86-194">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="57e86-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57e86-196">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="57e86-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57e86-198">a.</span><span class="sxs-lookup"><span data-stu-id="57e86-198">a.</span></span> <span data-ttu-id="57e86-199">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57e86-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57e86-200">b.</span><span class="sxs-lookup"><span data-stu-id="57e86-200">b.</span></span> <span data-ttu-id="57e86-201">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="57e86-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57e86-202">c.</span><span class="sxs-lookup"><span data-stu-id="57e86-202">c.</span></span> <span data-ttu-id="57e86-203">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="57e86-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="57e86-204">d.</span><span class="sxs-lookup"><span data-stu-id="57e86-204">d.</span></span> <span data-ttu-id="57e86-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="57e86-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="57e86-206">Een testgebruiker LogicMonitor maken</span><span class="sxs-lookup"><span data-stu-id="57e86-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="57e86-207">Voor AAD gebruikers toobe kunnen toosign in, moeten ze ingerichte toohello LogicMonitor toepassing met behulp van de namen van de Azure Active Directory-gebruiker zijn.</span><span class="sxs-lookup"><span data-stu-id="57e86-207">For AAD users toobe able toosign in, they must be provisioned toohello LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="57e86-208">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="57e86-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="57e86-209">Aanmelden tooyour LogicMonitor bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="57e86-209">Log in tooyour LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="57e86-210">Klik in het menu bovenaan Hallo Hallo **instellingen**, en klik vervolgens op **rollen en gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="57e86-210">In hello menu on hello top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="57e86-211">![Rollen en gebruikers](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "rollen en gebruikers")</span><span class="sxs-lookup"><span data-stu-id="57e86-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="57e86-212">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="57e86-212">Click **Add**.</span></span>

4. <span data-ttu-id="57e86-213">In Hallo **account toevoegen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="57e86-213">In hello **Add an account** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="57e86-214">![Toevoegen van een account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "account toevoegen")</span><span class="sxs-lookup"><span data-stu-id="57e86-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="57e86-215">a.</span><span class="sxs-lookup"><span data-stu-id="57e86-215">a.</span></span> <span data-ttu-id="57e86-216">Type Hallo **gebruikersnaam**, **e**, **wachtwoord**, en **Typ opnieuw wachtwoord** van hello Azure Active Directory-gebruiker gewenste tooprovision in Hallo gerelateerd tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="57e86-216">Type hello **Username**, **Email**, **Password**, and **Retype password** values of hello Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="57e86-217">b.</span><span class="sxs-lookup"><span data-stu-id="57e86-217">b.</span></span> <span data-ttu-id="57e86-218">Selecteer **rollen**, **machtigingen weergeven**, en Hallo **Status**.</span><span class="sxs-lookup"><span data-stu-id="57e86-218">Select **Roles**, **View Permissions**, and hello **Status**.</span></span>
   
   <span data-ttu-id="57e86-219">c.</span><span class="sxs-lookup"><span data-stu-id="57e86-219">c.</span></span> <span data-ttu-id="57e86-220">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="57e86-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="57e86-221">U kunt andere LogicMonitor gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door LogicMonitor tooprovision Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="57e86-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor tooprovision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="57e86-222">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="57e86-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="57e86-223">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooLogicMonitor toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="57e86-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLogicMonitor.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="57e86-225">**tooassign Britta Simon tooLogicMonitor, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="57e86-225">**tooassign Britta Simon tooLogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="57e86-226">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="57e86-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="57e86-228">Selecteer in de lijst met de toepassingen van Hallo **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="57e86-228">In hello applications list, select **LogicMonitor**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="57e86-230">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="57e86-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="57e86-232">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="57e86-232">Click **Add** button.</span></span> <span data-ttu-id="57e86-233">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57e86-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="57e86-235">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="57e86-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="57e86-236">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57e86-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57e86-237">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57e86-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="57e86-238">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="57e86-238">Testing single sign-on</span></span>

<span data-ttu-id="57e86-239">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="57e86-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="57e86-240">Als u op Hallo LogicMonitor tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour LogicMonitor toepassing.</span><span class="sxs-lookup"><span data-stu-id="57e86-240">When you click hello LogicMonitor tile in hello Access Panel, you should get automatically signed-on tooyour LogicMonitor application.</span></span>
<span data-ttu-id="57e86-241">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="57e86-241">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="57e86-242">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="57e86-242">Additional resources</span></span>

* [<span data-ttu-id="57e86-243">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57e86-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57e86-244">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="57e86-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

