---
title: 'Zelfstudie: Azure Active Directory-integratie met Workday | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en werkdag.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="2eb57-103">Zelfstudie: Azure Active Directory-integratie met Workday</span><span class="sxs-lookup"><span data-stu-id="2eb57-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="2eb57-104">In deze zelfstudie leert u hoe toointegrate Workday met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2eb57-104">In this tutorial, you learn how toointegrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2eb57-105">Werkdag integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2eb57-105">Integrating Workday with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2eb57-106">U kunt beheren in Azure AD die tooWorkday toegang heeft</span><span class="sxs-lookup"><span data-stu-id="2eb57-106">You can control in Azure AD who has access tooWorkday</span></span>
- <span data-ttu-id="2eb57-107">U kunt uw gebruikers tooautomatically get aangemelde tooWorkday (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="2eb57-107">You can enable your users tooautomatically get signed-on tooWorkday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2eb57-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2eb57-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2eb57-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2eb57-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2eb57-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2eb57-110">Prerequisites</span></span>

<span data-ttu-id="2eb57-111">Azure AD-integratie met Workday tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="2eb57-111">tooconfigure Azure AD integration with Workday, you need hello following items:</span></span>

- <span data-ttu-id="2eb57-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2eb57-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2eb57-113">Een werkdag eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2eb57-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2eb57-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2eb57-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2eb57-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2eb57-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2eb57-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2eb57-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2eb57-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2eb57-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2eb57-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2eb57-118">Scenario description</span></span>
<span data-ttu-id="2eb57-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2eb57-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2eb57-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2eb57-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2eb57-121">Het toevoegen van Workday van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2eb57-121">Adding Workday from hello gallery</span></span>
2. <span data-ttu-id="2eb57-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2eb57-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-hello-gallery"></a><span data-ttu-id="2eb57-123">Het toevoegen van Workday van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2eb57-123">Adding Workday from hello gallery</span></span>
<span data-ttu-id="2eb57-124">tooconfigure hello integratie van Workday in Azure AD, moet u tooadd Workday uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2eb57-124">tooconfigure hello integration of Workday into Azure AD, you need tooadd Workday from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2eb57-125">**tooadd Workday via Hallo gallery Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2eb57-125">**tooadd Workday from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2eb57-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2eb57-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2eb57-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2eb57-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2eb57-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2eb57-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2eb57-133">Typ in het zoekvak Hallo **Workday**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-133">In hello search box, type **Workday**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="2eb57-135">Selecteer in het deelvenster resultaten hello, **Workday**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2eb57-135">In hello results panel, select **Workday**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2eb57-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2eb57-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2eb57-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Workday op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="2eb57-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2eb57-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Workday is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2eb57-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workday is tooa user in Azure AD.</span></span> <span data-ttu-id="2eb57-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Workday toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="2eb57-140">In other words, a link relationship between an Azure AD user and hello related user in Workday needs toobe established.</span></span>

<span data-ttu-id="2eb57-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Workday.</span><span class="sxs-lookup"><span data-stu-id="2eb57-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workday.</span></span>

<span data-ttu-id="2eb57-142">tooconfigure en test eenmalige aanmelding Azure AD met behulp van Workday, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2eb57-142">tooconfigure and test Azure AD single sign-on with Workday, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2eb57-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="2eb57-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2eb57-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2eb57-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2eb57-145">**[Maken van een testgebruiker Workday](#creating-a-workday-test-user)**  -toohave een equivalent van Britta Simon in Workday die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2eb57-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - toohave a counterpart of Britta Simon in Workday that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2eb57-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2eb57-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2eb57-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2eb57-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2eb57-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2eb57-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2eb57-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Workday-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2eb57-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="2eb57-150">**Azure AD tooconfigure eenmalige aanmelding met werkdag, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2eb57-150">**tooconfigure Azure AD single sign-on with Workday, perform hello following steps:**</span></span>

1. <span data-ttu-id="2eb57-151">In de Azure-portal op Hallo Hallo **Workday** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-151">In hello Azure portal, on hello **Workday** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2eb57-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2eb57-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="2eb57-155">Op Hallo **Workday-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2eb57-155">On hello **Workday Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="2eb57-157">a.</span><span class="sxs-lookup"><span data-stu-id="2eb57-157">a.</span></span> <span data-ttu-id="2eb57-158">In Hallo **aanmeldings-URL** textbox Hallo typewaarde als:`https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="2eb57-158">In hello **Sign-on URL** textbox, type hello value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="2eb57-159">b.</span><span class="sxs-lookup"><span data-stu-id="2eb57-159">b.</span></span> <span data-ttu-id="2eb57-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="2eb57-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2eb57-161">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="2eb57-161">These values are not hello real.</span></span> <span data-ttu-id="2eb57-162">Deze waarden bijwerken met Hallo werkelijke aanmeldings-URL en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="2eb57-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="2eb57-163">Uw antwoord-URL bijvoorbeeld een subdomein moet hebben: www, wd2, wd3, wd3 impl, wd5, wd5 impl).</span><span class="sxs-lookup"><span data-stu-id="2eb57-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="2eb57-164">Met behulp van ongeveer '*http://www.myworkday.com*' werkt, maar '*http://myworkday.com*' niet.</span><span class="sxs-lookup"><span data-stu-id="2eb57-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="2eb57-165">Neem contact op met [Workday Client ondersteuningsteam](https://www.workday.com/en-us/partners-services/services/support.html) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2eb57-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget these values.</span></span> 
 

4. <span data-ttu-id="2eb57-166">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2eb57-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="2eb57-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2eb57-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2eb57-170">Op Hallo **Workday configuratie** sectie, klikt u op **configureren Workday** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="2eb57-170">On hello **Workday Configuration** section, click **Configure Workday** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2eb57-171">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="2eb57-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="2eb57-172">![Eenmalige aanmelding configureren](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="2eb57-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="2eb57-173">In een ander browservenster, meld u aan tooyour Workday bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="2eb57-173">In a different web browser window, log in tooyour Workday company site as an administrator.</span></span>

8. <span data-ttu-id="2eb57-174">Ga te**Menu \> Workbench**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-174">Go too**Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="2eb57-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span><span class="sxs-lookup"><span data-stu-id="2eb57-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="2eb57-176">Ga te**beheer**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-176">Go too**Account Administration**.</span></span>
   
    <span data-ttu-id="2eb57-177">![Beheer account](./media/active-directory-saas-workday-tutorial/IC782924.png "Account beheer")</span><span class="sxs-lookup"><span data-stu-id="2eb57-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="2eb57-178">Ga te**Tenant-instellingen bewerken – beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-178">Go too**Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="2eb57-179">![Beveiliging voor de Tenant bewerken](./media/active-directory-saas-workday-tutorial/IC782925.png "Tenant beveiliging bewerken")</span><span class="sxs-lookup"><span data-stu-id="2eb57-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="2eb57-180">In Hallo **Omleidings-URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2eb57-180">In hello **Redirection URLs** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="2eb57-181">![Omleidings-URL's](./media/active-directory-saas-workday-tutorial/IC7829581.png "Omleidings-URL's")</span><span class="sxs-lookup"><span data-stu-id="2eb57-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="2eb57-182">a.</span><span class="sxs-lookup"><span data-stu-id="2eb57-182">a.</span></span> <span data-ttu-id="2eb57-183">Klik op **rij toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="2eb57-184">b.</span><span class="sxs-lookup"><span data-stu-id="2eb57-184">b.</span></span> <span data-ttu-id="2eb57-185">In Hallo **aanmeldings-URL omleiden** textbox en Hallo **Omleidings-URL mobiele** textbox type Hallo **aanmeldings-URL** ingevoerde op Hallo **Workday-domein en URL's** sectie Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2eb57-185">In hello **Login Redirect URL** textbox and hello **Mobile Redirect URL** textbox, type hello **Sign-on URL** you have entered on hello **Workday Domain and URLs** section of hello Azure portal.</span></span>
   
    <span data-ttu-id="2eb57-186">c.</span><span class="sxs-lookup"><span data-stu-id="2eb57-186">c.</span></span> <span data-ttu-id="2eb57-187">In Azure-portal op Hallo Hallo **eenmalige aanmelding configureren** venster, kopie Hallo **Sign-Out URL**, en plak deze in Hallo **Omleidings-URL voor afmelden** textbox.</span><span class="sxs-lookup"><span data-stu-id="2eb57-187">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL**, and then paste it into hello **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="2eb57-188">d.</span><span class="sxs-lookup"><span data-stu-id="2eb57-188">d.</span></span>  <span data-ttu-id="2eb57-189">In **omgeving** textbox typenaam van het Hallo-omgeving.</span><span class="sxs-lookup"><span data-stu-id="2eb57-189">In **Environment** textbox, type hello environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="2eb57-190">Hallo waarde van Hallo omgeving kenmerk is gekoppeld toohello waarde van de tenant-URL Hallo:</span><span class="sxs-lookup"><span data-stu-id="2eb57-190">hello value of hello Environment attribute is tied toohello value of hello tenant URL:</span></span>  
    ><span data-ttu-id="2eb57-191">-Als de domeinnaam Hallo van Hallo tenant-URL voor Workday op de bijvoorbeeld met impl begint: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), Hallo **omgeving** kenmerk moet worden ingesteld als tooImplementation.</span><span class="sxs-lookup"><span data-stu-id="2eb57-191">-If hello domain name of hello Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), hello **Environment** attribute must be set tooImplementation.</span></span>  
    ><span data-ttu-id="2eb57-192">-Als de domeinnaam Hallo met iets anders begint, moet u toocontact [Workday Client ondersteuningsteam](https://www.workday.com/en-us/partners-services/services/support.html) tooget Hallo overeenkomende **omgeving** waarde.</span><span class="sxs-lookup"><span data-stu-id="2eb57-192">-If hello domain name starts with something else, you need toocontact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello matching **Environment** value.</span></span>

12. <span data-ttu-id="2eb57-193">In Hallo **SAML Setup** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2eb57-193">In hello **SAML Setup** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="2eb57-194">![Setup van SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span><span class="sxs-lookup"><span data-stu-id="2eb57-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="2eb57-195">a.</span><span class="sxs-lookup"><span data-stu-id="2eb57-195">a.</span></span>  <span data-ttu-id="2eb57-196">Selecteer **SAML-verificatie inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="2eb57-197">b.</span><span class="sxs-lookup"><span data-stu-id="2eb57-197">b.</span></span>  <span data-ttu-id="2eb57-198">Klik op **rij toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="2eb57-199">In Hallo sectie SAML-id-Providers, uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2eb57-199">In hello SAML Identity Providers section, perform hello following steps:</span></span>
   
    <span data-ttu-id="2eb57-200">![SAML-id-Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML-id-Providers")</span><span class="sxs-lookup"><span data-stu-id="2eb57-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="2eb57-201">a.</span><span class="sxs-lookup"><span data-stu-id="2eb57-201">a.</span></span> <span data-ttu-id="2eb57-202">Typ de providernaam van een in Hallo identiteit providernaam textbox (bijvoorbeeld: *SPInitiatedSSO*).</span><span class="sxs-lookup"><span data-stu-id="2eb57-202">In hello Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="2eb57-203">b.</span><span class="sxs-lookup"><span data-stu-id="2eb57-203">b.</span></span> <span data-ttu-id="2eb57-204">In de Azure-portal op Hallo Hallo **eenmalige aanmelding configureren** venster, kopie Hallo **SAML entiteit-ID** waarde en plak deze in Hallo **verlener** textbox.</span><span class="sxs-lookup"><span data-stu-id="2eb57-204">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Entity ID** value, and then paste it into hello **Issuer** textbox.</span></span>
   
    <span data-ttu-id="2eb57-205">c.</span><span class="sxs-lookup"><span data-stu-id="2eb57-205">c.</span></span> <span data-ttu-id="2eb57-206">Selecteer **werkdag geïnitieerd afmelding inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="2eb57-207">d.</span><span class="sxs-lookup"><span data-stu-id="2eb57-207">d.</span></span> <span data-ttu-id="2eb57-208">In Azure-portal op Hallo Hallo **eenmalige aanmelding configureren** venster, kopie Hallo **Sign-Out URL** waarde en plak deze in Hallo **verzoek-URL voor afmelden** textbox.</span><span class="sxs-lookup"><span data-stu-id="2eb57-208">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL** value, and then paste it into hello **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="2eb57-209">e.</span><span class="sxs-lookup"><span data-stu-id="2eb57-209">e.</span></span> <span data-ttu-id="2eb57-210">Klik op **openbare sleutel identiteitscertificaat-Provider**, en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="2eb57-211">![Maak](./media/active-directory-saas-workday-tutorial/IC782928.png "maken")</span><span class="sxs-lookup"><span data-stu-id="2eb57-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="2eb57-212">f.</span><span class="sxs-lookup"><span data-stu-id="2eb57-212">f.</span></span> <span data-ttu-id="2eb57-213">Klik op **x509 maken openbare sleutel**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="2eb57-214">![Maak](./media/active-directory-saas-workday-tutorial/IC782929.png "maken")</span><span class="sxs-lookup"><span data-stu-id="2eb57-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="2eb57-215">In Hallo **weergave x509 openbare sleutel** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2eb57-215">In hello **View x509 Public Key** section, perform hello following steps:</span></span> 
   
    <span data-ttu-id="2eb57-216">![De openbare sleutel weergave x509](./media/active-directory-saas-workday-tutorial/IC782930.png "weergave x509 openbare sleutel")</span><span class="sxs-lookup"><span data-stu-id="2eb57-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="2eb57-217">a.</span><span class="sxs-lookup"><span data-stu-id="2eb57-217">a.</span></span> <span data-ttu-id="2eb57-218">In Hallo **naam** textbox, typ een naam voor uw certificaat (bijvoorbeeld: *Beschermingsmiddel\_SP*).</span><span class="sxs-lookup"><span data-stu-id="2eb57-218">In hello **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="2eb57-219">b.</span><span class="sxs-lookup"><span data-stu-id="2eb57-219">b.</span></span> <span data-ttu-id="2eb57-220">In Hallo **geldig van** textbox type Hallo geldig vanaf kenmerkwaarde van uw certificaat.</span><span class="sxs-lookup"><span data-stu-id="2eb57-220">In hello **Valid From** textbox, type hello valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="2eb57-221">c.</span><span class="sxs-lookup"><span data-stu-id="2eb57-221">c.</span></span>  <span data-ttu-id="2eb57-222">In Hallo **geldig tot** textbox Hallo tooattribute geldige typewaarde van uw certificaat.</span><span class="sxs-lookup"><span data-stu-id="2eb57-222">In hello **Valid To** textbox, type hello valid tooattribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="2eb57-223">U kunt Hallo geldig ophalen uit de datum en Hallo geldig toodate van certificaat Hallo gedownload door erop te dubbelklikken.</span><span class="sxs-lookup"><span data-stu-id="2eb57-223">You can get hello valid from date and hello valid toodate from hello downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="2eb57-224">Hallo datums worden vermeld in Hallo **Details** tabblad.</span><span class="sxs-lookup"><span data-stu-id="2eb57-224">hello dates are listed under hello **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="2eb57-225">d.</span><span class="sxs-lookup"><span data-stu-id="2eb57-225">d.</span></span>  <span data-ttu-id="2eb57-226">Open uw base-64 gecodeerde certificaat in Kladblok en kopiëren Hallo inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="2eb57-226">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   
    <span data-ttu-id="2eb57-227">e.</span><span class="sxs-lookup"><span data-stu-id="2eb57-227">e.</span></span>  <span data-ttu-id="2eb57-228">In Hallo **certificaat** textbox plakken Hallo inhoud van het Klembord.</span><span class="sxs-lookup"><span data-stu-id="2eb57-228">In hello **Certificate** textbox, paste hello content of your clipboard.</span></span>
   
    <span data-ttu-id="2eb57-229">f.</span><span class="sxs-lookup"><span data-stu-id="2eb57-229">f.</span></span>  <span data-ttu-id="2eb57-230">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-230">Click **OK**.</span></span>

15. <span data-ttu-id="2eb57-231">Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2eb57-231">Perform hello following steps:</span></span> 
   
    <span data-ttu-id="2eb57-232">![Configuratie van de SSO-](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO-configuratie")</span><span class="sxs-lookup"><span data-stu-id="2eb57-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="2eb57-233">a.</span><span class="sxs-lookup"><span data-stu-id="2eb57-233">a.</span></span>  <span data-ttu-id="2eb57-234">Hallo inschakelen **x509 persoonlijke sleutelpaar**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-234">Enable hello **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="2eb57-235">b.</span><span class="sxs-lookup"><span data-stu-id="2eb57-235">b.</span></span>  <span data-ttu-id="2eb57-236">In Hallo **Provider-Service-ID** textbox type **http://www.workday.com**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-236">In hello **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="2eb57-237">c.</span><span class="sxs-lookup"><span data-stu-id="2eb57-237">c.</span></span>  <span data-ttu-id="2eb57-238">Selecteer **inschakelen SP geïnitieerd SAML-verificatie**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="2eb57-239">d.</span><span class="sxs-lookup"><span data-stu-id="2eb57-239">d.</span></span>  <span data-ttu-id="2eb57-240">In de Azure-portal op Hallo Hallo **eenmalige aanmelding configureren** venster, kopie Hallo **SAML Single Sign-On Service-URL** waarde en plak deze in Hallo **IdP SSO Service URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="2eb57-240">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="2eb57-241">e.</span><span class="sxs-lookup"><span data-stu-id="2eb57-241">e.</span></span> <span data-ttu-id="2eb57-242">Selecteer **doen Serviceprovider geïnitieerde verificatieaanvraag niet verkleinen**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="2eb57-243">f.</span><span class="sxs-lookup"><span data-stu-id="2eb57-243">f.</span></span> <span data-ttu-id="2eb57-244">Als **aanvragen handtekening verificatiemethode**, selecteer **SHA256**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="2eb57-245">![Handtekening van de verificatiemethode aanvraag](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "verificatiemethode aanvraag handtekening")</span><span class="sxs-lookup"><span data-stu-id="2eb57-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="2eb57-246">g.</span><span class="sxs-lookup"><span data-stu-id="2eb57-246">g.</span></span> <span data-ttu-id="2eb57-247">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="2eb57-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span><span class="sxs-lookup"><span data-stu-id="2eb57-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="2eb57-249">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="2eb57-249">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2eb57-250">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="2eb57-250">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2eb57-251">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2eb57-251">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2eb57-252">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2eb57-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="2eb57-253">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2eb57-253">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2eb57-255">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2eb57-255">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2eb57-256">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2eb57-256">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2eb57-258">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-258">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2eb57-260">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="2eb57-260">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2eb57-262">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2eb57-262">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2eb57-264">a.</span><span class="sxs-lookup"><span data-stu-id="2eb57-264">a.</span></span> <span data-ttu-id="2eb57-265">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-265">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2eb57-266">b.</span><span class="sxs-lookup"><span data-stu-id="2eb57-266">b.</span></span> <span data-ttu-id="2eb57-267">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2eb57-267">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2eb57-268">c.</span><span class="sxs-lookup"><span data-stu-id="2eb57-268">c.</span></span> <span data-ttu-id="2eb57-269">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-269">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2eb57-270">d.</span><span class="sxs-lookup"><span data-stu-id="2eb57-270">d.</span></span> <span data-ttu-id="2eb57-271">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="2eb57-272">Maken van een werkdag testgebruiker</span><span class="sxs-lookup"><span data-stu-id="2eb57-272">Creating a Workday test user</span></span>

<span data-ttu-id="2eb57-273">een testgebruiker ingericht in Workday tooget, moet u toocontact hello [Workday Client ondersteuningsteam](https://www.workday.com/en-us/partners-services/services/support.html).</span><span class="sxs-lookup"><span data-stu-id="2eb57-273">tooget a test user provisioned into Workday, you need toocontact hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="2eb57-274">Hallo [Workday Client ondersteuningsteam](https://www.workday.com/en-us/partners-services/services/support.html) Hallo gebruiker voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2eb57-274">hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates hello user for you.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2eb57-275">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2eb57-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2eb57-276">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooWorkday toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="2eb57-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkday.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2eb57-278">**tooassign Britta Simon tooWorkday, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2eb57-278">**tooassign Britta Simon tooWorkday, perform hello following steps:**</span></span>

1. <span data-ttu-id="2eb57-279">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2eb57-281">Selecteer in de lijst met de toepassingen van Hallo **Workday**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-281">In hello applications list, select **Workday**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="2eb57-283">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2eb57-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2eb57-285">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2eb57-285">Click **Add** button.</span></span> <span data-ttu-id="2eb57-286">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2eb57-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2eb57-288">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="2eb57-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2eb57-289">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2eb57-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2eb57-290">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2eb57-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2eb57-291">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2eb57-291">Testing single sign-on</span></span>

<span data-ttu-id="2eb57-292">Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="2eb57-292">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="2eb57-293">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2eb57-293">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2eb57-294">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2eb57-294">Additional resources</span></span>

* [<span data-ttu-id="2eb57-295">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2eb57-295">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2eb57-296">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2eb57-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="2eb57-297">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="2eb57-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

