---
title: 'Zelfstudie: Azure Active Directory-integratie met Canvas Lms | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Canvas LMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="4192d-103">Zelfstudie: Azure Active Directory-integratie met Canvas LMS</span><span class="sxs-lookup"><span data-stu-id="4192d-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="4192d-104">In deze zelfstudie leert u hoe toointegrate Canvas met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4192d-104">In this tutorial, you learn how toointegrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4192d-105">Canvas integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4192d-105">Integrating Canvas with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4192d-106">U kunt beheren in Azure AD die tooCanvas toegang heeft</span><span class="sxs-lookup"><span data-stu-id="4192d-106">You can control in Azure AD who has access tooCanvas</span></span>
- <span data-ttu-id="4192d-107">U kunt uw gebruikers tooautomatically get aangemelde tooCanvas (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="4192d-107">You can enable your users tooautomatically get signed-on tooCanvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4192d-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="4192d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4192d-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4192d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4192d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4192d-110">Prerequisites</span></span>

<span data-ttu-id="4192d-111">Azure AD-integratie met Canvas tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="4192d-111">tooconfigure Azure AD integration with Canvas, you need hello following items:</span></span>

- <span data-ttu-id="4192d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4192d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4192d-113">Een Canvas eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="4192d-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4192d-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4192d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4192d-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4192d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4192d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4192d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4192d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4192d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4192d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="4192d-118">Scenario description</span></span>
<span data-ttu-id="4192d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4192d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4192d-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="4192d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4192d-121">Het toevoegen van Canvas van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4192d-121">Adding Canvas from hello gallery</span></span>
2. <span data-ttu-id="4192d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4192d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-hello-gallery"></a><span data-ttu-id="4192d-123">Het toevoegen van Canvas van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4192d-123">Adding Canvas from hello gallery</span></span>
<span data-ttu-id="4192d-124">tooconfigure hello integratie van Canvas in Azure AD, moet u tooadd Canvas uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="4192d-124">tooconfigure hello integration of Canvas into Azure AD, you need tooadd Canvas from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4192d-125">**tooadd Canvas via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4192d-125">**tooadd Canvas from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4192d-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4192d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4192d-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4192d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4192d-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4192d-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="4192d-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4192d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="4192d-133">Typ in het zoekvak Hallo **Canvas**.</span><span class="sxs-lookup"><span data-stu-id="4192d-133">In hello search box, type **Canvas**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="4192d-135">Selecteer in het deelvenster resultaten hello, **Canvas**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4192d-135">In hello results panel, select **Canvas**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4192d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4192d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4192d-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Canvas op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4192d-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4192d-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in het Canvas is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4192d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Canvas is tooa user in Azure AD.</span></span> <span data-ttu-id="4192d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in het Canvas Hallo toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="4192d-140">In other words, a link relationship between an Azure AD user and hello related user in Canvas needs toobe established.</span></span>

<span data-ttu-id="4192d-141">In het canvas past, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="4192d-141">In Canvas, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4192d-142">tooconfigure en test eenmalige aanmelding Azure AD met Canvas, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4192d-142">tooconfigure and test Azure AD single sign-on with Canvas, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4192d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="4192d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4192d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4192d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4192d-145">**[Maken van een testgebruiker Canvas](#creating-a-canvas-test-user)**  -toohave een equivalent van Britta Simon in die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4192d-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - toohave a counterpart of Britta Simon in Canvas that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4192d-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4192d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4192d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="4192d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4192d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="4192d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4192d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Canvas.</span><span class="sxs-lookup"><span data-stu-id="4192d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="4192d-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Canvas Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4192d-150">**tooconfigure Azure AD single sign-on with Canvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="4192d-151">In de Azure-portal op Hallo Hallo **Canvas** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4192d-151">In hello Azure portal, on hello **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="4192d-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4192d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="4192d-155">Op Hallo **Canvas domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4192d-155">On hello **Canvas Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="4192d-157">a.</span><span class="sxs-lookup"><span data-stu-id="4192d-157">a.</span></span> <span data-ttu-id="4192d-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="4192d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="4192d-159">b.</span><span class="sxs-lookup"><span data-stu-id="4192d-159">b.</span></span> <span data-ttu-id="4192d-160">In Hallo **id** textbox Hallo typewaarde met Hallo patroon volgen:`https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="4192d-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4192d-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="4192d-161">These values are not real.</span></span> <span data-ttu-id="4192d-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="4192d-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4192d-163">Neem contact op met [Canvas Client ondersteuningsteam](https://community.canvaslms.com/community/help) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="4192d-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) tooget these values.</span></span> 
 
4. <span data-ttu-id="4192d-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="4192d-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="4192d-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4192d-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4192d-168">Op Hallo **configuratie tekenpapier** sectie, klikt u op **Canvas configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="4192d-168">On hello **Canvas Configuration** section, click **Configure Canvas** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4192d-169">Kopiëren Hallo **URL van wijzigen wachtwoord, Sign-Out URL SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="4192d-169">Copy hello **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="4192d-171">In een ander browservenster, meld u aan tooyour Canvas bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="4192d-171">In a different web browser window, log in tooyour Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="4192d-172">Ga te**cursussen \> beheerde Accounts \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="4192d-172">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="4192d-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="4192d-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="4192d-174">Selecteer in het navigatievenster aan de linkerkant Hallo Hallo **verificatie**, en klik vervolgens op **nieuwe SAML-configuratie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4192d-174">In hello navigation pane on hello left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="4192d-175">![Verificatie](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "verificatie")</span><span class="sxs-lookup"><span data-stu-id="4192d-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="4192d-176">Voer op Hallo integratie van de huidige pagina Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4192d-176">On hello Current Integration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="4192d-177">![Huidige integratie](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "huidige integratie")</span><span class="sxs-lookup"><span data-stu-id="4192d-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="4192d-178">a.</span><span class="sxs-lookup"><span data-stu-id="4192d-178">a.</span></span> <span data-ttu-id="4192d-179">In **IdP entiteit-ID** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4192d-179">In **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4192d-180">b.</span><span class="sxs-lookup"><span data-stu-id="4192d-180">b.</span></span> <span data-ttu-id="4192d-181">In **logboek URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4192d-181">In **Log On URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="4192d-182">c.</span><span class="sxs-lookup"><span data-stu-id="4192d-182">c.</span></span> <span data-ttu-id="4192d-183">In **afmeldings-URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4192d-183">In **Log Out URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4192d-184">d.</span><span class="sxs-lookup"><span data-stu-id="4192d-184">d.</span></span> <span data-ttu-id="4192d-185">In **koppeling van wijzigen wachtwoord** textbox plakken Hallo-waarde van **URL van wijzigen wachtwoord** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4192d-185">In **Change Password Link** textbox, paste hello value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="4192d-186">e.</span><span class="sxs-lookup"><span data-stu-id="4192d-186">e.</span></span> <span data-ttu-id="4192d-187">In **vingerafdruk van certificaat** textbox plakken Hallo **vingerafdruk** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4192d-187">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="4192d-188">f.</span><span class="sxs-lookup"><span data-stu-id="4192d-188">f.</span></span> <span data-ttu-id="4192d-189">Van Hallo **aanmelding kenmerk** selecteert **NameID**.</span><span class="sxs-lookup"><span data-stu-id="4192d-189">From hello **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="4192d-190">g.</span><span class="sxs-lookup"><span data-stu-id="4192d-190">g.</span></span> <span data-ttu-id="4192d-191">Van Hallo **id indeling** selecteert **emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="4192d-191">From hello **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="4192d-192">h.</span><span class="sxs-lookup"><span data-stu-id="4192d-192">h.</span></span> <span data-ttu-id="4192d-193">Klik op **verificatie-instellingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4192d-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="4192d-194">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="4192d-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4192d-195">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="4192d-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4192d-196">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4192d-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4192d-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4192d-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="4192d-198">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4192d-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="4192d-200">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4192d-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4192d-201">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4192d-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4192d-203">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4192d-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4192d-205">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="4192d-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4192d-207">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4192d-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4192d-209">a.</span><span class="sxs-lookup"><span data-stu-id="4192d-209">a.</span></span> <span data-ttu-id="4192d-210">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4192d-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4192d-211">b.</span><span class="sxs-lookup"><span data-stu-id="4192d-211">b.</span></span> <span data-ttu-id="4192d-212">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4192d-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4192d-213">c.</span><span class="sxs-lookup"><span data-stu-id="4192d-213">c.</span></span> <span data-ttu-id="4192d-214">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="4192d-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4192d-215">d.</span><span class="sxs-lookup"><span data-stu-id="4192d-215">d.</span></span> <span data-ttu-id="4192d-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4192d-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="4192d-217">Maken van een testgebruiker Canvas</span><span class="sxs-lookup"><span data-stu-id="4192d-217">Creating a Canvas test user</span></span>

<span data-ttu-id="4192d-218">Azure AD tooenable gebruikers toolog in tooCanvas, moeten ze worden ingericht in Canvas.</span><span class="sxs-lookup"><span data-stu-id="4192d-218">tooenable Azure AD users toolog in tooCanvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="4192d-219">In geval van een Canvas is gebruikersaanvragen een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="4192d-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="4192d-220">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4192d-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="4192d-221">Meld u bij tooyour **Canvas** tenant.</span><span class="sxs-lookup"><span data-stu-id="4192d-221">Log in tooyour **Canvas** tenant.</span></span>

2. <span data-ttu-id="4192d-222">Ga te**cursussen \> beheerde Accounts \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="4192d-222">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="4192d-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="4192d-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="4192d-224">Klik op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4192d-224">Click **Users**.</span></span>
   
   <span data-ttu-id="4192d-225">![Gebruikers](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="4192d-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="4192d-226">Klik op **nieuwe gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4192d-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="4192d-227">![Gebruikers](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="4192d-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="4192d-228">Op Hallo pagina dialoogvenster Nieuwe gebruiker toevoegen, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4192d-228">On hello Add a New User dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="4192d-229">![Gebruiker toevoegen](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="4192d-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="4192d-230">a.</span><span class="sxs-lookup"><span data-stu-id="4192d-230">a.</span></span> <span data-ttu-id="4192d-231">In Hallo **volledige naam** textbox Voer Hallo-naam van gebruiker zoals **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4192d-231">In hello **Full Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="4192d-232">b.</span><span class="sxs-lookup"><span data-stu-id="4192d-232">b.</span></span> <span data-ttu-id="4192d-233">In Hallo **e** textbox Voer Hallo e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="4192d-233">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="4192d-234">c.</span><span class="sxs-lookup"><span data-stu-id="4192d-234">c.</span></span> <span data-ttu-id="4192d-235">In Hallo **aanmelding** textbox Voer van Hallo gebruiker Azure AD e-mailadres zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="4192d-235">In hello **Login** textbox, enter hello user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="4192d-236">d.</span><span class="sxs-lookup"><span data-stu-id="4192d-236">d.</span></span> <span data-ttu-id="4192d-237">Selecteer **e-mailadres Hallo gebruikersnaam over het maken van dit account**.</span><span class="sxs-lookup"><span data-stu-id="4192d-237">Select **Email hello user about this account creation**.</span></span>

   <span data-ttu-id="4192d-238">e.</span><span class="sxs-lookup"><span data-stu-id="4192d-238">e.</span></span> <span data-ttu-id="4192d-239">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4192d-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="4192d-240">U kunt andere Canvas gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Canvas tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="4192d-240">You can use any other Canvas user account creation tools or APIs provided by Canvas tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4192d-241">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4192d-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4192d-242">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooCanvas toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="4192d-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCanvas.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="4192d-244">**tooassign Britta Simon tooCanvas, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4192d-244">**tooassign Britta Simon tooCanvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="4192d-245">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4192d-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="4192d-247">Selecteer in de lijst met de toepassingen van Hallo **Canvas**.</span><span class="sxs-lookup"><span data-stu-id="4192d-247">In hello applications list, select **Canvas**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="4192d-249">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="4192d-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="4192d-251">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4192d-251">Click **Add** button.</span></span> <span data-ttu-id="4192d-252">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4192d-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="4192d-254">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="4192d-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4192d-255">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4192d-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4192d-256">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4192d-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4192d-257">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4192d-257">Testing single sign-on</span></span>

<span data-ttu-id="4192d-258">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="4192d-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4192d-259">Als u op Hallo Canvas tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Canvas toepassing.</span><span class="sxs-lookup"><span data-stu-id="4192d-259">When you click hello Canvas tile in hello Access Panel, you should get automatically signed-on tooyour Canvas application.</span></span>
<span data-ttu-id="4192d-260">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4192d-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4192d-261">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4192d-261">Additional resources</span></span>

* [<span data-ttu-id="4192d-262">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4192d-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4192d-263">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4192d-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

