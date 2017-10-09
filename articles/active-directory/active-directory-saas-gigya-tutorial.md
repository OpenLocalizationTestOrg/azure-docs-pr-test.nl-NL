---
title: 'Zelfstudie: Azure Active Directory-integratie met Gigya | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Gigya.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 1992c5ad09b097563377a488fbf5a375f6511020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="0e2d8-103">Zelfstudie: Azure Active Directory-integratie met Gigya</span><span class="sxs-lookup"><span data-stu-id="0e2d8-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="0e2d8-104">In deze zelfstudie leert u hoe toointegrate Gigya met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e2d8-104">In this tutorial, you learn how toointegrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e2d8-105">Gigya integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="0e2d8-105">Integrating Gigya with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0e2d8-106">U kunt beheren in Azure AD die tooGigya toegang heeft</span><span class="sxs-lookup"><span data-stu-id="0e2d8-106">You can control in Azure AD who has access tooGigya</span></span>
- <span data-ttu-id="0e2d8-107">U kunt uw gebruikers tooautomatically get aangemelde tooGigya (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="0e2d8-107">You can enable your users tooautomatically get signed-on tooGigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0e2d8-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="0e2d8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0e2d8-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0e2d8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e2d8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0e2d8-110">Prerequisites</span></span>

<span data-ttu-id="0e2d8-111">Azure AD-integratie met Gigya tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="0e2d8-111">tooconfigure Azure AD integration with Gigya, you need hello following items:</span></span>

- <span data-ttu-id="0e2d8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="0e2d8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e2d8-113">Een Gigya eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="0e2d8-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e2d8-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e2d8-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="0e2d8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e2d8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e2d8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e2d8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e2d8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="0e2d8-118">Scenario description</span></span>
<span data-ttu-id="0e2d8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e2d8-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="0e2d8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e2d8-121">Het toevoegen van Gigya van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0e2d8-121">Adding Gigya from hello gallery</span></span>
2. <span data-ttu-id="0e2d8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0e2d8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-hello-gallery"></a><span data-ttu-id="0e2d8-123">Het toevoegen van Gigya van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0e2d8-123">Adding Gigya from hello gallery</span></span>
<span data-ttu-id="0e2d8-124">tooconfigure hello integratie van Gigya in Azure AD, moet u tooadd Gigya uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-124">tooconfigure hello integration of Gigya into Azure AD, you need tooadd Gigya from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0e2d8-125">**tooadd Gigya via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0e2d8-125">**tooadd Gigya from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e2d8-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0e2d8-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0e2d8-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="0e2d8-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="0e2d8-133">Typ in het zoekvak Hallo **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-133">In hello search box, type **Gigya**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="0e2d8-135">Selecteer in het deelvenster resultaten hello, **Gigya**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-135">In hello results panel, select **Gigya**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0e2d8-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0e2d8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0e2d8-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Gigya op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e2d8-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Gigya is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Gigya is tooa user in Azure AD.</span></span> <span data-ttu-id="0e2d8-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Gigya toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-140">In other words, a link relationship between an Azure AD user and hello related user in Gigya needs toobe established.</span></span>

<span data-ttu-id="0e2d8-141">Wijs in Gigya, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-141">In Gigya, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0e2d8-142">tooconfigure en eenmalige aanmelding Azure AD-test met Gigya, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0e2d8-142">tooconfigure and test Azure AD single sign-on with Gigya, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0e2d8-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0e2d8-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e2d8-145">**[Maken van een testgebruiker Gigya](#creating-a-gigya-test-user)**  -toohave een equivalent van Britta Simon in Gigya die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - toohave a counterpart of Britta Simon in Gigya that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e2d8-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e2d8-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0e2d8-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="0e2d8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0e2d8-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Gigya configureren.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="0e2d8-150">**Azure AD tooconfigure eenmalige aanmelding met Gigya, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0e2d8-150">**tooconfigure Azure AD single sign-on with Gigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e2d8-151">In de Azure-portal op Hallo Hallo **Gigya** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-151">In hello Azure portal, on hello **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="0e2d8-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="0e2d8-155">Op Hallo **Gigya domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0e2d8-155">On hello **Gigya Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="0e2d8-157">a.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-157">a.</span></span> <span data-ttu-id="0e2d8-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="0e2d8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="0e2d8-159">b.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-159">b.</span></span> <span data-ttu-id="0e2d8-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="0e2d8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0e2d8-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-161">These values are not real.</span></span> <span data-ttu-id="0e2d8-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0e2d8-163">Neem contact op met [Gigya Client ondersteuningsteam](https://www.gigya.com/support-policy/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) tooget these values.</span></span> 
 
4. <span data-ttu-id="0e2d8-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="0e2d8-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0e2d8-168">Op Hallo **Gigya configuratie** sectie, klikt u op **configureren Gigya** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-168">On hello **Gigya Configuration** section, click **Configure Gigya** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0e2d8-169">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="0e2d8-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="0e2d8-171">In een ander browservenster, meld u bij uw bedrijf Gigya site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="0e2d8-172">Ga te**instellingen \> SAML aanmelding**, en klik vervolgens op Hallo **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-172">Go too**Settings \> SAML Login**, and then click hello **Add** button.</span></span>
   
    <span data-ttu-id="0e2d8-173">![SAML-aanmelding](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML-aanmelding")</span><span class="sxs-lookup"><span data-stu-id="0e2d8-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="0e2d8-174">In Hallo **SAML aanmelding** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0e2d8-174">In hello **SAML Login** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="0e2d8-175">![De SAML-configuratie](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML-configuratie")</span><span class="sxs-lookup"><span data-stu-id="0e2d8-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="0e2d8-176">a.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-176">a.</span></span> <span data-ttu-id="0e2d8-177">In Hallo **naam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-177">In hello **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="0e2d8-178">b.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-178">b.</span></span> <span data-ttu-id="0e2d8-179">In **verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-179">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="0e2d8-180">c.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-180">c.</span></span> <span data-ttu-id="0e2d8-181">In **Single Sign-On Service-URL** textbox plakken Hallo-waarde van **Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-181">In **Single Sign-On Service URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="0e2d8-182">d.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-182">d.</span></span> <span data-ttu-id="0e2d8-183">In **indeling naam-ID** textbox plakken Hallo-waarde van **indeling van de id** die u hebt gekopieerd vanuit Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-183">In **Name ID Format** textbox, paste hello value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="0e2d8-184">e.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-184">e.</span></span> <span data-ttu-id="0e2d8-185">De base-64 gecodeerde certificaat openen in Kladblok gedownload vanuit Azure-portal kopie Hallo inhoud ervan naar het Klembord en plak deze toohello **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="0e2d8-186">f.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-186">f.</span></span> <span data-ttu-id="0e2d8-187">Klik op **instellingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="0e2d8-188">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0e2d8-189">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0e2d8-190">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0e2d8-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0e2d8-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="0e2d8-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="0e2d8-192">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="0e2d8-194">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0e2d8-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e2d8-195">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0e2d8-197">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0e2d8-199">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0e2d8-201">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0e2d8-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0e2d8-203">a.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-203">a.</span></span> <span data-ttu-id="0e2d8-204">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e2d8-205">b.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-205">b.</span></span> <span data-ttu-id="0e2d8-206">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0e2d8-207">c.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-207">c.</span></span> <span data-ttu-id="0e2d8-208">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0e2d8-209">d.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-209">d.</span></span> <span data-ttu-id="0e2d8-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="0e2d8-211">Een testgebruiker Gigya maken</span><span class="sxs-lookup"><span data-stu-id="0e2d8-211">Creating a Gigya test user</span></span>

<span data-ttu-id="0e2d8-212">In de volgorde tooenable Azure AD gebruikers toolog in Gigya, moeten ze worden ingericht in Gigya.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-212">In order tooenable Azure AD users toolog into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="0e2d8-213">In geval van Gigya Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-213">In hello case of Gigya, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="0e2d8-214">tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="0e2d8-214">tooprovision a user accounts, perform hello following steps:</span></span>

1. <span data-ttu-id="0e2d8-215">Meld u bij tooyour **Gigya** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-215">Log in tooyour **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="0e2d8-216">Ga te**Admin \> gebruikers beheren**, en klik vervolgens op **gebruikers uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-216">Go too**Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="0e2d8-217">![Gebruikers beheren](./media/active-directory-saas-gigya-tutorial/ic789535.png "gebruikers beheren")</span><span class="sxs-lookup"><span data-stu-id="0e2d8-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="0e2d8-218">Uitvoeren in het dialoogvenster Hallo gebruikers uitnodigen, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0e2d8-218">On hello Invite Users dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="0e2d8-219">![Gebruikers uitnodigen](./media/active-directory-saas-gigya-tutorial/ic789536.png "gebruikers uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="0e2d8-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="0e2d8-220">a.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-220">a.</span></span> <span data-ttu-id="0e2d8-221">In Hallo **e** textbox type Hallo e-mailalias op van een geldige Azure Active Directory-account dat u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-221">In hello **Email** textbox, type hello email alias of a valid Azure Active Directory account you want tooprovision.</span></span>
    
    <span data-ttu-id="0e2d8-222">b.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-222">b.</span></span> <span data-ttu-id="0e2d8-223">Klik op **gebruiker uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="0e2d8-224">Hello Azure Active Directory-accounthouder ontvangt een e-mailbericht met een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-224">hello Azure Active Directory account holder will receive an email that includes a link tooconfirm hello account before it becomes active.</span></span>
    > 
    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0e2d8-225">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e2d8-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0e2d8-226">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooGigya toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGigya.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="0e2d8-228">**tooassign Britta Simon tooGigya, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0e2d8-228">**tooassign Britta Simon tooGigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e2d8-229">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="0e2d8-231">Selecteer in de lijst met de toepassingen van Hallo **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-231">In hello applications list, select **Gigya**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="0e2d8-233">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="0e2d8-235">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-235">Click **Add** button.</span></span> <span data-ttu-id="0e2d8-236">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="0e2d8-238">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0e2d8-239">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e2d8-240">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0e2d8-241">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0e2d8-241">Testing single sign-on</span></span>

<span data-ttu-id="0e2d8-242">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="0e2d8-243">Als u op Hallo Gigya tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Gigya toepassing.</span><span class="sxs-lookup"><span data-stu-id="0e2d8-243">When you click hello Gigya tile in hello Access Panel, you should get automatically signed-on tooyour Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0e2d8-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="0e2d8-244">Additional resources</span></span>

* [<span data-ttu-id="0e2d8-245">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e2d8-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e2d8-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0e2d8-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

