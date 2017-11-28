---
title: 'Zelfstudie: Azure Active Directory-integratie met Yonyx interactieve gidsen | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en de interactieve gidsen Yonyx.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 07db4e01-319b-4cb6-9b93-4577bffd3cbc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: 24e30d243143651b8d32535c76dc300931ae5746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yonyx-interactive-guides"></a><span data-ttu-id="4bd4f-103">Zelfstudie: Azure Active Directory-integratie met Yonyx interactieve handleidingen</span><span class="sxs-lookup"><span data-stu-id="4bd4f-103">Tutorial: Azure Active Directory integration with Yonyx Interactive Guides</span></span>

<span data-ttu-id="4bd4f-104">In deze zelfstudie leert u hoe toointegrate Yonyx interactief leidt met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4bd4f-104">In this tutorial, you learn how toointegrate Yonyx Interactive Guides with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4bd4f-105">Interactieve gidsen Yonyx integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4bd4f-105">Integrating Yonyx Interactive Guides with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4bd4f-106">U kunt beheren in Azure AD wie toegang tot tooYonyx interactieve handleidingen heeft</span><span class="sxs-lookup"><span data-stu-id="4bd4f-106">You can control in Azure AD who has access tooYonyx Interactive Guides</span></span>
- <span data-ttu-id="4bd4f-107">U kunt uw gebruikers tooautomatically get aangemelde tooYonyx interactieve gidsen (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="4bd4f-107">You can enable your users tooautomatically get signed-on tooYonyx Interactive Guides (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4bd4f-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="4bd4f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4bd4f-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4bd4f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4bd4f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4bd4f-110">Prerequisites</span></span>

<span data-ttu-id="4bd4f-111">Azure AD-integratie met Yonyx interactieve gidsen tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="4bd4f-111">tooconfigure Azure AD integration with Yonyx Interactive Guides, you need hello following items:</span></span>

- <span data-ttu-id="4bd4f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4bd4f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4bd4f-113">Een interactieve gidsen Yonyx eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="4bd4f-113">A Yonyx Interactive Guides single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4bd4f-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4bd4f-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4bd4f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4bd4f-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4bd4f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4bd4f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4bd4f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="4bd4f-118">Scenario description</span></span>
<span data-ttu-id="4bd4f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4bd4f-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="4bd4f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4bd4f-121">Het toevoegen van interactieve gidsen Yonyx van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4bd4f-121">Adding Yonyx Interactive Guides from hello gallery</span></span>
2. <span data-ttu-id="4bd4f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4bd4f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yonyx-interactive-guides-from-hello-gallery"></a><span data-ttu-id="4bd4f-123">Het toevoegen van interactieve gidsen Yonyx van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4bd4f-123">Adding Yonyx Interactive Guides from hello gallery</span></span>
<span data-ttu-id="4bd4f-124">tooconfigure hello integratie van Yonyx interactieve handleidingen in Azure AD, moet u tooadd Yonyx interactieve gidsen uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-124">tooconfigure hello integration of Yonyx Interactive Guides into Azure AD, you need tooadd Yonyx Interactive Guides from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4bd4f-125">**tooadd Yonyx interactieve gidsen via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4bd4f-125">**tooadd Yonyx Interactive Guides from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bd4f-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="4bd4f-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4bd4f-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="4bd4f-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="4bd4f-133">Typ in het zoekvak Hallo **Yonyx interactieve gidsen**, selecteer **Yonyx interactieve gidsen** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-133">In hello search box, type **Yonyx Interactive Guides**, select  **Yonyx Interactive Guides**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Interactieve handleidingen in de lijst met resultaten Hallo Yonyx](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4bd4f-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bd4f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4bd4f-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Yonyx interactieve gidsen op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-136">In this section, you configure and test Azure AD single sign-on with Yonyx Interactive Guides based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4bd4f-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de interactieve handleidingen Yonyx is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Yonyx Interactive Guides is tooa user in Azure AD.</span></span> <span data-ttu-id="4bd4f-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in de interactieve handleidingen Yonyx Hallo toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-138">In other words, a link relationship between an Azure AD user and hello related user in Yonyx Interactive Guides needs toobe established.</span></span>

<span data-ttu-id="4bd4f-139">In de interactieve handleidingen Yonyx, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-139">In Yonyx Interactive Guides, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4bd4f-140">tooconfigure en eenmalige aanmelding Azure AD-test met Yonyx interactieve gidsen, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4bd4f-140">tooconfigure and test Azure AD single sign-on with Yonyx Interactive Guides, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4bd4f-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4bd4f-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4bd4f-143">**[Maak een testgebruiker Yonyx interactieve gidsen](#create-a-yonyx-interactive-guides-test-user)**  -toohave een equivalent van Britta Simon in Yonyx interactieve handleidingen die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-143">**[Create a Yonyx Interactive Guides test user](#create-a-yonyx-interactive-guides-test-user)** - toohave a counterpart of Britta Simon in Yonyx Interactive Guides that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4bd4f-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4bd4f-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4bd4f-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="4bd4f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4bd4f-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Yonyx interactieve gidsen.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="4bd4f-148">**tooconfigure eenmalige aanmelding Azure AD met Yonyx interactieve implementatiehandleidingen, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4bd4f-148">**tooconfigure Azure AD single sign-on with Yonyx Interactive Guides, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bd4f-149">In Azure-portal op Hallo Hallo **Yonyx interactieve gidsen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-149">In hello Azure portal, on hello **Yonyx Interactive Guides** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="4bd4f-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_samlbase.png)

3. <span data-ttu-id="4bd4f-153">Op Hallo **Yonyx interactieve handleidingen domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4bd4f-153">On hello **Yonyx Interactive Guides Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en Yonyx interactieve handleidingen domein eenmalige aanmelding informatie](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_url.png)

    <span data-ttu-id="4bd4f-155">a.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-155">a.</span></span> <span data-ttu-id="4bd4f-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span><span class="sxs-lookup"><span data-stu-id="4bd4f-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span></span>

    <span data-ttu-id="4bd4f-157">b.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-157">b.</span></span> <span data-ttu-id="4bd4f-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.yonyx.com`</span><span class="sxs-lookup"><span data-stu-id="4bd4f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.yonyx.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4bd4f-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-159">These values are not real.</span></span> <span data-ttu-id="4bd4f-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4bd4f-161">Neem contact op met [Yonyx interactieve handleidingen Client ondersteuningsteam](mailto:support@yonyx.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-161">Contact [Yonyx Interactive Guides Client support team](mailto:support@yonyx.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="4bd4f-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_certificate.png) 

5. <span data-ttu-id="4bd4f-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-yonyx-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4bd4f-166">Op Hallo **Yonyx interactieve handleidingen configuratie** sectie, klikt u op **Yonyx interactieve gidsen configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-166">On hello **Yonyx Interactive Guides Configuration** section, click **Configure Yonyx Interactive Guides** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4bd4f-167">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="4bd4f-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Yonyx interactieve gidsen configuratie](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_configure.png) 

7. <span data-ttu-id="4bd4f-169">tooconfigure eenmalige aanmelding op **Yonyx interactieve gidsen** zijde, moet u toosend Hallo gedownload **Certificate(Base64)**, **Sign-Out URL**, **SAML Single Sign-On Service-URL** **SAML entiteit-ID** te[Yonyx interactieve gidsen ondersteuningsteam](mailto:support@yonyx.com).</span><span class="sxs-lookup"><span data-stu-id="4bd4f-169">tooconfigure single sign-on on **Yonyx Interactive Guides** side, you need toosend hello downloaded **Certificate(Base64)**, **Sign-Out URL**, **SAML Single Sign-On Service URL** **SAML Entity ID** too[Yonyx Interactive Guides support team](mailto:support@yonyx.com).</span></span> <span data-ttu-id="4bd4f-170">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="4bd4f-171">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4bd4f-172">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4bd4f-173">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4bd4f-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4bd4f-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4bd4f-174">Create an Azure AD test user</span></span>

<span data-ttu-id="4bd4f-175">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

  ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="4bd4f-177">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4bd4f-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bd4f-178">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-yonyx-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4bd4f-180">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-yonyx-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4bd4f-182">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-yonyx-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4bd4f-184">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4bd4f-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-yonyx-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4bd4f-186">a.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-186">a.</span></span> <span data-ttu-id="4bd4f-187">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4bd4f-188">b.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-188">b.</span></span> <span data-ttu-id="4bd4f-189">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4bd4f-190">c.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-190">c.</span></span> <span data-ttu-id="4bd4f-191">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4bd4f-192">d.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-192">d.</span></span> <span data-ttu-id="4bd4f-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-193">Click **Create**.</span></span>
 
### <a name="create-a-yonyx-interactive-guides-test-user"></a><span data-ttu-id="4bd4f-194">Maak een testgebruiker Yonyx interactieve handleidingen</span><span class="sxs-lookup"><span data-stu-id="4bd4f-194">Create a Yonyx Interactive Guides test user</span></span>

<span data-ttu-id="4bd4f-195">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in de interactieve gidsen Yonyx van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-195">hello objective of this section is toocreate a user called Britta Simon in Yonyx Interactive Guides.</span></span> <span data-ttu-id="4bd4f-196">Interactieve gidsen Yonyx ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-196">Yonyx Interactive Guides supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="4bd4f-197">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-197">There is no action item for you in this section.</span></span> <span data-ttu-id="4bd4f-198">Een nieuwe gebruiker wordt tijdens een poging tooaccess Yonyx interactieve gidsen gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-198">A new user is created during an attempt tooaccess Yonyx Interactive Guides if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="4bd4f-199">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello Yonyx interactieve gidsen ondersteuningsteam via < mailto:support@yonyx.com >.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-199">If you need toocreate a user manually, you need toocontact hello Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4bd4f-200">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bd4f-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4bd4f-201">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooYonyx interactieve gidsen.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYonyx Interactive Guides.</span></span>

![Hallo-gebruikersrollen toewijzen][200]

<span data-ttu-id="4bd4f-203">**tooassign Britta Simon tooYonyx interactieve implementatiehandleidingen, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4bd4f-203">**tooassign Britta Simon tooYonyx Interactive Guides, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bd4f-204">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="4bd4f-206">Selecteer in de lijst met de toepassingen van Hallo **Yonyx interactieve gidsen**.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-206">In hello applications list, select **Yonyx Interactive Guides**.</span></span>

    ![Hallo Yonyx interactieve gidsen koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_app.png) 

3. <span data-ttu-id="4bd4f-208">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="4bd4f-210">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-210">Click **Add** button.</span></span> <span data-ttu-id="4bd4f-211">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="4bd4f-213">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4bd4f-214">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4bd4f-215">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4bd4f-216">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4bd4f-216">Test single sign-on</span></span>

<span data-ttu-id="4bd4f-217">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4bd4f-218">Als u op Hallo Yonyx interactieve gidsen-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Yonyx interactieve gidsen toepassing.</span><span class="sxs-lookup"><span data-stu-id="4bd4f-218">When you click hello Yonyx Interactive Guides tile in hello Access Panel, you should get automatically signed-on tooyour Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="4bd4f-219">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4bd4f-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4bd4f-220">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4bd4f-220">Additional resources</span></span>

* [<span data-ttu-id="4bd4f-221">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4bd4f-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4bd4f-222">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4bd4f-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_203.png

