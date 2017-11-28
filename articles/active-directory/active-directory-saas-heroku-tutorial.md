---
title: 'Zelfstudie: Azure Active Directory-integratie met Heroku | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Heroku.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee11db647fd385140f1dbcab2586dfafffe5d912
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="c284e-103">Zelfstudie: Azure Active Directory-integratie met Heroku</span><span class="sxs-lookup"><span data-stu-id="c284e-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="c284e-104">In deze zelfstudie leert u hoe toointegrate Heroku met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c284e-104">In this tutorial, you learn how toointegrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c284e-105">Heroku integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c284e-105">Integrating Heroku with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c284e-106">U kunt beheren in Azure AD die tooHeroku toegang heeft</span><span class="sxs-lookup"><span data-stu-id="c284e-106">You can control in Azure AD who has access tooHeroku</span></span>
- <span data-ttu-id="c284e-107">U kunt uw gebruikers tooautomatically get aangemelde tooHeroku (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="c284e-107">You can enable your users tooautomatically get signed-on tooHeroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c284e-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c284e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c284e-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c284e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c284e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c284e-110">Prerequisites</span></span>

<span data-ttu-id="c284e-111">Azure AD-integratie met Heroku tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="c284e-111">tooconfigure Azure AD integration with Heroku, you need hello following items:</span></span>

- <span data-ttu-id="c284e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c284e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c284e-113">Een Heroku eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c284e-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c284e-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c284e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c284e-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c284e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c284e-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c284e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c284e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c284e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c284e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c284e-118">Scenario description</span></span>
<span data-ttu-id="c284e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c284e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c284e-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c284e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c284e-121">Het toevoegen van Heroku van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c284e-121">Adding Heroku from hello gallery</span></span>
2. <span data-ttu-id="c284e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c284e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-hello-gallery"></a><span data-ttu-id="c284e-123">Het toevoegen van Heroku van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c284e-123">Adding Heroku from hello gallery</span></span>
<span data-ttu-id="c284e-124">tooconfigure hello integratie van Heroku in Azure AD, moet u tooadd Heroku uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c284e-124">tooconfigure hello integration of Heroku into Azure AD, you need tooadd Heroku from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c284e-125">**tooadd Heroku via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c284e-125">**tooadd Heroku from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c284e-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c284e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c284e-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c284e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c284e-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c284e-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c284e-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c284e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c284e-133">Typ in het zoekvak Hallo **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="c284e-133">In hello search box, type **Heroku**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="c284e-135">Selecteer in het deelvenster resultaten hello, **Heroku**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c284e-135">In hello results panel, select **Heroku**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c284e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c284e-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="c284e-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Heroku op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c284e-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c284e-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Heroku is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c284e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Heroku is tooa user in Azure AD.</span></span> <span data-ttu-id="c284e-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Heroku toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="c284e-140">In other words, a link relationship between an Azure AD user and hello related user in Heroku needs toobe established.</span></span>

<span data-ttu-id="c284e-141">Wijs in Heroku, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="c284e-141">In Heroku, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c284e-142">tooconfigure en eenmalige aanmelding Azure AD-test met Heroku, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c284e-142">tooconfigure and test Azure AD single sign-on with Heroku, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c284e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="c284e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c284e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c284e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c284e-145">**[Maken van een testgebruiker Heroku](#creating-a-heroku-test-user)**  -toohave een equivalent van Britta Simon in Heroku die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c284e-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - toohave a counterpart of Britta Simon in Heroku that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c284e-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c284e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c284e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c284e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c284e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c284e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c284e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Heroku configureren.</span><span class="sxs-lookup"><span data-stu-id="c284e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="c284e-150">**Azure AD tooconfigure eenmalige aanmelding met Heroku, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c284e-150">**tooconfigure Azure AD single sign-on with Heroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="c284e-151">In de Azure-portal op Hallo Hallo **Heroku** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c284e-151">In hello Azure portal, on hello **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c284e-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c284e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="c284e-155">Op Hallo **Heroku domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c284e-155">On hello **Heroku Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="c284e-157">a.</span><span class="sxs-lookup"><span data-stu-id="c284e-157">a.</span></span> <span data-ttu-id="c284e-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="c284e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="c284e-159">b.</span><span class="sxs-lookup"><span data-stu-id="c284e-159">b.</span></span> <span data-ttu-id="c284e-160">In Hallo **identificatie-URL** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="c284e-160">In hello **Identifier URL** textbox, type a URL using hello following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="c284e-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c284e-161">These values are not real.</span></span> <span data-ttu-id="c284e-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="c284e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c284e-163">U kunt deze waarden ophalen van Heroku-team in latere secties van dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="c284e-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="c284e-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c284e-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="c284e-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c284e-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c284e-168">tooenable SSO in Heroku, Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c284e-168">tooenable SSO in Heroku, perform hello following steps:</span></span>
   
    <span data-ttu-id="c284e-169">a.</span><span class="sxs-lookup"><span data-stu-id="c284e-169">a.</span></span> <span data-ttu-id="c284e-170">Aanmelden toohello Heroku account als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c284e-170">Log in toohello Heroku account as an administrator.</span></span>

    <span data-ttu-id="c284e-171">b.</span><span class="sxs-lookup"><span data-stu-id="c284e-171">b.</span></span> <span data-ttu-id="c284e-172">Klik op Hallo **instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c284e-172">Click hello **Settings** tab.</span></span>

    <span data-ttu-id="c284e-173">c.</span><span class="sxs-lookup"><span data-stu-id="c284e-173">c.</span></span> <span data-ttu-id="c284e-174">Op Hallo **eenmalige aanmelding op de pagina**, klikt u op **metagegevens uploaden**.</span><span class="sxs-lookup"><span data-stu-id="c284e-174">On hello **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="c284e-175">d.</span><span class="sxs-lookup"><span data-stu-id="c284e-175">d.</span></span> <span data-ttu-id="c284e-176">Hallo metagegevensbestand, dat u hebt gedownload van hello Azure-portal uploaden.</span><span class="sxs-lookup"><span data-stu-id="c284e-176">Upload hello metadata file, which you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="c284e-177">e.</span><span class="sxs-lookup"><span data-stu-id="c284e-177">e.</span></span> <span data-ttu-id="c284e-178">Wanneer het Hallo-installatie is geslaagd, beheerders bevestigen en Hallo URL Hallo SSO-aanmelding voor eindgebruikers wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c284e-178">When hello setup is successful, administrators see a confirmation dialog and hello URL of hello SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="c284e-179">f.</span><span class="sxs-lookup"><span data-stu-id="c284e-179">f.</span></span> <span data-ttu-id="c284e-180">Kopiëren Hallo **Heroku aanmeldings-URL** en **Heroku entiteit-ID** waarden en Ga naar het back-te**Heroku domein en de URL's** sectie in Azure-portal en plakt u deze waarden in Hallo **Aanmeldings-Url** en **id** tekstvakken respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="c284e-180">Copy hello **Heroku Login URL** and **Heroku Entity ID** values and go back too**Heroku Domain and URLs** section in Azure portal and paste these values into hello **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="c284e-182">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c284e-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="c284e-183">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="c284e-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c284e-184">Na het toevoegen van deze app van Hallo **Active Directory-bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="c284e-184">After adding this app from hello **Active Directory Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c284e-185">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c284e-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c284e-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c284e-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="c284e-187">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c284e-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c284e-189">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c284e-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c284e-190">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c284e-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c284e-192">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c284e-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c284e-194">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="c284e-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c284e-196">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c284e-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c284e-198">a.</span><span class="sxs-lookup"><span data-stu-id="c284e-198">a.</span></span> <span data-ttu-id="c284e-199">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c284e-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c284e-200">b.</span><span class="sxs-lookup"><span data-stu-id="c284e-200">b.</span></span> <span data-ttu-id="c284e-201">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c284e-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c284e-202">c.</span><span class="sxs-lookup"><span data-stu-id="c284e-202">c.</span></span> <span data-ttu-id="c284e-203">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c284e-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c284e-204">d.</span><span class="sxs-lookup"><span data-stu-id="c284e-204">d.</span></span> <span data-ttu-id="c284e-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c284e-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="c284e-206">Een testgebruiker Heroku maken</span><span class="sxs-lookup"><span data-stu-id="c284e-206">Creating a Heroku test user</span></span>

<span data-ttu-id="c284e-207">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Heroku maken.</span><span class="sxs-lookup"><span data-stu-id="c284e-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="c284e-208">Heroku ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c284e-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="c284e-209">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="c284e-209">There is no action item for you in this section.</span></span> <span data-ttu-id="c284e-210">Een nieuwe gebruiker wordt gemaakt bij het openen van Heroku als Hallo gebruiker nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="c284e-210">A new user is created when accessing Heroku if hello user doesn't exist yet.</span></span> <span data-ttu-id="c284e-211">Nadat het Hallo-account is ingericht, Hallo eindgebruiker ontvangt een bevestigingsmail en moet tooclick Hallo bevestiging koppelen.</span><span class="sxs-lookup"><span data-stu-id="c284e-211">After hello account is provisioned, hello end user receives a verification email and needs tooclick hello acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="c284e-212">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [Heroku Client ondersteuningsteam](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="c284e-212">If you need toocreate a user manually, you need toocontact hello [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c284e-213">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c284e-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c284e-214">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooHeroku toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="c284e-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHeroku.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c284e-216">**tooassign Britta Simon tooHeroku, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c284e-216">**tooassign Britta Simon tooHeroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="c284e-217">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c284e-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c284e-219">Selecteer in de lijst met de toepassingen van Hallo **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="c284e-219">In hello applications list, select **Heroku**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="c284e-221">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c284e-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c284e-223">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c284e-223">Click **Add** button.</span></span> <span data-ttu-id="c284e-224">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c284e-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c284e-226">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="c284e-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c284e-227">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c284e-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c284e-228">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c284e-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c284e-229">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c284e-229">Testing single sign-on</span></span>

<span data-ttu-id="c284e-230">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c284e-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c284e-231">Als u op Hallo Heroku tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Heroku toepassing.</span><span class="sxs-lookup"><span data-stu-id="c284e-231">When you click hello Heroku tile in hello Access Panel, you should get automatically signed-on tooyour Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c284e-232">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c284e-232">Additional resources</span></span>

* [<span data-ttu-id="c284e-233">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c284e-233">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c284e-234">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c284e-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
