---
title: 'Zelfstudie: Azure Active Directory-integratie met Inzoomen | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory- en uitzoomen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 623a1f428ad1f0aa2c8205b79d61720cad5fc6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="c8821-103">Zelfstudie: Azure Active Directory-integratie met zoomen</span><span class="sxs-lookup"><span data-stu-id="c8821-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="c8821-104">In deze zelfstudie leert u hoe toointegrate zoomen met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c8821-104">In this tutorial, you learn how toointegrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c8821-105">Inzoomen integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c8821-105">Integrating Zoom with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c8821-106">U kunt beheren in Azure AD die tooZoom toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="c8821-106">You can control in Azure AD who has access tooZoom.</span></span>
- <span data-ttu-id="c8821-107">U kunt uw gebruikers tooautomatically get aangemelde tooZoom (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c8821-107">You can enable your users tooautomatically get signed-on tooZoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c8821-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="c8821-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="c8821-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c8821-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8821-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c8821-110">Prerequisites</span></span>

<span data-ttu-id="c8821-111">tooconfigure Azure AD-integratie met inzoomen, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="c8821-111">tooconfigure Azure AD integration with Zoom, you need hello following items:</span></span>

- <span data-ttu-id="c8821-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c8821-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c8821-113">Een zoomen eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c8821-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c8821-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c8821-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c8821-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c8821-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c8821-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c8821-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c8821-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c8821-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c8821-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c8821-118">Scenario description</span></span>
<span data-ttu-id="c8821-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c8821-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c8821-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c8821-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c8821-121">Het toevoegen van zoomniveau van Hallo galerie</span><span class="sxs-lookup"><span data-stu-id="c8821-121">Adding Zoom from hello gallery</span></span>
2. <span data-ttu-id="c8821-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c8821-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-hello-gallery"></a><span data-ttu-id="c8821-123">Het toevoegen van zoomniveau van Hallo galerie</span><span class="sxs-lookup"><span data-stu-id="c8821-123">Adding Zoom from hello gallery</span></span>
<span data-ttu-id="c8821-124">Hallo-integratie tooconfigure zoompercentage met Azure AD, moet u tooadd zoomen uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c8821-124">tooconfigure hello integration of Zoom into Azure AD, you need tooadd Zoom from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c8821-125">**tooadd zoomen via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c8821-125">**tooadd Zoom from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8821-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c8821-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="c8821-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c8821-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c8821-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c8821-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="c8821-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c8821-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="c8821-133">Typ in het zoekvak Hallo **zoomen**, selecteer **zoomen** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c8821-133">In hello search box, type **Zoom**, select **Zoom** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lijst met resultaten Hallo Inzoomen](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c8821-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8821-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c8821-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Inzoomen op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="c8821-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c8821-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in zoomen is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8821-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoom is tooa user in Azure AD.</span></span> <span data-ttu-id="c8821-138">Met andere woorden, een relatie koppeling tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in zoomen behoeften toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="c8821-138">In other words, a link relationship between an Azure AD user and hello related user in Zoom needs toobe established.</span></span>

<span data-ttu-id="c8821-139">In zoomen, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="c8821-139">In Zoom, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c8821-140">tooconfigure en eenmalige aanmelding Azure AD-test met inzoomen, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c8821-140">tooconfigure and test Azure AD single sign-on with Zoom, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c8821-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="c8821-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c8821-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c8821-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c8821-143">**[Maak een testgebruiker zoomen](#create-a-zoom-test-user)**  -toohave een equivalent van Britta Simon in zoomen die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c8821-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - toohave a counterpart of Britta Simon in Zoom that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c8821-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c8821-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c8821-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c8821-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c8821-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c8821-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c8821-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Zoom.</span><span class="sxs-lookup"><span data-stu-id="c8821-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="c8821-148">**tooconfigure eenmalige aanmelding Azure AD met inzoomen, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c8821-148">**tooconfigure Azure AD single sign-on with Zoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8821-149">In de Azure-portal op Hallo Hallo **zoomen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c8821-149">In hello Azure portal, on hello **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c8821-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c8821-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="c8821-153">Op Hallo **domein zoomen en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c8821-153">On hello **Zoom Domain and URLs** section, perform hello following steps:</span></span>

    ![Domein- en URL's eenmalige aanmelding informatie zoomen](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="c8821-155">a.</span><span class="sxs-lookup"><span data-stu-id="c8821-155">a.</span></span> <span data-ttu-id="c8821-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="c8821-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="c8821-157">b.</span><span class="sxs-lookup"><span data-stu-id="c8821-157">b.</span></span> <span data-ttu-id="c8821-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="c8821-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c8821-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c8821-159">These values are not real.</span></span> <span data-ttu-id="c8821-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="c8821-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c8821-161">Neem contact op met [Client zoomen ondersteuningsteam](https://support.zoom.us/hc) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="c8821-161">Contact [Zoom Client support team](https://support.zoom.us/hc) tooget these values.</span></span> 
 
4. <span data-ttu-id="c8821-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c8821-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="c8821-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c8821-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c8821-166">Op Hallo **zoomen configuratie** sectie, klikt u op **configureren zoomen** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="c8821-166">On hello **Zoom Configuration** section, click **Configure Zoom** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c8821-167">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="c8821-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Inzoomen-configuratie](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="c8821-169">In een ander browservenster, meld u aan tooyour zoomen bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="c8821-169">In a different web browser window, log in tooyour Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="c8821-170">Klik op Hallo **Single Sign-On** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c8821-170">Click hello **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="c8821-171">![Eenmalige aanmelding op het tabblad](./media/active-directory-saas-zoom-tutorial/IC784700.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="c8821-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="c8821-172">Klik op Hallo **beveiligingscontrole** tabblad en gaat u toohello **Single Sign-On** instellingen.</span><span class="sxs-lookup"><span data-stu-id="c8821-172">Click hello **Security Control** tab, and then go toohello **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="c8821-173">Voer in Hallo Single Sign-On sectie, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c8821-173">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c8821-174">![Eenmalige aanmelding sectie](./media/active-directory-saas-zoom-tutorial/IC784701.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="c8821-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="c8821-175">a.</span><span class="sxs-lookup"><span data-stu-id="c8821-175">a.</span></span> <span data-ttu-id="c8821-176">In Hallo **aanmelden pagina-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c8821-176">In hello **Sign-in page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="c8821-177">b.</span><span class="sxs-lookup"><span data-stu-id="c8821-177">b.</span></span> <span data-ttu-id="c8821-178">In Hallo **afmelden pagina-URL** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c8821-178">In hello **Sign-out page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="c8821-179">c.</span><span class="sxs-lookup"><span data-stu-id="c8821-179">c.</span></span> <span data-ttu-id="c8821-180">De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **provider identiteitscertificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="c8821-180">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="c8821-181">d.</span><span class="sxs-lookup"><span data-stu-id="c8821-181">d.</span></span> <span data-ttu-id="c8821-182">In Hallo **verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c8821-182">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="c8821-183">e.</span><span class="sxs-lookup"><span data-stu-id="c8821-183">e.</span></span> <span data-ttu-id="c8821-184">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c8821-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c8821-185">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="c8821-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c8821-186">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="c8821-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c8821-187">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c8821-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c8821-188">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c8821-188">Create an Azure AD test user</span></span>

<span data-ttu-id="c8821-189">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c8821-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="c8821-191">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c8821-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8821-192">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="c8821-192">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c8821-194">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c8821-194">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c8821-196">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c8821-196">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c8821-198">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c8821-198">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c8821-200">a.</span><span class="sxs-lookup"><span data-stu-id="c8821-200">a.</span></span> <span data-ttu-id="c8821-201">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c8821-201">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c8821-202">b.</span><span class="sxs-lookup"><span data-stu-id="c8821-202">b.</span></span> <span data-ttu-id="c8821-203">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="c8821-203">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="c8821-204">c.</span><span class="sxs-lookup"><span data-stu-id="c8821-204">c.</span></span> <span data-ttu-id="c8821-205">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="c8821-205">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="c8821-206">d.</span><span class="sxs-lookup"><span data-stu-id="c8821-206">d.</span></span> <span data-ttu-id="c8821-207">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c8821-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="c8821-208">Maak een testgebruiker zoomen</span><span class="sxs-lookup"><span data-stu-id="c8821-208">Create a Zoom test user</span></span>

<span data-ttu-id="c8821-209">In volgorde tooenable Azure AD gebruikers toolog in tooZoom, moeten ze worden ingericht in zoomen.</span><span class="sxs-lookup"><span data-stu-id="c8821-209">In order tooenable Azure AD users toolog in tooZoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="c8821-210">In geval van zoomen Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="c8821-210">In hello case of Zoom, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="c8821-211">een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c8821-211">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="c8821-212">Meld u bij tooyour **zoomen** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c8821-212">Log in tooyour **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="c8821-213">Klik op Hallo **accountbeheer** tabblad en klik vervolgens op **Gebruikersbeheer**.</span><span class="sxs-lookup"><span data-stu-id="c8821-213">Click hello **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="c8821-214">Klik in de sectie beheer van de gebruiker Hallo, op **gebruikers toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c8821-214">In hello User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="c8821-215">![Gebruikersbeheer](./media/active-directory-saas-zoom-tutorial/IC784703.png "Gebruikersbeheer")</span><span class="sxs-lookup"><span data-stu-id="c8821-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="c8821-216">Op Hallo **gebruikers toevoegen** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c8821-216">On hello **Add users** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="c8821-217">![Gebruikers toevoegen](./media/active-directory-saas-zoom-tutorial/IC784704.png "gebruikers toevoegen")</span><span class="sxs-lookup"><span data-stu-id="c8821-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="c8821-218">a.</span><span class="sxs-lookup"><span data-stu-id="c8821-218">a.</span></span> <span data-ttu-id="c8821-219">Als **gebruikerstype**, selecteer **Basic**.</span><span class="sxs-lookup"><span data-stu-id="c8821-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="c8821-220">b.</span><span class="sxs-lookup"><span data-stu-id="c8821-220">b.</span></span> <span data-ttu-id="c8821-221">In Hallo **e-mailberichten** textbox type Hallo e-mailadres van een geldig Azure AD-account die u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="c8821-221">In hello **Emails** textbox, type hello email address of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="c8821-222">c.</span><span class="sxs-lookup"><span data-stu-id="c8821-222">c.</span></span> <span data-ttu-id="c8821-223">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="c8821-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="c8821-224">U kunt andere zoomen gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door zoomen tooprovision Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="c8821-224">You can use any other Zoom user account creation tools or APIs provided by Zoom tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c8821-225">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8821-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c8821-226">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooZoom toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="c8821-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoom.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="c8821-228">**tooassign Britta Simon tooZoom, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c8821-228">**tooassign Britta Simon tooZoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8821-229">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c8821-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c8821-231">Selecteer in de lijst met de toepassingen van Hallo **zoomen**.</span><span class="sxs-lookup"><span data-stu-id="c8821-231">In hello applications list, select **Zoom**.</span></span>

    ![Hallo zoomen koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="c8821-233">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c8821-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="c8821-235">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c8821-235">Click **Add** button.</span></span> <span data-ttu-id="c8821-236">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c8821-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="c8821-238">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="c8821-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c8821-239">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c8821-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c8821-240">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c8821-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c8821-241">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c8821-241">Test single sign-on</span></span>

<span data-ttu-id="c8821-242">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="c8821-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c8821-243">Als u op Hallo zoomen tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour zoomen toepassing.</span><span class="sxs-lookup"><span data-stu-id="c8821-243">When you click hello Zoom tile in hello Access Panel, you should get automatically signed-on tooyour Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c8821-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c8821-244">Additional resources</span></span>

* [<span data-ttu-id="c8821-245">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c8821-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c8821-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c8821-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

