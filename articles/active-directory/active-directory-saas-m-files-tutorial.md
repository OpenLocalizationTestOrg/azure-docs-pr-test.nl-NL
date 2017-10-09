---
title: 'Zelfstudie: Azure Active Directory-integratie met M-bestanden | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en M-bestanden.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e1d268da53312b1d2c12e29d66b1a5b66d0cdcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="fa498-103">Zelfstudie: Azure Active Directory-integratie met M-bestanden</span><span class="sxs-lookup"><span data-stu-id="fa498-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="fa498-104">In deze zelfstudie leert u hoe toointegrate M-bestanden met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fa498-104">In this tutorial, you learn how toointegrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fa498-105">M-bestanden worden geïntegreerd met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="fa498-105">Integrating M-Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fa498-106">U kunt beheren in Azure AD wie toegang tot tooM-bestanden heeft</span><span class="sxs-lookup"><span data-stu-id="fa498-106">You can control in Azure AD who has access tooM-Files</span></span>
- <span data-ttu-id="fa498-107">U kunt uw gebruikers tooautomatically get aangemelde tooM-bestanden (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="fa498-107">You can enable your users tooautomatically get signed-on tooM-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fa498-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="fa498-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fa498-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fa498-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa498-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fa498-110">Prerequisites</span></span>

<span data-ttu-id="fa498-111">tooconfigure Azure AD-integratie met M-bestanden, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="fa498-111">tooconfigure Azure AD integration with M-Files, you need hello following items:</span></span>

- <span data-ttu-id="fa498-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="fa498-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fa498-113">Een M bestanden eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="fa498-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fa498-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="fa498-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fa498-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="fa498-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fa498-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="fa498-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fa498-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fa498-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fa498-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="fa498-118">Scenario description</span></span>
<span data-ttu-id="fa498-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="fa498-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fa498-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="fa498-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fa498-121">M-bestanden uit de galerie Hallo toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="fa498-121">Adding M-Files from hello gallery</span></span>
2. <span data-ttu-id="fa498-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fa498-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-hello-gallery"></a><span data-ttu-id="fa498-123">M-bestanden uit de galerie Hallo toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="fa498-123">Adding M-Files from hello gallery</span></span>
<span data-ttu-id="fa498-124">tooconfigure hello integratie van M-bestanden met Azure AD, moet u tooadd M-bestanden uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="fa498-124">tooconfigure hello integration of M-Files into Azure AD, you need tooadd M-Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fa498-125">**tooadd M-bestanden uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fa498-125">**tooadd M-Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa498-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fa498-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fa498-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fa498-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fa498-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fa498-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="fa498-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fa498-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="fa498-133">Typ in het zoekvak Hallo **M bestanden**.</span><span class="sxs-lookup"><span data-stu-id="fa498-133">In hello search box, type **M-Files**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="fa498-135">Selecteer in het deelvenster resultaten hello, **M bestanden**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fa498-135">In hello results panel, select **M-Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fa498-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fa498-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fa498-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met M-bestanden op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="fa498-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fa498-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in M-bestanden is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa498-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in M-Files is tooa user in Azure AD.</span></span> <span data-ttu-id="fa498-140">Er moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in M-bestanden met andere woorden, toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="fa498-140">In other words, a link relationship between an Azure AD user and hello related user in M-Files needs toobe established.</span></span>

<span data-ttu-id="fa498-141">In de M-bestanden, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="fa498-141">In M-Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fa498-142">tooconfigure en test eenmalige aanmelding Azure AD met M-bestanden, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fa498-142">tooconfigure and test Azure AD single sign-on with M-Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fa498-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="fa498-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fa498-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fa498-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fa498-145">**[Maken van een testgebruiker M bestanden](#creating-a-m-files-test-user)**  -toohave een equivalent van Britta Simon in M-bestanden die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="fa498-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - toohave a counterpart of Britta Simon in M-Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fa498-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="fa498-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fa498-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="fa498-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fa498-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="fa498-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fa498-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing M-bestanden.</span><span class="sxs-lookup"><span data-stu-id="fa498-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="fa498-150">**Azure AD tooconfigure eenmalige aanmelding met M-bestanden uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fa498-150">**tooconfigure Azure AD single sign-on with M-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa498-151">In Azure-portal op Hallo Hallo **M bestanden** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="fa498-151">In hello Azure portal, on hello **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="fa498-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="fa498-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="fa498-155">Op Hallo **M bestanden domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fa498-155">On hello **M-Files Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="fa498-157">a.</span><span class="sxs-lookup"><span data-stu-id="fa498-157">a.</span></span> <span data-ttu-id="fa498-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="fa498-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="fa498-159">b.</span><span class="sxs-lookup"><span data-stu-id="fa498-159">b.</span></span> <span data-ttu-id="fa498-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="fa498-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fa498-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="fa498-161">These values are not real.</span></span> <span data-ttu-id="fa498-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="fa498-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fa498-163">Neem contact op met [M bestanden Client ondersteuningsteam](mailto:support@m-files.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="fa498-163">Contact [M-Files Client support team](mailto:support@m-files.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="fa498-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="fa498-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="fa498-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="fa498-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fa498-168">tooget SSO geconfigureerd voor uw toepassing, neem contact op met [M bestanden ondersteuningsteam](mailto:support@m-files.com) en bieden ze Hallo metagegevens gedownload.</span><span class="sxs-lookup"><span data-stu-id="fa498-168">tooget SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them hello downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="fa498-169">Voer Hallo volgende stappen uit als u wilt dat tooconfigure eenmalige aanmelding voor u bureaubladtoepassing M-bestand.</span><span class="sxs-lookup"><span data-stu-id="fa498-169">Follow hello next steps if you want tooconfigure SSO for you M-File desktop application.</span></span> <span data-ttu-id="fa498-170">Er zijn geen extra stappen vereist als u alleen tooconfigure eenmalige aanmelding voor de webversie M-bestanden.</span><span class="sxs-lookup"><span data-stu-id="fa498-170">No extra steps are required if you only want tooconfigure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="fa498-171">Ga als volgt Hallo volgende stappen tooconfigure Hallo M bestand bureaubladtoepassing tooenable eenmalige aanmelding met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa498-171">Follow hello next steps tooconfigure hello M-File desktop application tooenable SSO with Azure AD.</span></span> <span data-ttu-id="fa498-172">toodownload M-bestanden te gaan[M-bestanden downloaden](https://www.m-files.com/en/download-latest-version) pagina.</span><span class="sxs-lookup"><span data-stu-id="fa498-172">toodownload M-Files, go too[M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="fa498-173">Open Hallo **M bestanden bureaublad instellingen** venster.</span><span class="sxs-lookup"><span data-stu-id="fa498-173">Open hello **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="fa498-174">Klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fa498-174">Then, click **Add**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="fa498-176">Op Hallo **Document kluis verbindingseigenschappen** venster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="fa498-176">On hello **Document Vault Connection Properties** window, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="fa498-178">Hallo onder sectie servertype hello, als volgt waarden op:</span><span class="sxs-lookup"><span data-stu-id="fa498-178">Under hello Server section type, hello values as follows:</span></span>  

    <span data-ttu-id="fa498-179">a.</span><span class="sxs-lookup"><span data-stu-id="fa498-179">a.</span></span> <span data-ttu-id="fa498-180">Voor **naam**, type `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="fa498-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="fa498-181">b.</span><span class="sxs-lookup"><span data-stu-id="fa498-181">b.</span></span> <span data-ttu-id="fa498-182">Voor **poortnummer**, type **4466**.</span><span class="sxs-lookup"><span data-stu-id="fa498-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="fa498-183">c.</span><span class="sxs-lookup"><span data-stu-id="fa498-183">c.</span></span> <span data-ttu-id="fa498-184">Voor **Protocol**, selecteer **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="fa498-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="fa498-185">d.</span><span class="sxs-lookup"><span data-stu-id="fa498-185">d.</span></span> <span data-ttu-id="fa498-186">In Hallo **verificatie** optie **specifieke Windows-gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="fa498-186">In hello **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="fa498-187">Vervolgens wordt u gevraagd met een pagina ondertekenen.</span><span class="sxs-lookup"><span data-stu-id="fa498-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="fa498-188">Voeg in uw Azure AD-referenties.</span><span class="sxs-lookup"><span data-stu-id="fa498-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="fa498-189">e.</span><span class="sxs-lookup"><span data-stu-id="fa498-189">e.</span></span> <span data-ttu-id="fa498-190">Voor Hallo **kluis op Server**, selecteer Hallo betreffende kluis op de server.</span><span class="sxs-lookup"><span data-stu-id="fa498-190">For hello **Vault on Server**,  select hello corresponding vault on server.</span></span>
 
    <span data-ttu-id="fa498-191">f.</span><span class="sxs-lookup"><span data-stu-id="fa498-191">f.</span></span> <span data-ttu-id="fa498-192">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa498-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="fa498-193">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="fa498-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fa498-194">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="fa498-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fa498-195">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fa498-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fa498-196">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="fa498-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="fa498-197">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="fa498-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="fa498-199">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fa498-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa498-200">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fa498-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fa498-202">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="fa498-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fa498-204">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="fa498-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fa498-206">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fa498-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fa498-208">a.</span><span class="sxs-lookup"><span data-stu-id="fa498-208">a.</span></span> <span data-ttu-id="fa498-209">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fa498-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fa498-210">b.</span><span class="sxs-lookup"><span data-stu-id="fa498-210">b.</span></span> <span data-ttu-id="fa498-211">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fa498-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fa498-212">c.</span><span class="sxs-lookup"><span data-stu-id="fa498-212">c.</span></span> <span data-ttu-id="fa498-213">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="fa498-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fa498-214">d.</span><span class="sxs-lookup"><span data-stu-id="fa498-214">d.</span></span> <span data-ttu-id="fa498-215">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="fa498-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="fa498-216">Een testgebruiker M-bestanden maken</span><span class="sxs-lookup"><span data-stu-id="fa498-216">Creating a M-Files test user</span></span>

<span data-ttu-id="fa498-217">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in M-bestanden van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="fa498-217">hello objective of this section is toocreate a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="fa498-218">Werken met [M bestanden ondersteuningsteam](mailto:support@m-files.com) tooadd Hallo gebruikers in Hallo M-bestanden.</span><span class="sxs-lookup"><span data-stu-id="fa498-218">Work with  [M-Files support team](mailto:support@m-files.com) tooadd hello users in hello M-Files.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fa498-219">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa498-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fa498-220">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tot tooM-bestanden.</span><span class="sxs-lookup"><span data-stu-id="fa498-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooM-Files.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="fa498-222">**tooassign Britta Simon tooM-bestanden, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fa498-222">**tooassign Britta Simon tooM-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa498-223">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fa498-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="fa498-225">Selecteer in de lijst met de toepassingen van Hallo **M bestanden**.</span><span class="sxs-lookup"><span data-stu-id="fa498-225">In hello applications list, select **M-Files**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="fa498-227">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="fa498-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="fa498-229">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="fa498-229">Click **Add** button.</span></span> <span data-ttu-id="fa498-230">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fa498-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="fa498-232">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa498-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fa498-233">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fa498-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fa498-234">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fa498-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fa498-235">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fa498-235">Testing single sign-on</span></span>

<span data-ttu-id="fa498-236">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="fa498-236">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="fa498-237">Wanneer u klikt op Hallo M-bestanden in Hallo Toegangsvenster tegel, krijgt u de toepassing automatisch aangemelde tooyour M-bestanden.</span><span class="sxs-lookup"><span data-stu-id="fa498-237">When you click hello M-Files tile in hello Access Panel, you should get automatically signed-on tooyour M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fa498-238">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="fa498-238">Additional resources</span></span>

* [<span data-ttu-id="fa498-239">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa498-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fa498-240">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fa498-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

