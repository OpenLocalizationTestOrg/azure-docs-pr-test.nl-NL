---
title: 'Zelfstudie: Azure Active Directory-integratie met Panorama9 | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Panorama9.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 548fb6434d920e076db98a0193f8dfdf8a958a91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="2bc26-103">Zelfstudie: Azure Active Directory-integratie met Panorama9</span><span class="sxs-lookup"><span data-stu-id="2bc26-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="2bc26-104">In deze zelfstudie leert u hoe toointegrate Panorama9 met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2bc26-104">In this tutorial, you learn how toointegrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2bc26-105">Panorama9 integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2bc26-105">Integrating Panorama9 with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2bc26-106">U kunt beheren in Azure AD die tooPanorama9 toegang heeft</span><span class="sxs-lookup"><span data-stu-id="2bc26-106">You can control in Azure AD who has access tooPanorama9</span></span>
- <span data-ttu-id="2bc26-107">U kunt uw gebruikers tooautomatically get aangemelde tooPanorama9 inschakelen (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="2bc26-107">You can enable your users tooautomatically get signed-on tooPanorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2bc26-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2bc26-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2bc26-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2bc26-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bc26-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2bc26-110">Prerequisites</span></span>

<span data-ttu-id="2bc26-111">Azure AD-integratie met Panorama9 tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="2bc26-111">tooconfigure Azure AD integration with Panorama9, you need hello following items:</span></span>

- <span data-ttu-id="2bc26-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2bc26-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2bc26-113">Een Panorama9 eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2bc26-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2bc26-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2bc26-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2bc26-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2bc26-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2bc26-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2bc26-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2bc26-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2bc26-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2bc26-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2bc26-118">Scenario description</span></span>
<span data-ttu-id="2bc26-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2bc26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2bc26-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2bc26-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2bc26-121">Het toevoegen van Panorama9 van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2bc26-121">Adding Panorama9 from hello gallery</span></span>
2. <span data-ttu-id="2bc26-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2bc26-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-hello-gallery"></a><span data-ttu-id="2bc26-123">Het toevoegen van Panorama9 van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2bc26-123">Adding Panorama9 from hello gallery</span></span>
<span data-ttu-id="2bc26-124">tooconfigure hello integratie van Panorama9 in Azure AD, moet u tooadd Panorama9 uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2bc26-124">tooconfigure hello integration of Panorama9 into Azure AD, you need tooadd Panorama9 from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2bc26-125">**tooadd Panorama9 via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2bc26-125">**tooadd Panorama9 from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2bc26-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2bc26-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2bc26-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2bc26-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2bc26-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bc26-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2bc26-133">Typ in het zoekvak Hallo **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-133">In hello search box, type **Panorama9**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="2bc26-135">Selecteer in het deelvenster resultaten hello, **Panorama9**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2bc26-135">In hello results panel, select **Panorama9**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2bc26-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2bc26-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="2bc26-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Panorama9 op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="2bc26-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2bc26-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Panorama9 is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bc26-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panorama9 is tooa user in Azure AD.</span></span> <span data-ttu-id="2bc26-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Panorama9 toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="2bc26-140">In other words, a link relationship between an Azure AD user and hello related user in Panorama9 needs toobe established.</span></span>

<span data-ttu-id="2bc26-141">Wijs in Panorama9, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="2bc26-141">In Panorama9, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2bc26-142">tooconfigure en eenmalige aanmelding Azure AD-test met Panorama9, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2bc26-142">tooconfigure and test Azure AD single sign-on with Panorama9, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2bc26-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="2bc26-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2bc26-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2bc26-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2bc26-145">**[Maken van een testgebruiker Panorama9](#creating-a-panorama9-test-user)**  -toohave een equivalent van Britta Simon in Panorama9 die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2bc26-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - toohave a counterpart of Britta Simon in Panorama9 that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2bc26-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2bc26-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2bc26-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2bc26-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2bc26-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2bc26-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2bc26-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Panorama9 configureren.</span><span class="sxs-lookup"><span data-stu-id="2bc26-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="2bc26-150">**Azure AD tooconfigure eenmalige aanmelding met Panorama9, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2bc26-150">**tooconfigure Azure AD single sign-on with Panorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="2bc26-151">In de Azure-portal op Hallo Hallo **Panorama9** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-151">In hello Azure portal, on hello **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2bc26-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2bc26-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="2bc26-155">Op Hallo **Panorama9 domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2bc26-155">On hello **Panorama9 Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="2bc26-157">a.</span><span class="sxs-lookup"><span data-stu-id="2bc26-157">a.</span></span> <span data-ttu-id="2bc26-158">In Hallo **aanmeldings-URL** textbox, typ een URL als:`https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="2bc26-158">In hello **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="2bc26-159">b.</span><span class="sxs-lookup"><span data-stu-id="2bc26-159">b.</span></span> <span data-ttu-id="2bc26-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="2bc26-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2bc26-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="2bc26-161">These values are not real.</span></span> <span data-ttu-id="2bc26-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="2bc26-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2bc26-163">Neem contact op met [Panorama9 Client ondersteuningsteam](https://support.panorama9.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2bc26-163">Contact [Panorama9 Client support team](https://support.panorama9.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="2bc26-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="2bc26-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="2bc26-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2bc26-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2bc26-168">Op Hallo **Panorama9 configuratie** sectie, klikt u op **configureren Panorama9** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="2bc26-168">On hello **Panorama9 Configuration** section, click **Configure Panorama9** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2bc26-169">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="2bc26-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="2bc26-171">In een ander browservenster, meld u bij uw bedrijf Panorama9 site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="2bc26-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="2bc26-172">Klik in de werkbalk bovenaan Hallo Hallo op **beheren**, en klik vervolgens op **extensies**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-172">In hello toolbar on hello top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="2bc26-173">![Extensies](./media/active-directory-saas-panorama9-tutorial/ic790023.png "extensies")</span><span class="sxs-lookup"><span data-stu-id="2bc26-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="2bc26-174">Op Hallo **extensies** dialoogvenster, klikt u op **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-174">On hello **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="2bc26-175">![Eenmalige aanmelding](./media/active-directory-saas-panorama9-tutorial/ic790024.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="2bc26-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="2bc26-176">In Hallo **instellingen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2bc26-176">In hello **Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="2bc26-177">![Instellingen](./media/active-directory-saas-panorama9-tutorial/ic790025.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="2bc26-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="2bc26-178">a.</span><span class="sxs-lookup"><span data-stu-id="2bc26-178">a.</span></span> <span data-ttu-id="2bc26-179">In **identiteit provider URL** textbox plakken Hallo-waarde van **Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2bc26-179">In **Identity provider URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="2bc26-180">b.</span><span class="sxs-lookup"><span data-stu-id="2bc26-180">b.</span></span> <span data-ttu-id="2bc26-181">In **vingerafdruk van certificaat** textbox plakken Hallo **vingerafdruk** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2bc26-181">In **Certificate fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="2bc26-182">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2bc26-183">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="2bc26-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2bc26-184">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="2bc26-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2bc26-185">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2bc26-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2bc26-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2bc26-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="2bc26-187">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2bc26-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2bc26-189">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2bc26-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2bc26-190">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2bc26-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2bc26-192">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2bc26-194">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="2bc26-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2bc26-196">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2bc26-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2bc26-198">a.</span><span class="sxs-lookup"><span data-stu-id="2bc26-198">a.</span></span> <span data-ttu-id="2bc26-199">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2bc26-200">b.</span><span class="sxs-lookup"><span data-stu-id="2bc26-200">b.</span></span> <span data-ttu-id="2bc26-201">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2bc26-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2bc26-202">c.</span><span class="sxs-lookup"><span data-stu-id="2bc26-202">c.</span></span> <span data-ttu-id="2bc26-203">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2bc26-204">d.</span><span class="sxs-lookup"><span data-stu-id="2bc26-204">d.</span></span> <span data-ttu-id="2bc26-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="2bc26-206">Een testgebruiker Panorama9 maken</span><span class="sxs-lookup"><span data-stu-id="2bc26-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="2bc26-207">In de volgorde tooenable Azure AD gebruikers toolog in Panorama9, moeten ze worden ingericht in Panorama9.</span><span class="sxs-lookup"><span data-stu-id="2bc26-207">In order tooenable Azure AD users toolog into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="2bc26-208">In geval van Panorama9 Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="2bc26-208">In hello case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="2bc26-209">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2bc26-209">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="2bc26-210">Meld u bij tooyour **Panorama9** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="2bc26-210">Log in tooyour **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="2bc26-211">Klik in het menu bovenaan Hallo Hallo **beheren**, en klik vervolgens op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-211">In hello menu on hello top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="2bc26-212">![Gebruikers](./media/active-directory-saas-panorama9-tutorial/ic790027.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="2bc26-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="2bc26-213">Klik in de sectie gebruikers hello,  **+**  tooadd nieuwe gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2bc26-213">In hello Users section, Click **+** tooadd new user.</span></span>

 <span data-ttu-id="2bc26-214">![Gebruikers](./media/active-directory-saas-panorama9-tutorial/ic790028.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="2bc26-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="2bc26-215">Ga toohello gebruiker gegevenssectie type Hallo e-mailadres van een geldige Azure Active Directory-gebruiker gewenste tooprovision in Hallo **e** textbox.</span><span class="sxs-lookup"><span data-stu-id="2bc26-215">Go toohello User data section, type hello email address of a valid Azure Active Directory user you want tooprovision into hello **Email** textbox.</span></span>

5. <span data-ttu-id="2bc26-216">Afkomstig zijn van toohello sectie gebruikers, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-216">Come toohello Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="2bc26-217">Hello Azure Active Directory-accounthouder ontvangt een e-mailbericht en een koppeling tooconfirm volgt hun account voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="2bc26-217">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2bc26-218">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bc26-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2bc26-219">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooPanorama9 toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="2bc26-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanorama9.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2bc26-221">**tooassign Britta Simon tooPanorama9, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2bc26-221">**tooassign Britta Simon tooPanorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="2bc26-222">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2bc26-224">Selecteer in de lijst met de toepassingen van Hallo **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-224">In hello applications list, select **Panorama9**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="2bc26-226">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2bc26-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2bc26-228">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2bc26-228">Click **Add** button.</span></span> <span data-ttu-id="2bc26-229">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bc26-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2bc26-231">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="2bc26-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2bc26-232">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bc26-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2bc26-233">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bc26-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2bc26-234">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2bc26-234">Testing single sign-on</span></span>

<span data-ttu-id="2bc26-235">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="2bc26-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2bc26-236">Als u op Hallo Panorama9 tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooPanorama9 toepassing.</span><span class="sxs-lookup"><span data-stu-id="2bc26-236">When you click hello Panorama9 tile in hello Access Panel, you should get automatically signed-on tooPanorama9 application.</span></span>
<span data-ttu-id="2bc26-237">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2bc26-237">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2bc26-238">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2bc26-238">Additional resources</span></span>

* [<span data-ttu-id="2bc26-239">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2bc26-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2bc26-240">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2bc26-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

