---
title: 'Zelfstudie: Azure Active Directory-integratie met voorzijde | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en de voorgrond.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 4be363a3d338ec9268f3324daab4a80346ec3131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="2b16b-103">Zelfstudie: Azure Active Directory-integratie met voorzijde</span><span class="sxs-lookup"><span data-stu-id="2b16b-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="2b16b-104">In deze zelfstudie leert u hoe toointegrate voorzijde met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2b16b-104">In this tutorial, you learn how toointegrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2b16b-105">Begin integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2b16b-105">Integrating Front with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2b16b-106">U kunt beheren in Azure AD die tooFront toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="2b16b-106">You can control in Azure AD who has access tooFront.</span></span>
- <span data-ttu-id="2b16b-107">U kunt uw gebruikers tooautomatically get aangemelde tooFront (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2b16b-107">You can enable your users tooautomatically get signed-on tooFront (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2b16b-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="2b16b-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="2b16b-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2b16b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b16b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2b16b-110">Prerequisites</span></span>

<span data-ttu-id="2b16b-111">tooconfigure Azure AD-integratie met voorgrond, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="2b16b-111">tooconfigure Azure AD integration with Front, you need hello following items:</span></span>

- <span data-ttu-id="2b16b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2b16b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2b16b-113">Een begin eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2b16b-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2b16b-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2b16b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2b16b-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2b16b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2b16b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2b16b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2b16b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b16b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2b16b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2b16b-118">Scenario description</span></span>
<span data-ttu-id="2b16b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2b16b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2b16b-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2b16b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2b16b-121">Het toevoegen van voorzijde van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2b16b-121">Adding Front from hello gallery</span></span>
2. <span data-ttu-id="2b16b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2b16b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-hello-gallery"></a><span data-ttu-id="2b16b-123">Het toevoegen van voorzijde van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2b16b-123">Adding Front from hello gallery</span></span>
<span data-ttu-id="2b16b-124">tooconfigure hello integratie van vooraan in Azure AD, moet u tooadd vooraan in Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2b16b-124">tooconfigure hello integration of Front into Azure AD, you need tooadd Front from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2b16b-125">**tooadd voorzijde via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2b16b-125">**tooadd Front from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b16b-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2b16b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="2b16b-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2b16b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2b16b-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2b16b-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="2b16b-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b16b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="2b16b-133">Typ in het zoekvak Hallo **Front**, selecteer **Front** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2b16b-133">In hello search box, type **Front**, select **Front** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Vooraan in de lijst met resultaten Hallo](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2b16b-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b16b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2b16b-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met voorzijde op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2b16b-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2b16b-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent op de voorgrond is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b16b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Front is tooa user in Azure AD.</span></span> <span data-ttu-id="2b16b-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en het Hallo gerelateerde gebruiker op de voorgrond toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="2b16b-138">In other words, a link relationship between an Azure AD user and hello related user in Front needs toobe established.</span></span>

<span data-ttu-id="2b16b-139">Op de voorgrond, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="2b16b-139">In Front, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2b16b-140">tooconfigure en eenmalige aanmelding Azure AD-test met voorgrond, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2b16b-140">tooconfigure and test Azure AD single sign-on with Front, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2b16b-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="2b16b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2b16b-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2b16b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2b16b-143">**[Maak een testgebruiker voorzijde](#create-a-front-test-user)**  -toohave een equivalent van Britta Simon op de voorgrond is gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2b16b-143">**[Create a Front test user](#create-a-front-test-user)** - toohave a counterpart of Britta Simon in Front that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2b16b-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2b16b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2b16b-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2b16b-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2b16b-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2b16b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2b16b-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing voorgrond.</span><span class="sxs-lookup"><span data-stu-id="2b16b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="2b16b-148">**tooconfigure eenmalige aanmelding Azure AD met voorgrond, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2b16b-148">**tooconfigure Azure AD single sign-on with Front, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b16b-149">In de Azure-portal op Hallo Hallo **Front** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2b16b-149">In hello Azure portal, on hello **Front** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2b16b-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2b16b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="2b16b-153">Op Hallo **Front-domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="2b16b-153">On hello **Front Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="2b16b-155">a.</span><span class="sxs-lookup"><span data-stu-id="2b16b-155">a.</span></span> <span data-ttu-id="2b16b-156">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="2b16b-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="2b16b-157">b.</span><span class="sxs-lookup"><span data-stu-id="2b16b-157">b.</span></span> <span data-ttu-id="2b16b-158">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="2b16b-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="2b16b-159">Controleer **weergeven geavanceerde instellingen voor URL**, indien gewenst tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="2b16b-159">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="2b16b-161">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="2b16b-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2b16b-162">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="2b16b-162">These values are not real.</span></span> <span data-ttu-id="2b16b-163">Deze waarden met Hallo werkelijke id antwoord-URL en aanmeldings-URL die worden beschreven verderop in de zelfstudie of neem contact op met update [Front Client ondersteuningsteam](mailto:support@frontapp.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2b16b-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) tooget these values.</span></span> 

5. <span data-ttu-id="2b16b-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2b16b-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="2b16b-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2b16b-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="2b16b-168">Op Hallo **Front configuratie** sectie, klikt u op **Front configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="2b16b-168">On hello **Front Configuration** section, click **Configure Front** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2b16b-169">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="2b16b-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="2b16b-171">Eenmalige aanmelding tooyour voorzijde tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="2b16b-171">Sign-on tooyour Front tenant as an administrator.</span></span>

9. <span data-ttu-id="2b16b-172">Ga te**instellingen (tandwiel pictogram onderaan Hallo Hallo links zijbalk) > Voorkeuren**.</span><span class="sxs-lookup"><span data-stu-id="2b16b-172">Go too**Settings (cog icon at hello bottom of hello left sidebar) > Preferences**.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="2b16b-174">Klik op **eenmalige aanmelding** koppeling.</span><span class="sxs-lookup"><span data-stu-id="2b16b-174">Click **Single Sign On** link.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="2b16b-176">Selecteer **SAML** in Hallo vervolgkeuzelijst van **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2b16b-176">Select **SAML** in hello drop-down list of **Single Sign On**.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="2b16b-178">In Hallo **toegangspunt** textbox plaatsen Hallo-waarde van **één Service-URL aanmelding** van de configuratiewizard voor Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2b16b-178">In hello **Entry Point** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="2b16b-180">Open uw gedownloade **Certificate(Base64)** -bestand in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **handtekeningcertificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="2b16b-180">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Signing certificate** textbox.</span></span>
    
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="2b16b-182">Op Hallo **Service-Providerinstellingen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2b16b-182">On hello **Service provider settings** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="2b16b-184">a.</span><span class="sxs-lookup"><span data-stu-id="2b16b-184">a.</span></span> <span data-ttu-id="2b16b-185">Hallo-waarde van kopiëren **entiteit-ID** en plak deze in Hallo **id** textbox in **Front-domein en de URL's** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2b16b-185">Copy hello value of **Entity ID** and paste it into hello **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="2b16b-186">b.</span><span class="sxs-lookup"><span data-stu-id="2b16b-186">b.</span></span> <span data-ttu-id="2b16b-187">Hallo-waarde van kopiëren **ACS URL** en plak deze in Hallo **aanmeldings-URL** textbox in **Front-domein en de URL's** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2b16b-187">Copy hello value of **ACS URL** and paste it into hello **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="2b16b-188">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2b16b-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="2b16b-189">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="2b16b-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2b16b-190">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="2b16b-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2b16b-191">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2b16b-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2b16b-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2b16b-192">Create an Azure AD test user</span></span>

<span data-ttu-id="2b16b-193">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2b16b-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="2b16b-195">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2b16b-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b16b-196">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="2b16b-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2b16b-198">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2b16b-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2b16b-200">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b16b-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2b16b-202">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2b16b-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2b16b-204">a.</span><span class="sxs-lookup"><span data-stu-id="2b16b-204">a.</span></span> <span data-ttu-id="2b16b-205">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2b16b-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2b16b-206">b.</span><span class="sxs-lookup"><span data-stu-id="2b16b-206">b.</span></span> <span data-ttu-id="2b16b-207">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="2b16b-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="2b16b-208">c.</span><span class="sxs-lookup"><span data-stu-id="2b16b-208">c.</span></span> <span data-ttu-id="2b16b-209">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="2b16b-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="2b16b-210">d.</span><span class="sxs-lookup"><span data-stu-id="2b16b-210">d.</span></span> <span data-ttu-id="2b16b-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2b16b-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="2b16b-212">Een Front-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2b16b-212">Create a Front test user</span></span>

<span data-ttu-id="2b16b-213">In deze sectie maakt u een gebruiker op de voorgrond Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2b16b-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="2b16b-214">Werken met [Front Client ondersteuningsteam](mailto:support@frontapp.com) Hallo gebruikers toevoegen in Hallo Front-platform.</span><span class="sxs-lookup"><span data-stu-id="2b16b-214">Work with [Front Client support team](mailto:support@frontapp.com) to add hello users in hello Front platform.</span></span> <span data-ttu-id="2b16b-215">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2b16b-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2b16b-216">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b16b-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2b16b-217">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooFront toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="2b16b-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFront.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="2b16b-219">**tooassign Britta Simon tooFront, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2b16b-219">**tooassign Britta Simon tooFront, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b16b-220">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2b16b-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2b16b-222">Selecteer in de lijst met de toepassingen van Hallo **Front**.</span><span class="sxs-lookup"><span data-stu-id="2b16b-222">In hello applications list, select **Front**.</span></span>

    ![Hallo Front-koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="2b16b-224">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2b16b-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="2b16b-226">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2b16b-226">Click **Add** button.</span></span> <span data-ttu-id="2b16b-227">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b16b-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="2b16b-229">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="2b16b-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2b16b-230">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b16b-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2b16b-231">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b16b-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2b16b-232">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2b16b-232">Test single sign-on</span></span>

<span data-ttu-id="2b16b-233">Hallo-doel van deze sectie is tootest uw Azure AD SSOconfiguration met Toegangspaneel Hallo.</span><span class="sxs-lookup"><span data-stu-id="2b16b-233">hello objective of this section is tootest your Azure AD SSOconfiguration using hello Access Panel.</span></span>

<span data-ttu-id="2b16b-234">Als u op Hallo Front-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Front-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2b16b-234">When you click hello Front tile in hello Access Panel, you should get automatically signed-on tooyour Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2b16b-235">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2b16b-235">Additional resources</span></span>

* [<span data-ttu-id="2b16b-236">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b16b-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2b16b-237">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2b16b-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

