---
title: 'Zelfstudie: Azure Active Directory-integratie met Predictix ordening | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Predictix bestellen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2fe2f976-e97f-4368-9695-3e1624409e8b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 0418ef24d7942b6b751c0b4d64e7bd1fba1d6a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-ordering"></a><span data-ttu-id="94ac0-103">Zelfstudie: Azure Active Directory-integratie met Predictix ordenen</span><span class="sxs-lookup"><span data-stu-id="94ac0-103">Tutorial: Azure Active Directory integration with Predictix Ordering</span></span>

<span data-ttu-id="94ac0-104">In deze zelfstudie leert u hoe toointegrate Predictix ordening met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94ac0-104">In this tutorial, you learn how toointegrate Predictix Ordering with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94ac0-105">Predictix ordening integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="94ac0-105">Integrating Predictix Ordering with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="94ac0-106">U kunt beheren in Azure AD wie toegang tot tooPredictix heeft volgorde.</span><span class="sxs-lookup"><span data-stu-id="94ac0-106">You can control in Azure AD who has access tooPredictix Ordering.</span></span>
- <span data-ttu-id="94ac0-107">U kunt uw gebruikers tooautomatically get aangemelde tooPredictix inschakelen volgorde (Single Sign-On) met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="94ac0-107">You can enable your users tooautomatically get signed-on tooPredictix Ordering (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="94ac0-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="94ac0-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="94ac0-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="94ac0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94ac0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="94ac0-110">Prerequisites</span></span>

<span data-ttu-id="94ac0-111">Azure AD-integratie met Predictix ordening tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="94ac0-111">tooconfigure Azure AD integration with Predictix Ordering, you need hello following items:</span></span>

- <span data-ttu-id="94ac0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="94ac0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="94ac0-113">Een Predictix ordening eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="94ac0-113">A Predictix Ordering single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="94ac0-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="94ac0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="94ac0-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="94ac0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94ac0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="94ac0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="94ac0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94ac0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="94ac0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="94ac0-118">Scenario description</span></span>
<span data-ttu-id="94ac0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="94ac0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94ac0-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="94ac0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94ac0-121">Het toevoegen van Predictix ordening van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="94ac0-121">Adding Predictix Ordering from hello gallery</span></span>
2. <span data-ttu-id="94ac0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="94ac0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-ordering-from-hello-gallery"></a><span data-ttu-id="94ac0-123">Het toevoegen van Predictix ordening van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="94ac0-123">Adding Predictix Ordering from hello gallery</span></span>
<span data-ttu-id="94ac0-124">tooconfigure hello integratie van Predictix ordening in Azure AD, moet u tooadd Predictix ordening van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="94ac0-124">tooconfigure hello integration of Predictix Ordering into Azure AD, you need tooadd Predictix Ordering from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="94ac0-125">**tooadd Predictix bestellen via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="94ac0-125">**tooadd Predictix Ordering from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="94ac0-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="94ac0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="94ac0-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="94ac0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="94ac0-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="94ac0-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="94ac0-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="94ac0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="94ac0-133">Typ in het zoekvak Hallo **Predictix ordening**, selecteer **Predictix ordening** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="94ac0-133">In hello search box, type **Predictix Ordering**, select **Predictix Ordering** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Predictix bestellen in de lijst met resultaten Hallo](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="94ac0-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="94ac0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="94ac0-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Predictix ordenen op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="94ac0-136">In this section, you configure and test Azure AD single sign-on with Predictix Ordering based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="94ac0-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in volgorde van Predictix is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94ac0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Predictix Ordering is tooa user in Azure AD.</span></span> <span data-ttu-id="94ac0-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in volgorde van Predictix toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="94ac0-138">In other words, a link relationship between an Azure AD user and hello related user in Predictix Ordering needs toobe established.</span></span>

<span data-ttu-id="94ac0-139">Wijs in het Predictix ordenen wordt Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="94ac0-139">In Predictix Ordering, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="94ac0-140">tooconfigure en eenmalige aanmelding Azure AD-test met Predictix ordening, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="94ac0-140">tooconfigure and test Azure AD single sign-on with Predictix Ordering, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="94ac0-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="94ac0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="94ac0-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="94ac0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="94ac0-143">**[Maak een testgebruiker Predictix ordening](#create-a-predictix-ordering-test-user)**  -toohave een equivalent van Britta Simon in Predictix volgorde die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="94ac0-143">**[Create a Predictix Ordering test user](#create-a-predictix-ordering-test-user)** - toohave a counterpart of Britta Simon in Predictix Ordering that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="94ac0-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="94ac0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="94ac0-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="94ac0-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="94ac0-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="94ac0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="94ac0-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Predictix bestellen.</span><span class="sxs-lookup"><span data-stu-id="94ac0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Predictix Ordering application.</span></span>

<span data-ttu-id="94ac0-148">**Azure AD tooconfigure eenmalige aanmelding met het bestellen van Predictix uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="94ac0-148">**tooconfigure Azure AD single sign-on with Predictix Ordering, perform hello following steps:**</span></span>

1. <span data-ttu-id="94ac0-149">In Azure-portal op Hallo Hallo **Predictix ordening** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="94ac0-149">In hello Azure portal, on hello **Predictix Ordering** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="94ac0-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="94ac0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_samlbase.png)

3. <span data-ttu-id="94ac0-153">Op Hallo **Predictix ordening domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="94ac0-153">On hello **Predictix Ordering Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en Predictix ordening domein eenmalige aanmelding informatie](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_url.png)

    <span data-ttu-id="94ac0-155">a.</span><span class="sxs-lookup"><span data-stu-id="94ac0-155">a.</span></span> <span data-ttu-id="94ac0-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname-pricing>.ordering.predictix.com/sso/request`</span><span class="sxs-lookup"><span data-stu-id="94ac0-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname-pricing>.ordering.predictix.com/sso/request`</span></span>

    <span data-ttu-id="94ac0-157">b.</span><span class="sxs-lookup"><span data-stu-id="94ac0-157">b.</span></span> <span data-ttu-id="94ac0-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="94ac0-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span> 
    | |
    |--|
    | `https://<companyname-pricing>.dev.ordering.predictix.com` |
    | `https://<companyname-pricing>.ordering.predictix.com` |

    > [!NOTE] 
    > <span data-ttu-id="94ac0-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="94ac0-159">These values are not real.</span></span> <span data-ttu-id="94ac0-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="94ac0-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="94ac0-161">Neem contact op met [Predictix ordening Client ondersteuningsteam](https://www.predix.io/support/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="94ac0-161">Contact [Predictix Ordering Client support team](https://www.predix.io/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="94ac0-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="94ac0-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_certificate.png) 

5. <span data-ttu-id="94ac0-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="94ac0-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-predictixordering-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="94ac0-166">Op Hallo **Predictix ordening configuratie** sectie, klikt u op **Predictix ordening configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="94ac0-166">On hello **Predictix Ordering Configuration** section, click **Configure Predictix Ordering** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="94ac0-167">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="94ac0-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Predictix ordening configuratie](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_configure.png) 

7. <span data-ttu-id="94ac0-169">tooconfigure eenmalige aanmelding op **Predictix ordening** zijde, moet u toosend Hallo gedownload **certificaat (Base64)**, **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL**  te[ondersteuningsteam Predictix ordening](https://www.predix.io/support/).</span><span class="sxs-lookup"><span data-stu-id="94ac0-169">tooconfigure single sign-on on **Predictix Ordering** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Predictix Ordering support team](https://www.predix.io/support/).</span></span> <span data-ttu-id="94ac0-170">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="94ac0-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="94ac0-171">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="94ac0-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="94ac0-172">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="94ac0-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="94ac0-173">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="94ac0-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="94ac0-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="94ac0-174">Create an Azure AD test user</span></span>
<span data-ttu-id="94ac0-175">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="94ac0-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="94ac0-177">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="94ac0-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="94ac0-178">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="94ac0-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="94ac0-180">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="94ac0-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="94ac0-182">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="94ac0-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="94ac0-184">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="94ac0-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_04.png)

   <span data-ttu-id="94ac0-186">a.</span><span class="sxs-lookup"><span data-stu-id="94ac0-186">a.</span></span> <span data-ttu-id="94ac0-187">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="94ac0-187">In hello **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="94ac0-188">b.</span><span class="sxs-lookup"><span data-stu-id="94ac0-188">b.</span></span> <span data-ttu-id="94ac0-189">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="94ac0-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

   <span data-ttu-id="94ac0-190">c.</span><span class="sxs-lookup"><span data-stu-id="94ac0-190">c.</span></span> <span data-ttu-id="94ac0-191">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="94ac0-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

   <span data-ttu-id="94ac0-192">d.</span><span class="sxs-lookup"><span data-stu-id="94ac0-192">d.</span></span> <span data-ttu-id="94ac0-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="94ac0-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-ordering-test-user"></a><span data-ttu-id="94ac0-194">Een testgebruiker Predictix ordening maken</span><span class="sxs-lookup"><span data-stu-id="94ac0-194">Create a Predictix Ordering test user</span></span>

<span data-ttu-id="94ac0-195">In deze sectie maakt maken u een gebruiker Britta Simon in Predictix volgorde aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="94ac0-195">In this section, you create a user called Britta Simon in Predictix Ordering.</span></span> <span data-ttu-id="94ac0-196">Werken met [ondersteuningsteam Predictix ordening](https://www.predix.io/support/) tooadd Hallo gebruikers in Hallo Predictix ordening platform.</span><span class="sxs-lookup"><span data-stu-id="94ac0-196">Work with [Predictix Ordering support team](https://www.predix.io/support/) tooadd hello users in hello Predictix Ordering platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="94ac0-197">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="94ac0-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="94ac0-198">In deze sectie u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooPredictix volgorde.</span><span class="sxs-lookup"><span data-stu-id="94ac0-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPredictix Ordering.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="94ac0-200">**tooassign Britta Simon tooPredictix ordenen wordt Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="94ac0-200">**tooassign Britta Simon tooPredictix Ordering, perform hello following steps:**</span></span>

1. <span data-ttu-id="94ac0-201">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="94ac0-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="94ac0-203">Selecteer in de lijst met de toepassingen van Hallo **Predictix ordening**.</span><span class="sxs-lookup"><span data-stu-id="94ac0-203">In hello applications list, select **Predictix Ordering**.</span></span>

    ![Hallo Predictix ordening koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_app.png)  

3. <span data-ttu-id="94ac0-205">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="94ac0-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="94ac0-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="94ac0-207">Click **Add** button.</span></span> <span data-ttu-id="94ac0-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="94ac0-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="94ac0-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="94ac0-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="94ac0-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="94ac0-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="94ac0-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="94ac0-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="94ac0-213">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="94ac0-213">Test single sign-on</span></span>

<span data-ttu-id="94ac0-214">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="94ac0-214">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="94ac0-215">Als u op Hallo Predictix ordening tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Predictix ordening toepassing.</span><span class="sxs-lookup"><span data-stu-id="94ac0-215">When you click hello Predictix Ordering tile in hello Access Panel, you should get automatically signed-on tooyour Predictix Ordering application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="94ac0-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="94ac0-216">Additional resources</span></span>

* [<span data-ttu-id="94ac0-217">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94ac0-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="94ac0-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="94ac0-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_203.png

