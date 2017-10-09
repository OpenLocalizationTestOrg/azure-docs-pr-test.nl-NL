---
title: 'Zelfstudie: Azure Active Directory-integratie met herkennen | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en herkennen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f33fc3959f72f875b8c5c4f0abd4e9b6737ca615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="05425-103">Zelfstudie: Azure Active Directory-integratie met herkennen</span><span class="sxs-lookup"><span data-stu-id="05425-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="05425-104">In deze zelfstudie leert u hoe toointegrate herkennen met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05425-104">In this tutorial, you learn how toointegrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05425-105">Herkennen integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="05425-105">Integrating Recognize with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="05425-106">U kunt beheren in Azure AD die tooRecognize toegang heeft</span><span class="sxs-lookup"><span data-stu-id="05425-106">You can control in Azure AD who has access tooRecognize</span></span>
- <span data-ttu-id="05425-107">U kunt uw gebruikers tooautomatically get aangemelde tooRecognize (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="05425-107">You can enable your users tooautomatically get signed-on tooRecognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="05425-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="05425-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="05425-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="05425-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05425-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="05425-110">Prerequisites</span></span>

<span data-ttu-id="05425-111">tooconfigure Azure AD-integratie met herkennen, moet u de volgende items Hallo:</span><span class="sxs-lookup"><span data-stu-id="05425-111">tooconfigure Azure AD integration with Recognize, you need hello following items:</span></span>

- <span data-ttu-id="05425-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="05425-112">An Azure AD subscription</span></span>
- <span data-ttu-id="05425-113">Een herkennen eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="05425-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="05425-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="05425-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="05425-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="05425-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="05425-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="05425-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="05425-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05425-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="05425-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="05425-118">Scenario description</span></span>
<span data-ttu-id="05425-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="05425-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="05425-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="05425-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05425-121">Het toevoegen van herkennen van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="05425-121">Adding Recognize from hello gallery</span></span>
2. <span data-ttu-id="05425-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="05425-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-hello-gallery"></a><span data-ttu-id="05425-123">Het toevoegen van herkennen van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="05425-123">Adding Recognize from hello gallery</span></span>
<span data-ttu-id="05425-124">tooconfigure hello integratie van herkennen in Azure AD, moet u tooadd herkennen van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="05425-124">tooconfigure hello integration of Recognize into Azure AD, you need tooadd Recognize from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="05425-125">**tooadd herkennen vanuit Hallo-galerie, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="05425-125">**tooadd Recognize from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="05425-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="05425-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="05425-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="05425-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="05425-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="05425-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="05425-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="05425-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="05425-133">Typ in het zoekvak Hallo **herkennen**.</span><span class="sxs-lookup"><span data-stu-id="05425-133">In hello search box, type **Recognize**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="05425-135">Selecteer in het deelvenster resultaten hello, **herkennen**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="05425-135">In hello results panel, select **Recognize**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="05425-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="05425-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="05425-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met herkennen op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="05425-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="05425-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in herkennen is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05425-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Recognize is tooa user in Azure AD.</span></span> <span data-ttu-id="05425-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in herkennen toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="05425-140">In other words, a link relationship between an Azure AD user and hello related user in Recognize needs toobe established.</span></span>

<span data-ttu-id="05425-141">Wijs in herkennen, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="05425-141">In Recognize, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="05425-142">tooconfigure en Azure AD test eenmalige aanmelding bij het herkennen, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="05425-142">tooconfigure and test Azure AD single sign-on with Recognize, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="05425-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="05425-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="05425-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05425-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="05425-145">**[Maken van een testgebruiker herkennen](#creating-a-recognize-test-user)**  -toohave een equivalent van Britta Simon in herkennen die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="05425-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - toohave a counterpart of Britta Simon in Recognize that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="05425-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="05425-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="05425-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="05425-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="05425-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="05425-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="05425-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing herkennen.</span><span class="sxs-lookup"><span data-stu-id="05425-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="05425-150">**Azure AD tooconfigure eenmalige aanmelding met herkennen, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="05425-150">**tooconfigure Azure AD single sign-on with Recognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="05425-151">In de Azure-portal op Hallo Hallo **herkennen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="05425-151">In hello Azure portal, on hello **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="05425-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="05425-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="05425-155">Op Hallo **domein herkennen en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="05425-155">On hello **Recognize Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="05425-157">a.</span><span class="sxs-lookup"><span data-stu-id="05425-157">a.</span></span> <span data-ttu-id="05425-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="05425-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="05425-159">b.</span><span class="sxs-lookup"><span data-stu-id="05425-159">b.</span></span> <span data-ttu-id="05425-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="05425-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="05425-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="05425-161">These values are not real.</span></span> <span data-ttu-id="05425-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="05425-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="05425-163">Neem contact op met [Client herkennen support team](mailto:support@recognizeapp.com) ophalen aanmeldings-URL en u de id-waarde kunt ophalen door het openen van Hallo Service Provider metagegevens-URL van Hallo SSO zoekinstellingen die later in Hallo zelfstudie wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="05425-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening hello Service Provider Metadata URL from hello SSO Settings section that is explained later in hello tutorial.</span></span> <span data-ttu-id="05425-164">.</span><span class="sxs-lookup"><span data-stu-id="05425-164">.</span></span> 
 
4. <span data-ttu-id="05425-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="05425-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="05425-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="05425-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="05425-169">Op Hallo **herkent Configuration** sectie, klikt u op **configureren herkennen** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="05425-169">On hello **Recognize Configuration** section, click **Configure Recognize** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="05425-170">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="05425-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="05425-172">In een ander browservenster, aanmelding tooyour herkennen tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="05425-172">In a different web browser window, sign-on tooyour Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="05425-173">Klik op de rechterbovenhoek Hallo **Menu**.</span><span class="sxs-lookup"><span data-stu-id="05425-173">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="05425-174">Ga te**bedrijf Admin**.</span><span class="sxs-lookup"><span data-stu-id="05425-174">Go too**Company Admin**.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="05425-176">Klik op Hallo navigatiedeelvenster links **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="05425-176">On hello left navigation pane, click **Settings**.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="05425-178">Uitvoeren van de volgende stappen uit op Hallo **SSO instellingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="05425-178">Perform hello following steps on **SSO Settings** section.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="05425-180">a.</span><span class="sxs-lookup"><span data-stu-id="05425-180">a.</span></span> <span data-ttu-id="05425-181">Als **eenmalige aanmelding inschakelen**, selecteer **ON**.</span><span class="sxs-lookup"><span data-stu-id="05425-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="05425-182">b.</span><span class="sxs-lookup"><span data-stu-id="05425-182">b.</span></span> <span data-ttu-id="05425-183">In Hallo **IDP entiteit-ID** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="05425-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="05425-184">c.</span><span class="sxs-lookup"><span data-stu-id="05425-184">c.</span></span> <span data-ttu-id="05425-185">In Hallo **doel-url voor eenmalige aanmelding** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="05425-185">In hello **Sso target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="05425-186">d.</span><span class="sxs-lookup"><span data-stu-id="05425-186">d.</span></span> <span data-ttu-id="05425-187">In Hallo **Slo-doel-url** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="05425-187">In hello **Slo target url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="05425-188">e.</span><span class="sxs-lookup"><span data-stu-id="05425-188">e.</span></span> <span data-ttu-id="05425-189">Open uw gedownloade **certificaat (Base64)** -bestand in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="05425-189">Open your downloaded **Certificate (Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="05425-190">f.</span><span class="sxs-lookup"><span data-stu-id="05425-190">f.</span></span> <span data-ttu-id="05425-191">Klik op Hallo **instellingen opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="05425-191">Click hello **Save settings** button.</span></span> 

11. <span data-ttu-id="05425-192">Naast Hallo **SSO instellingen** sectie, Kopieer de URL Hallo onder **Service Provider metagegevens-url**.</span><span class="sxs-lookup"><span data-stu-id="05425-192">Beside hello **SSO Settings** section, copy hello URL under **Service Provider Metadata url**.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="05425-194">Open Hallo **metagegevens-URL koppeling** onder een lege browser toodownload Hallo-document met metagegevens.</span><span class="sxs-lookup"><span data-stu-id="05425-194">Open hello **Metadata URL link** under a blank browser toodownload hello metadata document.</span></span> <span data-ttu-id="05425-195">Kopieer Hallo EntityDescriptor value(entityID) van Hallo-bestand en plak deze in **id** textbox in **sectie domein herkennen en URL's** op Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="05425-195">Then copy hello EntityDescriptor value(entityID) from hello file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="05425-197">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="05425-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="05425-198">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="05425-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="05425-199">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="05425-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="05425-200">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="05425-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="05425-201">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="05425-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="05425-203">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="05425-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="05425-204">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="05425-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="05425-206">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="05425-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="05425-208">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="05425-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="05425-210">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="05425-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="05425-212">a.</span><span class="sxs-lookup"><span data-stu-id="05425-212">a.</span></span> <span data-ttu-id="05425-213">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05425-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="05425-214">b.</span><span class="sxs-lookup"><span data-stu-id="05425-214">b.</span></span> <span data-ttu-id="05425-215">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="05425-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="05425-216">c.</span><span class="sxs-lookup"><span data-stu-id="05425-216">c.</span></span> <span data-ttu-id="05425-217">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="05425-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="05425-218">d.</span><span class="sxs-lookup"><span data-stu-id="05425-218">d.</span></span> <span data-ttu-id="05425-219">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="05425-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="05425-220">Maken van een testgebruiker herkennen</span><span class="sxs-lookup"><span data-stu-id="05425-220">Creating a Recognize test user</span></span>

<span data-ttu-id="05425-221">In de volgorde tooenable Azure AD gebruikers toolog in herkennen, moeten ze worden ingericht in herkennen.</span><span class="sxs-lookup"><span data-stu-id="05425-221">In order tooenable Azure AD users toolog into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="05425-222">In geval van herkennen Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="05425-222">In hello case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="05425-223">Deze app biedt geen ondersteuning voor het inrichten van SCIM, maar heeft een andere gebruiker synchronisatie die gebruikers richt.</span><span class="sxs-lookup"><span data-stu-id="05425-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="05425-224">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="05425-224">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="05425-225">Meld u aan bij uw bedrijf herkennen site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="05425-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="05425-226">Klik op de rechterbovenhoek Hallo **Menu**.</span><span class="sxs-lookup"><span data-stu-id="05425-226">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="05425-227">Ga te**bedrijf Admin**.</span><span class="sxs-lookup"><span data-stu-id="05425-227">Go too**Company Admin**.</span></span>

3. <span data-ttu-id="05425-228">Klik op Hallo navigatiedeelvenster links **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="05425-228">On hello left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="05425-229">Uitvoeren van de volgende stappen uit op Hallo **gebruiker Sync** sectie.</span><span class="sxs-lookup"><span data-stu-id="05425-229">Perform hello following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="05425-230">![Nieuwe gebruiker](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="05425-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="05425-231">a.</span><span class="sxs-lookup"><span data-stu-id="05425-231">a.</span></span> <span data-ttu-id="05425-232">Als **synchroniseren ingeschakeld**, selecteer **ON**.</span><span class="sxs-lookup"><span data-stu-id="05425-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="05425-233">b.</span><span class="sxs-lookup"><span data-stu-id="05425-233">b.</span></span> <span data-ttu-id="05425-234">Als **Kies sync provider**, selecteer **Microsoft / Office 365**.</span><span class="sxs-lookup"><span data-stu-id="05425-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="05425-235">c.</span><span class="sxs-lookup"><span data-stu-id="05425-235">c.</span></span> <span data-ttu-id="05425-236">Klik op **Voer gebruiker synchronisatie**.</span><span class="sxs-lookup"><span data-stu-id="05425-236">Click **Run User Sync**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="05425-237">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="05425-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="05425-238">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooRecognize toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="05425-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRecognize.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="05425-240">**tooassign Britta Simon tooRecognize, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="05425-240">**tooassign Britta Simon tooRecognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="05425-241">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="05425-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="05425-243">Selecteer in de lijst met de toepassingen van Hallo **herkennen**.</span><span class="sxs-lookup"><span data-stu-id="05425-243">In hello applications list, select **Recognize**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="05425-245">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="05425-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="05425-247">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="05425-247">Click **Add** button.</span></span> <span data-ttu-id="05425-248">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="05425-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="05425-250">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="05425-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="05425-251">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="05425-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="05425-252">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="05425-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="05425-253">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="05425-253">Testing single sign-on</span></span>

<span data-ttu-id="05425-254">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="05425-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="05425-255">Als u op Hallo herkennen tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour herkennen toepassing.</span><span class="sxs-lookup"><span data-stu-id="05425-255">When you click hello Recognize tile in hello Access Panel, you should get automatically signed-on tooyour Recognize application.</span></span> <span data-ttu-id="05425-256">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="05425-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="05425-257">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="05425-257">Additional resources</span></span>

* [<span data-ttu-id="05425-258">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05425-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05425-259">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="05425-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

