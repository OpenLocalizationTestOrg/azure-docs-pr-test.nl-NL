---
title: 'Zelfstudie: Azure Active Directory-integratie met SAML SSO voor samenloop door resolutie GmbH | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SAML SSO voor samenloop door resolutie GmbH.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: fe50636709857ec49023e24bdc8c6cd8c58e3c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a><span data-ttu-id="ad71f-103">Zelfstudie: Azure Active Directory-integratie met SAML SSO voor samenloop door resolutie GmbH</span><span class="sxs-lookup"><span data-stu-id="ad71f-103">Tutorial: Azure Active Directory integration with SAML SSO for Confluence by resolution GmbH</span></span>

<span data-ttu-id="ad71f-104">In deze zelfstudie leert u hoe toointegrate SAML SSO voor samenloop door resolutie GmbH met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad71f-104">In this tutorial, you learn how toointegrate SAML SSO for Confluence by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad71f-105">Integratie van SAML SSO voor samenloop door resolutie GmbH met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ad71f-105">Integrating SAML SSO for Confluence by resolution GmbH with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ad71f-106">U kunt beheren in Azure AD wie toegang tot tooSAML SSO voor samenloop door resolutie GmbH heeft</span><span class="sxs-lookup"><span data-stu-id="ad71f-106">You can control in Azure AD who has access tooSAML SSO for Confluence by resolution GmbH</span></span>
- <span data-ttu-id="ad71f-107">U kunt uw gebruikers tooautomatically get aangemelde tooSAML SSO voor samenloop door resolutie GmbH (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ad71f-107">You can enable your users tooautomatically get signed-on tooSAML SSO for Confluence by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ad71f-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ad71f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ad71f-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad71f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad71f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ad71f-110">Prerequisites</span></span>

<span data-ttu-id="ad71f-111">Azure AD-integratie met SAML SSO voor samenloop door resolutie GmbH tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ad71f-111">tooconfigure Azure AD integration with SAML SSO for Confluence by resolution GmbH, you need hello following items:</span></span>

- <span data-ttu-id="ad71f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ad71f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ad71f-113">Een SAML SSO voor samenloop door resolutie GmbH eenmalige aanmelding voor ingeschakelde abonnement</span><span class="sxs-lookup"><span data-stu-id="ad71f-113">A SAML SSO for Confluence by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad71f-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ad71f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ad71f-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ad71f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad71f-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ad71f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ad71f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad71f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad71f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ad71f-118">Scenario description</span></span>
<span data-ttu-id="ad71f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ad71f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad71f-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ad71f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad71f-121">Het toevoegen van SAML SSO voor samenloop door resolutie GmbH van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ad71f-121">Adding SAML SSO for Confluence by resolution GmbH from hello gallery</span></span>
2. <span data-ttu-id="ad71f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ad71f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-hello-gallery"></a><span data-ttu-id="ad71f-123">Het toevoegen van SAML SSO voor samenloop door resolutie GmbH van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ad71f-123">Adding SAML SSO for Confluence by resolution GmbH from hello gallery</span></span>

<span data-ttu-id="ad71f-124">tooconfigure hello integratie van SAML SSO voor samenloop door resolutie GmbH in Azure AD, moet u tooadd SAML SSO door resolutie GmbH uit Hallo galerie tooyour lijst met beheerde SaaS-apps voor samenloop.</span><span class="sxs-lookup"><span data-stu-id="ad71f-124">tooconfigure hello integration of SAML SSO for Confluence by resolution GmbH into Azure AD, you need tooadd SAML SSO for Confluence by resolution GmbH from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ad71f-125">**tooadd SAML SSO voor samenloop door resolutie GmbH via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ad71f-125">**tooadd SAML SSO for Confluence by resolution GmbH from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad71f-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ad71f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ad71f-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ad71f-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ad71f-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad71f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ad71f-133">Typ in het zoekvak Hallo **SAML SSO voor samenloop door resolutie GmbH**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-133">In hello search box, type **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. <span data-ttu-id="ad71f-135">Selecteer in het deelvenster resultaten hello, **SAML SSO voor samenloop door resolutie GmbH**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad71f-135">In hello results panel, select **SAML SSO for Confluence by resolution GmbH**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ad71f-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ad71f-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="ad71f-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met SAML SSO voor samenloop door resolutie die GmbH op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="ad71f-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ad71f-139">Voor één aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in SAML SSO voor samenloop door resolutie GmbH is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad71f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAML SSO for Confluence by resolution GmbH is tooa user in Azure AD.</span></span> <span data-ttu-id="ad71f-140">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in SAML SSO voor samenloop door de resolutie moet GmbH toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="ad71f-140">In other words, a link relationship between an Azure AD user and hello related user in SAML SSO for Confluence by resolution GmbH needs toobe established.</span></span>

<span data-ttu-id="ad71f-141">Wijs in SAML SSO voor samenloop door resolutie GmbH, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="ad71f-141">In SAML SSO for Confluence by resolution GmbH, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ad71f-142">tooconfigure en test eenmalige aanmelding Azure AD met SAML SSO voor samenloop door resolutie GmbH, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ad71f-142">tooconfigure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ad71f-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="ad71f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ad71f-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad71f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ad71f-145">**[Maken van een SAML SSO voor samenloop door resolutie GmbH testgebruiker](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  -toohave een equivalent van Britta Simon in SAML SSO voor samenloop door resolutie GmbH die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ad71f-145">**[Creating a SAML SSO for Confluence by resolution GmbH test user](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)** - toohave a counterpart of Britta Simon in SAML SSO for Confluence by resolution GmbH that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ad71f-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ad71f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad71f-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ad71f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ad71f-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ad71f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ad71f-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en configureer eenmalige aanmelding in uw SAML SSO voor samenloop resolutie GmbH toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad71f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAML SSO for Confluence by resolution GmbH application.</span></span>

<span data-ttu-id="ad71f-150">**tooconfigure eenmalige aanmelding Azure AD met SAML SSO voor samenloop door resolutie GmbH, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ad71f-150">**tooconfigure Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad71f-151">In Azure-portal op Hallo Hallo **SAML SSO voor samenloop door resolutie GmbH** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-151">In hello Azure portal, on hello **SAML SSO for Confluence by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ad71f-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ad71f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. <span data-ttu-id="ad71f-155">Op Hallo **SAML SSO voor samenloop door resolutie GmbH domein en URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="ad71f-155">On hello **SAML SSO for Confluence by resolution GmbH Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    <span data-ttu-id="ad71f-157">a.</span><span class="sxs-lookup"><span data-stu-id="ad71f-157">a.</span></span> <span data-ttu-id="ad71f-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="ad71f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="ad71f-159">b.</span><span class="sxs-lookup"><span data-stu-id="ad71f-159">b.</span></span> <span data-ttu-id="ad71f-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="ad71f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="ad71f-161">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="ad71f-162">U kunt eventueel tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="ad71f-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    <span data-ttu-id="ad71f-164">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="ad71f-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="ad71f-165">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="ad71f-165">These values are not real.</span></span> <span data-ttu-id="ad71f-166">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="ad71f-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="ad71f-167">Neem contact op met [SAML SSO voor samenloop door resolutie GmbH Client ondersteuningsteam](https://www.resolution.de/go/support) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="ad71f-167">Contact [SAML SSO for Confluence by resolution GmbH Client support team](https://www.resolution.de/go/support) tooget these values.</span></span> 

5. <span data-ttu-id="ad71f-168">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ad71f-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. <span data-ttu-id="ad71f-170">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ad71f-170">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. <span data-ttu-id="ad71f-172">Aanmelden in een ander browservenster tooyour **SAML SSO voor samenloop door resolutie GmbH beheerportal** als beheerder.</span><span class="sxs-lookup"><span data-stu-id="ad71f-172">In a different web browser window, log in tooyour **SAML SSO for Confluence by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="ad71f-173">Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **invoegtoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-173">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. <span data-ttu-id="ad71f-175">U bent omgeleide tooAdministrator Access-pagina.</span><span class="sxs-lookup"><span data-stu-id="ad71f-175">You are redirected tooAdministrator Access page.</span></span> <span data-ttu-id="ad71f-176">Voer Hallo wachtwoord in en klik op **bevestigen** knop.</span><span class="sxs-lookup"><span data-stu-id="ad71f-176">Enter hello password and click **Confirm** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. <span data-ttu-id="ad71f-178">Onder **ATLASSIAN MARKETPLACE** tabblad **vinden van nieuwe invoegtoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-178">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. <span data-ttu-id="ad71f-180">Search **SAML eenmalige aanmelding op (SSO) voor samenloop** en klik op **installeren** knop tooinstall Hallo nieuwe SAML-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="ad71f-180">Search **SAML Single Sign On (SSO) for Confluence** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. <span data-ttu-id="ad71f-182">Hallo-invoegtoepassing installatie wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="ad71f-182">hello plugin installation will start.</span></span> <span data-ttu-id="ad71f-183">Klik op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-183">Click **Close**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. <span data-ttu-id="ad71f-186">Klik op **Beheren**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-186">Click **Manage**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. <span data-ttu-id="ad71f-188">Klik op **configureren** tooconfigure Hallo nieuwe invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="ad71f-188">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. <span data-ttu-id="ad71f-190">Deze nieuwe invoegtoepassing kunt u vinden onder **gebruikers & beveiliging** tabblad.</span><span class="sxs-lookup"><span data-stu-id="ad71f-190">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. <span data-ttu-id="ad71f-192">Op **SAML-configuratie voor invoegtoepassing van SingleSignOn** pagina, klikt u op **toevoegen van extra identiteitsprovider** knop tooconfigure Hallo-instellingen van de id-Provider.</span><span class="sxs-lookup"><span data-stu-id="ad71f-192">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button tooconfigure hello settings of Identity Provider.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. <span data-ttu-id="ad71f-194">Voer de volgende stappen uit op deze pagina:</span><span class="sxs-lookup"><span data-stu-id="ad71f-194">Perform following steps on this page:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    <span data-ttu-id="ad71f-196">a.</span><span class="sxs-lookup"><span data-stu-id="ad71f-196">a.</span></span> <span data-ttu-id="ad71f-197">Voeg **naam** Hallo identiteitsprovider (bijvoorbeeld Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad71f-197">Add **Name** of hello Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="ad71f-198">b.</span><span class="sxs-lookup"><span data-stu-id="ad71f-198">b.</span></span> <span data-ttu-id="ad71f-199">Voeg **beschrijving** Hallo identiteitsprovider (bijvoorbeeld Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad71f-199">Add **Description** of hello Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="ad71f-200">c.</span><span class="sxs-lookup"><span data-stu-id="ad71f-200">c.</span></span> <span data-ttu-id="ad71f-201">Klik op **XML** en selecteer Hallo **metagegevens** -bestand dat u hebt gedownload vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ad71f-201">Click **XML** and select hello **Metadata** file that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="ad71f-202">d.</span><span class="sxs-lookup"><span data-stu-id="ad71f-202">d.</span></span> <span data-ttu-id="ad71f-203">Klik op **Load** knop.</span><span class="sxs-lookup"><span data-stu-id="ad71f-203">Click **Load** button.</span></span>

    <span data-ttu-id="ad71f-204">e.</span><span class="sxs-lookup"><span data-stu-id="ad71f-204">e.</span></span> <span data-ttu-id="ad71f-205">Hallo IdP metagegevens worden gelezen en wordt ingevuld in velden als gemarkeerd in de schermafbeelding Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ad71f-205">It reads hello IdP metadata and populates hello fields as highlighted in hello screenshot.</span></span>   
18. <span data-ttu-id="ad71f-206">Klik op **instellingen opslaan** knop toosave Hallo instellingen.</span><span class="sxs-lookup"><span data-stu-id="ad71f-206">Click **Save settings** button toosave hello settings.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="ad71f-208">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="ad71f-208">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ad71f-209">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="ad71f-209">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ad71f-210">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ad71f-210">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ad71f-211">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ad71f-211">Creating an Azure AD test user</span></span>
<span data-ttu-id="ad71f-212">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ad71f-212">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ad71f-214">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ad71f-214">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad71f-215">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ad71f-215">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ad71f-217">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-217">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ad71f-219">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="ad71f-219">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ad71f-221">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ad71f-221">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ad71f-223">a.</span><span class="sxs-lookup"><span data-stu-id="ad71f-223">a.</span></span> <span data-ttu-id="ad71f-224">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-224">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad71f-225">b.</span><span class="sxs-lookup"><span data-stu-id="ad71f-225">b.</span></span> <span data-ttu-id="ad71f-226">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ad71f-226">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ad71f-227">c.</span><span class="sxs-lookup"><span data-stu-id="ad71f-227">c.</span></span> <span data-ttu-id="ad71f-228">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-228">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ad71f-229">d.</span><span class="sxs-lookup"><span data-stu-id="ad71f-229">d.</span></span> <span data-ttu-id="ad71f-230">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-230">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a><span data-ttu-id="ad71f-231">Maken van een SAML SSO voor samenloop door resolutie GmbH testgebruiker</span><span class="sxs-lookup"><span data-stu-id="ad71f-231">Creating a SAML SSO for Confluence by resolution GmbH test user</span></span>

<span data-ttu-id="ad71f-232">Azure AD tooenable gebruikers toolog in tooSAML SSO voor samenloop door resolutie GmbH deze moeten worden ingericht in SAML SSO voor samenloop door resolutie GmbH.</span><span class="sxs-lookup"><span data-stu-id="ad71f-232">tooenable Azure AD users toolog in tooSAML SSO for Confluence by resolution GmbH, they must be provisioned into SAML SSO for Confluence by resolution GmbH.</span></span>  
<span data-ttu-id="ad71f-233">In SAML SSO voor samenloop door resolutie GmbH is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="ad71f-233">In SAML SSO for Confluence by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="ad71f-234">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ad71f-234">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad71f-235">Tooyour SAML SSO voor samenloop door resolutie GmbH bedrijf site als een beheerder zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="ad71f-235">Log in tooyour SAML SSO for Confluence by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="ad71f-236">Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **Gebruikersbeheer**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-236">Hover on cog and click hello **User management**.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. <span data-ttu-id="ad71f-238">Klik onder de sectie gebruikers op **gebruikers toevoegen** tabblad. Op Hallo **'Gebruiker toevoegen'** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ad71f-238">Under Users section, click **Add users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    <span data-ttu-id="ad71f-240">a.</span><span class="sxs-lookup"><span data-stu-id="ad71f-240">a.</span></span> <span data-ttu-id="ad71f-241">In Hallo **gebruikersnaam** textbox type Hallo e-mailadres van de gebruiker zoals Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad71f-241">In hello **Username** textbox, type hello email of user like Britta Simon.</span></span>

    <span data-ttu-id="ad71f-242">b.</span><span class="sxs-lookup"><span data-stu-id="ad71f-242">b.</span></span> <span data-ttu-id="ad71f-243">In Hallo **volledige naam** textbox type Hallo volledige naam van gebruiker zoals Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad71f-243">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="ad71f-244">c.</span><span class="sxs-lookup"><span data-stu-id="ad71f-244">c.</span></span> <span data-ttu-id="ad71f-245">In Hallo **e** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ad71f-245">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="ad71f-246">d.</span><span class="sxs-lookup"><span data-stu-id="ad71f-246">d.</span></span> <span data-ttu-id="ad71f-247">In Hallo **wachtwoord** textbox Hallo een wachtwoord op voor Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad71f-247">In hello **Password** textbox, type hello password for Britta Simon.</span></span>

    <span data-ttu-id="ad71f-248">e.</span><span class="sxs-lookup"><span data-stu-id="ad71f-248">e.</span></span> <span data-ttu-id="ad71f-249">Klik op **wachtwoord bevestigen** Hallo wachtwoord opnieuw invoeren.</span><span class="sxs-lookup"><span data-stu-id="ad71f-249">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="ad71f-250">f.</span><span class="sxs-lookup"><span data-stu-id="ad71f-250">f.</span></span> <span data-ttu-id="ad71f-251">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ad71f-251">Click **Add** button.</span></span>    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ad71f-252">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad71f-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ad71f-253">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSAML SSO voor samenloop door resolutie GmbH.</span><span class="sxs-lookup"><span data-stu-id="ad71f-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAML SSO for Confluence by resolution GmbH.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ad71f-255">**tooassign Britta Simon tooSAML SSO voor samenloop door resolutie GmbH, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ad71f-255">**tooassign Britta Simon tooSAML SSO for Confluence by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad71f-256">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ad71f-258">Selecteer in de lijst met de toepassingen van Hallo **SAML SSO voor samenloop door resolutie GmbH**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-258">In hello applications list, select **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. <span data-ttu-id="ad71f-260">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ad71f-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ad71f-262">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ad71f-262">Click **Add** button.</span></span> <span data-ttu-id="ad71f-263">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad71f-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ad71f-265">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="ad71f-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ad71f-266">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad71f-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ad71f-267">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad71f-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ad71f-268">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ad71f-268">Testing single sign-on</span></span>

<span data-ttu-id="ad71f-269">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ad71f-269">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ad71f-270">Als u op Hallo SAML SSO voor samenloop door resolutie GmbH tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SAML SSO voor samenloop door resolutie GmbH toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad71f-270">When you click hello SAML SSO for Confluence by resolution GmbH tile in hello Access Panel, you should get automatically signed-on tooyour SAML SSO for Confluence by resolution GmbH application.</span></span>
<span data-ttu-id="ad71f-271">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ad71f-271">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ad71f-272">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ad71f-272">Additional resources</span></span>

* [<span data-ttu-id="ad71f-273">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad71f-273">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad71f-274">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ad71f-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

