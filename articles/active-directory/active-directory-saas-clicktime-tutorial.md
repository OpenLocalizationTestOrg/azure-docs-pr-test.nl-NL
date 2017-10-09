---
title: 'Zelfstudie: Azure Active Directory-integratie met ClickTime | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ClickTime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: a0259e31164cad6c6c77ed8aac1c50cd9a3e46ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="6e7ea-103">Zelfstudie: Azure Active Directory-integratie met ClickTime</span><span class="sxs-lookup"><span data-stu-id="6e7ea-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="6e7ea-104">In deze zelfstudie leert u hoe toointegrate ClickTime met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6e7ea-104">In this tutorial, you learn how toointegrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e7ea-105">ClickTime integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6e7ea-105">Integrating ClickTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6e7ea-106">U kunt beheren in Azure AD die tooClickTime toegang heeft</span><span class="sxs-lookup"><span data-stu-id="6e7ea-106">You can control in Azure AD who has access tooClickTime</span></span>
- <span data-ttu-id="6e7ea-107">U kunt uw gebruikers tooautomatically get aangemelde tooClickTime (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6e7ea-107">You can enable your users tooautomatically get signed-on tooClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6e7ea-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6e7ea-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6e7ea-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6e7ea-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e7ea-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6e7ea-110">Prerequisites</span></span>

<span data-ttu-id="6e7ea-111">Azure AD-integratie met ClickTime tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="6e7ea-111">tooconfigure Azure AD integration with ClickTime, you need hello following items:</span></span>

- <span data-ttu-id="6e7ea-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6e7ea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e7ea-113">Een ClickTime eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6e7ea-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e7ea-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e7ea-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6e7ea-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e7ea-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e7ea-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e7ea-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e7ea-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6e7ea-118">Scenario description</span></span>
<span data-ttu-id="6e7ea-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e7ea-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6e7ea-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e7ea-121">Het toevoegen van ClickTime van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="6e7ea-121">Adding ClickTime from hello gallery</span></span>
2. <span data-ttu-id="6e7ea-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6e7ea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-hello-gallery"></a><span data-ttu-id="6e7ea-123">Het toevoegen van ClickTime van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="6e7ea-123">Adding ClickTime from hello gallery</span></span>
<span data-ttu-id="6e7ea-124">tooconfigure hello integratie van ClickTime in Azure AD, moet u tooadd ClickTime uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-124">tooconfigure hello integration of ClickTime into Azure AD, you need tooadd ClickTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6e7ea-125">**tooadd ClickTime via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6e7ea-125">**tooadd ClickTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e7ea-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="6e7ea-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6e7ea-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="6e7ea-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="6e7ea-133">Typ in het zoekvak Hallo **ClickTime**, selecteer **ClickTime** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-133">In hello search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ClickTime in de lijst met resultaten Hallo](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6e7ea-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e7ea-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6e7ea-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met ClickTime op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6e7ea-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ClickTime is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ClickTime is tooa user in Azure AD.</span></span> <span data-ttu-id="6e7ea-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in ClickTime toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-138">In other words, a link relationship between an Azure AD user and hello related user in ClickTime needs toobe established.</span></span>

<span data-ttu-id="6e7ea-139">Wijs in ClickTime, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-139">In ClickTime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6e7ea-140">tooconfigure en eenmalige aanmelding Azure AD-test met ClickTime, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e7ea-140">tooconfigure and test Azure AD single sign-on with ClickTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6e7ea-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6e7ea-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6e7ea-143">**[Maak een testgebruiker ClickTime](#create-a-clicktime-test-user)**  -toohave een equivalent van Britta Simon in ClickTime die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - toohave a counterpart of Britta Simon in ClickTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6e7ea-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6e7ea-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6e7ea-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6e7ea-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6e7ea-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing ClickTime configureren.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="6e7ea-148">**Azure AD tooconfigure eenmalige aanmelding met ClickTime, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6e7ea-148">**tooconfigure Azure AD single sign-on with ClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e7ea-149">In de Azure-portal op Hallo Hallo **ClickTime** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-149">In hello Azure portal, on hello **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6e7ea-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="6e7ea-153">Op Hallo **ClickTime domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e7ea-153">On hello **ClickTime Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en ClickTime domein eenmalige aanmelding informatie](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="6e7ea-155">a.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-155">a.</span></span> <span data-ttu-id="6e7ea-156">In Hallo **id** textbox, typ een URL als:`https://app.clicktime.com/sp/`</span><span class="sxs-lookup"><span data-stu-id="6e7ea-156">In hello **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="6e7ea-157">b.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-157">b.</span></span> <span data-ttu-id="6e7ea-158">In Hallo **antwoord-URL** textbox, type patronen u een URL met hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e7ea-158">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="6e7ea-159">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="6e7ea-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-161">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6e7ea-163">Op Hallo **ClickTime configuratie** sectie, klikt u op **configureren ClickTime** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-163">On hello **ClickTime Configuration** section, click **Configure ClickTime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6e7ea-164">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="6e7ea-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![ClickTime configuratie](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="6e7ea-166">In een ander browservenster, meld u bij uw bedrijf ClickTime site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="6e7ea-167">Klik in de werkbalk bovenaan Hallo Hallo op **voorkeuren**, en klik vervolgens op **beveiligingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-167">In hello toolbar on hello top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="6e7ea-168">In Hallo **voorkeuren voor eenmalige aanmelding** configuratie sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e7ea-168">In hello **Single Sign-On Preferences** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6e7ea-169">![Beveiligingsinstellingen](./media/active-directory-saas-clicktime-tutorial/tic777280.png "beveiligingsinstellingen")</span><span class="sxs-lookup"><span data-stu-id="6e7ea-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="6e7ea-170">a.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-170">a.</span></span>  <span data-ttu-id="6e7ea-171">Selecteer **toestaan** aanmelden met eenmalige aanmelding (SSO) met **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="6e7ea-172">b.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-172">b.</span></span> <span data-ttu-id="6e7ea-173">In Hallo **eindpunt van de Provider identiteit** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-173">In hello **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="6e7ea-174">c.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-174">c.</span></span>  <span data-ttu-id="6e7ea-175">Open Hallo **base-64 gecodeerde certificaat** gedownload van Azure-portal op **Kladblok**Hallo inhoud kopieert en plakt u deze in Hallo **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-175">Open hello **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="6e7ea-176">d.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-176">d.</span></span>  <span data-ttu-id="6e7ea-177">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6e7ea-178">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6e7ea-179">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6e7ea-180">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6e7ea-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6e7ea-181">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6e7ea-181">Create an Azure AD test user</span></span>
<span data-ttu-id="6e7ea-182">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="6e7ea-184">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6e7ea-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e7ea-185">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-185">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6e7ea-187">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-187">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6e7ea-189">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-189">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6e7ea-191">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e7ea-191">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6e7ea-193">a.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-193">a.</span></span> <span data-ttu-id="6e7ea-194">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e7ea-195">b.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-195">b.</span></span> <span data-ttu-id="6e7ea-196">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6e7ea-197">c.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-197">c.</span></span> <span data-ttu-id="6e7ea-198">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6e7ea-199">d.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-199">d.</span></span> <span data-ttu-id="6e7ea-200">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="6e7ea-201">Een testgebruiker ClickTime maken</span><span class="sxs-lookup"><span data-stu-id="6e7ea-201">Create a ClickTime test user</span></span>

<span data-ttu-id="6e7ea-202">In de volgorde tooenable Azure AD gebruikers toolog in ClickTime, moeten ze worden ingericht in ClickTime.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-202">In order tooenable Azure AD users toolog into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="6e7ea-203">In geval van ClickTime Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-203">In hello case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="6e7ea-204">U kunt andere ClickTime gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door ClickTime tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime tooprovision Azure AD user accounts.</span></span>

<span data-ttu-id="6e7ea-205">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6e7ea-205">**tooprovision a user account, perform hello following steps:**</span></span>
1. <span data-ttu-id="6e7ea-206">Meld u bij tooyour **ClickTime** tenant.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-206">Log in tooyour **ClickTime** tenant.</span></span>
2. <span data-ttu-id="6e7ea-207">Klik in de werkbalk bovenaan Hallo Hallo op **bedrijf**, en klik vervolgens op **mensen**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-207">In hello toolbar on hello top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="6e7ea-208">![Mensen](./media/active-directory-saas-clicktime-tutorial/tic777282.png "personen")</span><span class="sxs-lookup"><span data-stu-id="6e7ea-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="6e7ea-209">Klik op **persoon toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="6e7ea-210">![Persoon toevoegen](./media/active-directory-saas-clicktime-tutorial/tic777283.png "persoon toevoegen")</span><span class="sxs-lookup"><span data-stu-id="6e7ea-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="6e7ea-211">Voer in de sectie nieuwe persoon Hallo, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e7ea-211">In hello New Person section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6e7ea-212">![Mensen](./media/active-directory-saas-clicktime-tutorial/tic777284.png "personen")</span><span class="sxs-lookup"><span data-stu-id="6e7ea-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="6e7ea-213">a.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-213">a.</span></span>  <span data-ttu-id="6e7ea-214">In Hallo **volledige naam** textbox type volledige naam van gebruiker zoals **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-214">In hello **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="6e7ea-215">b.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-215">b.</span></span>  <span data-ttu-id="6e7ea-216">In Hallo **e-mailadres** textbox type Hallo e-mailadres van de gebruiker, zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="6e7ea-216">In hello **email address** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="6e7ea-217">Als u wilt, kunt u extra eigenschappen van het nieuwe persoon object Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-217">If you want to, you can set additional properties of hello new person object.</span></span>
   
    <span data-ttu-id="6e7ea-218">c.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-218">c.</span></span>  <span data-ttu-id="6e7ea-219">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-219">Click **Save**.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6e7ea-220">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e7ea-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6e7ea-221">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooClickTime toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClickTime.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="6e7ea-223">**tooassign Britta Simon tooClickTime, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6e7ea-223">**tooassign Britta Simon tooClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e7ea-224">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6e7ea-226">Selecteer in de lijst met de toepassingen van Hallo **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-226">In hello applications list, select **ClickTime**.</span></span>

    ![ClickTimne koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="6e7ea-228">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. <span data-ttu-id="6e7ea-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-230">Click **Add** button.</span></span> <span data-ttu-id="6e7ea-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="6e7ea-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6e7ea-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6e7ea-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6e7ea-236">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6e7ea-236">Test single sign-on</span></span>

<span data-ttu-id="6e7ea-237">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6e7ea-238">Als u op Hallo ClickTime tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ClickTime toepassing.</span><span class="sxs-lookup"><span data-stu-id="6e7ea-238">When you click hello ClickTime tile in hello Access Panel, you should get automatically signed-on tooyour ClickTime application.</span></span>
<span data-ttu-id="6e7ea-239">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6e7ea-239">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6e7ea-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6e7ea-240">Additional resources</span></span>

* [<span data-ttu-id="6e7ea-241">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e7ea-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6e7ea-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6e7ea-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

