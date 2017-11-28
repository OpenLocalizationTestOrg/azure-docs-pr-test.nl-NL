---
title: 'Zelfstudie: Azure Active Directory-integratie met Jive | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Jive.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: f22bf78a55e8a4a9ea2f0020ef2f535be88b6302
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="a5550-103">Zelfstudie: Azure Active Directory-integratie met Jive</span><span class="sxs-lookup"><span data-stu-id="a5550-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="a5550-104">In deze zelfstudie leert u hoe toointegrate Jive met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a5550-104">In this tutorial, you learn how toointegrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a5550-105">Jive integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a5550-105">Integrating Jive with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a5550-106">U kunt beheren in Azure AD die tooJive toegang heeft</span><span class="sxs-lookup"><span data-stu-id="a5550-106">You can control in Azure AD who has access tooJive</span></span>
- <span data-ttu-id="a5550-107">U kunt uw gebruikers tooautomatically get aangemelde tooJive (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="a5550-107">You can enable your users tooautomatically get signed-on tooJive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a5550-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a5550-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a5550-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a5550-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5550-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a5550-110">Prerequisites</span></span>

<span data-ttu-id="a5550-111">Azure AD-integratie met Jive tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="a5550-111">tooconfigure Azure AD integration with Jive, you need hello following items:</span></span>

- <span data-ttu-id="a5550-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a5550-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a5550-113">Een Jive eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a5550-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a5550-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a5550-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a5550-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a5550-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a5550-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a5550-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a5550-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a5550-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a5550-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a5550-118">Scenario description</span></span>
<span data-ttu-id="a5550-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a5550-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a5550-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a5550-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a5550-121">Het toevoegen van Jive van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a5550-121">Adding Jive from hello gallery</span></span>
2. <span data-ttu-id="a5550-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a5550-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-hello-gallery"></a><span data-ttu-id="a5550-123">Het toevoegen van Jive van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a5550-123">Adding Jive from hello gallery</span></span>
<span data-ttu-id="a5550-124">tooconfigure hello integratie van Jive met Azure AD, moet u tooadd Jive uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a5550-124">tooconfigure hello integration of Jive into Azure AD, you need tooadd Jive from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a5550-125">**tooadd Jive via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a5550-125">**tooadd Jive from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a5550-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a5550-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a5550-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a5550-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a5550-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a5550-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a5550-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a5550-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a5550-133">Typ in het zoekvak Hallo **Jive**.</span><span class="sxs-lookup"><span data-stu-id="a5550-133">In hello search box, type **Jive**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="a5550-135">Selecteer in het deelvenster resultaten hello, **Jive**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a5550-135">In hello results panel, select **Jive**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a5550-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a5550-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a5550-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Jive op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a5550-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a5550-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Jive is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5550-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jive is tooa user in Azure AD.</span></span> <span data-ttu-id="a5550-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Jive toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="a5550-140">In other words, a link relationship between an Azure AD user and hello related user in Jive needs toobe established.</span></span>

<span data-ttu-id="a5550-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Jive.</span><span class="sxs-lookup"><span data-stu-id="a5550-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Jive.</span></span>

<span data-ttu-id="a5550-142">tooconfigure en eenmalige aanmelding Azure AD-test met Jive, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a5550-142">tooconfigure and test Azure AD single sign-on with Jive, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a5550-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="a5550-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a5550-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5550-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a5550-145">**[Maken van een testgebruiker Jive](#creating-a-jive-test-user)**  -toohave een equivalent van Britta Simon in Jive die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a5550-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - toohave a counterpart of Britta Simon in Jive that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a5550-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a5550-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a5550-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a5550-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a5550-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a5550-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a5550-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Jive configureren.</span><span class="sxs-lookup"><span data-stu-id="a5550-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="a5550-150">**tooconfigure eenmalige aanmelding Azure AD met Jive, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a5550-150">**tooconfigure Azure AD single sign-on with Jive, perform hello following steps:**</span></span>

1. <span data-ttu-id="a5550-151">In de Azure-portal op Hallo Hallo **Jive** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a5550-151">In hello Azure portal, on hello **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a5550-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a5550-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="a5550-155">Op Hallo **Jive domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a5550-155">On hello **Jive Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="a5550-157">a.</span><span class="sxs-lookup"><span data-stu-id="a5550-157">a.</span></span> <span data-ttu-id="a5550-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="a5550-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="a5550-159">b.</span><span class="sxs-lookup"><span data-stu-id="a5550-159">b.</span></span> <span data-ttu-id="a5550-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="a5550-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a5550-161">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="a5550-161">These values are not hello real.</span></span> <span data-ttu-id="a5550-162">Deze waarden bijwerken met Hallo werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="a5550-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="a5550-163">Neem contact op met [Jive Client ondersteuningsteam](https://www.jivesoftware.com/services-support/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a5550-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="a5550-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a5550-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="a5550-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a5550-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a5550-168">tooconfigure eenmalige aanmelding op **Jive** clientzijde, aanmelding tooyour Jive tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a5550-168">tooconfigure single sign-on on **Jive** side, sign-on tooyour Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="a5550-169">Klik in het menu bovenaan Hallo Hallo '**Saml**. "</span><span class="sxs-lookup"><span data-stu-id="a5550-169">In hello menu on hello top, Click "**Saml**."</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="a5550-171">a.</span><span class="sxs-lookup"><span data-stu-id="a5550-171">a.</span></span> <span data-ttu-id="a5550-172">Selecteer **ingeschakeld** onder Hallo **algemene** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a5550-172">Select **Enabled** under hello **General** tab.</span></span>   
    <span data-ttu-id="a5550-173">b.</span><span class="sxs-lookup"><span data-stu-id="a5550-173">b.</span></span> <span data-ttu-id="a5550-174">Klik op Hallo '**alle saml-instellingen opslaan**' knop.</span><span class="sxs-lookup"><span data-stu-id="a5550-174">Click hello "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="a5550-175">Navigeer toohello '**Idp metagegevens**' tabblad.</span><span class="sxs-lookup"><span data-stu-id="a5550-175">Navigate toohello "**Idp Metadata**" tab.</span></span>
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="a5550-177">a.</span><span class="sxs-lookup"><span data-stu-id="a5550-177">a.</span></span> <span data-ttu-id="a5550-178">Hallo-inhoud van XML-bestand met metagegevens Hallo gedownload kopiëren en plak deze in Hallo **Identity-Provider (IDP) metagegevens** textbox.</span><span class="sxs-lookup"><span data-stu-id="a5550-178">Copy hello content of hello downloaded metadata XML file, and then paste it into hello **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="a5550-179">b.</span><span class="sxs-lookup"><span data-stu-id="a5550-179">b.</span></span> <span data-ttu-id="a5550-180">Klik op Hallo '**alle saml-instellingen opslaan**' knop.</span><span class="sxs-lookup"><span data-stu-id="a5550-180">Click hello "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="a5550-181">Ga toohello '**kenmerk Gebruikerskoppeling**' tabblad.</span><span class="sxs-lookup"><span data-stu-id="a5550-181">Go toohello "**User Attribute Mapping**" tab.</span></span>
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="a5550-183">a.</span><span class="sxs-lookup"><span data-stu-id="a5550-183">a.</span></span> <span data-ttu-id="a5550-184">In Hallo **e** textbox, kopiëren en plakken Hallo kenmerknaam van **mail** waarde.</span><span class="sxs-lookup"><span data-stu-id="a5550-184">In hello **Email** textbox, copy and paste hello attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="a5550-185">b.</span><span class="sxs-lookup"><span data-stu-id="a5550-185">b.</span></span> <span data-ttu-id="a5550-186">In Hallo **voornaam** textbox, kopiëren en plakken Hallo kenmerknaam van **givenname** waarde.</span><span class="sxs-lookup"><span data-stu-id="a5550-186">In hello **First Name** textbox, copy and paste hello attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="a5550-187">c.</span><span class="sxs-lookup"><span data-stu-id="a5550-187">c.</span></span> <span data-ttu-id="a5550-188">In Hallo **achternaam** textbox, kopiëren en plakken Hallo kenmerknaam van **achternaam** waarde.</span><span class="sxs-lookup"><span data-stu-id="a5550-188">In hello **Last Name** textbox, copy and paste hello attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="a5550-189">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="a5550-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a5550-190">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="a5550-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a5550-191">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a5550-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a5550-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a5550-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="a5550-193">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a5550-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a5550-195">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a5550-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a5550-196">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a5550-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a5550-198">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a5550-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a5550-200">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="a5550-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a5550-202">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a5550-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a5550-204">a.</span><span class="sxs-lookup"><span data-stu-id="a5550-204">a.</span></span> <span data-ttu-id="a5550-205">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a5550-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a5550-206">b.</span><span class="sxs-lookup"><span data-stu-id="a5550-206">b.</span></span> <span data-ttu-id="a5550-207">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a5550-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a5550-208">c.</span><span class="sxs-lookup"><span data-stu-id="a5550-208">c.</span></span> <span data-ttu-id="a5550-209">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a5550-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a5550-210">d.</span><span class="sxs-lookup"><span data-stu-id="a5550-210">d.</span></span> <span data-ttu-id="a5550-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a5550-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="a5550-212">Een testgebruiker Jive maken</span><span class="sxs-lookup"><span data-stu-id="a5550-212">Creating a Jive test user</span></span>

<span data-ttu-id="a5550-213">Werken met [Jive Client ondersteuningsteam](https://www.jivesoftware.com/services-support/) tooadd Hallo gebruikers in Hallo Jive platform.</span><span class="sxs-lookup"><span data-stu-id="a5550-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) tooadd hello users in hello Jive platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a5550-214">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5550-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a5550-215">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooJive toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="a5550-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJive.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a5550-217">**tooassign Britta Simon tooJive, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a5550-217">**tooassign Britta Simon tooJive, perform hello following steps:**</span></span>

1. <span data-ttu-id="a5550-218">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a5550-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a5550-220">Selecteer in de lijst met de toepassingen van Hallo **Jive**.</span><span class="sxs-lookup"><span data-stu-id="a5550-220">In hello applications list, select **Jive**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="a5550-222">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a5550-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a5550-224">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a5550-224">Click **Add** button.</span></span> <span data-ttu-id="a5550-225">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a5550-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a5550-227">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="a5550-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a5550-228">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a5550-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a5550-229">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a5550-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a5550-230">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a5550-230">Testing single sign-on</span></span>

<span data-ttu-id="a5550-231">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="a5550-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a5550-232">Als u op Hallo Jive tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Jive toepassing.</span><span class="sxs-lookup"><span data-stu-id="a5550-232">When you click hello Jive tile in hello Access Panel, you should get automatically signed-on tooyour Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a5550-233">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a5550-233">Additional resources</span></span>

* [<span data-ttu-id="a5550-234">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5550-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a5550-235">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a5550-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a5550-236">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="a5550-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

