---
title: 'Zelfstudie: Azure Active Directory-integratie met ArcGIS Online | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding van Azure Active Directory en ArcGIS Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="312db-103">Zelfstudie: Azure Active Directory-integratie met ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="312db-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="312db-104">In deze zelfstudie leert u hoe toointegrate ArcGIS Online met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="312db-104">In this tutorial, you learn how toointegrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="312db-105">Online ArcGIS integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="312db-105">Integrating ArcGIS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="312db-106">U kunt beheren in Azure AD die Online tooArcGIS toegang heeft</span><span class="sxs-lookup"><span data-stu-id="312db-106">You can control in Azure AD who has access tooArcGIS Online</span></span>
- <span data-ttu-id="312db-107">U kunt uw gebruikers tooautomatically get aangemelde tooArcGIS Online (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="312db-107">You can enable your users tooautomatically get signed-on tooArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="312db-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="312db-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="312db-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="312db-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="312db-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="312db-110">Prerequisites</span></span>

<span data-ttu-id="312db-111">Azure AD-integratie met ArcGIS Online tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="312db-111">tooconfigure Azure AD integration with ArcGIS Online, you need hello following items:</span></span>

- <span data-ttu-id="312db-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="312db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="312db-113">Een ArcGIS Online eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="312db-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="312db-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="312db-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="312db-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="312db-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="312db-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="312db-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="312db-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="312db-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="312db-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="312db-118">Scenario description</span></span>
<span data-ttu-id="312db-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="312db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="312db-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="312db-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="312db-121">Het toevoegen van Online ArcGIS van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="312db-121">Adding ArcGIS Online from hello gallery</span></span>
2. <span data-ttu-id="312db-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="312db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-hello-gallery"></a><span data-ttu-id="312db-123">Het toevoegen van Online ArcGIS van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="312db-123">Adding ArcGIS Online from hello gallery</span></span>
<span data-ttu-id="312db-124">tooconfigure hello integratie ArcGIS online met Azure AD, moet u tooadd ArcGIS Online uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="312db-124">tooconfigure hello integration of ArcGIS Online into Azure AD, you need tooadd ArcGIS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="312db-125">**tooadd ArcGIS Online via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="312db-125">**tooadd ArcGIS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="312db-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="312db-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="312db-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="312db-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="312db-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="312db-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="312db-131">Klik op **nieuwe toepassing** knop bovenaan Hallo van Hallo dialoogvenster tooadd nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="312db-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="312db-133">Typ in het zoekvak Hallo **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="312db-133">In hello search box, type **ArcGIS Online**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="312db-135">Selecteer in het deelvenster resultaten hello, **ArcGIS Online**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="312db-135">In hello results panel, select **ArcGIS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="312db-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="312db-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="312db-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met ArcGIS Online op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="312db-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="312db-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ArcGIS Online is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="312db-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ArcGIS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="312db-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in ArcGIS Online toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="312db-140">In other words, a link relationship between an Azure AD user and hello related user in ArcGIS Online needs toobe established.</span></span>

<span data-ttu-id="312db-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="312db-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="312db-142">tooconfigure en test eenmalige aanmelding Azure AD met ArcGIS Online, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="312db-142">tooconfigure and test Azure AD single sign-on with ArcGIS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="312db-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="312db-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="312db-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="312db-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="312db-145">**[Maken van een Online ArcGIS testgebruiker](#creating-an-arcgis-online-test-user)**  -toohave een equivalent van Britta Simon in ArcGIS Online die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="312db-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - toohave a counterpart of Britta Simon in ArcGIS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="312db-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="312db-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="312db-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="312db-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="312db-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="312db-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="312db-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing ArcGIS Online configureren.</span><span class="sxs-lookup"><span data-stu-id="312db-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="312db-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Online ArcGIS, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="312db-150">**tooconfigure Azure AD single sign-on with ArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="312db-151">In de Azure-portal op Hallo Hallo **ArcGIS Online** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="312db-151">In hello Azure portal, on hello **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="312db-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="312db-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="312db-155">Op Hallo **ArcGIS Online domein en de URL's** sectie, voert u Hallo stap:</span><span class="sxs-lookup"><span data-stu-id="312db-155">On hello **ArcGIS Online Domain and URLs** section, perform hello following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="312db-157">In Hallo **aanmeldings-URL** textbox Hallo typewaarde met Hallo patroon volgen:`https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="312db-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="312db-158">Deze waarde is geen echte Hallo.</span><span class="sxs-lookup"><span data-stu-id="312db-158">This value is not hello real.</span></span> <span data-ttu-id="312db-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="312db-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="312db-160">Neem contact op met [ArcGIS Online Client ondersteuningsteam](http://support.esri.com/) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="312db-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) tooget this value.</span></span> 

4. <span data-ttu-id="312db-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="312db-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="312db-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="312db-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="312db-165">In een ander browservenster, meld u bij uw bedrijf ArcGIS site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="312db-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="312db-166">Klik op **bewerken van instellingen**.</span><span class="sxs-lookup"><span data-stu-id="312db-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="312db-167">![Instellingen bewerken](./media/active-directory-saas-arcgis-tutorial/ic784742.png "instellingen bewerken")</span><span class="sxs-lookup"><span data-stu-id="312db-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="312db-168">Klik op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="312db-168">Click **Security**.</span></span>

    <span data-ttu-id="312db-169">![Beveiliging](./media/active-directory-saas-arcgis-tutorial/ic784743.png "beveiliging")</span><span class="sxs-lookup"><span data-stu-id="312db-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="312db-170">Onder **Enterprise aanmeldingen**, klikt u op **IDENTITEITSPROVIDER ingesteld**.</span><span class="sxs-lookup"><span data-stu-id="312db-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="312db-171">![Enterprise-aanmeldingen](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise-aanmeldingen")</span><span class="sxs-lookup"><span data-stu-id="312db-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="312db-172">Op Hallo **identiteitsprovider ingesteld** configuratie pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="312db-172">On hello **Set Identity Provider** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="312db-173">![Instellen van de identiteitsprovider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "identiteitsprovider instellen")</span><span class="sxs-lookup"><span data-stu-id="312db-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="312db-174">a.</span><span class="sxs-lookup"><span data-stu-id="312db-174">a.</span></span> <span data-ttu-id="312db-175">In Hallo **naam** textbox, typ de naam van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="312db-175">In hello **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="312db-176">b.</span><span class="sxs-lookup"><span data-stu-id="312db-176">b.</span></span> <span data-ttu-id="312db-177">Voor **metagegevens voor Hallo Enterprise-id-Provider worden opgegeven met behulp van**, selecteer **een bestand**.</span><span class="sxs-lookup"><span data-stu-id="312db-177">For **Metadata for hello Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="312db-178">c.</span><span class="sxs-lookup"><span data-stu-id="312db-178">c.</span></span> <span data-ttu-id="312db-179">tooupload uw gedownloade metagegevensbestand, klikt u op **bestand kiezen**.</span><span class="sxs-lookup"><span data-stu-id="312db-179">tooupload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="312db-180">d.</span><span class="sxs-lookup"><span data-stu-id="312db-180">d.</span></span> <span data-ttu-id="312db-181">Klik op **SET IDENTITEITSPROVIDER**.</span><span class="sxs-lookup"><span data-stu-id="312db-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="312db-182">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="312db-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="312db-183">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="312db-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="312db-184">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="312db-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="312db-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="312db-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="312db-186">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="312db-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="312db-188">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="312db-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="312db-189">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="312db-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="312db-191">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="312db-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="312db-193">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="312db-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="312db-195">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="312db-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="312db-197">a.</span><span class="sxs-lookup"><span data-stu-id="312db-197">a.</span></span> <span data-ttu-id="312db-198">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="312db-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="312db-199">b.</span><span class="sxs-lookup"><span data-stu-id="312db-199">b.</span></span> <span data-ttu-id="312db-200">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="312db-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="312db-201">c.</span><span class="sxs-lookup"><span data-stu-id="312db-201">c.</span></span> <span data-ttu-id="312db-202">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="312db-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="312db-203">d.</span><span class="sxs-lookup"><span data-stu-id="312db-203">d.</span></span> <span data-ttu-id="312db-204">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="312db-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="312db-205">Maken van een Online ArcGIS testgebruiker</span><span class="sxs-lookup"><span data-stu-id="312db-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="312db-206">In volgorde tooenable Azure AD gebruikers toolog in ArcGIS Online, moeten ze worden ingericht in ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="312db-206">In order tooenable Azure AD users toolog into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="312db-207">In geval van ArcGIS Online Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="312db-207">In hello case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="312db-208">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="312db-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="312db-209">Meld u bij tooyour **ArcGIS** tenant.</span><span class="sxs-lookup"><span data-stu-id="312db-209">Log in tooyour **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="312db-210">Klik op **leden UITNODIGEN**.</span><span class="sxs-lookup"><span data-stu-id="312db-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="312db-211">![Leden uitnodigen](./media/active-directory-saas-arcgis-tutorial/ic784747.png "leden uit te nodigen")</span><span class="sxs-lookup"><span data-stu-id="312db-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="312db-212">Selecteer **automatisch leden toevoegen zonder een e-mailbericht te verzenden**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="312db-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="312db-213">![Automatisch toevoegen van leden](./media/active-directory-saas-arcgis-tutorial/ic784748.png "automatisch toevoegen van leden")</span><span class="sxs-lookup"><span data-stu-id="312db-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="312db-214">Op Hallo **leden** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="312db-214">On hello **Members** dialog page, perform hello following steps:</span></span>
   
     <span data-ttu-id="312db-215">![Toevoegen en controleren](./media/active-directory-saas-arcgis-tutorial/ic784749.png "toevoegen en controleren")</span><span class="sxs-lookup"><span data-stu-id="312db-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="312db-216">a.</span><span class="sxs-lookup"><span data-stu-id="312db-216">a.</span></span> <span data-ttu-id="312db-217">Voer Hallo **e**, **voornaam**, en **achternaam** van een geldige AAD-account dat u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="312db-217">Enter hello **Email**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision.</span></span>
  
     <span data-ttu-id="312db-218">b.</span><span class="sxs-lookup"><span data-stu-id="312db-218">b.</span></span> <span data-ttu-id="312db-219">Klik op **toevoegen en bekijk**.</span><span class="sxs-lookup"><span data-stu-id="312db-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="312db-220">Bekijk Hallo gegevens die u hebt ingevoerd, en klik vervolgens op **leden toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="312db-220">Review hello data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="312db-221">![Lid toevoegen](./media/active-directory-saas-arcgis-tutorial/ic784750.png "lid toevoegen")</span><span class="sxs-lookup"><span data-stu-id="312db-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="312db-222">Hello Azure Active Directory-accounthouder wordt een e-mailbericht ontvangen en volg een koppeling tooconfirm hun account maken voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="312db-222">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="312db-223">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="312db-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="312db-224">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="312db-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooArcGIS Online.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="312db-226">**tooassign Britta Simon tooArcGIS Online uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="312db-226">**tooassign Britta Simon tooArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="312db-227">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="312db-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="312db-229">Selecteer in de lijst met de toepassingen van Hallo **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="312db-229">In hello applications list, select **ArcGIS Online**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="312db-231">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="312db-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="312db-233">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="312db-233">Click **Add** button.</span></span> <span data-ttu-id="312db-234">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="312db-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="312db-236">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="312db-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="312db-237">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="312db-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="312db-238">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="312db-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="312db-239">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="312db-239">Testing single sign-on</span></span>

<span data-ttu-id="312db-240">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="312db-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="312db-241">Wanneer u Online ArcGIS Hallo-tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour ArcGIS on line toepassing.</span><span class="sxs-lookup"><span data-stu-id="312db-241">When you click hello ArcGIS Online tile in hello Access Panel, you should get automatically signed-on tooyour ArcGIS Online application.</span></span>
<span data-ttu-id="312db-242">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="312db-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="312db-243">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="312db-243">Additional resources</span></span>

* [<span data-ttu-id="312db-244">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="312db-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="312db-245">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="312db-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

