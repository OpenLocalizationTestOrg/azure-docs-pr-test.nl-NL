---
title: 'Zelfstudie: Azure Active Directory-integratie met OpsGenie | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en OpsGenie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 50d31c234fb9716d05d681b9bc4164740a3a662b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="eefd3-103">Zelfstudie: Azure Active Directory-integratie met OpsGenie</span><span class="sxs-lookup"><span data-stu-id="eefd3-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>

<span data-ttu-id="eefd3-104">In deze zelfstudie leert u hoe toointegrate OpsGenie met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eefd3-104">In this tutorial, you learn how toointegrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eefd3-105">OpsGenie integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="eefd3-105">Integrating OpsGenie with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eefd3-106">U kunt beheren in Azure AD die tooOpsGenie toegang heeft</span><span class="sxs-lookup"><span data-stu-id="eefd3-106">You can control in Azure AD who has access tooOpsGenie</span></span>
- <span data-ttu-id="eefd3-107">U kunt uw gebruikers tooautomatically get aangemelde tooOpsGenie (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="eefd3-107">You can enable your users tooautomatically get signed-on tooOpsGenie (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eefd3-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="eefd3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eefd3-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eefd3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eefd3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="eefd3-110">Prerequisites</span></span>

<span data-ttu-id="eefd3-111">Azure AD-integratie met OpsGenie tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="eefd3-111">tooconfigure Azure AD integration with OpsGenie, you need hello following items:</span></span>

- <span data-ttu-id="eefd3-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="eefd3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eefd3-113">Een OpsGenie eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="eefd3-113">A OpsGenie single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eefd3-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="eefd3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eefd3-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="eefd3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eefd3-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="eefd3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eefd3-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eefd3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eefd3-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="eefd3-118">Scenario description</span></span>
<span data-ttu-id="eefd3-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="eefd3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eefd3-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="eefd3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eefd3-121">Het toevoegen van OpsGenie van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="eefd3-121">Adding OpsGenie from hello gallery</span></span>
2. <span data-ttu-id="eefd3-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="eefd3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opsgenie-from-hello-gallery"></a><span data-ttu-id="eefd3-123">Het toevoegen van OpsGenie van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="eefd3-123">Adding OpsGenie from hello gallery</span></span>
<span data-ttu-id="eefd3-124">tooconfigure hello integratie van OpsGenie in Azure AD, moet u tooadd OpsGenie uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="eefd3-124">tooconfigure hello integration of OpsGenie into Azure AD, you need tooadd OpsGenie from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eefd3-125">**tooadd OpsGenie via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="eefd3-125">**tooadd OpsGenie from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eefd3-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="eefd3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eefd3-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eefd3-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="eefd3-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eefd3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="eefd3-133">Typ in het zoekvak Hallo **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-133">In hello search box, type **OpsGenie**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. <span data-ttu-id="eefd3-135">Selecteer in het deelvenster resultaten hello, **OpsGenie**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="eefd3-135">In hello results panel, select **OpsGenie**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eefd3-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="eefd3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eefd3-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met OpsGenie op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="eefd3-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eefd3-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in OpsGenie is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eefd3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OpsGenie is tooa user in Azure AD.</span></span> <span data-ttu-id="eefd3-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in OpsGenie toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="eefd3-140">In other words, a link relationship between an Azure AD user and hello related user in OpsGenie needs toobe established.</span></span>

<span data-ttu-id="eefd3-141">Wijs in OpsGenie, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="eefd3-141">In OpsGenie, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eefd3-142">tooconfigure en eenmalige aanmelding Azure AD-test met OpsGenie, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="eefd3-142">tooconfigure and test Azure AD single sign-on with OpsGenie, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eefd3-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="eefd3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eefd3-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eefd3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eefd3-145">**[Maken van een testgebruiker OpsGenie](#creating-a-opsgenie-test-user)**  -toohave een equivalent van Britta Simon in OpsGenie die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="eefd3-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - toohave a counterpart of Britta Simon in OpsGenie that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eefd3-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="eefd3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eefd3-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="eefd3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eefd3-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="eefd3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eefd3-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing OpsGenie configureren.</span><span class="sxs-lookup"><span data-stu-id="eefd3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OpsGenie application.</span></span>

<span data-ttu-id="eefd3-150">**Azure AD tooconfigure eenmalige aanmelding met OpsGenie, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="eefd3-150">**tooconfigure Azure AD single sign-on with OpsGenie, perform hello following steps:**</span></span>

1. <span data-ttu-id="eefd3-151">In de Azure-portal op Hallo Hallo **OpsGenie** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-151">In hello Azure portal, on hello **OpsGenie** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="eefd3-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="eefd3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. <span data-ttu-id="eefd3-155">Op Hallo **OpsGenie domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="eefd3-155">On hello **OpsGenie Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    <span data-ttu-id="eefd3-157">In Hallo **aanmeldings-URL** textbox type Hallo URL:`https://app.opsgenie.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="eefd3-157">In hello **Sign-on URL** textbox, type hello URL: `https://app.opsgenie.com/auth/login`</span></span>

4. <span data-ttu-id="eefd3-158">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="eefd3-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. <span data-ttu-id="eefd3-160">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="eefd3-160">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eefd3-162">Op Hallo **OpsGenie configuratie** sectie, klikt u op **configureren OpsGenie** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="eefd3-162">On hello **OpsGenie Configuration** section, click **Configure OpsGenie** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eefd3-163">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="eefd3-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. <span data-ttu-id="eefd3-165">Open een ander browserexemplaar, en vervolgens aanmelden tooOpsGenie als beheerder.</span><span class="sxs-lookup"><span data-stu-id="eefd3-165">Open another browser instance, and then log-in tooOpsGenie as an administrator.</span></span>

8. <span data-ttu-id="eefd3-166">Klik op **instellingen**, en klik vervolgens op Hallo **eenmalige aanmelding** tabblad.</span><span class="sxs-lookup"><span data-stu-id="eefd3-166">Click **Settings**, and then click hello **Single Sign On** tab.</span></span>
   
    ![OpsGenie voor eenmalige aanmelding](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. <span data-ttu-id="eefd3-168">tooenable SSO, selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-168">tooenable SSO, select **Enabled**.</span></span>
   
    ![OpsGenie instellingen](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. <span data-ttu-id="eefd3-170">In Hallo **Provider** sectie, klikt u op Hallo **Azure Active Directory** tabblad.</span><span class="sxs-lookup"><span data-stu-id="eefd3-170">In hello **Provider** section, click hello **Azure Active Directory** tab.</span></span>
   
    ![OpsGenie instellingen](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. <span data-ttu-id="eefd3-172">Voer op Hallo Azure Active Directory dialoogvenster pagina Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="eefd3-172">On hello Azure Active Directory dialog page, perform hello following steps:</span></span>
   
    ![OpsGenie instellingen](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    <span data-ttu-id="eefd3-174">a.</span><span class="sxs-lookup"><span data-stu-id="eefd3-174">a.</span></span> <span data-ttu-id="eefd3-175">Plakken **aanmelding op Service-URL met eenmalige**, die u hebt gekopieerd uit hello Azure-portal in Hallo **SAML 2.0 eindpunt** textbox.</span><span class="sxs-lookup"><span data-stu-id="eefd3-175">Paste **Single Sign On Service URL**, which you have copied from hello Azure portal into hello **SAML 2.0 Endpoint** textbox.</span></span>
    
    <span data-ttu-id="eefd3-176">b.</span><span class="sxs-lookup"><span data-stu-id="eefd3-176">b.</span></span> <span data-ttu-id="eefd3-177">De gedownloade base-64 gecodeerde certificaat Open in Kladblok en kopieer Hallo inhoud ervan naar het Klembord en plak deze in Hallo **X.500 certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="eefd3-177">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **X.500 Certificate** textbox.</span></span>
    
    <span data-ttu-id="eefd3-178">c.</span><span class="sxs-lookup"><span data-stu-id="eefd3-178">c.</span></span> <span data-ttu-id="eefd3-179">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-179">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="eefd3-180">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="eefd3-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eefd3-181">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="eefd3-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eefd3-182">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eefd3-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eefd3-183">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="eefd3-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="eefd3-184">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="eefd3-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="eefd3-186">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="eefd3-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eefd3-187">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="eefd3-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eefd3-189">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eefd3-191">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="eefd3-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eefd3-193">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="eefd3-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eefd3-195">a.</span><span class="sxs-lookup"><span data-stu-id="eefd3-195">a.</span></span> <span data-ttu-id="eefd3-196">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eefd3-197">b.</span><span class="sxs-lookup"><span data-stu-id="eefd3-197">b.</span></span> <span data-ttu-id="eefd3-198">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eefd3-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eefd3-199">c.</span><span class="sxs-lookup"><span data-stu-id="eefd3-199">c.</span></span> <span data-ttu-id="eefd3-200">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eefd3-201">d.</span><span class="sxs-lookup"><span data-stu-id="eefd3-201">d.</span></span> <span data-ttu-id="eefd3-202">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-202">Click **Create**.</span></span>
 
### <a name="creating-a-opsgenie-test-user"></a><span data-ttu-id="eefd3-203">Een testgebruiker OpsGenie maken</span><span class="sxs-lookup"><span data-stu-id="eefd3-203">Creating a OpsGenie test user</span></span>

<span data-ttu-id="eefd3-204">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in OpsGenie van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="eefd3-204">hello objective of this section is toocreate a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="eefd3-205">Meld u aan bij uw tenant OpsGenie als een beheerder in een browservenster.</span><span class="sxs-lookup"><span data-stu-id="eefd3-205">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>

2. <span data-ttu-id="eefd3-206">Navigeer tooUsers lijst door te klikken op **gebruiker** in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="eefd3-206">Navigate tooUsers list by clicking **User** in left panel.</span></span>
   
   ![OpsGenie instellingen](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. <span data-ttu-id="eefd3-208">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-208">Click **Add User**.</span></span>

4. <span data-ttu-id="eefd3-209">Op Hallo **gebruiker toevoegen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="eefd3-209">On hello **Add User** dialog, perform hello following steps:</span></span>
   
   ![OpsGenie instellingen](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   <span data-ttu-id="eefd3-211">a.</span><span class="sxs-lookup"><span data-stu-id="eefd3-211">a.</span></span> <span data-ttu-id="eefd3-212">In Hallo **e** textbox type Hallo e-mailadres van BrittaSimon behandeld in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eefd3-212">In hello **Email** textbox, type hello email address of BrittaSimon addressed in Azure Active Directory.</span></span>
   
   <span data-ttu-id="eefd3-213">b.</span><span class="sxs-lookup"><span data-stu-id="eefd3-213">b.</span></span> <span data-ttu-id="eefd3-214">In Hallo **volledige naam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-214">In hello **Full Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="eefd3-215">c.</span><span class="sxs-lookup"><span data-stu-id="eefd3-215">c.</span></span> <span data-ttu-id="eefd3-216">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-216">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="eefd3-217">Britta Hiermee haalt u een e-mailbericht met instructies voor het instellen van haar profiel.</span><span class="sxs-lookup"><span data-stu-id="eefd3-217">Britta gets an email with instructions for setting up her profile.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eefd3-218">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="eefd3-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eefd3-219">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooOpsGenie toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="eefd3-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOpsGenie.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="eefd3-221">**tooassign Britta Simon tooOpsGenie, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="eefd3-221">**tooassign Britta Simon tooOpsGenie, perform hello following steps:**</span></span>

1. <span data-ttu-id="eefd3-222">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="eefd3-224">Selecteer in de lijst met de toepassingen van Hallo **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-224">In hello applications list, select **OpsGenie**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. <span data-ttu-id="eefd3-226">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="eefd3-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="eefd3-228">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="eefd3-228">Click **Add** button.</span></span> <span data-ttu-id="eefd3-229">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eefd3-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="eefd3-231">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="eefd3-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eefd3-232">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eefd3-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eefd3-233">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eefd3-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eefd3-234">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="eefd3-234">Testing single sign-on</span></span>

<span data-ttu-id="eefd3-235">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="eefd3-235">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="eefd3-236">Als u op Hallo OpsGenie tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour OpsGenie toepassing.</span><span class="sxs-lookup"><span data-stu-id="eefd3-236">When you click hello OpsGenie tile in hello Access Panel, you should get automatically signed-on tooyour OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eefd3-237">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="eefd3-237">Additional resources</span></span>

* [<span data-ttu-id="eefd3-238">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eefd3-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eefd3-239">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eefd3-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

