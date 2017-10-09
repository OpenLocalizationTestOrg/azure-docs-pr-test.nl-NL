---
title: 'Zelfstudie: Azure Active Directory-integratie met FilesAnywhere | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en FilesAnywhere.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="9b561-103">Zelfstudie: Azure Active Directory-integratie met FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="9b561-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="9b561-104">In deze zelfstudie leert u hoe toointegrate FilesAnywhere met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9b561-104">In this tutorial, you learn how toointegrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9b561-105">FilesAnywhere integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9b561-105">Integrating FilesAnywhere with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9b561-106">U kunt beheren in Azure AD die tooFilesAnywhere toegang heeft</span><span class="sxs-lookup"><span data-stu-id="9b561-106">You can control in Azure AD who has access tooFilesAnywhere</span></span>
- <span data-ttu-id="9b561-107">U kunt uw gebruikers tooautomatically get aangemelde tooFilesAnywhere (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="9b561-107">You can enable your users tooautomatically get signed-on tooFilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9b561-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="9b561-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="9b561-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9b561-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b561-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9b561-110">Prerequisites</span></span>

<span data-ttu-id="9b561-111">Azure AD-integratie met FilesAnywhere tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="9b561-111">tooconfigure Azure AD integration with FilesAnywhere, you need hello following items:</span></span>

- <span data-ttu-id="9b561-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9b561-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9b561-113">Een FilesAnywhere eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="9b561-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="9b561-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="9b561-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="9b561-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="9b561-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9b561-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="9b561-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9b561-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9b561-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="9b561-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="9b561-118">Scenario description</span></span>
<span data-ttu-id="9b561-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="9b561-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9b561-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="9b561-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9b561-121">Het toevoegen van FilesAnywhere van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="9b561-121">Adding FilesAnywhere from hello gallery</span></span>
2. <span data-ttu-id="9b561-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9b561-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-hello-gallery"></a><span data-ttu-id="9b561-123">Het toevoegen van FilesAnywhere van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="9b561-123">Adding FilesAnywhere from hello gallery</span></span>
<span data-ttu-id="9b561-124">tooconfigure hello integratie van FilesAnywhere in Azure AD, moet u tooadd FilesAnywhere uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="9b561-124">tooconfigure hello integration of FilesAnywhere into Azure AD, you need tooadd FilesAnywhere from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9b561-125">**tooadd FilesAnywhere via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9b561-125">**tooadd FilesAnywhere from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b561-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9b561-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9b561-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9b561-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9b561-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9b561-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="9b561-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="9b561-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="9b561-133">Typ in het zoekvak Hallo **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="9b561-133">In hello search box, type **FilesAnywhere**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="9b561-135">Selecteer in het deelvenster resultaten hello, **FilesAnywhere**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="9b561-135">In hello results panel, select **FilesAnywhere**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9b561-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9b561-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9b561-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met FilesAnywhere op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="9b561-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9b561-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in FilesAnywhere is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b561-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FilesAnywhere is tooa user in Azure AD.</span></span> <span data-ttu-id="9b561-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in FilesAnywhere toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="9b561-140">In other words, a link relationship between an Azure AD user and hello related user in FilesAnywhere needs toobe established.</span></span>

<span data-ttu-id="9b561-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="9b561-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="9b561-142">tooconfigure en eenmalige aanmelding Azure AD-test met FilesAnywhere, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9b561-142">tooconfigure and test Azure AD single sign-on with FilesAnywhere, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9b561-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="9b561-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9b561-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b561-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9b561-145">**[Maken van een testgebruiker FilesAnywhere](#creating-a-filesanywhere-test-user)**  -toohave een equivalent van Britta Simon in FilesAnywhere die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="9b561-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - toohave a counterpart of Britta Simon in FilesAnywhere that is linked toohello Azure AD representation of her.</span></span>
3. <span data-ttu-id="9b561-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9b561-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="9b561-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="9b561-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9b561-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9b561-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9b561-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding in uw toepassing FilesAnywhere configureren.</span><span class="sxs-lookup"><span data-stu-id="9b561-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="9b561-150">**Azure AD tooconfigure eenmalige aanmelding met FilesAnywhere, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9b561-150">**tooconfigure Azure AD single sign-on with FilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b561-151">In hello Azure Management portal op Hallo **FilesAnywhere** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="9b561-151">In hello Azure Management portal, on hello **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="9b561-153">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9b561-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="9b561-155">Op Hallo **FilesAnywhere domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP geïnitieerd modus**:</span><span class="sxs-lookup"><span data-stu-id="9b561-155">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="9b561-157">a.</span><span class="sxs-lookup"><span data-stu-id="9b561-157">a.</span></span> <span data-ttu-id="9b561-158">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="9b561-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="9b561-159">Houd er rekening mee dat waarde Hallo **215** is een **clientid** en is slechts een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="9b561-159">Please note that hello value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="9b561-160">U moet tooreplace met Hallo clientid Werkelijke waarde.</span><span class="sxs-lookup"><span data-stu-id="9b561-160">You need tooreplace it with hello actual clientid value.</span></span>

4. <span data-ttu-id="9b561-161">Op Hallo **FilesAnywhere domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **SP geïnitieerd modus**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="9b561-161">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="9b561-163">a.</span><span class="sxs-lookup"><span data-stu-id="9b561-163">a.</span></span> <span data-ttu-id="9b561-164">Klik op Hallo **weergeven geavanceerde instellingen voor URL** optie</span><span class="sxs-lookup"><span data-stu-id="9b561-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="9b561-165">b.</span><span class="sxs-lookup"><span data-stu-id="9b561-165">b.</span></span> <span data-ttu-id="9b561-166">In Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="9b561-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9b561-167">Houd er rekening mee dat deze niet Hallo echte waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="9b561-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="9b561-168">U hebt deze waarden door de werkelijke aanmelding op de URL en de antwoord-URL Hallo tooupdate.</span><span class="sxs-lookup"><span data-stu-id="9b561-168">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="9b561-169">Neem contact op met [FilesAnywhere ondersteuningsteam](mailto:support@FilesAnywhere.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="9b561-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) tooget these values.</span></span> 

5. <span data-ttu-id="9b561-170">Hallo SAML asserties verwacht FilesAnywhere softwaretoepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="9b561-170">FilesAnywhere Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="9b561-171">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="9b561-171">Please configure hello following claims for this application.</span></span> <span data-ttu-id="9b561-172">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="9b561-172">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="9b561-173">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="9b561-173">hello following screenshot shows an example for this.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="9b561-175">Wanneer gebruikers zich up met FilesAnywhere ze Hallo-waarde van krijgen Hallo **clientid** kenmerk uit [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="9b561-175">When hello users signs up with FilesAnywhere they get hello value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="9b561-176">U hebt tooadd Hallo 'Client-Id-kenmerk met Hallo unieke waarde die door FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="9b561-176">You have tooadd hello "Client Id" attribute with hello unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="9b561-177">Alle deze kenmerken die hierboven zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="9b561-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="9b561-178">Houd er rekening mee dat waarde Hallo **. 2331** van **clientid** is slechts een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="9b561-178">Please note that hello value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="9b561-179">U moet tooprovide Hallo werkelijke waarde.</span><span class="sxs-lookup"><span data-stu-id="9b561-179">You need tooprovide hello actual value.</span></span>


6. <span data-ttu-id="9b561-180">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in Hallo afbeelding hierboven en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9b561-180">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="9b561-181">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="9b561-181">Attribute Name</span></span> | <span data-ttu-id="9b561-182">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="9b561-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="9b561-183">clientid</span><span class="sxs-lookup"><span data-stu-id="9b561-183">clientid</span></span> | <span data-ttu-id="9b561-184">*'uniquevalue'*</span><span class="sxs-lookup"><span data-stu-id="9b561-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="9b561-185">a.</span><span class="sxs-lookup"><span data-stu-id="9b561-185">a.</span></span> <span data-ttu-id="9b561-186">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9b561-186">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="9b561-189">b.</span><span class="sxs-lookup"><span data-stu-id="9b561-189">b.</span></span> <span data-ttu-id="9b561-190">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="9b561-190">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="9b561-191">c.</span><span class="sxs-lookup"><span data-stu-id="9b561-191">c.</span></span> <span data-ttu-id="9b561-192">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="9b561-192">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="9b561-193">d.</span><span class="sxs-lookup"><span data-stu-id="9b561-193">d.</span></span> <span data-ttu-id="9b561-194">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="9b561-194">Click **Ok**</span></span>

7. <span data-ttu-id="9b561-195">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="9b561-195">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9b561-197">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9b561-197">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="9b561-199">Op Hallo **FilesAnywhere configuratie** sectie, klikt u op **configureren FilesAnywhere** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="9b561-199">On hello **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** tooopen **Configure sign-on** window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="9b561-202">tooget SSO configuratie voltooid voor uw toepassing aan het einde van FilesAnywhere contact [FilesAnywhere ondersteuningsteam](mailto:support@FilesAnywhere.com) en bieden ze Hallo gedownload ondertekenen certificaat en eenmalige aanmelding op (SSO) de URL van SAML-token.</span><span class="sxs-lookup"><span data-stu-id="9b561-202">tooget SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them hello downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9b561-203">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9b561-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="9b561-204">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9b561-204">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="9b561-206">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9b561-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b561-207">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9b561-207">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9b561-209">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9b561-209">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9b561-211">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9b561-211">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9b561-213">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9b561-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9b561-215">a.</span><span class="sxs-lookup"><span data-stu-id="9b561-215">a.</span></span> <span data-ttu-id="9b561-216">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9b561-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9b561-217">b.</span><span class="sxs-lookup"><span data-stu-id="9b561-217">b.</span></span> <span data-ttu-id="9b561-218">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9b561-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9b561-219">c.</span><span class="sxs-lookup"><span data-stu-id="9b561-219">c.</span></span> <span data-ttu-id="9b561-220">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="9b561-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9b561-221">d.</span><span class="sxs-lookup"><span data-stu-id="9b561-221">d.</span></span> <span data-ttu-id="9b561-222">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9b561-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="9b561-223">Een testgebruiker FilesAnywhere maken</span><span class="sxs-lookup"><span data-stu-id="9b561-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="9b561-224">Toepassing ondersteunt Just in tijd gebruikers inrichten en na verificatie gebruikers wordt in de toepassing hello automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b561-224">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9b561-225">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b561-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9b561-226">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooFilesAnywhere toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="9b561-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFilesAnywhere.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="9b561-228">**tooassign Britta Simon tooFilesAnywhere, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9b561-228">**tooassign Britta Simon tooFilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b561-229">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9b561-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="9b561-231">Selecteer in de lijst met de toepassingen van Hallo **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="9b561-231">In hello applications list, select **FilesAnywhere**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="9b561-233">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="9b561-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="9b561-235">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="9b561-235">Click **Add** button.</span></span> <span data-ttu-id="9b561-236">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9b561-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="9b561-238">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="9b561-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9b561-239">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9b561-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9b561-240">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9b561-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="9b561-241">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9b561-241">Testing single sign-on</span></span>

<span data-ttu-id="9b561-242">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="9b561-242">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9b561-243">Als u op Hallo FilesAnywhere tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour FilesAnywhere toepassing.</span><span class="sxs-lookup"><span data-stu-id="9b561-243">When you click hello FilesAnywhere tile in hello Access Panel, you should get automatically signed-on tooyour FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9b561-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9b561-244">Additional resources</span></span>

* [<span data-ttu-id="9b561-245">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b561-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9b561-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9b561-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
