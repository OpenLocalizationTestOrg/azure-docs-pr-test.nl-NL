---
title: 'Zelfstudie: Azure Active Directory-integratie met HireVue | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en HireVue.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aadfc342-14db-4d74-a83d-f0c76f0cf63c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f890633ee4f13919c32a43d7b6cf30f2270ef6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hirevue"></a><span data-ttu-id="a2d3b-103">Zelfstudie: Azure Active Directory-integratie met HireVue</span><span class="sxs-lookup"><span data-stu-id="a2d3b-103">Tutorial: Azure Active Directory integration with HireVue</span></span>

<span data-ttu-id="a2d3b-104">In deze zelfstudie leert u hoe toointegrate HireVue met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2d3b-104">In this tutorial, you learn how toointegrate HireVue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2d3b-105">HireVue integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a2d3b-105">Integrating HireVue with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a2d3b-106">U kunt beheren in Azure AD die tooHireVue toegang heeft</span><span class="sxs-lookup"><span data-stu-id="a2d3b-106">You can control in Azure AD who has access tooHireVue</span></span>
- <span data-ttu-id="a2d3b-107">U kunt uw gebruikers tooautomatically get aangemelde tooHireVue (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="a2d3b-107">You can enable your users tooautomatically get signed-on tooHireVue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2d3b-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a2d3b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a2d3b-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a2d3b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2d3b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a2d3b-110">Prerequisites</span></span>

<span data-ttu-id="a2d3b-111">Azure AD-integratie met HireVue tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="a2d3b-111">tooconfigure Azure AD integration with HireVue, you need hello following items:</span></span>

- <span data-ttu-id="a2d3b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a2d3b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2d3b-113">Een HireVue eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a2d3b-113">A HireVue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2d3b-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2d3b-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a2d3b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2d3b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2d3b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2d3b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2d3b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a2d3b-118">Scenario description</span></span>
<span data-ttu-id="a2d3b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2d3b-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a2d3b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2d3b-121">Het toevoegen van HireVue van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a2d3b-121">Adding HireVue from hello gallery</span></span>
2. <span data-ttu-id="a2d3b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a2d3b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hirevue-from-hello-gallery"></a><span data-ttu-id="a2d3b-123">Het toevoegen van HireVue van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a2d3b-123">Adding HireVue from hello gallery</span></span>
<span data-ttu-id="a2d3b-124">tooconfigure hello integratie van HireVue in Azure AD, moet u tooadd HireVue uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-124">tooconfigure hello integration of HireVue into Azure AD, you need tooadd HireVue from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a2d3b-125">**tooadd HireVue via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a2d3b-125">**tooadd HireVue from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2d3b-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a2d3b-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a2d3b-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a2d3b-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a2d3b-133">Typ in het zoekvak Hallo **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-133">In hello search box, type **HireVue**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_search.png)

5. <span data-ttu-id="a2d3b-135">Selecteer in het deelvenster resultaten hello, **HireVue**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-135">In hello results panel, select **HireVue**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2d3b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a2d3b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a2d3b-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met HireVue op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-138">In this section, you configure and test Azure AD single sign-on with HireVue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a2d3b-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in HireVue is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HireVue is tooa user in Azure AD.</span></span> <span data-ttu-id="a2d3b-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in HireVue toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-140">In other words, a link relationship between an Azure AD user and hello related user in HireVue needs toobe established.</span></span>

<span data-ttu-id="a2d3b-141">Wijs in HireVue, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-141">In HireVue, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a2d3b-142">tooconfigure en eenmalige aanmelding Azure AD-test met HireVue, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a2d3b-142">tooconfigure and test Azure AD single sign-on with HireVue, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a2d3b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a2d3b-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2d3b-145">**[Maken van een testgebruiker HireVue](#creating-a-hirevue-test-user)**  -toohave een equivalent van Britta Simon in HireVue die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-145">**[Creating a HireVue test user](#creating-a-hirevue-test-user)** - toohave a counterpart of Britta Simon in HireVue that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2d3b-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2d3b-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2d3b-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a2d3b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2d3b-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing HireVue configureren.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HireVue application.</span></span>

<span data-ttu-id="a2d3b-150">**Azure AD tooconfigure eenmalige aanmelding met HireVue, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a2d3b-150">**tooconfigure Azure AD single sign-on with HireVue, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2d3b-151">In de Azure-portal op Hallo Hallo **HireVue** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-151">In hello Azure portal, on hello **HireVue** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a2d3b-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_samlbase.png)

3. <span data-ttu-id="a2d3b-155">Op Hallo **HireVue domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a2d3b-155">On hello **HireVue Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_url.png)

    <span data-ttu-id="a2d3b-157">a.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-157">a.</span></span> <span data-ttu-id="a2d3b-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="a2d3b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>

    | <span data-ttu-id="a2d3b-159">Omgeving</span><span class="sxs-lookup"><span data-stu-id="a2d3b-159">Environment</span></span> | <span data-ttu-id="a2d3b-160">URL</span><span class="sxs-lookup"><span data-stu-id="a2d3b-160">URL</span></span> |
    |-------------|---|
    | <span data-ttu-id="a2d3b-161">Productie</span><span class="sxs-lookup"><span data-stu-id="a2d3b-161">Production</span></span> | `https://<companyname>.hirevue.com` |
    | <span data-ttu-id="a2d3b-162">Fasering</span><span class="sxs-lookup"><span data-stu-id="a2d3b-162">Staging</span></span>    | `https://<companyname>.stghv.com` |
    
    <span data-ttu-id="a2d3b-163">b.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-163">b.</span></span> <span data-ttu-id="a2d3b-164">In Hallo **id** textbox, typ een URL als:</span><span class="sxs-lookup"><span data-stu-id="a2d3b-164">In hello **Identifier** textbox, type a URL as:</span></span>
    
    | <span data-ttu-id="a2d3b-165">Omgeving</span><span class="sxs-lookup"><span data-stu-id="a2d3b-165">Environment</span></span> | <span data-ttu-id="a2d3b-166">URN</span><span class="sxs-lookup"><span data-stu-id="a2d3b-166">URN</span></span> |
    |-------------|-----|
    | <span data-ttu-id="a2d3b-167">Productie</span><span class="sxs-lookup"><span data-stu-id="a2d3b-167">Production</span></span> |`urn:federation:hirevue.com:saml:sp:prod` |
    | <span data-ttu-id="a2d3b-168">Fasering</span><span class="sxs-lookup"><span data-stu-id="a2d3b-168">Staging</span></span>    | `urn:federation:hirevue.com:saml:sp:staging`|
    
    > [!NOTE] 
    > <span data-ttu-id="a2d3b-169">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-169">These values are not real.</span></span> <span data-ttu-id="a2d3b-170">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-170">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a2d3b-171">Neem contact op met [HireVue Client ondersteuningsteam](mailto:samlsupport@hirevue.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-171">Contact [HireVue Client support team](mailto:samlsupport@hirevue.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="a2d3b-172">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-172">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_certificate.png) 

5. <span data-ttu-id="a2d3b-174">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-174">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hirevue-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a2d3b-176">Op Hallo **HireVue configuratie** sectie, klikt u op **configureren HireVue** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-176">On hello **HireVue Configuration** section, click **Configure HireVue** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a2d3b-177">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="a2d3b-177">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_configure.png) 

7. <span data-ttu-id="a2d3b-179">tooconfigure eenmalige aanmelding op **HireVue** zijde, moet u toosend Hallo gedownload **Certificate(Base64)** en **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** te[HireVue ondersteuningsteam](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="a2d3b-179">tooconfigure single sign-on on **HireVue** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[HireVue support team](mailto:samlsupport@hirevue.com).</span></span> <span data-ttu-id="a2d3b-180">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-180">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a2d3b-181">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a2d3b-182">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a2d3b-183">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a2d3b-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2d3b-184">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a2d3b-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="a2d3b-185">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a2d3b-187">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a2d3b-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2d3b-188">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hirevue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2d3b-190">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hirevue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2d3b-192">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hirevue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2d3b-194">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a2d3b-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hirevue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2d3b-196">a.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-196">a.</span></span> <span data-ttu-id="a2d3b-197">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2d3b-198">b.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-198">b.</span></span> <span data-ttu-id="a2d3b-199">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a2d3b-200">c.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-200">c.</span></span> <span data-ttu-id="a2d3b-201">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a2d3b-202">d.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-202">d.</span></span> <span data-ttu-id="a2d3b-203">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-203">Click **Create**.</span></span>
 
### <a name="creating-a-hirevue-test-user"></a><span data-ttu-id="a2d3b-204">Een testgebruiker HireVue maken</span><span class="sxs-lookup"><span data-stu-id="a2d3b-204">Creating a HireVue test user</span></span>

<span data-ttu-id="a2d3b-205">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in HireVue maken.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-205">In this section, you create a user called Britta Simon in HireVue.</span></span> <span data-ttu-id="a2d3b-206">Neem contact op met [HireVue ondersteuningsteam](mailto:samlsupport@hirevue.com) tooadd Hallo gebruikers in Hallo HireVue platform.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-206">Please work with [HireVue support team](mailto:samlsupport@hirevue.com) tooadd hello users in hello HireVue platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a2d3b-207">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2d3b-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a2d3b-208">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooHireVue toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHireVue.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a2d3b-210">**tooassign Britta Simon tooHireVue, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a2d3b-210">**tooassign Britta Simon tooHireVue, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2d3b-211">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a2d3b-213">Selecteer in de lijst met de toepassingen van Hallo **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-213">In hello applications list, select **HireVue**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_app.png) 

3. <span data-ttu-id="a2d3b-215">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a2d3b-217">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-217">Click **Add** button.</span></span> <span data-ttu-id="a2d3b-218">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a2d3b-220">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a2d3b-221">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2d3b-222">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2d3b-223">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a2d3b-223">Testing single sign-on</span></span>

<span data-ttu-id="a2d3b-224">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a2d3b-225">Als u op Hallo HireVue tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour HireVue toepassing.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-225">When you click hello HireVue tile in hello Access Panel, you should get automatically signed-on tooyour HireVue application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a2d3b-226">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a2d3b-226">Additional resources</span></span>

* [<span data-ttu-id="a2d3b-227">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2d3b-227">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2d3b-228">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a2d3b-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_203.png

