---
title: 'Zelfstudie: Azure Active Directory-integratie met Kantega SSO voor JIRA | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Kantega SSO voor JIRA.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2af4891-e3c8-43b3-bdcb-0500c493e9b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 67894cc55ef91d0991c62e0e4f1be712723cb474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-jira"></a><span data-ttu-id="70e20-103">Zelfstudie: Azure Active Directory-integratie met Kantega SSO voor JIRA</span><span class="sxs-lookup"><span data-stu-id="70e20-103">Tutorial: Azure Active Directory integration with Kantega SSO for JIRA</span></span>

<span data-ttu-id="70e20-104">In deze zelfstudie leert u hoe toointegrate Kantega SSO voor JIRA met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70e20-104">In this tutorial, you learn how toointegrate Kantega SSO for JIRA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70e20-105">Kantega SSO voor JIRA integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="70e20-105">Integrating Kantega SSO for JIRA with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="70e20-106">U kunt beheren in Azure AD wie heeft er toegang tooKantega eenmalige aanmelding voor JIRA</span><span class="sxs-lookup"><span data-stu-id="70e20-106">You can control in Azure AD who has access tooKantega SSO for JIRA</span></span>
- <span data-ttu-id="70e20-107">U kunt uw gebruikers tooautomatically get aangemelde tooKantega eenmalige aanmelding inschakelen voor JIRA (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="70e20-107">You can enable your users tooautomatically get signed-on tooKantega SSO for JIRA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70e20-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="70e20-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="70e20-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="70e20-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70e20-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="70e20-110">Prerequisites</span></span>

<span data-ttu-id="70e20-111">Azure AD-integratie met Kantega SSO voor JIRA tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="70e20-111">tooconfigure Azure AD integration with Kantega SSO for JIRA, you need hello following items:</span></span>

- <span data-ttu-id="70e20-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="70e20-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70e20-113">Een Kantega SSO voor eenmalige aanmelding JIRA abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="70e20-113">A Kantega SSO for JIRA single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70e20-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="70e20-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70e20-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="70e20-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70e20-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="70e20-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70e20-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70e20-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70e20-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="70e20-118">Scenario description</span></span>
<span data-ttu-id="70e20-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="70e20-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70e20-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="70e20-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70e20-121">Het toevoegen van Kantega SSO voor JIRA van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="70e20-121">Adding Kantega SSO for JIRA from hello gallery</span></span>
2. <span data-ttu-id="70e20-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="70e20-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-jira-from-hello-gallery"></a><span data-ttu-id="70e20-123">Het toevoegen van Kantega SSO voor JIRA van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="70e20-123">Adding Kantega SSO for JIRA from hello gallery</span></span>
<span data-ttu-id="70e20-124">tooconfigure hello integratie van Kantega SSO voor JIRA in Azure AD, moet u tooadd Kantega SSO van hello galerie tooyour lijst met beheerde SaaS-apps voor JIRA.</span><span class="sxs-lookup"><span data-stu-id="70e20-124">tooconfigure hello integration of Kantega SSO for JIRA into Azure AD, you need tooadd Kantega SSO for JIRA from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="70e20-125">**tooadd Kantega SSO voor JIRA via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="70e20-125">**tooadd Kantega SSO for JIRA from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="70e20-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="70e20-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70e20-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="70e20-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="70e20-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="70e20-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="70e20-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="70e20-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="70e20-133">Typ in het zoekvak Hallo **Kantega SSO voor JIRA**.</span><span class="sxs-lookup"><span data-stu-id="70e20-133">In hello search box, type **Kantega SSO for JIRA**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_search.png)

5. <span data-ttu-id="70e20-135">Selecteer in het deelvenster resultaten hello, **Kantega SSO voor JIRA**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="70e20-135">In hello results panel, select **Kantega SSO for JIRA**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70e20-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="70e20-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="70e20-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Kantega SSO voor JIRA op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="70e20-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for JIRA based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="70e20-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Kantega SSO voor JIRA is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70e20-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for JIRA is tooa user in Azure AD.</span></span> <span data-ttu-id="70e20-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Kantega SSO voor JIRA toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="70e20-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for JIRA needs toobe established.</span></span>

<span data-ttu-id="70e20-141">Wijs in Kantega SSO voor JIRA, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als Hallo-waarde van Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="70e20-141">In Kantega SSO for JIRA, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="70e20-142">tooconfigure en test eenmalige aanmelding Azure AD met Kantega SSO voor JIRA, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="70e20-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for JIRA, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="70e20-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="70e20-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="70e20-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70e20-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70e20-145">**[Maken van een SSO Kantega voor de testgebruiker JIRA](#creating-a-kantega-sso-for-jira-test-user)**  -toohave een equivalent van Britta Simon in Kantega SSO voor JIRA die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="70e20-145">**[Creating a Kantega SSO for JIRA test user](#creating-a-kantega-sso-for-jira-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for JIRA that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="70e20-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="70e20-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70e20-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="70e20-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70e20-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="70e20-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70e20-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw Kantega SSO voor JIRA toepassing configureren.</span><span class="sxs-lookup"><span data-stu-id="70e20-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for JIRA application.</span></span>

<span data-ttu-id="70e20-150">**tooconfigure eenmalige aanmelding Azure AD met Kantega SSO voor JIRA, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="70e20-150">**tooconfigure Azure AD single sign-on with Kantega SSO for JIRA, perform hello following steps:**</span></span>

1. <span data-ttu-id="70e20-151">In de Azure-portal op Hallo Hallo **Kantega SSO voor JIRA** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="70e20-151">In hello Azure portal, on hello **Kantega SSO for JIRA** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="70e20-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="70e20-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_samlbase.png)

3. <span data-ttu-id="70e20-155">In **IDP** modus op Hallo geïnitieerd **Kantega SSO voor JIRA domein en URL's** sectie Hallo stap uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="70e20-155">In **IDP** initiated mode, on hello **Kantega SSO for JIRA Domain and URLs** section perform hello following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url1.png)

    <span data-ttu-id="70e20-157">a.</span><span class="sxs-lookup"><span data-stu-id="70e20-157">a.</span></span> <span data-ttu-id="70e20-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="70e20-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="70e20-159">b.</span><span class="sxs-lookup"><span data-stu-id="70e20-159">b.</span></span> <span data-ttu-id="70e20-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="70e20-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="70e20-161">In **SP** geïnitieerd modus selectievakje **weergeven geavanceerde instellingen voor URL** en Hallo stap uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="70e20-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform hello following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url2.png)

    <span data-ttu-id="70e20-163">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="70e20-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="70e20-164">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="70e20-164">These values are not real.</span></span> <span data-ttu-id="70e20-165">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="70e20-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="70e20-166">Deze waarden worden ontvangen tijdens de configuratie van Hallo van Jira-invoegtoepassing wordt verderop in de zelfstudie Hallo besproken.</span><span class="sxs-lookup"><span data-stu-id="70e20-166">These values are received during hello configuration of Jira plugin, which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="70e20-167">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="70e20-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_certificate.png) 

6. <span data-ttu-id="70e20-169">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="70e20-169">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="70e20-171">Meld u in een ander browservenster in tooyour JIRA op de lokale server als beheerder.</span><span class="sxs-lookup"><span data-stu-id="70e20-171">In a different web browser window, log in tooyour JIRA on premise server as an administrator.</span></span>

8. <span data-ttu-id="70e20-172">Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **invoegtoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="70e20-172">Hover on cog and click hello **Add-ons**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/addon1.png)

9. <span data-ttu-id="70e20-174">Klik onder sectie tabblad invoegtoepassingen op **vinden van nieuwe invoegtoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="70e20-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="70e20-175">Search **Kantega SSO voor JIRA (SAML & Kerberos)** en klik op **installeren** knop tooinstall Hallo nieuwe SAML-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="70e20-175">Search **Kantega SSO for JIRA (SAML & Kerberos)** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/addon2.png)

10. <span data-ttu-id="70e20-177">Hallo-invoegtoepassing installatie wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="70e20-177">hello plugin installation starts.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/addon3.png)

11. <span data-ttu-id="70e20-179">Zodra het Hallo-installatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="70e20-179">Once hello installation is complete.</span></span> <span data-ttu-id="70e20-180">Klik op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="70e20-180">Click **Close**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/addon33.png)

12. <span data-ttu-id="70e20-182">Klik op **Beheren**.</span><span class="sxs-lookup"><span data-stu-id="70e20-182">Click **Manage**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/addon34.png)
    
13. <span data-ttu-id="70e20-184">Nieuwe invoegtoepassing wordt vermeld onder **INTEGRATIES**.</span><span class="sxs-lookup"><span data-stu-id="70e20-184">New plugin is listed under **INTEGRATIONS**.</span></span> <span data-ttu-id="70e20-185">Klik op **configureren** tooconfigure Hallo nieuwe invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="70e20-185">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/addon35.png)

14. <span data-ttu-id="70e20-187">In Hallo **SAML** sectie.</span><span class="sxs-lookup"><span data-stu-id="70e20-187">In hello **SAML** section.</span></span> <span data-ttu-id="70e20-188">Selecteer **Azure Active Directory (Azure AD)** van Hallo **toevoegen identiteitsprovider** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="70e20-188">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/addon4.png)

15. <span data-ttu-id="70e20-190">Abonnement als selecteren **Basic**.</span><span class="sxs-lookup"><span data-stu-id="70e20-190">Select subscription level as **Basic**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/addon5.png)     

16. <span data-ttu-id="70e20-192">Op Hallo **App-eigenschappen** sectie, voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="70e20-192">On hello **App properties** section, perform following steps:</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/addon6.png)

    <span data-ttu-id="70e20-194">a.</span><span class="sxs-lookup"><span data-stu-id="70e20-194">a.</span></span> <span data-ttu-id="70e20-195">Kopiëren Hallo **App ID URI** waarde en deze gebruiken als **id, de antwoord-URL en de aanmeldings-URL** op Hallo **Kantega SSO voor JIRA domein en URL's** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="70e20-195">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for JIRA Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="70e20-196">b.</span><span class="sxs-lookup"><span data-stu-id="70e20-196">b.</span></span> <span data-ttu-id="70e20-197">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="70e20-197">Click **Next**.</span></span>

17. <span data-ttu-id="70e20-198">Op Hallo **metagegevens importeren** sectie, voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="70e20-198">On hello **Metadata import** section, perform following steps:</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/addon7.png)

    <span data-ttu-id="70e20-200">a.</span><span class="sxs-lookup"><span data-stu-id="70e20-200">a.</span></span> <span data-ttu-id="70e20-201">Selecteer **metagegevensbestand op mijn computer**, en de metagegevens-uploadbestand, die u hebt gedownload vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="70e20-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="70e20-202">b.</span><span class="sxs-lookup"><span data-stu-id="70e20-202">b.</span></span> <span data-ttu-id="70e20-203">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="70e20-203">Click **Next**.</span></span>

18. <span data-ttu-id="70e20-204">Op Hallo **en SSO** sectie, voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="70e20-204">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/addon8.png)
    
    <span data-ttu-id="70e20-206">a.</span><span class="sxs-lookup"><span data-stu-id="70e20-206">a.</span></span> <span data-ttu-id="70e20-207">Naam van de identiteitsprovider Hallo toevoegen in **identiteit providernaam** textbox (bijvoorbeeld Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70e20-207">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="70e20-208">b.</span><span class="sxs-lookup"><span data-stu-id="70e20-208">b.</span></span> <span data-ttu-id="70e20-209">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="70e20-209">Click **Next**.</span></span>

19. <span data-ttu-id="70e20-210">Hallo-handtekeningcertificaat en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="70e20-210">Verify hello Signing certificate and click **Next**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/addon9.png)

20. <span data-ttu-id="70e20-212">Op Hallo **JIRA gebruikersaccounts** sectie, voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="70e20-212">On hello **JIRA user accounts** section, perform following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/addon10.png)

    <span data-ttu-id="70e20-214">a.</span><span class="sxs-lookup"><span data-stu-id="70e20-214">a.</span></span> <span data-ttu-id="70e20-215">Selecteer **gebruikers in de JIRA interne Directory maken, indien nodig** en Voer Hallo juiste naam van groep Hallo voor gebruikers (kan meerdere Nee.</span><span class="sxs-lookup"><span data-stu-id="70e20-215">Select **Create users in JIRA's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="70e20-216">van groepen van elkaar gescheiden door komma's).</span><span class="sxs-lookup"><span data-stu-id="70e20-216">of groups separated by comma).</span></span>

    <span data-ttu-id="70e20-217">b.</span><span class="sxs-lookup"><span data-stu-id="70e20-217">b.</span></span> <span data-ttu-id="70e20-218">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="70e20-218">Click **Next**.</span></span>

21. <span data-ttu-id="70e20-219">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="70e20-219">Click **Finish**.</span></span>   

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/addon11.png)

22. <span data-ttu-id="70e20-221">Op Hallo **bekend domeinen voor Azure AD** sectie, voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="70e20-221">On hello **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/addon12.png)

    <span data-ttu-id="70e20-223">a.</span><span class="sxs-lookup"><span data-stu-id="70e20-223">a.</span></span> <span data-ttu-id="70e20-224">Selecteer **domeinen bekend** van Hallo linkerpaneel van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="70e20-224">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="70e20-225">b.</span><span class="sxs-lookup"><span data-stu-id="70e20-225">b.</span></span> <span data-ttu-id="70e20-226">Voer in Hallo domeinnaam **domeinen bekend** textbox.</span><span class="sxs-lookup"><span data-stu-id="70e20-226">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="70e20-227">c.</span><span class="sxs-lookup"><span data-stu-id="70e20-227">c.</span></span> <span data-ttu-id="70e20-228">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="70e20-228">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="70e20-229">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="70e20-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="70e20-230">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="70e20-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="70e20-231">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="70e20-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70e20-232">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="70e20-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="70e20-233">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="70e20-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="70e20-235">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="70e20-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="70e20-236">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="70e20-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70e20-238">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="70e20-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70e20-240">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="70e20-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70e20-242">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="70e20-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70e20-244">a.</span><span class="sxs-lookup"><span data-stu-id="70e20-244">a.</span></span> <span data-ttu-id="70e20-245">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="70e20-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70e20-246">b.</span><span class="sxs-lookup"><span data-stu-id="70e20-246">b.</span></span> <span data-ttu-id="70e20-247">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="70e20-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70e20-248">c.</span><span class="sxs-lookup"><span data-stu-id="70e20-248">c.</span></span> <span data-ttu-id="70e20-249">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="70e20-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="70e20-250">d.</span><span class="sxs-lookup"><span data-stu-id="70e20-250">d.</span></span> <span data-ttu-id="70e20-251">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="70e20-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-jira-test-user"></a><span data-ttu-id="70e20-252">Maken van een SSO Kantega voor JIRA testgebruiker</span><span class="sxs-lookup"><span data-stu-id="70e20-252">Creating a Kantega SSO for JIRA test user</span></span>

<span data-ttu-id="70e20-253">Azure AD tooenable gebruikers toolog in tooJIRA, ze in JIRA moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="70e20-253">tooenable Azure AD users toolog in tooJIRA, they must be provisioned into JIRA.</span></span> <span data-ttu-id="70e20-254">In Kantega SSO voor JIRA is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="70e20-254">In Kantega SSO for JIRA, provisioning is a manual task.</span></span>

<span data-ttu-id="70e20-255">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="70e20-255">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="70e20-256">Tooyour JIRA op de lokale server aanmelden als beheerder.</span><span class="sxs-lookup"><span data-stu-id="70e20-256">Log in tooyour JIRA on premise server as an administrator.</span></span>

2. <span data-ttu-id="70e20-257">Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **Gebruikersbeheer**.</span><span class="sxs-lookup"><span data-stu-id="70e20-257">Hover on cog and click hello **User management**.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-kantegassoforjira-tutorial/user1.png) 

3. <span data-ttu-id="70e20-259">Onder **Gebruikersbeheer** tabblad gedeelte, klikt u op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="70e20-259">Under **User management** tab section, click **Create user**.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-kantegassoforjira-tutorial/user2.png) 

4. <span data-ttu-id="70e20-261">Op Hallo **'Een nieuwe gebruiker maken'** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="70e20-261">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-kantegassoforjira-tutorial/user3.png) 

    <span data-ttu-id="70e20-263">a.</span><span class="sxs-lookup"><span data-stu-id="70e20-263">a.</span></span> <span data-ttu-id="70e20-264">In Hallo **e-mailadres** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="70e20-264">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="70e20-265">b.</span><span class="sxs-lookup"><span data-stu-id="70e20-265">b.</span></span> <span data-ttu-id="70e20-266">In Hallo **volledige naam** textbox, volledige naam van de gebruiker Hallo zoals Britta Simon type.</span><span class="sxs-lookup"><span data-stu-id="70e20-266">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="70e20-267">c.</span><span class="sxs-lookup"><span data-stu-id="70e20-267">c.</span></span> <span data-ttu-id="70e20-268">In Hallo **gebruikersnaam** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="70e20-268">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="70e20-269">d.</span><span class="sxs-lookup"><span data-stu-id="70e20-269">d.</span></span> <span data-ttu-id="70e20-270">In Hallo **wachtwoord** textbox type Hallo wachtwoord van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="70e20-270">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="70e20-271">e.</span><span class="sxs-lookup"><span data-stu-id="70e20-271">e.</span></span> <span data-ttu-id="70e20-272">Klik op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="70e20-272">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="70e20-273">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="70e20-273">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="70e20-274">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooKantega eenmalige aanmelding voor JIRA.</span><span class="sxs-lookup"><span data-stu-id="70e20-274">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for JIRA.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="70e20-276">**tooassign Britta Simon tooKantega SSO voor JIRA, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="70e20-276">**tooassign Britta Simon tooKantega SSO for JIRA, perform hello following steps:**</span></span>

1. <span data-ttu-id="70e20-277">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="70e20-277">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="70e20-279">Selecteer in de lijst met de toepassingen van Hallo **Kantega SSO voor JIRA**.</span><span class="sxs-lookup"><span data-stu-id="70e20-279">In hello applications list, select **Kantega SSO for JIRA**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_app.png) 

3. <span data-ttu-id="70e20-281">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="70e20-281">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="70e20-283">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="70e20-283">Click **Add** button.</span></span> <span data-ttu-id="70e20-284">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="70e20-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="70e20-286">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="70e20-286">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="70e20-287">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="70e20-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70e20-288">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="70e20-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="70e20-289">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="70e20-289">Testing single sign-on</span></span>

<span data-ttu-id="70e20-290">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="70e20-290">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="70e20-291">Als u op Hallo Kantega SSO JIRA tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour Kantega SSO voor JIRA toepassing.</span><span class="sxs-lookup"><span data-stu-id="70e20-291">When you click hello Kantega SSO for JIRA tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for JIRA application.</span></span>
<span data-ttu-id="70e20-292">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="70e20-292">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="70e20-293">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="70e20-293">Additional resources</span></span>

* [<span data-ttu-id="70e20-294">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70e20-294">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70e20-295">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="70e20-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_203.png

