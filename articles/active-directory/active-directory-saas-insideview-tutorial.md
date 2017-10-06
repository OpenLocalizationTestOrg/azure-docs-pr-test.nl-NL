---
title: 'Zelfstudie: Azure Active Directory-integratie met InsideView | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en InsideView.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 979c0c24f3a18a193616061b8c2e78292233a56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a><span data-ttu-id="6b2fb-103">Zelfstudie: Azure Active Directory-integratie met InsideView</span><span class="sxs-lookup"><span data-stu-id="6b2fb-103">Tutorial: Azure Active Directory integration with InsideView</span></span>

<span data-ttu-id="6b2fb-104">In deze zelfstudie leert u hoe toointegrate InsideView met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6b2fb-104">In this tutorial, you learn how toointegrate InsideView with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6b2fb-105">InsideView integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6b2fb-105">Integrating InsideView with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6b2fb-106">U kunt beheren in Azure AD die tooInsideView toegang heeft</span><span class="sxs-lookup"><span data-stu-id="6b2fb-106">You can control in Azure AD who has access tooInsideView</span></span>
- <span data-ttu-id="6b2fb-107">U kunt uw gebruikers tooautomatically get aangemelde tooInsideView (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6b2fb-107">You can enable your users tooautomatically get signed-on tooInsideView (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6b2fb-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6b2fb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6b2fb-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6b2fb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b2fb-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6b2fb-110">Prerequisites</span></span>

<span data-ttu-id="6b2fb-111">Azure AD-integratie met InsideView tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="6b2fb-111">tooconfigure Azure AD integration with InsideView, you need hello following items:</span></span>

- <span data-ttu-id="6b2fb-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6b2fb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6b2fb-113">Een InsideView eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6b2fb-113">A InsideView single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6b2fb-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6b2fb-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6b2fb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6b2fb-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6b2fb-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6b2fb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6b2fb-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6b2fb-118">Scenario description</span></span>
<span data-ttu-id="6b2fb-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6b2fb-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6b2fb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6b2fb-121">Het toevoegen van InsideView van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="6b2fb-121">Adding InsideView from hello gallery</span></span>
2. <span data-ttu-id="6b2fb-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6b2fb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insideview-from-hello-gallery"></a><span data-ttu-id="6b2fb-123">Het toevoegen van InsideView van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="6b2fb-123">Adding InsideView from hello gallery</span></span>
<span data-ttu-id="6b2fb-124">tooconfigure hello integratie van InsideView in tooAzure AD, moet u tooadd InsideView uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-124">tooconfigure hello integration of InsideView in tooAzure AD, you need tooadd InsideView from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6b2fb-125">**tooadd InsideView via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6b2fb-125">**tooadd InsideView from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b2fb-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6b2fb-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6b2fb-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6b2fb-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6b2fb-133">Typ in het zoekvak Hallo **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-133">In hello search box, type **InsideView**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. <span data-ttu-id="6b2fb-135">Selecteer in het deelvenster resultaten hello, **InsideView**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-135">In hello results panel, select **InsideView**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6b2fb-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6b2fb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6b2fb-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met InsideView op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6b2fb-138">In this section, you configure and test Azure AD single sign-on with InsideView based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6b2fb-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in InsideView is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in InsideView is tooa user in Azure AD.</span></span> <span data-ttu-id="6b2fb-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in InsideView toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-140">In other words, a link relationship between an Azure AD user and hello related user in InsideView needs toobe established.</span></span>

<span data-ttu-id="6b2fb-141">Wijs in InsideView, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-141">In InsideView, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6b2fb-142">tooconfigure en eenmalige aanmelding Azure AD-test met InsideView, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6b2fb-142">tooconfigure and test Azure AD single sign-on with InsideView, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6b2fb-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6b2fb-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6b2fb-145">**[Maken van een testgebruiker InsideView](#creating-a-insideview-test-user)**  -toohave een equivalent van Britta Simon in InsideView die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-145">**[Creating a InsideView test user](#creating-a-insideview-test-user)** - toohave a counterpart of Britta Simon in InsideView that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6b2fb-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6b2fb-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6b2fb-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6b2fb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6b2fb-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing InsideView configureren.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your InsideView application.</span></span>

<span data-ttu-id="6b2fb-150">**Azure AD tooconfigure eenmalige aanmelding met InsideView, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6b2fb-150">**tooconfigure Azure AD single sign-on with InsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b2fb-151">In de Azure-portal op Hallo Hallo **InsideView** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-151">In hello Azure portal, on hello **InsideView** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6b2fb-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. <span data-ttu-id="6b2fb-155">Op Hallo **InsideView domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6b2fb-155">On hello **InsideView Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    <span data-ttu-id="6b2fb-157">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://my.insideview.com/iv/<STS Name>/login.iv`</span><span class="sxs-lookup"><span data-stu-id="6b2fb-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://my.insideview.com/iv/<STS Name>/login.iv`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6b2fb-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-158">This value is not real.</span></span> <span data-ttu-id="6b2fb-159">Deze waarde met de werkelijke antwoord-URL Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="6b2fb-160">Neem contact op met [InsideView ondersteuningsteam ](mailto:support@insideview.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-160">Contact [InsideView support team ](mailto:support@insideview.com) tooget this value.</span></span>
 
4. <span data-ttu-id="6b2fb-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Raw)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. <span data-ttu-id="6b2fb-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6b2fb-165">Op Hallo **InsideView configuratie** sectie, klikt u op **configureren InsideView** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-165">On hello **InsideView Configuration** section, click **Configure InsideView** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6b2fb-166">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="6b2fb-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. <span data-ttu-id="6b2fb-168">In een ander browservenster, meld u aan tooyour InsideView bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-168">In a different web browser window, log in tooyour InsideView company site as an administrator.</span></span>

8. <span data-ttu-id="6b2fb-169">Klik in de werkbalk bovenaan Hallo Hallo op **Admin**, **SingleSignOn instellingen**, en klik vervolgens op **SAML toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-169">In hello toolbar on hello top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span></span>
   
   <span data-ttu-id="6b2fb-170">![SAML voor eenmalige aanmelding instellingen](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML voor eenmalige aanmelding instellingen")</span><span class="sxs-lookup"><span data-stu-id="6b2fb-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span></span>

9. <span data-ttu-id="6b2fb-171">In Hallo **toevoegen van een nieuwe SAML** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6b2fb-171">In hello **Add a New SAML** section, perform hello following steps:</span></span>

    <span data-ttu-id="6b2fb-172">![Voeg een nieuwe SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "toevoegen van een nieuwe SAML")</span><span class="sxs-lookup"><span data-stu-id="6b2fb-172">![Add a New SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Add a New SAML")</span></span>
   
    <span data-ttu-id="6b2fb-173">a.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-173">a.</span></span> <span data-ttu-id="6b2fb-174">In Hallo **STS Name** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-174">In hello **STS Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="6b2fb-175">b.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-175">b.</span></span> <span data-ttu-id="6b2fb-176">In **WS-SamlP-Fed ongevraagde eindpunt** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-176">In **SamlP/WS-Fed Unsolicited EndPoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="6b2fb-177">c.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-177">c.</span></span> <span data-ttu-id="6b2fb-178">Open uw base-64 gecodeerde certificaat dat u hebt gedownload van Azure portal, kopie Hallo inhoud ervan naar het Klembord, en plak deze toohello **STS Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-178">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **STS Certificate** textbox.</span></span>

    <span data-ttu-id="6b2fb-179">d.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-179">d.</span></span> <span data-ttu-id="6b2fb-180">In Hallo **Crm-Id Gebruikerskoppeling** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-180">In hello **Crm User Id Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
        
    <span data-ttu-id="6b2fb-181">e.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-181">e.</span></span> <span data-ttu-id="6b2fb-182">In Hallo **Crm e toewijzing** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-182">In hello **Crm Email Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="6b2fb-183">f.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-183">f.</span></span> <span data-ttu-id="6b2fb-184">In Hallo **Crm voornaam toewijzing** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-184">In hello **Crm First Name Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="6b2fb-185">g.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-185">g.</span></span> <span data-ttu-id="6b2fb-186">In Hallo **Crm lastName toewijzing** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-186">In hello **Crm lastName Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>  

    <span data-ttu-id="6b2fb-187">h.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-187">h.</span></span> <span data-ttu-id="6b2fb-188">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6b2fb-189">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6b2fb-190">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6b2fb-191">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6b2fb-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6b2fb-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6b2fb-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="6b2fb-193">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6b2fb-195">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6b2fb-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b2fb-196">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6b2fb-198">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6b2fb-200">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6b2fb-202">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6b2fb-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6b2fb-204">a.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-204">a.</span></span> <span data-ttu-id="6b2fb-205">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6b2fb-206">b.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-206">b.</span></span> <span data-ttu-id="6b2fb-207">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6b2fb-208">c.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-208">c.</span></span> <span data-ttu-id="6b2fb-209">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6b2fb-210">d.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-210">d.</span></span> <span data-ttu-id="6b2fb-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-211">Click **Create**.</span></span>
 
### <a name="creating-a-insideview-test-user"></a><span data-ttu-id="6b2fb-212">Een testgebruiker InsideView maken</span><span class="sxs-lookup"><span data-stu-id="6b2fb-212">Creating a InsideView test user</span></span>

<span data-ttu-id="6b2fb-213">Azure AD tooenable gebruikers toolog in tooInsideView, ze in tooInsideView moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-213">tooenable Azure AD users toolog in tooInsideView, they must be provisioned in tooInsideView.</span></span> <span data-ttu-id="6b2fb-214">In geval van InsideView Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-214">In hello case of InsideView, provisioning is a manual task.</span></span>

<span data-ttu-id="6b2fb-215">tooget gebruikers of contactpersonen die zijn gemaakt in InsideView, neem contact op met [InsideView ondersteuningsteam](mailto:support@insideview.com).</span><span class="sxs-lookup"><span data-stu-id="6b2fb-215">tooget users or contacts created in InsideView, Contact [InsideView support team](mailto:support@insideview.com).</span></span>

>[!NOTE]
><span data-ttu-id="6b2fb-216">U kunt andere InsideView gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door InsideView tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-216">You can use any other InsideView user account creation tools or APIs provided by InsideView tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6b2fb-217">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b2fb-217">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6b2fb-218">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooInsideView toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInsideView.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6b2fb-220">**tooassign Britta Simon tooInsideView, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6b2fb-220">**tooassign Britta Simon tooInsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b2fb-221">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6b2fb-223">Selecteer in de lijst met de toepassingen van Hallo **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-223">In hello applications list, select **InsideView**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. <span data-ttu-id="6b2fb-225">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6b2fb-227">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-227">Click **Add** button.</span></span> <span data-ttu-id="6b2fb-228">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6b2fb-230">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6b2fb-231">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6b2fb-232">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6b2fb-233">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6b2fb-233">Testing single sign-on</span></span>

<span data-ttu-id="6b2fb-234">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6b2fb-235">Als u op Hallo InsideView tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour InsideView toepassing.</span><span class="sxs-lookup"><span data-stu-id="6b2fb-235">When you click hello InsideView tile in hello Access Panel, you should get automatically signed-on tooyour InsideView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6b2fb-236">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6b2fb-236">Additional resources</span></span>

* [<span data-ttu-id="6b2fb-237">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b2fb-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6b2fb-238">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6b2fb-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_203.png

