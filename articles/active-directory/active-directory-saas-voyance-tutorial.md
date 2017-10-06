---
title: 'Zelfstudie: Azure Active Directory-integratie met Voyance | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Voyance.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e2cb9eb6b20e8611a9f6e8529b7c85a8d86ec3e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="f09ee-103">Zelfstudie: Azure Active Directory-integratie met Voyance</span><span class="sxs-lookup"><span data-stu-id="f09ee-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="f09ee-104">In deze zelfstudie leert u hoe toointegrate Voyance met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f09ee-104">In this tutorial, you learn how toointegrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f09ee-105">Voyance integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f09ee-105">Integrating Voyance with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f09ee-106">U kunt beheren in Azure AD die tooVoyance toegang heeft</span><span class="sxs-lookup"><span data-stu-id="f09ee-106">You can control in Azure AD who has access tooVoyance</span></span>
- <span data-ttu-id="f09ee-107">U kunt uw gebruikers tooautomatically get aangemelde tooVoyance (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f09ee-107">You can enable your users tooautomatically get signed-on tooVoyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f09ee-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f09ee-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f09ee-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f09ee-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f09ee-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f09ee-110">Prerequisites</span></span>

<span data-ttu-id="f09ee-111">Azure AD-integratie met Voyance tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="f09ee-111">tooconfigure Azure AD integration with Voyance, you need hello following items:</span></span>

- <span data-ttu-id="f09ee-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f09ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f09ee-113">Een Voyance eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f09ee-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f09ee-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f09ee-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f09ee-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f09ee-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f09ee-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f09ee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f09ee-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f09ee-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f09ee-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f09ee-118">Scenario description</span></span>
<span data-ttu-id="f09ee-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f09ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f09ee-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f09ee-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f09ee-121">Het toevoegen van Voyance van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f09ee-121">Adding Voyance from hello gallery</span></span>
2. <span data-ttu-id="f09ee-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f09ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-hello-gallery"></a><span data-ttu-id="f09ee-123">Het toevoegen van Voyance van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f09ee-123">Adding Voyance from hello gallery</span></span>
<span data-ttu-id="f09ee-124">tooconfigure hello integratie van Voyance in Azure AD, moet u tooadd Voyance uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f09ee-124">tooconfigure hello integration of Voyance into Azure AD, you need tooadd Voyance from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f09ee-125">**tooadd Voyance via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f09ee-125">**tooadd Voyance from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f09ee-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f09ee-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="f09ee-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f09ee-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f09ee-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f09ee-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="f09ee-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f09ee-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="f09ee-133">Typ in het zoekvak Hallo **Voyance**, selecteer **Voyance** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f09ee-133">In hello search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Voyance in de lijst met resultaten Hallo](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f09ee-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="f09ee-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f09ee-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Voyance op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f09ee-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f09ee-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Voyance is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f09ee-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Voyance is tooa user in Azure AD.</span></span> <span data-ttu-id="f09ee-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Voyance toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="f09ee-138">In other words, a link relationship between an Azure AD user and hello related user in Voyance needs toobe established.</span></span>

<span data-ttu-id="f09ee-139">Wijs in Voyance, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="f09ee-139">In Voyance, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f09ee-140">tooconfigure en eenmalige aanmelding Azure AD-test met Voyance, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f09ee-140">tooconfigure and test Azure AD single sign-on with Voyance, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f09ee-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="f09ee-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f09ee-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f09ee-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f09ee-143">**[Maak een testgebruiker Voyance](#create-a-voyance-test-user)**  -toohave een equivalent van Britta Simon in Voyance die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f09ee-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - toohave a counterpart of Britta Simon in Voyance that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f09ee-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f09ee-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f09ee-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f09ee-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f09ee-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f09ee-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f09ee-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Voyance configureren.</span><span class="sxs-lookup"><span data-stu-id="f09ee-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="f09ee-148">**Azure AD tooconfigure eenmalige aanmelding met Voyance, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f09ee-148">**tooconfigure Azure AD single sign-on with Voyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="f09ee-149">In de Azure-portal op Hallo Hallo **Voyance** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f09ee-149">In hello Azure portal, on hello **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f09ee-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f09ee-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="f09ee-153">Op Hallo **Voyance domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="f09ee-153">On hello **Voyance Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Voyance domein en URL's eenmalige aanmelding-informatie voor IDP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="f09ee-155">a.</span><span class="sxs-lookup"><span data-stu-id="f09ee-155">a.</span></span> <span data-ttu-id="f09ee-156">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="f09ee-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="f09ee-157">b.</span><span class="sxs-lookup"><span data-stu-id="f09ee-157">b.</span></span> <span data-ttu-id="f09ee-158">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="f09ee-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="f09ee-159">Controleer **weergeven geavanceerde instellingen voor URL** en uitvoeren van de volgende stap als u wilt dat tooconfigure Hallo toepassing in Hallo **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="f09ee-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Voyance domein en URL's eenmalige aanmelding-informatie voor SP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="f09ee-161">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="f09ee-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="f09ee-162">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="f09ee-162">These values are not real.</span></span> <span data-ttu-id="f09ee-163">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="f09ee-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f09ee-164">Neem contact op met [Voyance Client ondersteuningsteam](mailto:support@nyansa.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="f09ee-164">Contact [Voyance Client support team](mailto:support@nyansa.com) tooget these values.</span></span> 

5. <span data-ttu-id="f09ee-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f09ee-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="f09ee-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f09ee-167">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="f09ee-169">Op Hallo **Voyance configuratie** sectie, klikt u op **configureren Voyance** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f09ee-169">On hello **Voyance Configuration** section, click **Configure Voyance** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f09ee-170">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="f09ee-170">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Voyance configuratie](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="f09ee-172">In een ander browservenster, aanmelding tooyour Voyance tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f09ee-172">In a different web browser window, sign-on tooyour Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="f09ee-173">Ga toohello rechtsboven Hallo navigatiebalk en klik op Hallo vervolgkeuzelijst met de tekst "**Top universiteit**'.</span><span class="sxs-lookup"><span data-stu-id="f09ee-173">Go toohello top right corner of hello navigation bar and click on hello drop-down that says "**Acme University**".</span></span>
    
    ![Eenmalige aanmelding op App aan clientzijde Top universiteit configureren](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="f09ee-175">Klik op '**beheerdersinstellingen**'.</span><span class="sxs-lookup"><span data-stu-id="f09ee-175">Click "**Admin Settings**".</span></span>

    ![Eenmalige aanmelding op App aan clientzijde beheerdersinstellingen configureren](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="f09ee-177">Klik op '**gebruikerstoegang**' tabblad.</span><span class="sxs-lookup"><span data-stu-id="f09ee-177">Click "**User Access**" tab.</span></span>

    ![Eenmalige aanmelding configureren voor toegang voor App-zijde van gebruiker](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="f09ee-179">Klik op Hallo '**SSO is uitgeschakeld**' knop tooconfigure Azure AD als een IdP SAML 2.0 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f09ee-179">Click hello "**SSO is disabled**" button tooconfigure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Configureren van eenmalige aanmelding op App aan clientzijde SSO is uitgeschakeld knop](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="f09ee-181">Ga te**SAML v2** sectie en Voer onderstaande stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f09ee-181">Go too**SAML v2** section and perform below steps:</span></span>

    ![Eenmalige aanmelding configureren op App aan clientzijde SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="f09ee-183">a.</span><span class="sxs-lookup"><span data-stu-id="f09ee-183">a.</span></span> <span data-ttu-id="f09ee-184">Selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="f09ee-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="f09ee-185">b.</span><span class="sxs-lookup"><span data-stu-id="f09ee-185">b.</span></span> <span data-ttu-id="f09ee-186">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd uit hello Azure-portal in Hallo **IdP aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f09ee-186">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal Into hello **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="f09ee-187">c.</span><span class="sxs-lookup"><span data-stu-id="f09ee-187">c.</span></span> <span data-ttu-id="f09ee-188">Het gedownloade Base64-gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **IdP Cert** textbox.</span><span class="sxs-lookup"><span data-stu-id="f09ee-188">Open your downloaded Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="f09ee-189">d.</span><span class="sxs-lookup"><span data-stu-id="f09ee-189">d.</span></span> <span data-ttu-id="f09ee-190">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f09ee-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f09ee-191">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="f09ee-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f09ee-192">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="f09ee-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f09ee-193">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f09ee-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f09ee-194">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f09ee-194">Create an Azure AD test user</span></span>

<span data-ttu-id="f09ee-195">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f09ee-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="f09ee-197">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f09ee-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f09ee-198">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f09ee-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f09ee-200">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f09ee-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f09ee-202">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f09ee-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f09ee-204">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f09ee-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f09ee-206">a.</span><span class="sxs-lookup"><span data-stu-id="f09ee-206">a.</span></span> <span data-ttu-id="f09ee-207">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f09ee-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f09ee-208">b.</span><span class="sxs-lookup"><span data-stu-id="f09ee-208">b.</span></span> <span data-ttu-id="f09ee-209">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f09ee-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f09ee-210">c.</span><span class="sxs-lookup"><span data-stu-id="f09ee-210">c.</span></span> <span data-ttu-id="f09ee-211">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f09ee-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f09ee-212">d.</span><span class="sxs-lookup"><span data-stu-id="f09ee-212">d.</span></span> <span data-ttu-id="f09ee-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f09ee-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="f09ee-214">Een testgebruiker Voyance maken</span><span class="sxs-lookup"><span data-stu-id="f09ee-214">Create a Voyance test user</span></span>

<span data-ttu-id="f09ee-215">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Voyance van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f09ee-215">hello objective of this section is toocreate a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="f09ee-216">Voyance ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f09ee-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="f09ee-217">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="f09ee-217">There is no action item for you in this section.</span></span> <span data-ttu-id="f09ee-218">Een nieuwe gebruiker wordt tijdens een poging tooaccess Voyance gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="f09ee-218">A new user is created during an attempt tooaccess Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="f09ee-219">Als u een gebruiker toocreate handmatig nodig hebt, moet u toocontact [Voyance ondersteuningsteam](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="f09ee-219">If you need toocreate a user manually, you need toocontact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="f09ee-220">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f09ee-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="f09ee-221">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooVoyance toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="f09ee-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVoyance.</span></span>

![Hallo-gebruikersrollen toewijzen][200]

<span data-ttu-id="f09ee-223">**tooassign Britta Simon tooVoyance, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f09ee-223">**tooassign Britta Simon tooVoyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="f09ee-224">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f09ee-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f09ee-226">Selecteer in de lijst met de toepassingen van Hallo **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="f09ee-226">In hello applications list, select **Voyance**.</span></span>

    ![Hallo Voyance koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="f09ee-228">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f09ee-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="f09ee-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f09ee-230">Click **Add** button.</span></span> <span data-ttu-id="f09ee-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f09ee-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="f09ee-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="f09ee-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f09ee-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f09ee-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f09ee-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f09ee-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f09ee-236">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f09ee-236">Test single sign-on</span></span>

<span data-ttu-id="f09ee-237">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="f09ee-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f09ee-238">Als u op Hallo Voyance tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Voyance toepassing.</span><span class="sxs-lookup"><span data-stu-id="f09ee-238">When you click hello Voyance tile in hello Access Panel, you should get automatically signed-on tooyour Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f09ee-239">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f09ee-239">Additional resources</span></span>

* [<span data-ttu-id="f09ee-240">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f09ee-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f09ee-241">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f09ee-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

