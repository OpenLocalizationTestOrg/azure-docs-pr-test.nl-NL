---
title: 'Zelfstudie: Azure Active Directory-integratie met Questetra BPM Suite | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Questetra BPM Suite.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="f2481-103">Zelfstudie: Azure Active Directory-integratie met Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="f2481-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="f2481-104">Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate Questetra BPM Suite met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f2481-104">hello objective of this tutorial is tooshow you how toointegrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="f2481-105">Questetra BPM Suite integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f2481-105">Integrating Questetra BPM Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="f2481-106">U kunt beheren in Azure AD wie toegang tot tooQuestetra BPM Suite heeft</span><span class="sxs-lookup"><span data-stu-id="f2481-106">You can control in Azure AD who has access tooQuestetra BPM Suite</span></span> 
* <span data-ttu-id="f2481-107">U kunt uw gebruikers tooautomatically get aangemelde tooQuestetra BPM Suite (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="f2481-107">You can enable your users tooautomatically get signed-on tooQuestetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="f2481-108">U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f2481-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="f2481-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f2481-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2481-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f2481-110">Prerequisites</span></span>
<span data-ttu-id="f2481-111">Azure AD-integratie met Questetra BPM Suite tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="f2481-111">tooconfigure Azure AD integration with Questetra BPM Suite, you need hello following items:</span></span>

* <span data-ttu-id="f2481-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f2481-112">An Azure AD subscription</span></span>
* <span data-ttu-id="f2481-113">Een [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f2481-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f2481-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f2481-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="f2481-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f2481-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="f2481-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f2481-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="f2481-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f2481-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="f2481-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f2481-118">Scenario Description</span></span>
<span data-ttu-id="f2481-119">Hallo-doel van deze zelfstudie is tooenable u tootest Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f2481-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="f2481-120">Hallo scenario beschreven in deze zelfstudie bestaat uit drie belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f2481-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="f2481-121">Het toevoegen van Questetra BPM Suite van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f2481-121">Adding Questetra BPM Suite from hello gallery</span></span> 
2. <span data-ttu-id="f2481-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f2481-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a><span data-ttu-id="f2481-123">Het toevoegen van Questetra BPM Suite van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f2481-123">Adding Questetra BPM Suite from hello gallery</span></span>
<span data-ttu-id="f2481-124">tooconfigure hello integratie van Questetra BPM Suite in Azure AD, moet u tooadd Questetra BPM Suite van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f2481-124">tooconfigure hello integration of Questetra BPM Suite into Azure AD, you need tooadd Questetra BPM Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f2481-125">**tooadd Questetra BPM Suite van Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f2481-125">**tooadd Questetra BPM Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2481-126">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f2481-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="f2481-128">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="f2481-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="f2481-129">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="f2481-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Toepassingen][2]

4. <span data-ttu-id="f2481-131">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="f2481-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Toepassingen][3]

5. <span data-ttu-id="f2481-133">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="f2481-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Toepassingen][4]

6. <span data-ttu-id="f2481-135">Typ in het zoekvak Hallo **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="f2481-135">In hello search box, type **Questetra BPM Suite**.</span></span>
   
    ![Toepassingen][5]

7. <span data-ttu-id="f2481-137">Selecteer in het deelvenster met resultaten Hallo **Questetra BPM Suite**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f2481-137">In hello results pane, select **Questetra BPM Suite**, and then click **Complete** tooadd hello application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f2481-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f2481-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f2481-139">Hallo-doel van deze sectie is tooshow u hoe tooconfigure en test eenmalige aanmelding Azure AD met Questetra BPM Suite op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f2481-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f2481-140">Voor één aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in Questetra BPM Suite tooan gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2481-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Questetra BPM Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="f2481-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Questetra BPM Suite toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="f2481-141">In other words, a link relationship between an Azure AD user and hello related user in Questetra BPM Suite needs toobe established.</span></span>  
<span data-ttu-id="f2481-142">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="f2481-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="f2481-143">tooconfigure en test eenmalige aanmelding Azure AD met Questetra BPM Suite, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f2481-143">tooconfigure and test Azure AD single sign-on with Questetra BPM Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f2481-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="f2481-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f2481-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f2481-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f2481-146">**[Maken van een testgebruiker Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)**  -toohave een equivalent van Britta Simon in Questetra BPM-pakket dat is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="f2481-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - toohave a counterpart of Britta Simon in Questetra BPM Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="f2481-147">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f2481-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f2481-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f2481-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f2481-149">Azure AD voor eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="f2481-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="f2481-150">Hallo-doel van deze sectie is tooenable Azure AD eenmalige aanmelding in de klassieke Azure-portal Hallo en tooconfigure eenmalige aanmelding in uw toepassing Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="f2481-150">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="f2481-151">**tooconfigure eenmalige aanmelding Azure AD met Questetra BPM Suite Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f2481-151">**tooconfigure Azure AD single sign-on with Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2481-152">In de klassieke Azure-portal op Hallo Hallo **Questetra BPM Suite** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On**  het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f2481-152">In hello Azure classic portal, on hello **Questetra BPM Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Eenmalige aanmelding configureren][8]

2. <span data-ttu-id="f2481-154">Op Hallo **wilt u hoe gebruikers toosign op tooQuestetra BPM Suite** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f2481-154">On hello **How would you like users toosign on tooQuestetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][9]

3. <span data-ttu-id="f2481-156">In een ander browservenster, meld u aan bij uw **Questetra BPM Suite** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f2481-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="f2481-157">Klik in het menu bovenaan Hallo Hallo **systeeminstellingen**.</span><span class="sxs-lookup"><span data-stu-id="f2481-157">In hello menu on hello top, click **System Settings**.</span></span> 
   
    ![Azure AD voor eenmalige aanmelding][10]

5. <span data-ttu-id="f2481-159">Hallo tooopen **SingleSignOnSAML** pagina, klikt u op **eenmalige aanmelding (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="f2481-159">tooopen hello **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Azure AD voor eenmalige aanmelding][11]

6. <span data-ttu-id="f2481-161">In de klassieke Azure-portal op Hallo Hallo **App-instellingen configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f2481-161">In hello Azure classic portal, on hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![App-instellingen configureren][13]
   
    <span data-ttu-id="f2481-163">a.</span><span class="sxs-lookup"><span data-stu-id="f2481-163">a.</span></span> <span data-ttu-id="f2481-164">Op uw **Questetra BPM Suite** bedrijf site in de sectie SP informatie hello, kopie Hallo **ACS URL**, en plak deze in Hallo **aanmelding op URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f2481-164">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="f2481-165">b.</span><span class="sxs-lookup"><span data-stu-id="f2481-165">b.</span></span> <span data-ttu-id="f2481-166">Op uw **Questetra BPM Suite** bedrijf site in de sectie SP informatie hello, kopie Hallo **entiteit-ID**, en plak deze in Hallo **URL-verlener** textbox.</span><span class="sxs-lookup"><span data-stu-id="f2481-166">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **Entity ID**, and then paste it into hello **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="f2481-167">c.</span><span class="sxs-lookup"><span data-stu-id="f2481-167">c.</span></span> <span data-ttu-id="f2481-168">Op uw **Questetra BPM Suite** bedrijf site in de sectie SP informatie hello, kopie Hallo **ACS URL**, en plak deze in Hallo **antwoord-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f2481-168">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="f2481-169">d.</span><span class="sxs-lookup"><span data-stu-id="f2481-169">d.</span></span> <span data-ttu-id="f2481-170">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f2481-170">Click **Next**.</span></span>

7. <span data-ttu-id="f2481-171">Op Hallo **op Questetra BPM Suite eenmalige aanmelding configureren** pagina, klikt u op **certificaat downloaden**, en sla Hallo certificaatbestand lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f2481-171">On hello **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Eenmalige aanmelding configureren][14]

8. <span data-ttu-id="f2481-173">Op uw **Questetra BPM Suite** bedrijf site, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f2481-173">On you **Questetra BPM Suite** company site, perform hello following steps:</span></span> 
   
    ![Eenmalige aanmelding configureren][15]
   
    <span data-ttu-id="f2481-175">a.</span><span class="sxs-lookup"><span data-stu-id="f2481-175">a.</span></span> <span data-ttu-id="f2481-176">Selecteer **eenmalige aanmelding inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="f2481-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="f2481-177">b.</span><span class="sxs-lookup"><span data-stu-id="f2481-177">b.</span></span> <span data-ttu-id="f2481-178">Kopieer op Hallo klassieke Azure-portal, Hallo **URL-verlener** waarde en plak deze in Hallo **entiteit-ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="f2481-178">On hello Azure classic portal, copy hello **Issuer URL** value, and then paste it into hello **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="f2481-179">c.</span><span class="sxs-lookup"><span data-stu-id="f2481-179">c.</span></span> <span data-ttu-id="f2481-180">Kopieer op Hallo klassieke Azure-portal, Hallo **Single Sign-On Service-URL** waarde en plak deze in Hallo **aanmelden pagina-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f2481-180">On hello Azure classic portal, copy hello **Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="f2481-181">d.</span><span class="sxs-lookup"><span data-stu-id="f2481-181">d.</span></span> <span data-ttu-id="f2481-182">Kopieer op Hallo klassieke Azure-portal, Hallo **Service-URL met eenmalige Sign-Out** waarde en plak deze in Hallo **afmelden pagina-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f2481-182">On hello Azure classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="f2481-183">e.</span><span class="sxs-lookup"><span data-stu-id="f2481-183">e.</span></span> <span data-ttu-id="f2481-184">In Hallo **NameID indeling** textbox type **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="f2481-184">In hello **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="f2481-185">f.</span><span class="sxs-lookup"><span data-stu-id="f2481-185">f.</span></span> <span data-ttu-id="f2481-186">Maak een Base64-gecodeerde bestand uit het gedownloade certificaat.</span><span class="sxs-lookup"><span data-stu-id="f2481-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="f2481-187">Zie voor meer informatie [hoe tooconvert een binair bestand van het certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="f2481-187">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="f2481-188">g.</span><span class="sxs-lookup"><span data-stu-id="f2481-188">g.</span></span> <span data-ttu-id="f2481-189">De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze in Hallo **validatiecertificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="f2481-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="f2481-190">h.</span><span class="sxs-lookup"><span data-stu-id="f2481-190">h.</span></span> <span data-ttu-id="f2481-191">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f2481-191">Click **Save**.</span></span>

1. <span data-ttu-id="f2481-192">Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f2481-192">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Wat is Azure AD Connect?][17]

2. <span data-ttu-id="f2481-194">Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="f2481-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Wat is Azure AD Connect?][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f2481-196">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f2481-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="f2481-197">Hallo-doel van deze sectie is toocreate een testgebruiker in Hallo klassieke Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f2481-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="f2481-198">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f2481-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2481-199">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f2481-199">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD-testgebruiker maken][100] 

2. <span data-ttu-id="f2481-201">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="f2481-201">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="f2481-202">Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f2481-202">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Azure AD-testgebruiker maken][101] 

4. <span data-ttu-id="f2481-204">Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f2481-204">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Azure AD-testgebruiker maken][102] 

5. <span data-ttu-id="f2481-206">Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f2481-206">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD-testgebruiker maken][103]
   
    <span data-ttu-id="f2481-208">a.</span><span class="sxs-lookup"><span data-stu-id="f2481-208">a.</span></span> <span data-ttu-id="f2481-209">Als **Type gebruiker**, selecteer **nieuwe gebruiker in uw organisatie**.</span><span class="sxs-lookup"><span data-stu-id="f2481-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="f2481-210">b.</span><span class="sxs-lookup"><span data-stu-id="f2481-210">b.</span></span> <span data-ttu-id="f2481-211">In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f2481-211">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="f2481-212">c.</span><span class="sxs-lookup"><span data-stu-id="f2481-212">c.</span></span> <span data-ttu-id="f2481-213">Klik op Volgende.</span><span class="sxs-lookup"><span data-stu-id="f2481-213">Click Next.</span></span>

6. <span data-ttu-id="f2481-214">Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f2481-214">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Azure AD-testgebruiker maken][104] 
   
    <span data-ttu-id="f2481-216">a.</span><span class="sxs-lookup"><span data-stu-id="f2481-216">a.</span></span> <span data-ttu-id="f2481-217">In Hallo **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f2481-217">In hello **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="f2481-218">b.</span><span class="sxs-lookup"><span data-stu-id="f2481-218">b.</span></span> <span data-ttu-id="f2481-219">In Hallo **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f2481-219">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="f2481-220">c.</span><span class="sxs-lookup"><span data-stu-id="f2481-220">c.</span></span> <span data-ttu-id="f2481-221">In Hallo **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f2481-221">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="f2481-222">d.</span><span class="sxs-lookup"><span data-stu-id="f2481-222">d.</span></span> <span data-ttu-id="f2481-223">In Hallo **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="f2481-223">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="f2481-224">e.</span><span class="sxs-lookup"><span data-stu-id="f2481-224">e.</span></span> <span data-ttu-id="f2481-225">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f2481-225">Click **Next**.</span></span>

7. <span data-ttu-id="f2481-226">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="f2481-226">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD-testgebruiker maken][105]  

8. <span data-ttu-id="f2481-228">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f2481-228">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD-testgebruiker maken][106]   
   
    <span data-ttu-id="f2481-230">a.</span><span class="sxs-lookup"><span data-stu-id="f2481-230">a.</span></span> <span data-ttu-id="f2481-231">Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f2481-231">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="f2481-232">b.</span><span class="sxs-lookup"><span data-stu-id="f2481-232">b.</span></span> <span data-ttu-id="f2481-233">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f2481-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="f2481-234">Maken van een testgebruiker Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="f2481-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="f2481-235">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Questetra BPM Suite van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f2481-235">hello objective of this section is toocreate a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="f2481-236">**een gebruiker Britta Simon aangeroepen in Questetra BPM Suite toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f2481-236">**toocreate a user called Britta Simon in Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2481-237">Eenmalige aanmelding tooyour Questetra BPM Suite bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f2481-237">Sign-on tooyour Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="f2481-238">Ga te**systeeminstellingen > gebruikerslijst > nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="f2481-238">Go too**System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="f2481-239">Voer in het dialoogvenster van de nieuwe gebruiker Hallo, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f2481-239">On hello New User dialog, perform hello following steps:</span></span> 
   
    ![Testgebruiker maken][300] 
   
    <span data-ttu-id="f2481-241">a.</span><span class="sxs-lookup"><span data-stu-id="f2481-241">a.</span></span> <span data-ttu-id="f2481-242">In Hallo **naam** textbox, typ de gebruikersnaam van Britta in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2481-242">In hello **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="f2481-243">b.</span><span class="sxs-lookup"><span data-stu-id="f2481-243">b.</span></span> <span data-ttu-id="f2481-244">In Hallo **e** textbox, typ de gebruikersnaam van Britta in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2481-244">In hello **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="f2481-245">c.</span><span class="sxs-lookup"><span data-stu-id="f2481-245">c.</span></span> <span data-ttu-id="f2481-246">In Hallo **wachtwoord** textbox, typ een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="f2481-246">In hello **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="f2481-247">Klik op **nieuwe gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f2481-247">Click **Add new user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f2481-248">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2481-248">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="f2481-249">Hallo-doel van deze sectie is tooenabling Britta Simon toouse Azure eenmalige aanmelding haar toegang tooQuestetra BPM Suite verleent.</span><span class="sxs-lookup"><span data-stu-id="f2481-249">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooQuestetra BPM Suite.</span></span>

![Wat is Azure AD Connect?][200]

<span data-ttu-id="f2481-251">**tooassign Britta Simon tooQuestetra BPM Suite Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f2481-251">**tooassign Britta Simon tooQuestetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2481-252">Klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, klik op Hallo Azure **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="f2481-252">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Wat is Azure AD Connect?][201]
2. <span data-ttu-id="f2481-254">Selecteer in de lijst met de toepassingen van Hallo **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="f2481-254">In hello applications list, select **Questetra BPM Suite**.</span></span>
   
    ![Wat is Azure AD Connect?][205]
3. <span data-ttu-id="f2481-256">Klik in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f2481-256">In hello menu on hello top, click **Users**.</span></span>
   
    ![Wat is Azure AD Connect?][202]
4. <span data-ttu-id="f2481-258">Selecteer in de lijst gebruikers Hallo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f2481-258">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Wat is Azure AD Connect?][203]
5. <span data-ttu-id="f2481-260">Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="f2481-260">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Wat is Azure AD Connect?][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="f2481-262">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f2481-262">Testing Single Sign-On</span></span>
<span data-ttu-id="f2481-263">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="f2481-263">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="f2481-264">Als u op Hallo Questetra BPM Suite tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Questetra BPM Suite-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f2481-264">When you click hello Questetra BPM Suite tile in hello Access Panel, you should get automatically signed-on tooyour Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f2481-265">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="f2481-265">Additional Resources</span></span>
* [<span data-ttu-id="f2481-266">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f2481-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f2481-267">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f2481-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
