---
title: 'Zelfstudie: Azure Active Directory-integratie met halogeen Software | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en halogeen Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bdb67de713771d6e306f287c4b13895f6336f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="7b83d-103">Zelfstudie: Azure Active Directory-integratie met halogeen Software</span><span class="sxs-lookup"><span data-stu-id="7b83d-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="7b83d-104">In deze zelfstudie leert u hoe toointegrate halogeen Software met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b83d-104">In this tutorial, you learn how toointegrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b83d-105">Halogeen Software integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7b83d-105">Integrating Halogen Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7b83d-106">U kunt beheren in Azure AD wie toegang tot tooHalogen Software heeft</span><span class="sxs-lookup"><span data-stu-id="7b83d-106">You can control in Azure AD who has access tooHalogen Software</span></span>
- <span data-ttu-id="7b83d-107">U kunt uw gebruikers tooautomatically get aangemelde tooHalogen Software (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="7b83d-107">You can enable your users tooautomatically get signed-on tooHalogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7b83d-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="7b83d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7b83d-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7b83d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b83d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7b83d-110">Prerequisites</span></span>

<span data-ttu-id="7b83d-111">Azure AD-integratie met halogeen Software tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="7b83d-111">tooconfigure Azure AD integration with Halogen Software, you need hello following items:</span></span>

- <span data-ttu-id="7b83d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="7b83d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b83d-113">Een halogeen Software eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="7b83d-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b83d-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7b83d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b83d-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="7b83d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b83d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="7b83d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b83d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b83d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b83d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="7b83d-118">Scenario description</span></span>

<span data-ttu-id="7b83d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="7b83d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b83d-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="7b83d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b83d-121">Het toevoegen van halogeen Software van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7b83d-121">Adding Halogen Software from hello gallery</span></span>
2. <span data-ttu-id="7b83d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7b83d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-hello-gallery"></a><span data-ttu-id="7b83d-123">Het toevoegen van halogeen Software van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7b83d-123">Adding Halogen Software from hello gallery</span></span>

<span data-ttu-id="7b83d-124">tooconfigure hello integratie van halogeen Software in Azure AD, moet u tooadd halogeen Software uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="7b83d-124">tooconfigure hello integration of Halogen Software into Azure AD, you need tooadd Halogen Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7b83d-125">**tooadd halogeen Software uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7b83d-125">**tooadd Halogen Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b83d-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7b83d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7b83d-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7b83d-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="7b83d-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b83d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="7b83d-133">Typ in het zoekvak Hallo **halogeen Software**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-133">In hello search box, type **Halogen Software**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="7b83d-135">Selecteer in het deelvenster resultaten hello, **halogeen Software**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b83d-135">In hello results panel, select **Halogen Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7b83d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7b83d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7b83d-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met halogeen Software op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="7b83d-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7b83d-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in halogeen Software is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b83d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halogen Software is tooa user in Azure AD.</span></span> <span data-ttu-id="7b83d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in halogeen Software toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="7b83d-140">In other words, a link relationship between an Azure AD user and hello related user in Halogen Software needs toobe established.</span></span>

<span data-ttu-id="7b83d-141">In halogeen Software, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="7b83d-141">In Halogen Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7b83d-142">tooconfigure en test eenmalige aanmelding Azure AD met halogeen Software, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b83d-142">tooconfigure and test Azure AD single sign-on with Halogen Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7b83d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="7b83d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7b83d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b83d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b83d-145">**[Maken van een testgebruiker halogeen Software](#creating-a-halogen-software-test-user)**  -toohave een equivalent van Britta Simon in halogeen-Software die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7b83d-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in Halogen Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7b83d-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7b83d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b83d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="7b83d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7b83d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="7b83d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7b83d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing halogeen Software configureren.</span><span class="sxs-lookup"><span data-stu-id="7b83d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="7b83d-150">**Voer tooconfigure Azure AD eenmalige aanmelding met halogeen Software Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7b83d-150">**tooconfigure Azure AD single sign-on with Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b83d-151">In de Azure-portal op Hallo Hallo **halogeen Software** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-151">In hello Azure portal, on hello **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="7b83d-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7b83d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="7b83d-155">Op Hallo **halogeen Software domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b83d-155">On hello **Halogen Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="7b83d-157">a.</span><span class="sxs-lookup"><span data-stu-id="7b83d-157">a.</span></span> <span data-ttu-id="7b83d-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="7b83d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="7b83d-159">b.</span><span class="sxs-lookup"><span data-stu-id="7b83d-159">b.</span></span> <span data-ttu-id="7b83d-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen: `https://global.halogensoftware.com/<companyname>`,`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="7b83d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7b83d-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="7b83d-161">These values are not real.</span></span> <span data-ttu-id="7b83d-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="7b83d-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7b83d-163">Neem contact op met [halogeen Software Client ondersteuningsteam](https://support.halogensoftware.com/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="7b83d-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="7b83d-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7b83d-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="7b83d-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7b83d-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7b83d-168">In een ander browservenster aanmelding tooyour **halogeen Software** toepassing als beheerder.</span><span class="sxs-lookup"><span data-stu-id="7b83d-168">In a different browser window, sign-on tooyour **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="7b83d-169">Klik op Hallo **opties** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7b83d-169">Click hello **Options** tab.</span></span> 
   
    ![Wat is Azure AD Connect?][12]

8. <span data-ttu-id="7b83d-171">Klik in het Hallo navigatiedeelvenster links op **SAML-configuratie**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-171">In hello left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![Wat is Azure AD Connect?][13]

9. <span data-ttu-id="7b83d-173">Op Hallo **SAML-configuratie** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b83d-173">On hello **SAML Configuration** page, perform hello following steps:</span></span> 

    ![Wat is Azure AD Connect?][14]

     <span data-ttu-id="7b83d-175">a.</span><span class="sxs-lookup"><span data-stu-id="7b83d-175">a.</span></span> <span data-ttu-id="7b83d-176">Als **unieke id**, selecteer **NameID**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="7b83d-177">b.</span><span class="sxs-lookup"><span data-stu-id="7b83d-177">b.</span></span> <span data-ttu-id="7b83d-178">Als **unieke id gerelateerd aan**, selecteer **gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="7b83d-179">c.</span><span class="sxs-lookup"><span data-stu-id="7b83d-179">c.</span></span> <span data-ttu-id="7b83d-180">tooupload uw gedownloade metagegevensbestand, klikt u op **Bladeren** tooselect Hallo-bestand, en vervolgens **-bestand uploaden**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-180">tooupload your downloaded metadata file, click **Browse** tooselect hello file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="7b83d-181">d.</span><span class="sxs-lookup"><span data-stu-id="7b83d-181">d.</span></span> <span data-ttu-id="7b83d-182">tootest hello configuratie, klikt u op **Test uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-182">tootest hello configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="7b83d-183">U toowait nodig voor het Hallo-bericht '*Hallo SAML-test is voltooid. Sluit dit venster*'.</span><span class="sxs-lookup"><span data-stu-id="7b83d-183">You need toowait for hello message "*hello SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="7b83d-184">Sluit het geopende browservenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b83d-184">Then, close hello opened browser window.</span></span> <span data-ttu-id="7b83d-185">Hallo **SAML inschakelen** selectievakje is alleen beschikbaar als het Hallo-test is voltooid.</span><span class="sxs-lookup"><span data-stu-id="7b83d-185">hello **Enable SAML** checkbox is only enabled if hello test has been completed.</span></span> 
     
     <span data-ttu-id="7b83d-186">e.</span><span class="sxs-lookup"><span data-stu-id="7b83d-186">e.</span></span> <span data-ttu-id="7b83d-187">Selecteer **SAML inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="7b83d-188">f.</span><span class="sxs-lookup"><span data-stu-id="7b83d-188">f.</span></span> <span data-ttu-id="7b83d-189">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="7b83d-190">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="7b83d-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7b83d-191">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="7b83d-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7b83d-192">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7b83d-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7b83d-193">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7b83d-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="7b83d-194">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7b83d-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="7b83d-196">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7b83d-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b83d-197">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7b83d-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7b83d-199">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7b83d-201">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="7b83d-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7b83d-203">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b83d-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7b83d-205">a.</span><span class="sxs-lookup"><span data-stu-id="7b83d-205">a.</span></span> <span data-ttu-id="7b83d-206">In Hallo **naam** textbox typenaam als **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-206">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="7b83d-207">b.</span><span class="sxs-lookup"><span data-stu-id="7b83d-207">b.</span></span> <span data-ttu-id="7b83d-208">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7b83d-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7b83d-209">c.</span><span class="sxs-lookup"><span data-stu-id="7b83d-209">c.</span></span> <span data-ttu-id="7b83d-210">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7b83d-211">d.</span><span class="sxs-lookup"><span data-stu-id="7b83d-211">d.</span></span> <span data-ttu-id="7b83d-212">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="7b83d-213">Een testgebruiker halogeen Software maken</span><span class="sxs-lookup"><span data-stu-id="7b83d-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="7b83d-214">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in halogeen Software van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7b83d-214">hello objective of this section is toocreate a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="7b83d-215">**toocreate een gebruiker Britta Simon aangeroepen in halogeen Software, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7b83d-215">**toocreate a user called Britta Simon in Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b83d-216">Meld u aan bij tooyour **halogeen Software** toepassing als beheerder.</span><span class="sxs-lookup"><span data-stu-id="7b83d-216">Sign on tooyour **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="7b83d-217">Klik op Hallo **gebruiker Center** tabblad en klik vervolgens op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-217">Click hello **User Center** tab, and then click **Create User**.</span></span>
   
    ![Wat is Azure AD Connect?][300]  

3. <span data-ttu-id="7b83d-219">Op Hallo **nieuwe gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b83d-219">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    ![Wat is Azure AD Connect?][301]

    <span data-ttu-id="7b83d-221">a.</span><span class="sxs-lookup"><span data-stu-id="7b83d-221">a.</span></span> <span data-ttu-id="7b83d-222">In Hallo **voornaam** textbox type voornaam van de gebruiker Hallo zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-222">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>
    
    <span data-ttu-id="7b83d-223">b.</span><span class="sxs-lookup"><span data-stu-id="7b83d-223">b.</span></span> <span data-ttu-id="7b83d-224">In Hallo **achternaam** textbox type achternaam van de gebruiker Hallo zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-224">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span> 

    <span data-ttu-id="7b83d-225">c.</span><span class="sxs-lookup"><span data-stu-id="7b83d-225">c.</span></span> <span data-ttu-id="7b83d-226">In Hallo **gebruikersnaam** textbox type **Britta Simon**, de gebruikersnaam Hallo zoals hello Azure-portal in.</span><span class="sxs-lookup"><span data-stu-id="7b83d-226">In hello **Username** textbox, type **Britta Simon**, hello user name as in hello Azure portal.</span></span>

    <span data-ttu-id="7b83d-227">d.</span><span class="sxs-lookup"><span data-stu-id="7b83d-227">d.</span></span> <span data-ttu-id="7b83d-228">In Hallo **wachtwoord** textbox, typ een wachtwoord voor Britta.</span><span class="sxs-lookup"><span data-stu-id="7b83d-228">In hello **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="7b83d-229">e.</span><span class="sxs-lookup"><span data-stu-id="7b83d-229">e.</span></span> <span data-ttu-id="7b83d-230">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-230">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7b83d-231">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b83d-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7b83d-232">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooHalogen Software.</span><span class="sxs-lookup"><span data-stu-id="7b83d-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHalogen Software.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="7b83d-234">**tooassign Britta Simon tooHalogen Software, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7b83d-234">**tooassign Britta Simon tooHalogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b83d-235">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="7b83d-237">Selecteer in de lijst met de toepassingen van Hallo **halogeen Software**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-237">In hello applications list, select **Halogen Software**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="7b83d-239">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="7b83d-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="7b83d-241">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7b83d-241">Click **Add** button.</span></span> <span data-ttu-id="7b83d-242">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b83d-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="7b83d-244">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b83d-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7b83d-245">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b83d-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b83d-246">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b83d-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7b83d-247">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7b83d-247">Testing single sign-on</span></span>

<span data-ttu-id="7b83d-248">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="7b83d-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="7b83d-249">Als u op Hallo halogeen Software tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour halogeen softwaretoepassing.</span><span class="sxs-lookup"><span data-stu-id="7b83d-249">When you click hello Halogen Software tile in hello Access Panel, you should get automatically signed-on tooyour Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7b83d-250">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7b83d-250">Additional resources</span></span>

* [<span data-ttu-id="7b83d-251">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b83d-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b83d-252">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7b83d-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
