---
title: 'Zelfstudie: Azure Active Directory-integratie met RFPIO | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en RFPIO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="a456e-103">Zelfstudie: Azure Active Directory-integratie met RFPIO</span><span class="sxs-lookup"><span data-stu-id="a456e-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="a456e-104">In deze zelfstudie leert u hoe toointegrate RFPIO met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a456e-104">In this tutorial, you learn how toointegrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a456e-105">RFPIO integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a456e-105">Integrating RFPIO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a456e-106">U kunt bepalen wie in Azure AD die tooRFPIO toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="a456e-106">You can control who in Azure AD who has access tooRFPIO.</span></span>
- <span data-ttu-id="a456e-107">U kunt uw gebruikers tooautomatically get aangemelde tooRFPIO (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a456e-107">You can enable your users tooautomatically get signed-on tooRFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a456e-108">U kunt uw accounts op één centrale locatie--hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="a456e-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="a456e-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a456e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a456e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a456e-110">Prerequisites</span></span>

<span data-ttu-id="a456e-111">Azure AD-integratie met RFPIO tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="a456e-111">tooconfigure Azure AD integration with RFPIO, you need hello following items:</span></span>

- <span data-ttu-id="a456e-112">Een Azure AD-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a456e-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="a456e-113">Een RFPIO eenmalige aanmelding op ingeschakeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="a456e-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a456e-114">Niet aanbevolen dat u een productie-omgeving tootest Hallo stappen in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a456e-114">We don't recommend that you use a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="a456e-115">tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="a456e-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="a456e-116">Gebruik uw productieomgeving tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a456e-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="a456e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a456e-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a456e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a456e-118">Scenario description</span></span>
<span data-ttu-id="a456e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a456e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a456e-120">Hallo-scenario dat wordt beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a456e-120">hello scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a456e-121">Het toevoegen van RFPIO van Hallo-galerie.</span><span class="sxs-lookup"><span data-stu-id="a456e-121">Adding RFPIO from hello gallery.</span></span>
2. <span data-ttu-id="a456e-122">Configureren en testen van Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a456e-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-hello-gallery"></a><span data-ttu-id="a456e-123">RFPIO van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a456e-123">Add RFPIO from hello gallery</span></span>
<span data-ttu-id="a456e-124">tooconfigure hello integratie van RFPIO in Azure AD, moet u tooadd RFPIO uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a456e-124">tooconfigure hello integration of RFPIO into Azure AD, you need tooadd RFPIO from hello gallery tooyour list of managed SaaS apps.</span></span>

### <a name="tooadd-rfpio-from-hello-gallery"></a><span data-ttu-id="a456e-125">tooadd RFPIO uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a456e-125">tooadd RFPIO from hello gallery</span></span>

1. <span data-ttu-id="a456e-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, op Hallo navigatiedeelvenster links, selecteert u Hallo **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a456e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a456e-128">Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a456e-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a456e-130">tooadd een nieuwe toepassing selecteert Hallo **nieuwe toepassing** knop op Hallo bovenaan in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a456e-130">tooadd a new application, select hello **New application** button on hello top of dialog box.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a456e-132">Typ in het zoekvak Hallo **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="a456e-132">In hello search box, type **RFPIO**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="a456e-134">Selecteer in het deelvenster resultaten hello, **RFPIO**, en selecteer vervolgens Hallo **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a456e-134">In hello results panel, select **RFPIO**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a456e-136">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="a456e-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a456e-137">In deze sectie configureert en test eenmalige aanmelding Azure AD met RFPIO op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a456e-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a456e-138">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo-relatie is tussen de gebruiker die equivalent in RFPIO en een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a456e-138">For single sign-on toowork, Azure AD needs tooknow what hello relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="a456e-139">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in RFPIO toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="a456e-139">In other words, a link relationship between an Azure AD user and hello related user in RFPIO needs toobe established.</span></span>

<span data-ttu-id="a456e-140">Wijs in RFPIO, Hallo-waarde van **gebruikersnaam** in Azure AD als Hallo-waarde van **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="a456e-140">In RFPIO, assign hello value of **user name** in Azure AD as hello value of  **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a456e-141">tooconfigure en eenmalige aanmelding Azure AD-test met RFPIO, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a456e-141">tooconfigure and test Azure AD single sign-on with RFPIO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a456e-142">**[Azure AD eenmalige aanmelding configureren](#configuring-azure-ad-single-sign-on)**--tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="a456e-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a456e-143">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**--tootest eenmalige aanmelding Azure AD met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a456e-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a456e-144">**[Maak een testgebruiker RFPIO](#creating-a-rfpio-test-user)**  --toohave een equivalent van Britta Simon in RFPIO die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a456e-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --toohave a counterpart of Britta Simon in RFPIO that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a456e-145">**[Toewijzen van de testgebruiker hello Azure AD](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a456e-145">**[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a456e-146">**[Test eenmalige aanmelding](#testing-single-sign-on)**  --tooverify als Hallo configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a456e-146">**[Test Single Sign-On](#testing-single-sign-on)** --tooverify if hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a456e-147">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a456e-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a456e-148">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing RFPIO configureren.</span><span class="sxs-lookup"><span data-stu-id="a456e-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="a456e-149">**Azure AD tooconfigure eenmalige aanmelding met RFPIO, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a456e-149">**tooconfigure Azure AD single sign-on with RFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="a456e-150">In de Azure-portal op Hallo Hallo **RFPIO** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a456e-150">In hello Azure portal, on hello **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a456e-152">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a456e-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="a456e-154">Op Hallo **RFPIO domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="a456e-154">On hello **RFPIO Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="a456e-156">a.</span><span class="sxs-lookup"><span data-stu-id="a456e-156">a.</span></span> <span data-ttu-id="a456e-157">In Hallo **id** textbox type Hallo URL:`https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="a456e-157">In hello **Identifier** textbox, type hello URL: `https://www.rfpio.com`</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="a456e-159">b.</span><span class="sxs-lookup"><span data-stu-id="a456e-159">b.</span></span> <span data-ttu-id="a456e-160">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="a456e-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="a456e-161">c.</span><span class="sxs-lookup"><span data-stu-id="a456e-161">c.</span></span> <span data-ttu-id="a456e-162">In Hallo **Relay status** textbox een tekenreekswaarde invoeren.</span><span class="sxs-lookup"><span data-stu-id="a456e-162">In hello **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="a456e-163">Neem contact op met [RFPIO ondersteuningsteam](https://www.rfpio.com/contact/) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="a456e-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) tooget this value.</span></span> 

4. <span data-ttu-id="a456e-164">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="a456e-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="a456e-165">U kunt eventueel tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="a456e-165">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>   

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="a456e-167">In Hallo **aanmelden URL** textbox type Hallo URL:`https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="a456e-167">In hello **Sign on URL** textbox, type hello URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="a456e-168">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a456e-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="a456e-170">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a456e-170">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="a456e-172">In een andere web-browservenster aanmelding toohello **RFPIO** website als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a456e-172">In a different web browser window, login toohello **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="a456e-173">Klik op Hallo onder linkerhoek vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="a456e-173">Click on hello bottom left corner dropdown.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="a456e-175">Klik op Hallo **organisatie-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="a456e-175">Click on hello **Organization Settings**.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="a456e-177">Klik op Hallo **functies & integratie**.</span><span class="sxs-lookup"><span data-stu-id="a456e-177">Click on hello **FEATURES & INTEGRATION**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="a456e-179">In Hallo **SAML-configuratie van SSO** klikt u op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="a456e-179">In hello **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="a456e-181">In deze sectie voert u volgende acties:</span><span class="sxs-lookup"><span data-stu-id="a456e-181">In this Section perform following actions:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="a456e-183">a.</span><span class="sxs-lookup"><span data-stu-id="a456e-183">a.</span></span> <span data-ttu-id="a456e-184">Hallo inhoud Hallo kopiëren **gedownload van metagegevens-XML** en plak deze in Hallo **identiteit configuratie** veld.</span><span class="sxs-lookup"><span data-stu-id="a456e-184">Copy hello content of hello **Downloaded Metadata XML** and paste it into hello **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="a456e-185">toocopy Hallo van inhoud gedownload **Metadata XML** gebruik **Kladblok ++** of de juiste **XML-Editor**.</span><span class="sxs-lookup"><span data-stu-id="a456e-185">toocopy hello content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="a456e-186">b.</span><span class="sxs-lookup"><span data-stu-id="a456e-186">b.</span></span> <span data-ttu-id="a456e-187">Klik op **valideren**.</span><span class="sxs-lookup"><span data-stu-id="a456e-187">Click **Validate**.</span></span>

    <span data-ttu-id="a456e-188">c.</span><span class="sxs-lookup"><span data-stu-id="a456e-188">c.</span></span> <span data-ttu-id="a456e-189">Na klikken **valideren**, spiegelen **SAML(Enabled)** tooon.</span><span class="sxs-lookup"><span data-stu-id="a456e-189">After Clicking **Validate**, Flip **SAML(Enabled)** tooon.</span></span>

    <span data-ttu-id="a456e-190">d.</span><span class="sxs-lookup"><span data-stu-id="a456e-190">d.</span></span> <span data-ttu-id="a456e-191">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="a456e-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="a456e-192">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="a456e-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a456e-193">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="a456e-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a456e-194">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a456e-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a456e-195">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a456e-195">Create an Azure AD test user</span></span>
<span data-ttu-id="a456e-196">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a456e-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a456e-198">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a456e-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a456e-199">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a456e-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a456e-201">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a456e-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a456e-203">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="a456e-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a456e-205">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a456e-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a456e-207">a.</span><span class="sxs-lookup"><span data-stu-id="a456e-207">a.</span></span> <span data-ttu-id="a456e-208">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a456e-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a456e-209">b.</span><span class="sxs-lookup"><span data-stu-id="a456e-209">b.</span></span> <span data-ttu-id="a456e-210">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a456e-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a456e-211">c.</span><span class="sxs-lookup"><span data-stu-id="a456e-211">c.</span></span> <span data-ttu-id="a456e-212">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a456e-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a456e-213">d.</span><span class="sxs-lookup"><span data-stu-id="a456e-213">d.</span></span> <span data-ttu-id="a456e-214">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a456e-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="a456e-215">Een testgebruiker RFPIO maken</span><span class="sxs-lookup"><span data-stu-id="a456e-215">Create a RFPIO test user</span></span>

<span data-ttu-id="a456e-216">Azure AD tooenable gebruikers toolog in tooRFPIO, ze in RFPIO moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="a456e-216">tooenable Azure AD users toolog in tooRFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="a456e-217">In geval van RFPIO Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="a456e-217">In hello case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="a456e-218">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a456e-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a456e-219">Aanmelden tooyour RFPIO bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a456e-219">Log in tooyour RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="a456e-220">Klik op Hallo onder linkerhoek vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="a456e-220">Click on hello bottom left corner dropdown.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="a456e-222">Klik op Hallo **organisatie-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="a456e-222">Click on hello **Organization Settings**.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="a456e-224">Klik op **TEAMLEDEN**.</span><span class="sxs-lookup"><span data-stu-id="a456e-224">Click **TEAM MEMBERS**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="a456e-226">Klik op **leden toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a456e-226">Click on **ADD MEMBERS**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="a456e-228">In Hallo **nieuwe leden toevoegen** sectie.</span><span class="sxs-lookup"><span data-stu-id="a456e-228">In hello **Add New Members** section.</span></span> <span data-ttu-id="a456e-229">Voer de volgende acties:</span><span class="sxs-lookup"><span data-stu-id="a456e-229">Perform following actions:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="a456e-231">a.</span><span class="sxs-lookup"><span data-stu-id="a456e-231">a.</span></span> <span data-ttu-id="a456e-232">Voer **e-mailadres** in Hallo **Voer één e-mailadres per regel** veld.</span><span class="sxs-lookup"><span data-stu-id="a456e-232">Enter **Email address** in hello **Enter one email per line** field.</span></span>

    <span data-ttu-id="a456e-233">b.</span><span class="sxs-lookup"><span data-stu-id="a456e-233">b.</span></span> <span data-ttu-id="a456e-234">Selecteer Plese **rol** volgens uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="a456e-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="a456e-235">c.</span><span class="sxs-lookup"><span data-stu-id="a456e-235">c.</span></span> <span data-ttu-id="a456e-236">Klik op **leden toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a456e-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="a456e-237">Hello Azure Active Directory-accounthouder ontvangt een e-mailbericht en een koppeling tooconfirm volgt hun account voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="a456e-237">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a456e-238">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a456e-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a456e-239">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooRFPIO toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="a456e-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRFPIO.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a456e-241">**tooassign Britta Simon tooRFPIO, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a456e-241">**tooassign Britta Simon tooRFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="a456e-242">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a456e-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a456e-244">Selecteer in de lijst met de toepassingen van Hallo **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="a456e-244">In hello applications list, select **RFPIO**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="a456e-246">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a456e-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a456e-248">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a456e-248">Click **Add** button.</span></span> <span data-ttu-id="a456e-249">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a456e-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a456e-251">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="a456e-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a456e-252">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a456e-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a456e-253">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a456e-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a456e-254">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a456e-254">Test single sign-on</span></span>

<span data-ttu-id="a456e-255">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie testen met behulp van Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="a456e-255">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="a456e-256">Als u op Hallo RFPIO-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour RFPIO toepassing.</span><span class="sxs-lookup"><span data-stu-id="a456e-256">When you click hello RFPIO tile in hello Access Panel, you should get automatically signed-on tooyour RFPIO application.</span></span>
<span data-ttu-id="a456e-257">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a456e-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a456e-258">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a456e-258">Additional resources</span></span>

* [<span data-ttu-id="a456e-259">Lijst met zelfstudies over het toointegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a456e-259">List of tutorials about how toointegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a456e-260">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a456e-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

