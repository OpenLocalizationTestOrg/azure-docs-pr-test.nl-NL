---
title: 'Zelfstudie: Azure Active Directory-integratie met Intacct | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Intacct.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="f8163-103">Zelfstudie: Azure Active Directory-integratie met Intacct</span><span class="sxs-lookup"><span data-stu-id="f8163-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="f8163-104">In deze zelfstudie leert u hoe toointegrate Intacct met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f8163-104">In this tutorial, you learn how toointegrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f8163-105">Intacct integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f8163-105">Integrating Intacct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f8163-106">U kunt beheren in Azure AD die tooIntacct toegang heeft</span><span class="sxs-lookup"><span data-stu-id="f8163-106">You can control in Azure AD who has access tooIntacct</span></span>
- <span data-ttu-id="f8163-107">U kunt uw gebruikers tooautomatically get aangemelde tooIntacct (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f8163-107">You can enable your users tooautomatically get signed-on tooIntacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f8163-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f8163-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f8163-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f8163-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8163-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f8163-110">Prerequisites</span></span>

<span data-ttu-id="f8163-111">Azure AD-integratie met Intacct tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="f8163-111">tooconfigure Azure AD integration with Intacct, you need hello following items:</span></span>

- <span data-ttu-id="f8163-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f8163-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f8163-113">Een Intacct eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f8163-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f8163-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f8163-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f8163-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f8163-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f8163-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f8163-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f8163-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f8163-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f8163-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f8163-118">Scenario description</span></span>
<span data-ttu-id="f8163-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f8163-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f8163-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f8163-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f8163-121">Het toevoegen van Intacct van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f8163-121">Adding Intacct from hello gallery</span></span>
2. <span data-ttu-id="f8163-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f8163-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-hello-gallery"></a><span data-ttu-id="f8163-123">Het toevoegen van Intacct van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f8163-123">Adding Intacct from hello gallery</span></span>
<span data-ttu-id="f8163-124">tooconfigure hello integratie van Intacct in Azure AD, moet u tooadd Intacct uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f8163-124">tooconfigure hello integration of Intacct into Azure AD, you need tooadd Intacct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f8163-125">**tooadd Intacct via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f8163-125">**tooadd Intacct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8163-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f8163-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f8163-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f8163-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f8163-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f8163-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f8163-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f8163-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f8163-133">Typ in het zoekvak Hallo **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="f8163-133">In hello search box, type **Intacct**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="f8163-135">Selecteer in het deelvenster resultaten hello, **Intacct**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f8163-135">In hello results panel, select **Intacct**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f8163-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f8163-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f8163-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Intacct op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f8163-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f8163-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Intacct is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8163-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intacct is tooa user in Azure AD.</span></span> <span data-ttu-id="f8163-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Intacct toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="f8163-140">In other words, a link relationship between an Azure AD user and hello related user in Intacct needs toobe established.</span></span>

<span data-ttu-id="f8163-141">Wijs in Intacct, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="f8163-141">In Intacct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f8163-142">tooconfigure en eenmalige aanmelding Azure AD-test met Intacct, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f8163-142">tooconfigure and test Azure AD single sign-on with Intacct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f8163-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="f8163-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f8163-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8163-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f8163-145">**[Maken van een testgebruiker Intacct](#creating-an-intacct-test-user)**  -toohave een equivalent van Britta Simon in Intacct die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f8163-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - toohave a counterpart of Britta Simon in Intacct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f8163-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f8163-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f8163-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f8163-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f8163-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f8163-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f8163-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Intacct configureren.</span><span class="sxs-lookup"><span data-stu-id="f8163-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="f8163-150">**Azure AD tooconfigure eenmalige aanmelding met Intacct, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f8163-150">**tooconfigure Azure AD single sign-on with Intacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8163-151">In de Azure-portal op Hallo Hallo **Intacct** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f8163-151">In hello Azure portal, on hello **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f8163-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f8163-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="f8163-155">Op Hallo **Intacct domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f8163-155">On hello **Intacct Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="f8163-157">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="f8163-157">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="f8163-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="f8163-158">This value is not real.</span></span> <span data-ttu-id="f8163-159">Deze waarde met de werkelijke antwoord-URL Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="f8163-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="f8163-160">Neem contact op met [Intacct ondersteuningsteam](https://us.intacct.com/support) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="f8163-160">Contact [Intacct support team](https://us.intacct.com/support) tooget this value.</span></span>

4. <span data-ttu-id="f8163-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f8163-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="f8163-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f8163-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f8163-165">Op Hallo **Intacct configuratie** sectie, klikt u op **configureren Intacct** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f8163-165">On hello **Intacct Configuration** section, click **Configure Intacct** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f8163-166">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="f8163-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="f8163-168">Meld u tooyour Intacct bedrijf site als een beheerder in een ander browservenster.</span><span class="sxs-lookup"><span data-stu-id="f8163-168">In a different web browser window, sign in tooyour Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="f8163-169">Klik op Hallo **bedrijf** tabblad en klik vervolgens op **bedrijfsgegevens**.</span><span class="sxs-lookup"><span data-stu-id="f8163-169">Click hello **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="f8163-170">![Bedrijf](./media/active-directory-saas-intacct-tutorial/ic790037.png "bedrijf")</span><span class="sxs-lookup"><span data-stu-id="f8163-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="f8163-171">Klik op Hallo **beveiliging** tabblad en klik vervolgens op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="f8163-171">Click hello **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="f8163-172">![Beveiliging](./media/active-directory-saas-intacct-tutorial/ic790038.png "beveiliging")</span><span class="sxs-lookup"><span data-stu-id="f8163-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="f8163-173">In Hallo **eenmalige aanmelding (SSO)** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f8163-173">In hello **Single sign on (SSO)** section, perform hello following steps:</span></span>

    <span data-ttu-id="f8163-174">![Eenmalige aanmelding](./media/active-directory-saas-intacct-tutorial/ic790039.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="f8163-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="f8163-175">a.</span><span class="sxs-lookup"><span data-stu-id="f8163-175">a.</span></span> <span data-ttu-id="f8163-176">Selecteer **eenmalige aanmelding inschakelen op**.</span><span class="sxs-lookup"><span data-stu-id="f8163-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="f8163-177">b.</span><span class="sxs-lookup"><span data-stu-id="f8163-177">b.</span></span> <span data-ttu-id="f8163-178">Als **identiteit providertype**, selecteer **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="f8163-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="f8163-179">c.</span><span class="sxs-lookup"><span data-stu-id="f8163-179">c.</span></span> <span data-ttu-id="f8163-180">In **URL-verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f8163-180">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f8163-181">d.</span><span class="sxs-lookup"><span data-stu-id="f8163-181">d.</span></span> <span data-ttu-id="f8163-182">In **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f8163-182">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f8163-183">e.</span><span class="sxs-lookup"><span data-stu-id="f8163-183">e.</span></span> <span data-ttu-id="f8163-184">Open uw **base 64-** gecodeerd certificaat in Kladblok en kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **certificaat** vak.</span><span class="sxs-lookup"><span data-stu-id="f8163-184">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** box.</span></span>
   
    <span data-ttu-id="f8163-185">f.</span><span class="sxs-lookup"><span data-stu-id="f8163-185">f.</span></span> <span data-ttu-id="f8163-186">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f8163-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f8163-187">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="f8163-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f8163-188">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="f8163-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f8163-189">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f8163-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f8163-190">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f8163-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="f8163-191">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f8163-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f8163-193">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f8163-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8163-194">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f8163-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f8163-196">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f8163-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f8163-198">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f8163-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f8163-200">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f8163-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f8163-202">a.</span><span class="sxs-lookup"><span data-stu-id="f8163-202">a.</span></span> <span data-ttu-id="f8163-203">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f8163-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f8163-204">b.</span><span class="sxs-lookup"><span data-stu-id="f8163-204">b.</span></span> <span data-ttu-id="f8163-205">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f8163-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f8163-206">c.</span><span class="sxs-lookup"><span data-stu-id="f8163-206">c.</span></span> <span data-ttu-id="f8163-207">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f8163-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f8163-208">d.</span><span class="sxs-lookup"><span data-stu-id="f8163-208">d.</span></span> <span data-ttu-id="f8163-209">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f8163-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="f8163-210">Een testgebruiker Intacct maken</span><span class="sxs-lookup"><span data-stu-id="f8163-210">Creating an Intacct test user</span></span>

<span data-ttu-id="f8163-211">tooset van Azure AD-gebruikers zodat ze kunnen zich in tooIntacct, deze moeten worden ingericht in Intacct.</span><span class="sxs-lookup"><span data-stu-id="f8163-211">tooset up Azure AD users so they can sign in tooIntacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="f8163-212">Voor Intacct is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="f8163-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="f8163-213">**tooprovision gebruikersaccounts, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f8163-213">**tooprovision user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8163-214">Meld u aan tooyour **Intacct** tenant.</span><span class="sxs-lookup"><span data-stu-id="f8163-214">Sign in tooyour **Intacct** tenant.</span></span>

2. <span data-ttu-id="f8163-215">Klik op Hallo **bedrijf** tabblad en klik vervolgens op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f8163-215">Click hello **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="f8163-216">![Gebruikers](./media/active-directory-saas-intacct-tutorial/ic790041.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="f8163-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="f8163-217">Klik op Hallo **toevoegen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f8163-217">Click hello **Add** tab.</span></span>

    <span data-ttu-id="f8163-218">![Voeg](./media/active-directory-saas-intacct-tutorial/ic790042.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="f8163-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="f8163-219">In Hallo **gebruikersgegevens** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f8163-219">In hello **User Information** section, perform hello following steps:</span></span>

    <span data-ttu-id="f8163-220">![Gebruikersgegevens](./media/active-directory-saas-intacct-tutorial/ic790043.png "gebruikersgegevens")</span><span class="sxs-lookup"><span data-stu-id="f8163-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="f8163-221">a.</span><span class="sxs-lookup"><span data-stu-id="f8163-221">a.</span></span> <span data-ttu-id="f8163-222">Voer Hallo **gebruikers-ID**, Hallo **achternaam**, **voornaam**, Hallo **e-mailadres**, Hallo **titel**, en Hallo **Phone** van een Azure AD-account dat u wilt dat tooprovision in Hallo **gebruikersgegevens** sectie.</span><span class="sxs-lookup"><span data-stu-id="f8163-222">Enter hello **User ID**, hello **Last name**, **First name**, hello **Email address**, hello **Title**, and hello **Phone** of an Azure AD account that you want tooprovision into hello **User Information** section.</span></span>

    <span data-ttu-id="f8163-223">b.</span><span class="sxs-lookup"><span data-stu-id="f8163-223">b.</span></span> <span data-ttu-id="f8163-224">Selecteer Hallo **beheerdersbevoegdheden** van een Azure AD-account dat u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="f8163-224">Select hello **Admin privileges** of an Azure AD account that you want tooprovision.</span></span>
   
    <span data-ttu-id="f8163-225">c.</span><span class="sxs-lookup"><span data-stu-id="f8163-225">c.</span></span> <span data-ttu-id="f8163-226">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f8163-226">Click **Save**.</span></span> <span data-ttu-id="f8163-227">Hello Azure AD-accounthouder ontvangt een e-mailbericht en een koppeling tooconfirm volgt hun account voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="f8163-227">hello Azure AD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="f8163-228">gebruikersaccounts voor tooprovision Azure AD, kunt u andere hulpprogramma's voor Intacct gebruiker-account maken of API's die worden geleverd door Intacct.</span><span class="sxs-lookup"><span data-stu-id="f8163-228">tooprovision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f8163-229">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8163-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f8163-230">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooIntacct toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="f8163-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntacct.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f8163-232">**tooassign Britta Simon tooIntacct, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f8163-232">**tooassign Britta Simon tooIntacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8163-233">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f8163-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f8163-235">Selecteer in de lijst met de toepassingen van Hallo **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="f8163-235">In hello applications list, select **Intacct**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="f8163-237">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f8163-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f8163-239">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f8163-239">Click **Add** button.</span></span> <span data-ttu-id="f8163-240">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f8163-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f8163-242">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="f8163-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f8163-243">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f8163-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f8163-244">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f8163-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f8163-245">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f8163-245">Testing single sign-on</span></span>

<span data-ttu-id="f8163-246">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie testen met behulp van Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="f8163-246">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="f8163-247">Wanneer u Hallo Intacct tegel in Hallo toegangsvenster klikt, moet u tooyour Intacct toepassing automatisch worden aangemeld.</span><span class="sxs-lookup"><span data-stu-id="f8163-247">When you click hello Intacct tile in hello Access Panel, you should be automatically signed in tooyour Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f8163-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f8163-248">Additional resources</span></span>

* [<span data-ttu-id="f8163-249">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8163-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f8163-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f8163-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

