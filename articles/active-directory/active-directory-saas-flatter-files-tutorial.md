---
title: 'Zelfstudie: Azure Active Directory-integratie met houden bestanden | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en houden bestanden.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 73ca2613b7bbaf9992ecf624ff5defabaa44f7a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="3ebd0-103">Zelfstudie: Azure Active Directory-integratie met houden bestanden</span><span class="sxs-lookup"><span data-stu-id="3ebd0-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="3ebd0-104">In deze zelfstudie leert u hoe toointegrate houden bestanden met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3ebd0-104">In this tutorial, you learn how toointegrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ebd0-105">Houden bestanden integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3ebd0-105">Integrating Flatter Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3ebd0-106">U kunt beheren in Azure AD die toegang heeft tooFlatter bestanden</span><span class="sxs-lookup"><span data-stu-id="3ebd0-106">You can control in Azure AD who has access tooFlatter Files</span></span>
- <span data-ttu-id="3ebd0-107">U kunt uw gebruikers tooautomatically inschakelen aangemelde tooFlatter-bestanden (Single Sign-On) met hun Azure AD-account ophalen</span><span class="sxs-lookup"><span data-stu-id="3ebd0-107">You can enable your users tooautomatically get signed-on tooFlatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3ebd0-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="3ebd0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3ebd0-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3ebd0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ebd0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3ebd0-110">Prerequisites</span></span>

<span data-ttu-id="3ebd0-111">Azure AD-integratie met houden bestanden tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="3ebd0-111">tooconfigure Azure AD integration with Flatter Files, you need hello following items:</span></span>

- <span data-ttu-id="3ebd0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3ebd0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3ebd0-113">Een houden bestanden eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3ebd0-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ebd0-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ebd0-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3ebd0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ebd0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ebd0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ebd0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ebd0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3ebd0-118">Scenario description</span></span>
<span data-ttu-id="3ebd0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ebd0-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3ebd0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ebd0-121">Houden bestanden uit de galerie Hallo toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-121">Adding Flatter Files from hello gallery</span></span>
2. <span data-ttu-id="3ebd0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3ebd0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-hello-gallery"></a><span data-ttu-id="3ebd0-123">Houden bestanden uit de galerie Hallo toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-123">Adding Flatter Files from hello gallery</span></span>
<span data-ttu-id="3ebd0-124">tooconfigure hello integratie van houden bestanden met Azure AD, moet u tooadd houden bestanden uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-124">tooconfigure hello integration of Flatter Files into Azure AD, you need tooadd Flatter Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3ebd0-125">**tooadd houden bestanden uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3ebd0-125">**tooadd Flatter Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ebd0-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3ebd0-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3ebd0-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="3ebd0-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="3ebd0-133">Typ in het zoekvak Hallo **houden bestanden**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-133">In hello search box, type **Flatter Files**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="3ebd0-135">Selecteer in het deelvenster resultaten hello, **houden bestanden**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-135">In hello results panel, select **Flatter Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3ebd0-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3ebd0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3ebd0-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met houden bestanden op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3ebd0-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in houden bestanden is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Flatter Files is tooa user in Azure AD.</span></span> <span data-ttu-id="3ebd0-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in houden bestanden toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-140">In other words, a link relationship between an Azure AD user and hello related user in Flatter Files needs toobe established.</span></span>

<span data-ttu-id="3ebd0-141">In houden bestanden, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-141">In Flatter Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3ebd0-142">tooconfigure en test eenmalige aanmelding Azure AD met houden bestanden, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3ebd0-142">tooconfigure and test Azure AD single sign-on with Flatter Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3ebd0-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3ebd0-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3ebd0-145">**[Maken van een testgebruiker houden bestanden](#creating-a-flatter-files-test-user)**  -toohave een equivalent van Britta Simon in houden bestanden die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - toohave a counterpart of Britta Simon in Flatter Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3ebd0-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3ebd0-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3ebd0-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3ebd0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3ebd0-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing houden bestanden.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="3ebd0-150">**Voer tooconfigure Azure AD eenmalige aanmelding met houden bestanden Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3ebd0-150">**tooconfigure Azure AD single sign-on with Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ebd0-151">In de Azure-portal op Hallo Hallo **houden bestanden** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-151">In hello Azure portal, on hello **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3ebd0-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="3ebd0-155">Op Hallo **houden bestanden domein en de URL's** sectie, hello gebruiker beschikt niet over tooperform eventuele stappen zoals Hallo app al vooraf is geïntegreerd met Azure.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-155">On hello **Flatter Files Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="3ebd0-157">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="3ebd0-159">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-159">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3ebd0-161">Op Hallo **houden bestanden configuratie** sectie, klikt u op **houden bestanden configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-161">On hello **Flatter Files Configuration** section, click **Configure Flatter Files** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3ebd0-162">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="3ebd0-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="3ebd0-164">Eenmalige aanmelding tooyour houden bestanden toepassing als beheerder.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-164">Sign-on tooyour Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="3ebd0-165">Klik op **DASHBOARD**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-165">Click **DASHBOARD**.</span></span> 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="3ebd0-167">Klik op **instellingen**, en voer de volgende stappen uit op Hallo Hallo **bedrijf** tabblad:</span><span class="sxs-lookup"><span data-stu-id="3ebd0-167">Click **Settings**, and then perform hello following steps on hello **Company** tab:</span></span> 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="3ebd0-169">a.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-169">a.</span></span> <span data-ttu-id="3ebd0-170">Selecteer **SAML 2.0 gebruiken voor verificatie**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="3ebd0-171">b.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-171">b.</span></span> <span data-ttu-id="3ebd0-172">Klik op **SAML configureren**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="3ebd0-173">Op Hallo **SAML-configuratie** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="3ebd0-173">On hello **SAML Configuration** dialog, perform hello following steps:</span></span> 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="3ebd0-175">a.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-175">a.</span></span> <span data-ttu-id="3ebd0-176">In Hallo **domein** textbox het geregistreerde domein opgeven.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-176">In hello **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="3ebd0-177">Als u een geregistreerde domeinnaam nog contact op met hebt uw houden bestanden ondersteuningsteam via [ support@flatterfiles.com ](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="3ebd0-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="3ebd0-178">b.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-178">b.</span></span> <span data-ttu-id="3ebd0-179">In **identiteit Provider URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vormen van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-179">In **Identity Provider URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="3ebd0-180">c.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-180">c.</span></span>  <span data-ttu-id="3ebd0-181">De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **Provider identiteitscertificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-181">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="3ebd0-182">d.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-182">d.</span></span> <span data-ttu-id="3ebd0-183">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="3ebd0-184">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3ebd0-185">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3ebd0-186">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3ebd0-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3ebd0-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3ebd0-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="3ebd0-188">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="3ebd0-190">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3ebd0-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ebd0-191">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3ebd0-193">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3ebd0-195">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3ebd0-197">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3ebd0-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3ebd0-199">a.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-199">a.</span></span> <span data-ttu-id="3ebd0-200">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ebd0-201">b.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-201">b.</span></span> <span data-ttu-id="3ebd0-202">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3ebd0-203">c.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-203">c.</span></span> <span data-ttu-id="3ebd0-204">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3ebd0-205">d.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-205">d.</span></span> <span data-ttu-id="3ebd0-206">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="3ebd0-207">Een testgebruiker houden bestanden maken</span><span class="sxs-lookup"><span data-stu-id="3ebd0-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="3ebd0-208">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in houden bestanden van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-208">hello objective of this section is toocreate a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="3ebd0-209">**toocreate Britta Simon aangeroepen in houden bestanden van een gebruiker uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3ebd0-209">**toocreate a user called Britta Simon in Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ebd0-210">Meld u aan bij tooyour **houden bestanden** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-210">Sign on tooyour **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="3ebd0-211">Klik in het navigatievenster aan de linkerkant Hallo Hallo op **instellingen**, en klik vervolgens op Hallo **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-211">In hello navigation pane on hello left, click **Settings**, and then click hello **Users** tab.</span></span>
   
    ![Een gebruiker met houden bestanden maken](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="3ebd0-213">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="3ebd0-214">Op Hallo **gebruiker toevoegen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="3ebd0-214">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    ![Een gebruiker met houden bestanden maken](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="3ebd0-216">a.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-216">a.</span></span> <span data-ttu-id="3ebd0-217">In Hallo **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-217">In hello **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="3ebd0-218">b.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-218">b.</span></span> <span data-ttu-id="3ebd0-219">In Hallo **achternaam** textbox type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-219">In hello **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="3ebd0-220">c.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-220">c.</span></span> <span data-ttu-id="3ebd0-221">In Hallo **e-mailadres** textbox Britta van e-mailadres typt in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-221">In hello **Email Address** textbox, type Britta's email address in hello Azure portal.</span></span>
   
    <span data-ttu-id="3ebd0-222">d.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-222">d.</span></span> <span data-ttu-id="3ebd0-223">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-223">Click **Submit**.</span></span>   


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3ebd0-224">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ebd0-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3ebd0-225">In deze sectie, schakelt u Britta Simon toouse Azure eenmalige aanmelding verleent toegang tot tooFlatter bestanden.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFlatter Files.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3ebd0-227">**tooassign Britta Simon tooFlatter bestanden, Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3ebd0-227">**tooassign Britta Simon tooFlatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ebd0-228">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3ebd0-230">Selecteer in de lijst met de toepassingen van Hallo **houden bestanden**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-230">In hello applications list, select **Flatter Files**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="3ebd0-232">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="3ebd0-234">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-234">Click **Add** button.</span></span> <span data-ttu-id="3ebd0-235">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="3ebd0-237">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3ebd0-238">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3ebd0-239">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3ebd0-240">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3ebd0-240">Testing single sign-on</span></span>

<span data-ttu-id="3ebd0-241">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3ebd0-242">Als u op Hallo houden bestanden-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour houden bestanden toepassing.</span><span class="sxs-lookup"><span data-stu-id="3ebd0-242">When you click hello Flatter Files tile in hello Access Panel, you should get automatically signed-on tooyour Flatter Files application.</span></span>
<span data-ttu-id="3ebd0-243">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3ebd0-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3ebd0-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3ebd0-244">Additional resources</span></span>

* [<span data-ttu-id="3ebd0-245">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ebd0-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3ebd0-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3ebd0-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

