---
title: 'Zelfstudie: Azure Active Directory-integratie met namelijk | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en namelijk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0477ca6fa52a21abea7de458f8a99a01e8c25c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="a9b93-103">Zelfstudie: Azure Active Directory-integratie met namelijk</span><span class="sxs-lookup"><span data-stu-id="a9b93-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="a9b93-104">In deze zelfstudie leert u hoe toointegrate namelijk met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a9b93-104">In this tutorial, you learn how toointegrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a9b93-105">Namelijk integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a9b93-105">Integrating Namely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a9b93-106">U kunt beheren in Azure AD die tooNamely toegang heeft</span><span class="sxs-lookup"><span data-stu-id="a9b93-106">You can control in Azure AD who has access tooNamely</span></span>
- <span data-ttu-id="a9b93-107">U kunt uw gebruikers tooautomatically get aangemelde tooNamely (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="a9b93-107">You can enable your users tooautomatically get signed-on tooNamely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a9b93-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a9b93-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a9b93-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a9b93-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9b93-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a9b93-110">Prerequisites</span></span>

<span data-ttu-id="a9b93-111">tooconfigure Azure AD-integratie met namelijk u Hallo volgende items nodig:</span><span class="sxs-lookup"><span data-stu-id="a9b93-111">tooconfigure Azure AD integration with Namely, you need hello following items:</span></span>

- <span data-ttu-id="a9b93-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a9b93-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a9b93-113">Een namelijk eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a9b93-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a9b93-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a9b93-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a9b93-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a9b93-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a9b93-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a9b93-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a9b93-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a9b93-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a9b93-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a9b93-118">Scenario description</span></span>
<span data-ttu-id="a9b93-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a9b93-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a9b93-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a9b93-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a9b93-121">Het toevoegen van namelijk van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a9b93-121">Adding Namely from hello gallery</span></span>
2. <span data-ttu-id="a9b93-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a9b93-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-hello-gallery"></a><span data-ttu-id="a9b93-123">Het toevoegen van namelijk van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a9b93-123">Adding Namely from hello gallery</span></span>
<span data-ttu-id="a9b93-124">tooconfigure hello integratie van namelijk in Azure AD, moet u tooadd namelijk van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a9b93-124">tooconfigure hello integration of Namely into Azure AD, you need tooadd Namely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a9b93-125">**tooadd namelijk via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a9b93-125">**tooadd Namely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9b93-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a9b93-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a9b93-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a9b93-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a9b93-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a9b93-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a9b93-133">Typ in het zoekvak Hallo **namelijk**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-133">In hello search box, type **Namely**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="a9b93-135">Selecteer in het deelvenster resultaten hello, **namelijk**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a9b93-135">In hello results panel, select **Namely**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a9b93-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a9b93-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a9b93-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met namelijk op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a9b93-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a9b93-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in namelijk is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9b93-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Namely is tooa user in Azure AD.</span></span> <span data-ttu-id="a9b93-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in Hallo namelijk toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="a9b93-140">In other words, a link relationship between an Azure AD user and hello related user in Namely needs toobe established.</span></span>

<span data-ttu-id="a9b93-141">In waarde Hallo Hallo namelijk toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="a9b93-141">In Namely, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a9b93-142">tooconfigure en test eenmalige aanmelding Azure AD met namelijk u beschikken over toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a9b93-142">tooconfigure and test Azure AD single sign-on with Namely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a9b93-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="a9b93-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a9b93-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9b93-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a9b93-145">**[Maken van een namelijk testgebruiker](#creating-a-namely-test-user)**  -toohave een equivalent van Britta Simon in namelijk die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a9b93-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - toohave a counterpart of Britta Simon in Namely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a9b93-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a9b93-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a9b93-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a9b93-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a9b93-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a9b93-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a9b93-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing namelijk configureren.</span><span class="sxs-lookup"><span data-stu-id="a9b93-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="a9b93-150">**Azure AD tooconfigure eenmalige aanmelding met namelijk uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a9b93-150">**tooconfigure Azure AD single sign-on with Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9b93-151">In de Azure-portal op Hallo Hallo **namelijk** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-151">In hello Azure portal, on hello **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a9b93-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a9b93-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="a9b93-155">Op Hallo **namelijk domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a9b93-155">On hello **Namely Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="a9b93-157">a.</span><span class="sxs-lookup"><span data-stu-id="a9b93-157">a.</span></span> <span data-ttu-id="a9b93-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="a9b93-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="a9b93-159">b.</span><span class="sxs-lookup"><span data-stu-id="a9b93-159">b.</span></span> <span data-ttu-id="a9b93-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="a9b93-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a9b93-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="a9b93-161">These values are not real.</span></span> <span data-ttu-id="a9b93-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="a9b93-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a9b93-163">Neem contact op met [namelijk Client ondersteuningsteam](https://www.namely.com/contact/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a9b93-163">Contact [Namely Client support team](https://www.namely.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="a9b93-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a9b93-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="a9b93-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a9b93-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a9b93-168">Op Hallo **namelijk configuratie** sectie, klikt u op **namelijk configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="a9b93-168">On hello **Namely Configuration** section, click **Configure Namely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a9b93-169">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="a9b93-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="a9b93-171">Een ander browservenster geopend Meld u aan bij tooyour namelijk bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a9b93-171">In another browser window, sign on tooyour Namely company site as an administrator.</span></span>

8. <span data-ttu-id="a9b93-172">Klik in de werkbalk bovenaan Hallo Hallo op **bedrijf**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-172">In hello toolbar on hello top, click **Company**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="a9b93-174">Klik op Hallo **instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a9b93-174">Click hello **Settings** tab.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="a9b93-176">Klik op **SAML**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-176">Click **SAML**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="a9b93-178">Op Hallo **SAML instellingen** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a9b93-178">On hello **SAML Settings** page, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="a9b93-180">a.</span><span class="sxs-lookup"><span data-stu-id="a9b93-180">a.</span></span> <span data-ttu-id="a9b93-181">Klik op **SAML inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="a9b93-182">b.</span><span class="sxs-lookup"><span data-stu-id="a9b93-182">b.</span></span> <span data-ttu-id="a9b93-183">In Hallo **identiteit provider SSO url** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a9b93-183">In hello **Identity provider SSO url** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="a9b93-184">c.</span><span class="sxs-lookup"><span data-stu-id="a9b93-184">c.</span></span> <span data-ttu-id="a9b93-185">Open uw gedownloade certificaat in Kladblok, kopieer Hallo inhoud, en plak deze in Hallo **provider identiteitscertificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="a9b93-185">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="a9b93-186">d.</span><span class="sxs-lookup"><span data-stu-id="a9b93-186">d.</span></span> <span data-ttu-id="a9b93-187">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a9b93-188">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="a9b93-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a9b93-189">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="a9b93-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a9b93-190">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a9b93-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a9b93-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a9b93-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="a9b93-192">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a9b93-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a9b93-194">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a9b93-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9b93-195">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a9b93-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a9b93-197">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a9b93-199">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="a9b93-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a9b93-201">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a9b93-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a9b93-203">a.</span><span class="sxs-lookup"><span data-stu-id="a9b93-203">a.</span></span> <span data-ttu-id="a9b93-204">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a9b93-205">b.</span><span class="sxs-lookup"><span data-stu-id="a9b93-205">b.</span></span> <span data-ttu-id="a9b93-206">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a9b93-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a9b93-207">c.</span><span class="sxs-lookup"><span data-stu-id="a9b93-207">c.</span></span> <span data-ttu-id="a9b93-208">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a9b93-209">d.</span><span class="sxs-lookup"><span data-stu-id="a9b93-209">d.</span></span> <span data-ttu-id="a9b93-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="a9b93-211">Maken van een namelijk testgebruiker</span><span class="sxs-lookup"><span data-stu-id="a9b93-211">Creating a Namely test user</span></span>

<span data-ttu-id="a9b93-212">Hallo-doel van deze sectie is toocreate Britta Simon namelijk naam in van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a9b93-212">hello objective of this section is toocreate a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="a9b93-213">**toocreate Britta Simon namelijk naam in van een gebruiker uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a9b93-213">**toocreate a user called Britta Simon in Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9b93-214">Eenmalige aanmelding tooyour bedrijf namelijk site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a9b93-214">Sign-on tooyour Namely company site as an administrator.</span></span>

2. <span data-ttu-id="a9b93-215">Klik in de werkbalk bovenaan Hallo Hallo op **mensen**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-215">In hello toolbar on hello top, click **People**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="a9b93-217">Klik op Hallo **Directory** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a9b93-217">Click hello **Directory** tab.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="a9b93-219">Klik op **toevoegen van nieuwe persoon**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-219">Click **Add New Person**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="a9b93-221">Op Hallo **nieuwe persoon toevoegen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="a9b93-221">On hello **Add New Person** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="a9b93-222">a.</span><span class="sxs-lookup"><span data-stu-id="a9b93-222">a.</span></span> <span data-ttu-id="a9b93-223">In Hallo **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-223">In hello **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="a9b93-224">b.</span><span class="sxs-lookup"><span data-stu-id="a9b93-224">b.</span></span> <span data-ttu-id="a9b93-225">In Hallo **achternaam** textbox type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-225">In hello **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="a9b93-226">c.</span><span class="sxs-lookup"><span data-stu-id="a9b93-226">c.</span></span> <span data-ttu-id="a9b93-227">In Hallo **e** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a9b93-227">In hello **Email** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a9b93-228">d.</span><span class="sxs-lookup"><span data-stu-id="a9b93-228">d.</span></span> <span data-ttu-id="a9b93-229">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-229">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a9b93-230">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9b93-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a9b93-231">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooNamely toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="a9b93-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNamely.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a9b93-233">**tooassign Britta Simon tooNamely, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a9b93-233">**tooassign Britta Simon tooNamely, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9b93-234">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a9b93-236">Selecteer in de lijst met de toepassingen van Hallo **namelijk**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-236">In hello applications list, select **Namely**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="a9b93-238">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a9b93-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a9b93-240">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a9b93-240">Click **Add** button.</span></span> <span data-ttu-id="a9b93-241">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a9b93-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a9b93-243">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="a9b93-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a9b93-244">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a9b93-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a9b93-245">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a9b93-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a9b93-246">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a9b93-246">Testing single sign-on</span></span>

<span data-ttu-id="a9b93-247">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="a9b93-247">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="a9b93-248">Wanneer u klikt op Hallo namelijk-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour namelijk toepassing</span><span class="sxs-lookup"><span data-stu-id="a9b93-248">When you click hello Namely tile in hello Access Panel, you should get automatically signed-on tooyour Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a9b93-249">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a9b93-249">Additional resources</span></span>

* [<span data-ttu-id="a9b93-250">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9b93-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a9b93-251">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a9b93-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

