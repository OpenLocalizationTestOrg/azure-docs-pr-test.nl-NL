---
title: 'Zelfstudie: Azure Active Directory-integratie met SuccessFactors | Microsoft Docs'
description: Lees hoe toouse SuccessFactors met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="535ff-103">Zelfstudie: Azure Active Directory-integratie met SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="535ff-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="535ff-104">Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate SuccessFactors met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="535ff-104">hello objective of this tutorial is tooshow you how toointegrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="535ff-105">SuccessFactors integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="535ff-105">Integrating SuccessFactors with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="535ff-106">U kunt beheren in Azure AD die tooSuccessFactors toegang heeft</span><span class="sxs-lookup"><span data-stu-id="535ff-106">You can control in Azure AD who has access tooSuccessFactors</span></span>
* <span data-ttu-id="535ff-107">U kunt uw gebruikers tooautomatically get aangemelde tooSuccessFactors (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="535ff-107">You can enable your users tooautomatically get signed-on tooSuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="535ff-108">U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="535ff-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="535ff-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="535ff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="535ff-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="535ff-110">Prerequisites</span></span>
<span data-ttu-id="535ff-111">Azure AD-integratie met SuccessFactors tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="535ff-111">tooconfigure Azure AD integration with SuccessFactors, you need hello following items:</span></span>

* <span data-ttu-id="535ff-112">Een geldige Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="535ff-112">A valid Azure subscription</span></span>
* <span data-ttu-id="535ff-113">Een tenant in SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="535ff-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="535ff-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="535ff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="535ff-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="535ff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="535ff-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="535ff-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="535ff-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="535ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="535ff-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="535ff-118">Scenario description</span></span>
<span data-ttu-id="535ff-119">Hallo-doel van deze zelfstudie is tooenable u tootest Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="535ff-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="535ff-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="535ff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="535ff-121">Het toevoegen van SuccessFactors van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="535ff-121">Adding SuccessFactors from hello gallery</span></span>
2. <span data-ttu-id="535ff-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="535ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-hello-gallery"></a><span data-ttu-id="535ff-123">Het toevoegen van SuccessFactors van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="535ff-123">Adding SuccessFactors from hello gallery</span></span>
<span data-ttu-id="535ff-124">tooconfigure hello integratie van SuccessFactors in Azure AD, moet u tooadd SuccessFactors uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="535ff-124">tooconfigure hello integration of SuccessFactors into Azure AD, you need tooadd SuccessFactors from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="535ff-125">**tooadd SuccessFactors via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="535ff-125">**tooadd SuccessFactors from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="535ff-126">Klik in de klassieke Azure-portal op Hallo linkernavigatievenster, Hallo op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="535ff-126">In hello Azure classic portal, on hello left navigation panel, click **Active Directory**.</span></span>
   
    ![Eenmalige aanmelding configureren][1]
2. <span data-ttu-id="535ff-128">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="535ff-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="535ff-129">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="535ff-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Eenmalige aanmelding configureren][2]
4. <span data-ttu-id="535ff-131">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="535ff-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Toepassingen][3]
5. <span data-ttu-id="535ff-133">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="535ff-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Eenmalige aanmelding configureren][4]
6. <span data-ttu-id="535ff-135">In Hallo **zoekvak**, type **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="535ff-135">In hello **search box**, type **SuccessFactors**.</span></span>
   
    ![Eenmalige aanmelding configureren][5]
7. <span data-ttu-id="535ff-137">Selecteer in het deelvenster resultaten hello, **SuccessFactors**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="535ff-137">In hello results panel, select **SuccessFactors**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Eenmalige aanmelding configureren][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="535ff-139">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="535ff-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="535ff-140">Hallo-doel van deze sectie is tooshow u hoe tooconfigure en eenmalige aanmelding Azure AD-test met SuccessFactors op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="535ff-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="535ff-141">Voor één aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in SuccessFactors tooan gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="535ff-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SuccessFactors tooan user in Azure AD is.</span></span> <span data-ttu-id="535ff-142">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in SuccessFactors toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="535ff-142">In other words, a link relationship between an Azure AD user and hello related user in SuccessFactors needs toobe established.</span></span>

<span data-ttu-id="535ff-143">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="535ff-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SuccessFactors.</span></span>

<span data-ttu-id="535ff-144">tooconfigure en eenmalige aanmelding Azure AD-test met SuccessFactors, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="535ff-144">tooconfigure and test Azure AD single sign-on with SuccessFactors, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="535ff-145">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="535ff-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="535ff-146">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="535ff-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="535ff-147">**[Maken van een testgebruiker SuccessFactors](#creating-a-successfactors-test-user)**  -toohave een equivalent van Britta Simon in SuccessFactors die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="535ff-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - toohave a counterpart of Britta Simon in SuccessFactors that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="535ff-148">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="535ff-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="535ff-149">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="535ff-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="535ff-150">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="535ff-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="535ff-151">In deze sectie Azure AD eenmalige aanmelding in de klassieke portal Hallo inschakelen en configureren van eenmalige aanmelding in uw toepassing SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="535ff-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="535ff-152">**Azure AD tooconfigure eenmalige aanmelding met SuccessFactors, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="535ff-152">**tooconfigure Azure AD single sign-on with SuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="535ff-153">In de klassieke Azure-portal op Hallo Hallo **SuccessFactors** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="535ff-153">In hello Azure classic portal, on hello **SuccessFactors** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    ![Eenmalige aanmelding configureren][7]
2. <span data-ttu-id="535ff-155">Op Hallo **wilt u hoe gebruikers toosign op tooSuccessFactors** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="535ff-155">On hello **How would you like users toosign on tooSuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Eenmalige aanmelding configureren][8]
3. <span data-ttu-id="535ff-157">Op Hallo **App-URL configureren** pagina, het uitvoeren van Hallo volgende stappen uit en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="535ff-157">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    ![Eenmalige aanmelding configureren][9]
   
    <span data-ttu-id="535ff-159">a.</span><span class="sxs-lookup"><span data-stu-id="535ff-159">a.</span></span> <span data-ttu-id="535ff-160">In Hallo **aanmelding op URL** textbox, typ een URL met een Hallo patronen te volgen:</span><span class="sxs-lookup"><span data-stu-id="535ff-160">In hello **Sign On URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="535ff-161">b.</span><span class="sxs-lookup"><span data-stu-id="535ff-161">b.</span></span> <span data-ttu-id="535ff-162">In Hallo **antwoord-URL** textbox, typ een URL met een Hallo patronen te volgen:</span><span class="sxs-lookup"><span data-stu-id="535ff-162">In hello **Reply URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="535ff-163">c.</span><span class="sxs-lookup"><span data-stu-id="535ff-163">c.</span></span> <span data-ttu-id="535ff-164">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="535ff-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="535ff-165">Houd er rekening mee dat deze niet Hallo echte waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="535ff-165">Please note that these are not hello real values.</span></span> <span data-ttu-id="535ff-166">U hebt deze waarden door de werkelijke aanmelding op de URL en de antwoord-URL Hallo tooupdate.</span><span class="sxs-lookup"><span data-stu-id="535ff-166">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="535ff-167">Neem contact op met tooget deze waarden [SuccessFactors ondersteuningsteam](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="535ff-167">tooget these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="535ff-168">Op Hallo **eenmalige aanmelding configureren op SuccessFactors** pagina, klikt u op **certificaat downloaden**, en sla Hallo certificaatbestand lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="535ff-168">On hello **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Eenmalige aanmelding configureren][10]

2. <span data-ttu-id="535ff-170">In een ander browservenster, meld u aan bij uw **SuccessFactors-beheerportal** als beheerder.</span><span class="sxs-lookup"><span data-stu-id="535ff-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="535ff-171">Ga naar **Toepassingsbeveiliging** en systeemeigen te**eenmalige aanmelding op functie**.</span><span class="sxs-lookup"><span data-stu-id="535ff-171">Visit **Application Security** and native too**Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="535ff-172">De waarde van een plaats in Hallo **Token opnieuw** en klik op **Token opslaan** tooenable SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="535ff-172">Place any value in hello **Reset Token** and click **Save Token** tooenable SAML SSO.</span></span>
   
    ![Configureren van eenmalige aanmelding op app aan clientzijde][11]

    > [!NOTE] 
    > <span data-ttu-id="535ff-174">Deze waarde wordt alleen gebruikt als Hallo aan/uit-knop.</span><span class="sxs-lookup"><span data-stu-id="535ff-174">This value is just used as hello on/off switch.</span></span> <span data-ttu-id="535ff-175">Als een willekeurige waarde wordt opgeslagen, is Hallo SAML SSO ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="535ff-175">If any value is saved, hello SAML SSO is ON.</span></span> <span data-ttu-id="535ff-176">Als een lege waarde wordt opgeslagen is Hallo SAML SSO uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="535ff-176">If a blank value is saved hello SAML SSO is OFF.</span></span>

1. <span data-ttu-id="535ff-177">Systeemeigen toobelow schermafbeelding en Hallo van de volgende activiteiten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="535ff-177">Native toobelow screenshot and perform hello following actions.</span></span>
   
    ![Configureren van eenmalige aanmelding op app aan clientzijde][12]
   
    <span data-ttu-id="535ff-179">a.</span><span class="sxs-lookup"><span data-stu-id="535ff-179">a.</span></span> <span data-ttu-id="535ff-180">Selecteer Hallo **SAML v2 SSO** keuzerondje</span><span class="sxs-lookup"><span data-stu-id="535ff-180">Select hello **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="535ff-181">b.</span><span class="sxs-lookup"><span data-stu-id="535ff-181">b.</span></span> <span data-ttu-id="535ff-182">Hallo SAML aantonen partij Name(e.g. SAml issuer + company name) ingesteld.</span><span class="sxs-lookup"><span data-stu-id="535ff-182">Set hello SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="535ff-183">c.</span><span class="sxs-lookup"><span data-stu-id="535ff-183">c.</span></span> <span data-ttu-id="535ff-184">In Hallo **SAML verlener** textbox plaatsen Hallo-waarde van **URL-verlener** van de configuratiewizard voor Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="535ff-184">In hello **SAML Issuer** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="535ff-185">d.</span><span class="sxs-lookup"><span data-stu-id="535ff-185">d.</span></span> <span data-ttu-id="535ff-186">Selecteer **(klant gegenereerd/IdP/AP) antwoord** als **verplichte handtekening vereisen**.</span><span class="sxs-lookup"><span data-stu-id="535ff-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="535ff-187">e.</span><span class="sxs-lookup"><span data-stu-id="535ff-187">e.</span></span> <span data-ttu-id="535ff-188">Selecteer **ingeschakeld** als **inschakelen SAML vlag**.</span><span class="sxs-lookup"><span data-stu-id="535ff-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="535ff-189">f.</span><span class="sxs-lookup"><span data-stu-id="535ff-189">f.</span></span> <span data-ttu-id="535ff-190">Selecteer **Nee** als **aanmelding Aanvraaghandtekening (SF gegenereerd/SP/RP)**.</span><span class="sxs-lookup"><span data-stu-id="535ff-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="535ff-191">g.</span><span class="sxs-lookup"><span data-stu-id="535ff-191">g.</span></span> <span data-ttu-id="535ff-192">Selecteer **Browser/Post profiel** als **SAML profiel**.</span><span class="sxs-lookup"><span data-stu-id="535ff-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="535ff-193">h.</span><span class="sxs-lookup"><span data-stu-id="535ff-193">h.</span></span> <span data-ttu-id="535ff-194">Selecteer **Nee** als **geldigheidsduur van certificaat afdwingen**.</span><span class="sxs-lookup"><span data-stu-id="535ff-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="535ff-195">ik.</span><span class="sxs-lookup"><span data-stu-id="535ff-195">i.</span></span> <span data-ttu-id="535ff-196">Hallo-inhoud van de gedownloade certificaatbestand Hallo kopiëren en plak deze in Hallo **SAML verifiëren certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="535ff-196">Copy hello content of hello downloaded certificate file, and then paste it into hello **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="535ff-197">inhoud van de certificaten Hallo moet certificaat en certificaat afsluitcodes hebben beginnen.</span><span class="sxs-lookup"><span data-stu-id="535ff-197">hello certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="535ff-198">Navigeer tooSAML V2 en voer vervolgens Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="535ff-198">Navigate tooSAML V2, and then perform hello following steps:</span></span>
   
    ![Configureren van eenmalige aanmelding op app aan clientzijde][13]
   
    <span data-ttu-id="535ff-200">a.</span><span class="sxs-lookup"><span data-stu-id="535ff-200">a.</span></span> <span data-ttu-id="535ff-201">Selecteer **Ja** als **ondersteuning voor globale afmelding Serviceprovider geïnitieerde**.</span><span class="sxs-lookup"><span data-stu-id="535ff-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="535ff-202">b.</span><span class="sxs-lookup"><span data-stu-id="535ff-202">b.</span></span> <span data-ttu-id="535ff-203">In Hallo **globale afmelding Service-URL (LogoutRequest doel)** textbox plaatsen Hallo-waarde van **externe URL voor afmelden** van de configuratiewizard voor Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="535ff-203">In hello **Global Logout Service URL (LogoutRequest destination)** textbox put hello value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="535ff-204">c.</span><span class="sxs-lookup"><span data-stu-id="535ff-204">c.</span></span> <span data-ttu-id="535ff-205">Selecteer **Nee** als **vereisen sp alle NameID element moet versleutelen**.</span><span class="sxs-lookup"><span data-stu-id="535ff-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="535ff-206">d.</span><span class="sxs-lookup"><span data-stu-id="535ff-206">d.</span></span> <span data-ttu-id="535ff-207">Selecteer **niet nader omschreven** als **NameID indeling**.</span><span class="sxs-lookup"><span data-stu-id="535ff-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="535ff-208">e.</span><span class="sxs-lookup"><span data-stu-id="535ff-208">e.</span></span> <span data-ttu-id="535ff-209">Selecteer **Ja** als **inschakelen geïnitieerd sp aanmelding (AuthnRequest)**.</span><span class="sxs-lookup"><span data-stu-id="535ff-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="535ff-210">f.</span><span class="sxs-lookup"><span data-stu-id="535ff-210">f.</span></span> <span data-ttu-id="535ff-211">In Hallo **Verzendaanvraag als uitgever van het hele bedrijf** textbox plaatsen Hallo-waarde van **externe aanmeldings-URL** van de configuratiewizard voor Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="535ff-211">In hello **Send request as Company-Wide issuer** textbox put hello value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="535ff-212">Voer deze stappen uit als u wilt dat toomake Hallo aanmelding gebruikersnamen niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="535ff-212">Perform these steps if you want toomake hello login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="535ff-213">a.</span><span class="sxs-lookup"><span data-stu-id="535ff-213">a.</span></span> <span data-ttu-id="535ff-214">Ga naar **Bedrijfsinstellingen**(aan de onderkant van de Hallo).</span><span class="sxs-lookup"><span data-stu-id="535ff-214">Visit **Company Settings**(near hello bottom).</span></span>
   
    <span data-ttu-id="535ff-215">b.</span><span class="sxs-lookup"><span data-stu-id="535ff-215">b.</span></span> <span data-ttu-id="535ff-216">Schakel dit selectievakje in bij **inschakelen niet hoofdlettergevoelig gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="535ff-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="535ff-217">c.Click **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="535ff-217">c.Click **Save**.</span></span>
   
    ![Eenmalige aanmelding configureren][29]

    > [!NOTE] 
    > <span data-ttu-id="535ff-219">Als u tooenable dit probeert, systeemcontroles Hallo als een dubbele naam van de SAML-aanmelding wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="535ff-219">If you try tooenable this, hello system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="535ff-220">Bijvoorbeeld als de klant Hallo heeft gebruikersnamen Gebruiker1 als Gebruiker1.</span><span class="sxs-lookup"><span data-stu-id="535ff-220">For example if hello customer has usernames User1 and user1.</span></span> <span data-ttu-id="535ff-221">Blijf de hoofdlettergevoeligheid, kunt u deze dubbele vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="535ff-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="535ff-222">Hallo-systeem, krijgt u een foutbericht weergegeven en wordt het Hallo-functie niet inschakelt.</span><span class="sxs-lookup"><span data-stu-id="535ff-222">hello system will give you an error message and will not enable hello feature.</span></span> <span data-ttu-id="535ff-223">Hallo-klant moet toochange een Hallo gebruikersnamen zodat deze daadwerkelijk gespeld verschillende.</span><span class="sxs-lookup"><span data-stu-id="535ff-223">hello customer will need toochange one of hello usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="535ff-224">Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="535ff-224">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    ![Toepassingen][14]
2. <span data-ttu-id="535ff-226">Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="535ff-226">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Toepassingen][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="535ff-228">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="535ff-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="535ff-229">Hallo-doel van deze sectie is toocreate een testgebruiker in de klassieke portal Hallo Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="535ff-229">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][16]

<span data-ttu-id="535ff-231">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="535ff-231">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="535ff-232">In Hallo **klassieke Azure-Portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="535ff-232">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Een Azure AD-testgebruiker maken][17]
2. <span data-ttu-id="535ff-234">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="535ff-234">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="535ff-235">Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="535ff-235">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Een Azure AD-testgebruiker maken][18]
4. <span data-ttu-id="535ff-237">Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="535ff-237">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Een Azure AD-testgebruiker maken][19]
5. <span data-ttu-id="535ff-239">Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="535ff-239">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken][20]
   
    <span data-ttu-id="535ff-241">a.</span><span class="sxs-lookup"><span data-stu-id="535ff-241">a.</span></span> <span data-ttu-id="535ff-242">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="535ff-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="535ff-243">b.</span><span class="sxs-lookup"><span data-stu-id="535ff-243">b.</span></span> <span data-ttu-id="535ff-244">In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="535ff-244">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="535ff-245">c.</span><span class="sxs-lookup"><span data-stu-id="535ff-245">c.</span></span> <span data-ttu-id="535ff-246">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="535ff-246">Click **Next**.</span></span>
6. <span data-ttu-id="535ff-247">Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="535ff-247">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken][21]
   
    <span data-ttu-id="535ff-249">a.</span><span class="sxs-lookup"><span data-stu-id="535ff-249">a.</span></span> <span data-ttu-id="535ff-250">In Hallo **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="535ff-250">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="535ff-251">b.</span><span class="sxs-lookup"><span data-stu-id="535ff-251">b.</span></span> <span data-ttu-id="535ff-252">In Hallo **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="535ff-252">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="535ff-253">c.</span><span class="sxs-lookup"><span data-stu-id="535ff-253">c.</span></span> <span data-ttu-id="535ff-254">In Hallo **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="535ff-254">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="535ff-255">d.</span><span class="sxs-lookup"><span data-stu-id="535ff-255">d.</span></span> <span data-ttu-id="535ff-256">In Hallo **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="535ff-256">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="535ff-257">e.</span><span class="sxs-lookup"><span data-stu-id="535ff-257">e.</span></span> <span data-ttu-id="535ff-258">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="535ff-258">Click **Next**.</span></span>
7. <span data-ttu-id="535ff-259">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="535ff-259">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Een Azure AD-testgebruiker maken][22]
8. <span data-ttu-id="535ff-261">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="535ff-261">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken][23]
   
    <span data-ttu-id="535ff-263">a.</span><span class="sxs-lookup"><span data-stu-id="535ff-263">a.</span></span> <span data-ttu-id="535ff-264">Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="535ff-264">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="535ff-265">b.</span><span class="sxs-lookup"><span data-stu-id="535ff-265">b.</span></span> <span data-ttu-id="535ff-266">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="535ff-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="535ff-267">Een testgebruiker SuccessFactors maken</span><span class="sxs-lookup"><span data-stu-id="535ff-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="535ff-268">In de volgorde tooenable Azure AD gebruikers toolog in SuccessFactors, moeten ze worden ingericht in SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="535ff-268">In order tooenable Azure AD users toolog into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="535ff-269">In geval van SuccessFactors Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="535ff-269">In hello case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="535ff-270">tooget gebruikers in SuccessFactors hebt gemaakt, moet u toocontact hello [SuccessFactors ondersteuningsteam](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="535ff-270">tooget users created in SuccessFactors, you need toocontact hello [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="535ff-271">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="535ff-271">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="535ff-272">Hallo-doel van deze sectie is tooenabling Britta Simon toouse Azure eenmalige aanmelding haar tooSuccessFactors toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="535ff-272">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSuccessFactors.</span></span>

![Gebruiker toewijzen][24]

<span data-ttu-id="535ff-274">**tooassign Britta Simon tooSuccessFactors, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="535ff-274">**tooassign Britta Simon tooSuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="535ff-275">Klik op Hallo klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="535ff-275">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Gebruiker toewijzen][25]
2. <span data-ttu-id="535ff-277">Selecteer in de lijst met de toepassingen van Hallo **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="535ff-277">In hello applications list, select **SuccessFactors**.</span></span>
   
    ![Eenmalige aanmelding configureren][26]
3. <span data-ttu-id="535ff-279">Klik in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="535ff-279">In hello menu on hello top, click **Users**.</span></span>
   
    ![Gebruiker toewijzen][27]
4. <span data-ttu-id="535ff-281">Selecteer in de lijst gebruikers Hallo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="535ff-281">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="535ff-282">Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="535ff-282">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Gebruiker toewijzen][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="535ff-284">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="535ff-284">Testing single sign-on</span></span>
<span data-ttu-id="535ff-285">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="535ff-285">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="535ff-286">Als u op Hallo SuccessFactors-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SuccessFactors toepassing.</span><span class="sxs-lookup"><span data-stu-id="535ff-286">When you click hello SuccessFactors tile in hello Access Panel, you should get automatically signed-on tooyour SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="535ff-287">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="535ff-287">Additional resources</span></span>
* [<span data-ttu-id="535ff-288">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="535ff-288">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="535ff-289">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="535ff-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
