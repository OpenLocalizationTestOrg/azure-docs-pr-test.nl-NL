---
title: 'Zelfstudie: Azure Active Directory-integratie met Tableau Server | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Tableau-Server.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="7e0c1-103">Zelfstudie: Azure Active Directory-integratie met Tableau Server</span><span class="sxs-lookup"><span data-stu-id="7e0c1-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="7e0c1-104">In deze zelfstudie leert u hoe toointegrate Tableau Server met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e0c1-104">In this tutorial, you learn how toointegrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7e0c1-105">Tableau Server integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7e0c1-105">Integrating Tableau Server with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7e0c1-106">U kunt beheren in Azure AD wie toegang tot tooTableau Server heeft</span><span class="sxs-lookup"><span data-stu-id="7e0c1-106">You can control in Azure AD who has access tooTableau Server</span></span>
- <span data-ttu-id="7e0c1-107">U kunt uw gebruikers tooautomatically get aangemelde tooTableau Server (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="7e0c1-107">You can enable your users tooautomatically get signed-on tooTableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7e0c1-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="7e0c1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7e0c1-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7e0c1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e0c1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7e0c1-110">Prerequisites</span></span>

<span data-ttu-id="7e0c1-111">Azure AD-integratie met Tableau Server tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="7e0c1-111">tooconfigure Azure AD integration with Tableau Server, you need hello following items:</span></span>

- <span data-ttu-id="7e0c1-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="7e0c1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7e0c1-113">Een Server Tableau eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="7e0c1-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7e0c1-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7e0c1-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="7e0c1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7e0c1-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7e0c1-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e0c1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7e0c1-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="7e0c1-118">Scenario description</span></span>
<span data-ttu-id="7e0c1-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7e0c1-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="7e0c1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7e0c1-121">Tableau Server uit de galerie Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="7e0c1-121">Adding Tableau Server from hello gallery</span></span>
2. <span data-ttu-id="7e0c1-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7e0c1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-hello-gallery"></a><span data-ttu-id="7e0c1-123">Tableau Server uit de galerie Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="7e0c1-123">Adding Tableau Server from hello gallery</span></span>
<span data-ttu-id="7e0c1-124">tooconfigure hello integratie van Tableau Server in Azure AD, moet u tooadd Tableau Server uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-124">tooconfigure hello integration of Tableau Server into Azure AD, you need tooadd Tableau Server from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7e0c1-125">**tooadd Tableau Server uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7e0c1-125">**tooadd Tableau Server from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e0c1-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7e0c1-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7e0c1-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="7e0c1-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="7e0c1-133">Typ in het zoekvak Hallo **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-133">In hello search box, type **Tableau Server**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="7e0c1-135">Selecteer in het deelvenster resultaten hello, **Tableau Server**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-135">In hello results panel, select **Tableau Server**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7e0c1-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7e0c1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7e0c1-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Tableau-Server op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="7e0c1-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7e0c1-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Tableau Server is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Server is tooa user in Azure AD.</span></span> <span data-ttu-id="7e0c1-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Tableau Server toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Server needs toobe established.</span></span>

<span data-ttu-id="7e0c1-141">In het vak Tableau Server Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-141">In Tableau Server, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7e0c1-142">tooconfigure en test eenmalige aanmelding Azure AD met Tableau Server, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e0c1-142">tooconfigure and test Azure AD single sign-on with Tableau Server, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7e0c1-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7e0c1-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7e0c1-145">**[Maken van een testgebruiker Tableau Server](#creating-a-tableau-server-test-user)**  -toohave een equivalent van Britta Simon in Tableau-Server die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - toohave a counterpart of Britta Simon in Tableau Server that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7e0c1-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7e0c1-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7e0c1-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="7e0c1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7e0c1-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Tableau Server configureren.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="7e0c1-150">**Voer tooconfigure Azure AD eenmalige aanmelding met de Server Tableau, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7e0c1-150">**tooconfigure Azure AD single sign-on with Tableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e0c1-151">In de Azure-portal op Hallo Hallo **Tableau Server** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-151">In hello Azure portal, on hello **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="7e0c1-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="7e0c1-155">Op Hallo **Tableau-serverdomein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e0c1-155">On hello **Tableau Server Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="7e0c1-157">a.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-157">a.</span></span> <span data-ttu-id="7e0c1-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="7e0c1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="7e0c1-159">b.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-159">b.</span></span> <span data-ttu-id="7e0c1-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="7e0c1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="7e0c1-161">c.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-161">c.</span></span> <span data-ttu-id="7e0c1-162">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="7e0c1-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7e0c1-163">Hallo voorgaande waarden zijn niet echte waarden.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-163">hello preceding values are not real values.</span></span> <span data-ttu-id="7e0c1-164">Later kunt bijwerken u Hallo waarden met de Hallo werkelijke URL en de id van de configuratiepagina voor Hallo Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-164">Later, you update hello values with hello actual URL and identifier from hello Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="7e0c1-165">Hallo SAML asserties verwacht tableau servertoepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-165">Tableau Server application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="7e0c1-166">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="7e0c1-167">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **'Gebruikerskenmerken'** sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-167">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="7e0c1-168">Hallo volgende schermafbeelding ziet u een voorbeeld van Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-168">hello following screenshot shows an example for hello same.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="7e0c1-170">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in Hallo afbeelding hierboven en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e0c1-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="7e0c1-171">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="7e0c1-171">Attribute Name</span></span> | <span data-ttu-id="7e0c1-172">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="7e0c1-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="7e0c1-173">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="7e0c1-173">username</span></span> | <span data-ttu-id="7e0c1-174">*User.DisplayName*</span><span class="sxs-lookup"><span data-stu-id="7e0c1-174">*user.displayname*</span></span> |

    <span data-ttu-id="7e0c1-175">a.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-175">a.</span></span> <span data-ttu-id="7e0c1-176">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="7e0c1-179">b.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-179">b.</span></span> <span data-ttu-id="7e0c1-180">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="7e0c1-181">c.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-181">c.</span></span> <span data-ttu-id="7e0c1-182">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7e0c1-183">d.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-183">d.</span></span> <span data-ttu-id="7e0c1-184">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="7e0c1-184">Click **Ok**</span></span>


6. <span data-ttu-id="7e0c1-185">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="7e0c1-187">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-187">Click **Save** button.</span></span>

    <span data-ttu-id="7e0c1-188">![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="7e0c1-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="7e0c1-189">tooget SSO is geconfigureerd voor uw toepassing, moet u toosign op tooyour Tableau Server tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-189">tooget SSO configured for your application, you need toosign-on tooyour Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="7e0c1-190">a.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-190">a.</span></span> <span data-ttu-id="7e0c1-191">In het Tableau serverconfiguratie hello, klikt u op Hallo **SAML** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-191">In hello Tableau Server configuration, click hello **SAML** tab.</span></span>
  
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="7e0c1-193">b.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-193">b.</span></span> <span data-ttu-id="7e0c1-194">Schakel dit selectievakje in Hallo van **gebruik SAML voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-194">Select hello checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="7e0c1-195">c.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-195">c.</span></span> <span data-ttu-id="7e0c1-196">Tableau Server retour-URL-URL die Tableau Server-gebruikers toegang, zoals http://tableau_server tot krijgen Hallo.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-196">Tableau Server return URL—hello URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="7e0c1-197">Gebruik http://localhost wordt niet aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="7e0c1-198">Via een URL met een slash (bijvoorbeeld http://tableau_server/) wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="7e0c1-199">Kopiëren **Tableau Server retour-URL** en plak deze tooAzure AD **aanmelding op URL** textbox in **Tableau-serverdomein en URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-199">Copy **Tableau Server return URL** and paste it tooAzure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="7e0c1-200">d.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-200">d.</span></span> <span data-ttu-id="7e0c1-201">Entiteit-ID van SAML-Hallo entiteit-ID is uniek voor uw Server Tableau installatie toohello IdP.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-201">SAML entity ID—hello entity ID uniquely identifies your Tableau Server installation toohello IdP.</span></span> <span data-ttu-id="7e0c1-202">Hier geeft u de URL van de Server Tableau opnieuw, indien gewenst, maar er geen toobe uw Tableau Server-URL.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-202">You can enter your Tableau Server URL again here, if you like, but it does not have toobe your Tableau Server URL.</span></span> <span data-ttu-id="7e0c1-203">Kopiëren **SAML entiteit-ID** en plak deze tooAzure AD **id** textbox in **Tableau-serverdomein en URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-203">Copy **SAML entity ID** and paste it tooAzure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="7e0c1-204">e.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-204">e.</span></span> <span data-ttu-id="7e0c1-205">Klik op Hallo **metagegevensbestand exporteren** en open het in Hallo text editor-toepassing.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-205">Click hello **Export Metadata File** and open it in hello text editor application.</span></span> <span data-ttu-id="7e0c1-206">Zoek Assertion Consumer Service-URL met Http Post en 0-Index en kopiëren Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy hello URL.</span></span> <span data-ttu-id="7e0c1-207">Plak nu tooAzure AD **antwoord-URL** textbox in **Tableau-serverdomein en URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-207">Now paste it tooAzure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="7e0c1-208">f.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-208">f.</span></span> <span data-ttu-id="7e0c1-209">Zoek uw Federatiemetagegevens bestand gedownload van Azure-portal en uploadt u dit in Hallo **SAML Idp metagegevensbestand**.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in hello **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="7e0c1-210">g.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-210">g.</span></span> <span data-ttu-id="7e0c1-211">Klik op Hallo **OK** knop in Hallo Tableau configuratiepagina op de Server.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-211">Click hello **OK** button in hello Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="7e0c1-212">Klant hebben tooupload alle certificaten in Hallo Tableau Server SAML SSO-configuratie en het in Hallo SSO stroom ophalen genegeerd.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-212">Customer have tooupload any certificate in hello Tableau Server SAML SSO configuration and it will get ignored in hello SSO flow.</span></span>
    ><span data-ttu-id="7e0c1-213">Als u moet helpen SAML configureren op de Server Tableau Raadpleeg toothis artikel [SAML configureren](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="7e0c1-213">If you need help configuring SAML on Tableau Server then please refer toothis article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="7e0c1-214">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7e0c1-215">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7e0c1-216">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7e0c1-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7e0c1-217">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7e0c1-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="7e0c1-218">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="7e0c1-220">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7e0c1-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e0c1-221">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7e0c1-223">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7e0c1-225">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7e0c1-227">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e0c1-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7e0c1-229">a.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-229">a.</span></span> <span data-ttu-id="7e0c1-230">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7e0c1-231">b.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-231">b.</span></span> <span data-ttu-id="7e0c1-232">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7e0c1-233">c.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-233">c.</span></span> <span data-ttu-id="7e0c1-234">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7e0c1-235">d.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-235">d.</span></span> <span data-ttu-id="7e0c1-236">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="7e0c1-237">Een testgebruiker Tableau Server maken</span><span class="sxs-lookup"><span data-stu-id="7e0c1-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="7e0c1-238">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Tableau Server van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-238">hello objective of this section is toocreate a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="7e0c1-239">U moet alle Hallo gebruikers in Hallo Tableau server tooprovision.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-239">You need tooprovision all hello users in hello Tableau server.</span></span> 

<span data-ttu-id="7e0c1-240">Deze gebruikersnaam van de gebruiker Hallo moet overeenkomen met de Hallo-waarde die u hebt geconfigureerd in het aangepaste kenmerk hello Azure AD van **gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-240">That username of hello user should match hello value which you have configured in hello Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="7e0c1-241">Met de juiste toewijzing Hallo integratie moet werken Hallo [eenmalige aanmelding configureren Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="7e0c1-241">With hello correct mapping hello integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="7e0c1-242">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello Tableau Server-beheerder in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-242">If you need toocreate a user manually, you need toocontact hello Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7e0c1-243">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e0c1-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7e0c1-244">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooTableau Server.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Server.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="7e0c1-246">**tooassign Britta Simon tooTableau Server, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7e0c1-246">**tooassign Britta Simon tooTableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e0c1-247">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="7e0c1-249">Selecteer in de lijst met de toepassingen van Hallo **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-249">In hello applications list, select **Tableau Server**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="7e0c1-251">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="7e0c1-253">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-253">Click **Add** button.</span></span> <span data-ttu-id="7e0c1-254">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="7e0c1-256">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7e0c1-257">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7e0c1-258">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7e0c1-259">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7e0c1-259">Testing single sign-on</span></span>

<span data-ttu-id="7e0c1-260">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7e0c1-261">Als u op Hallo Tableau Server tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Tableau servertoepassing.</span><span class="sxs-lookup"><span data-stu-id="7e0c1-261">When you click hello Tableau Server tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Server application.</span></span>
<span data-ttu-id="7e0c1-262">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="7e0c1-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7e0c1-263">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7e0c1-263">Additional resources</span></span>

* [<span data-ttu-id="7e0c1-264">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e0c1-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7e0c1-265">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7e0c1-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

