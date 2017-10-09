---
title: 'Zelfstudie: Azure Active Directory-integratie met Kantega SSO voor Bamboe | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Kantega SSO voor Bamboe.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e238b574-9e9b-43b7-ab98-d2a87ff89d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 8bf637ff440e8e3948db882861bee6e73f8aa879
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bamboo"></a><span data-ttu-id="9c5ff-103">Zelfstudie: Azure Active Directory-integratie met Kantega SSO voor Bamboe</span><span class="sxs-lookup"><span data-stu-id="9c5ff-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bamboo</span></span>

<span data-ttu-id="9c5ff-104">In deze zelfstudie leert u hoe toointegrate Kantega SSO voor Bamboe met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9c5ff-104">In this tutorial, you learn how toointegrate Kantega SSO for Bamboo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9c5ff-105">Kantega SSO voor Bamboe integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9c5ff-105">Integrating Kantega SSO for Bamboo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9c5ff-106">U kunt beheren in Azure AD wie toegang tot tooKantega SSO voor Bamboe heeft</span><span class="sxs-lookup"><span data-stu-id="9c5ff-106">You can control in Azure AD who has access tooKantega SSO for Bamboo</span></span>
- <span data-ttu-id="9c5ff-107">U kunt uw gebruikers tooautomatically get aangemelde tooKantega SSO voor Bamboe (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="9c5ff-107">You can enable your users tooautomatically get signed-on tooKantega SSO for Bamboo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9c5ff-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="9c5ff-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9c5ff-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9c5ff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c5ff-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9c5ff-110">Prerequisites</span></span>

<span data-ttu-id="9c5ff-111">Azure AD-integratie met Kantega SSO voor Bamboe tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="9c5ff-111">tooconfigure Azure AD integration with Kantega SSO for Bamboo, you need hello following items:</span></span>

- <span data-ttu-id="9c5ff-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9c5ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9c5ff-113">Een Kantega SSO voor eenmalige aanmelding Bamboe abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="9c5ff-113">A Kantega SSO for Bamboo single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9c5ff-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9c5ff-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="9c5ff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9c5ff-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9c5ff-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9c5ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9c5ff-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="9c5ff-118">Scenario description</span></span>
<span data-ttu-id="9c5ff-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9c5ff-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="9c5ff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9c5ff-121">Het toevoegen van Kantega SSO voor Bamboe van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="9c5ff-121">Adding Kantega SSO for Bamboo from hello gallery</span></span>
2. <span data-ttu-id="9c5ff-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9c5ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bamboo-from-hello-gallery"></a><span data-ttu-id="9c5ff-123">Het toevoegen van Kantega SSO voor Bamboe van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="9c5ff-123">Adding Kantega SSO for Bamboo from hello gallery</span></span>
<span data-ttu-id="9c5ff-124">tooconfigure hello integratie van Kantega SSO voor Bamboe in Azure AD, moet u tooadd Kantega SSO van hello galerie tooyour lijst met beheerde SaaS-apps voor Bamboe.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-124">tooconfigure hello integration of Kantega SSO for Bamboo into Azure AD, you need tooadd Kantega SSO for Bamboo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9c5ff-125">**tooadd Kantega SSO voor Bamboe via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9c5ff-125">**tooadd Kantega SSO for Bamboo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c5ff-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9c5ff-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9c5ff-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="9c5ff-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="9c5ff-133">Typ in het zoekvak Hallo **Kantega SSO voor Bamboe**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-133">In hello search box, type **Kantega SSO for Bamboo**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_search.png)

5. <span data-ttu-id="9c5ff-135">Selecteer in het deelvenster resultaten hello, **Kantega SSO voor Bamboe**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-135">In hello results panel, select **Kantega SSO for Bamboo**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9c5ff-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9c5ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9c5ff-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Kantega SSO voor Bamboe op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bamboo based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9c5ff-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Kantega SSO voor Bamboe is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for Bamboo is tooa user in Azure AD.</span></span> <span data-ttu-id="9c5ff-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Kantega SSO voor Bamboe toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for Bamboo needs toobe established.</span></span>

<span data-ttu-id="9c5ff-141">Wijs in Kantega SSO voor Bamboe, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als Hallo-waarde van Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-141">In Kantega SSO for Bamboo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9c5ff-142">tooconfigure en test eenmalige aanmelding Azure AD met Kantega SSO voor Bamboe, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9c5ff-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for Bamboo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9c5ff-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9c5ff-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9c5ff-145">**[Maken van een SSO Kantega voor de testgebruiker Bamboe](#creating-a-kantega-sso-for-bamboo-test-user)**  -toohave een equivalent van Britta Simon in Kantega SSO voor Bamboe die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-145">**[Creating a Kantega SSO for Bamboo test user](#creating-a-kantega-sso-for-bamboo-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for Bamboo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9c5ff-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9c5ff-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9c5ff-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9c5ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9c5ff-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw Kantega SSO voor Bamboe toepassing configureren.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for Bamboo application.</span></span>

<span data-ttu-id="9c5ff-150">**tooconfigure eenmalige aanmelding Azure AD met Kantega SSO voor Bamboe, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9c5ff-150">**tooconfigure Azure AD single sign-on with Kantega SSO for Bamboo, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c5ff-151">In de Azure-portal op Hallo Hallo **Kantega SSO voor Bamboe** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-151">In hello Azure portal, on hello **Kantega SSO for Bamboo** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="9c5ff-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_samlbase.png)

3. <span data-ttu-id="9c5ff-155">In **IDP** modus op Hallo geïnitieerd **Kantega SSO voor Bamboe domein en URL's** sectie Hallo stap uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9c5ff-155">In **IDP** initiated mode, on hello **Kantega SSO for Bamboo Domain and URLs** section perform hello following step :</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url1.png)
    
    <span data-ttu-id="9c5ff-157">a.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-157">a.</span></span> <span data-ttu-id="9c5ff-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="9c5ff-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="9c5ff-159">b.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-159">b.</span></span> <span data-ttu-id="9c5ff-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="9c5ff-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="9c5ff-161">In **SP** geïnitieerd modus selectievakje **weergeven geavanceerde instellingen voor URL** en Hallo stap uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="9c5ff-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform hello following step :</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url2.png)
    
    <span data-ttu-id="9c5ff-163">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="9c5ff-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9c5ff-164">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-164">These values are not real.</span></span> <span data-ttu-id="9c5ff-165">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9c5ff-166">Deze waarden worden ontvangen tijdens de configuratie van Hallo van bamboe invoegtoepassing die later in Hallo zelfstudie wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-166">These values are recieved during hello configuration of Bamboo plugin which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="9c5ff-167">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_certificate.png) 

6. <span data-ttu-id="9c5ff-169">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-169">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="9c5ff-171">Meld u in een ander browservenster in tooyour Bamboe op de lokale server als beheerder.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-171">In a different web browser window, log in tooyour Bamboo  on premise server as an administrator.</span></span>

8. <span data-ttu-id="9c5ff-172">Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **invoegtoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-172">Hover on cog and click hello **Add-ons**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon1.png)

9. <span data-ttu-id="9c5ff-174">Klik onder sectie tabblad invoegtoepassingen op **vinden van nieuwe invoegtoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="9c5ff-175">Search **Kantega SSO voor Bamboe (SAML & Kerberos)** en klik op **installeren** knop tooinstall Hallo nieuwe SAML-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-175">Search **Kantega SSO for Bamboo (SAML & Kerberos)** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon2.png)

10. <span data-ttu-id="9c5ff-177">Hallo-invoegtoepassing installatie wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-177">hello plugin installation will start.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon21.png)

11. <span data-ttu-id="9c5ff-179">Zodra het Hallo-installatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-179">Once hello installation is complete.</span></span> <span data-ttu-id="9c5ff-180">Klik op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-180">Click **Close**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon33.png)

12. <span data-ttu-id="9c5ff-182">Klik op **Beheren**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-182">Click **Manage**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon34.png)
    
13. <span data-ttu-id="9c5ff-184">Klik op **configureren** tooconfigure Hallo nieuwe invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-184">Click **Configure** tooconfigure hello new plugin.</span></span>  

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon3.png)

14. <span data-ttu-id="9c5ff-186">In Hallo **SAML** sectie.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-186">In hello **SAML** section.</span></span> <span data-ttu-id="9c5ff-187">Selecteer **Azure Active Directory (Azure AD)** van Hallo **toevoegen identiteitsprovider** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-187">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon4.png)

15. <span data-ttu-id="9c5ff-189">Abonnement als selecteren **Basic**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-189">Select subscription level as **Basic**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon5.png)

16. <span data-ttu-id="9c5ff-191">Op Hallo **App-eigenschappen** sectie, voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="9c5ff-191">On hello **App properties** section, perform following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon6.png)

    <span data-ttu-id="9c5ff-193">a.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-193">a.</span></span> <span data-ttu-id="9c5ff-194">Kopiëren Hallo **App ID URI** waarde en deze gebruiken als **id, de antwoord-URL en de aanmeldings-URL** op Hallo **Kantega SSO voor Bamboe domein en URL's** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-194">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for Bamboo Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="9c5ff-195">b.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-195">b.</span></span> <span data-ttu-id="9c5ff-196">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-196">Click **Next**.</span></span>

17. <span data-ttu-id="9c5ff-197">Op Hallo **metagegevens importeren** sectie, voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="9c5ff-197">On hello **Metadata import** section, perform following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon7.png)

    <span data-ttu-id="9c5ff-199">a.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-199">a.</span></span> <span data-ttu-id="9c5ff-200">Selecteer **metagegevensbestand op mijn computer**, en de metagegevens-uploadbestand, die u hebt gedownload vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-200">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="9c5ff-201">b.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-201">b.</span></span> <span data-ttu-id="9c5ff-202">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-202">Click **Next**.</span></span>

18. <span data-ttu-id="9c5ff-203">Op Hallo **en SSO** sectie, voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="9c5ff-203">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon8.png)

    <span data-ttu-id="9c5ff-205">a.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-205">a.</span></span> <span data-ttu-id="9c5ff-206">Naam van de identiteitsprovider Hallo toevoegen in **identiteit providernaam** textbox (bijvoorbeeld Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9c5ff-206">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="9c5ff-207">b.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-207">b.</span></span> <span data-ttu-id="9c5ff-208">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-208">Click **Next**.</span></span>

19. <span data-ttu-id="9c5ff-209">Hallo-handtekeningcertificaat en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-209">Verify hello Signing certificate and click **Next**.</span></span>    

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon9.png)

20. <span data-ttu-id="9c5ff-211">Op Hallo **Bamboe gebruikersaccounts** sectie, voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="9c5ff-211">On hello **Bamboo user accounts** section, perform following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon10.png)

    <span data-ttu-id="9c5ff-213">a.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-213">a.</span></span> <span data-ttu-id="9c5ff-214">Selecteer **gebruikers in de Bamboe interne Directory maken, indien nodig** en Voer Hallo juiste naam van groep Hallo voor gebruikers (kan meerdere Nee.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-214">Select **Create users in Bamboo's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="9c5ff-215">van groepen van elkaar gescheiden door komma's).</span><span class="sxs-lookup"><span data-stu-id="9c5ff-215">of groups separated by comma).</span></span>

    <span data-ttu-id="9c5ff-216">b.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-216">b.</span></span> <span data-ttu-id="9c5ff-217">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-217">Click **Next**.</span></span>

21. <span data-ttu-id="9c5ff-218">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-218">Click **Finish**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon11.png)

22. <span data-ttu-id="9c5ff-220">Op Hallo **bekend domeinen voor Azure AD** sectie, voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="9c5ff-220">On hello **Known domains for Azure AD** section, perform following steps:</span></span>   

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon12.png)

    <span data-ttu-id="9c5ff-222">a.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-222">a.</span></span> <span data-ttu-id="9c5ff-223">Selecteer **domeinen bekend** van Hallo linkerpaneel van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-223">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="9c5ff-224">b.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-224">b.</span></span> <span data-ttu-id="9c5ff-225">Voer in Hallo domeinnaam **domeinen bekend** textbox.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-225">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="9c5ff-226">c.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-226">c.</span></span> <span data-ttu-id="9c5ff-227">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-227">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9c5ff-228">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-228">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9c5ff-229">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-229">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9c5ff-230">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9c5ff-230">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9c5ff-231">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9c5ff-231">Creating an Azure AD test user</span></span>
<span data-ttu-id="9c5ff-232">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-232">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="9c5ff-234">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9c5ff-234">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c5ff-235">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-235">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9c5ff-237">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-237">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9c5ff-239">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-239">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9c5ff-241">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9c5ff-241">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9c5ff-243">a.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-243">a.</span></span> <span data-ttu-id="9c5ff-244">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-244">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9c5ff-245">b.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-245">b.</span></span> <span data-ttu-id="9c5ff-246">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-246">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9c5ff-247">c.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-247">c.</span></span> <span data-ttu-id="9c5ff-248">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-248">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9c5ff-249">d.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-249">d.</span></span> <span data-ttu-id="9c5ff-250">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-250">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bamboo-test-user"></a><span data-ttu-id="9c5ff-251">Maken van een SSO Kantega voor Bamboe testgebruiker</span><span class="sxs-lookup"><span data-stu-id="9c5ff-251">Creating a Kantega SSO for Bamboo test user</span></span>

<span data-ttu-id="9c5ff-252">Azure AD tooenable gebruikers toolog in tooBamboo, ze in Bamboe moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-252">tooenable Azure AD users toolog in tooBamboo, they must be provisioned into Bamboo.</span></span> <span data-ttu-id="9c5ff-253">In Kantega SSO voor Bamboe is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-253">In Kantega SSO for Bamboo, provisioning is a manual task.</span></span>

<span data-ttu-id="9c5ff-254">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9c5ff-254">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c5ff-255">Tooyour Bamboe op de lokale server aanmelden als beheerder.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-255">Log in tooyour Bamboo on premise server as an administrator.</span></span>

2. <span data-ttu-id="9c5ff-256">Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **Gebruikersbeheer**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-256">Hover on cog and click hello **User management**.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-kantegassoforbamboo-tutorial/user1.png) 

3. <span data-ttu-id="9c5ff-258">Klik op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-258">Click **Users**.</span></span> <span data-ttu-id="9c5ff-259">Onder Hallo **gebruiker toevoegen** sectie, dit stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9c5ff-259">Under hello **Add user** section, Perform follwing steps:</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-kantegassoforbamboo-tutorial/user2.png) 

    <span data-ttu-id="9c5ff-261">a.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-261">a.</span></span> <span data-ttu-id="9c5ff-262">In Hallo **gebruikersnaam** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-262">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="9c5ff-263">b.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-263">b.</span></span> <span data-ttu-id="9c5ff-264">In Hallo **wachtwoord** textbox type Hallo wachtwoord van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-264">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="9c5ff-265">c.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-265">c.</span></span> <span data-ttu-id="9c5ff-266">In Hallo **wachtwoord bevestigen** textbox Hallo Bevestig het wachtwoord van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-266">In hello **Confirm Password** textbox, reenter hello password of user.</span></span>
    
    <span data-ttu-id="9c5ff-267">d.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-267">d.</span></span> <span data-ttu-id="9c5ff-268">In Hallo **volledige naam** textbox, volledige naam van de gebruiker Hallo zoals Britta Simon type.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-268">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="9c5ff-269">e.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-269">e.</span></span> <span data-ttu-id="9c5ff-270">In Hallo **e** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-270">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="9c5ff-271">f.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-271">f.</span></span> <span data-ttu-id="9c5ff-272">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-272">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9c5ff-273">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c5ff-273">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9c5ff-274">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooKantega SSO voor Bamboe.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-274">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for Bamboo.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="9c5ff-276">**tooassign Britta Simon tooKantega SSO voor Bamboe, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9c5ff-276">**tooassign Britta Simon tooKantega SSO for Bamboo, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c5ff-277">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-277">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="9c5ff-279">Selecteer in de lijst met de toepassingen van Hallo **Kantega SSO voor Bamboe**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-279">In hello applications list, select **Kantega SSO for Bamboo**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_app.png) 

3. <span data-ttu-id="9c5ff-281">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-281">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="9c5ff-283">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-283">Click **Add** button.</span></span> <span data-ttu-id="9c5ff-284">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="9c5ff-286">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-286">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9c5ff-287">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9c5ff-288">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9c5ff-289">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9c5ff-289">Testing single sign-on</span></span>

<span data-ttu-id="9c5ff-290">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-290">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9c5ff-291">Als u op Hallo Kantega SSO Bamboe tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour Kantega SSO voor Bamboe toepassing.</span><span class="sxs-lookup"><span data-stu-id="9c5ff-291">When you click hello Kantega SSO for Bamboo tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for Bamboo application.</span></span>
<span data-ttu-id="9c5ff-292">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9c5ff-292">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9c5ff-293">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9c5ff-293">Additional resources</span></span>

* [<span data-ttu-id="9c5ff-294">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9c5ff-294">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9c5ff-295">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9c5ff-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_203.png

