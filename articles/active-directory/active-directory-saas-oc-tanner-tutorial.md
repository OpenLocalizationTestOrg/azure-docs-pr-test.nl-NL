---
title: 'Zelfstudie: Azure Active Directory-integratie met O.C. Tan - AppreciateHub | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en O.C. Tan - AppreciateHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 45052cf56e35746d7df5910162e40e3bbcad1aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="b4b32-105">Zelfstudie: Azure Active Directory-integratie met O.C.</span><span class="sxs-lookup"><span data-stu-id="b4b32-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="b4b32-106">Tan - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="b4b32-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="b4b32-107">In deze zelfstudie leert u hoe toointegrate O.C.</span><span class="sxs-lookup"><span data-stu-id="b4b32-107">In this tutorial, you learn how toointegrate O.C.</span></span> <span data-ttu-id="b4b32-108">Tan - AppreciateHub met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b4b32-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b4b32-109">Integratie van O.C.</span><span class="sxs-lookup"><span data-stu-id="b4b32-109">Integrating O.C.</span></span> <span data-ttu-id="b4b32-110">Tan - AppreciateHub met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b4b32-110">Tanner - AppreciateHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b4b32-111">U kunt beheren in Azure AD die tooO.C toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="b4b32-111">You can control in Azure AD who has access tooO.C.</span></span> <span data-ttu-id="b4b32-112">Tan - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="b4b32-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="b4b32-113">U kunt uw gebruikers tooautomatically get aangemelde tooO.C inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b4b32-113">You can enable your users tooautomatically get signed-on tooO.C.</span></span> <span data-ttu-id="b4b32-114">Tan - AppreciateHub (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="b4b32-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b4b32-115">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b4b32-115">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b4b32-116">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b4b32-116">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4b32-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b4b32-117">Prerequisites</span></span>

<span data-ttu-id="b4b32-118">Azure AD-integratie met O.C. tooconfigure</span><span class="sxs-lookup"><span data-stu-id="b4b32-118">tooconfigure Azure AD integration with O.C.</span></span> <span data-ttu-id="b4b32-119">Tan - AppreciateHub, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="b4b32-119">Tanner - AppreciateHub, you need hello following items:</span></span>

- <span data-ttu-id="b4b32-120">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b4b32-120">An Azure AD subscription</span></span>
- <span data-ttu-id="b4b32-121">EEN O.C.</span><span class="sxs-lookup"><span data-stu-id="b4b32-121">A O.C.</span></span> <span data-ttu-id="b4b32-122">Tan - AppreciateHub eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b4b32-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b4b32-123">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b4b32-123">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b4b32-124">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b4b32-124">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b4b32-125">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b4b32-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b4b32-126">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b4b32-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b4b32-127">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b4b32-127">Scenario description</span></span>
<span data-ttu-id="b4b32-128">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b4b32-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b4b32-129">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b4b32-129">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b4b32-130">O.C. toevoegen</span><span class="sxs-lookup"><span data-stu-id="b4b32-130">Adding O.C.</span></span> <span data-ttu-id="b4b32-131">Tan - AppreciateHub uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b4b32-131">Tanner - AppreciateHub from hello gallery</span></span>
2. <span data-ttu-id="b4b32-132">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b4b32-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-hello-gallery"></a><span data-ttu-id="b4b32-133">O.C. toevoegen</span><span class="sxs-lookup"><span data-stu-id="b4b32-133">Adding O.C.</span></span> <span data-ttu-id="b4b32-134">Tan - AppreciateHub uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b4b32-134">Tanner - AppreciateHub from hello gallery</span></span>
<span data-ttu-id="b4b32-135">tooconfigure hello integratie van O.C.</span><span class="sxs-lookup"><span data-stu-id="b4b32-135">tooconfigure hello integration of O.C.</span></span> <span data-ttu-id="b4b32-136">Tan - AppreciateHub in Azure AD, moet u tooadd O.C.</span><span class="sxs-lookup"><span data-stu-id="b4b32-136">Tanner - AppreciateHub into Azure AD, you need tooadd O.C.</span></span> <span data-ttu-id="b4b32-137">Tan - AppreciateHub uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b4b32-137">Tanner - AppreciateHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b4b32-138">**tooadd O.C. Tan - AppreciateHub via Hallo gallery Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b4b32-138">**tooadd O.C. Tanner - AppreciateHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4b32-139">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b4b32-139">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b4b32-141">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b4b32-141">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b4b32-142">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b4b32-142">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b4b32-144">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b4b32-144">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b4b32-146">Typ in het zoekvak Hallo **O.C. Tan - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="b4b32-146">In hello search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="b4b32-148">Selecteer in het deelvenster resultaten hello, **O.C. Tan - AppreciateHub**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b4b32-148">In hello results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b4b32-150">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b4b32-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b4b32-151">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met O.C.</span><span class="sxs-lookup"><span data-stu-id="b4b32-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="b4b32-152">Tan - AppreciateHub op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b4b32-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b4b32-153">Voor één aanmelding toowork moet Azure AD tooknow welke gebruiker van het bijbehorende equivalent Hallo in O.C.</span><span class="sxs-lookup"><span data-stu-id="b4b32-153">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in O.C.</span></span> <span data-ttu-id="b4b32-154">Tan - AppreciateHub is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4b32-154">Tanner - AppreciateHub is tooa user in Azure AD.</span></span> <span data-ttu-id="b4b32-155">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in O.C.</span><span class="sxs-lookup"><span data-stu-id="b4b32-155">In other words, a link relationship between an Azure AD user and hello related user in O.C.</span></span> <span data-ttu-id="b4b32-156">Tan - AppreciateHub moet toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="b4b32-156">Tanner - AppreciateHub needs toobe established.</span></span>

<span data-ttu-id="b4b32-157">In O.C.</span><span class="sxs-lookup"><span data-stu-id="b4b32-157">In O.C.</span></span> <span data-ttu-id="b4b32-158">Tan - AppreciateHub, toewijzen Hallo waarde Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="b4b32-158">Tanner - AppreciateHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b4b32-159">tooconfigure en eenmalige aanmelding Azure AD-test met O.C.</span><span class="sxs-lookup"><span data-stu-id="b4b32-159">tooconfigure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="b4b32-160">Tan - AppreciateHub, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b4b32-160">Tanner - AppreciateHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b4b32-161">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="b4b32-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b4b32-162">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b4b32-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b4b32-163">**[Maken van een O.C. Tan - testgebruiker AppreciateHub](#creating-a-oc-tanner---appreciatehub-test-user)**  -toohave een equivalent van Britta Simon in O.C.</span><span class="sxs-lookup"><span data-stu-id="b4b32-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - toohave a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="b4b32-164">Tan - AppreciateHub die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b4b32-164">Tanner - AppreciateHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b4b32-165">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b4b32-165">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b4b32-166">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b4b32-166">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b4b32-167">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b4b32-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b4b32-168">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw O.C. configureren</span><span class="sxs-lookup"><span data-stu-id="b4b32-168">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="b4b32-169">Tan - AppreciateHub toepassing.</span><span class="sxs-lookup"><span data-stu-id="b4b32-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="b4b32-170">**Azure AD tooconfigure eenmalige aanmelding met O.C. Tan - AppreciateHub, Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="b4b32-170">**tooconfigure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4b32-171">In de Azure-portal op Hallo Hallo **O.C. Tan - AppreciateHub** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b4b32-171">In hello Azure portal, on hello **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b4b32-173">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b4b32-173">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="b4b32-175">Op Hallo **O.C. Tan - URL's en AppreciateHub domein** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b4b32-175">On hello **O.C. Tanner - AppreciateHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="b4b32-177">a.</span><span class="sxs-lookup"><span data-stu-id="b4b32-177">a.</span></span> <span data-ttu-id="b4b32-178">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="b4b32-178">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b4b32-179">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="b4b32-179">This value is not real.</span></span> <span data-ttu-id="b4b32-180">Deze waarde met de werkelijke antwoord-URL Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b4b32-180">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="b4b32-181">Neem contact op met [O.C. Tan - ondersteuningsteam AppreciateHub](mailto:sso@octanner.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="b4b32-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) tooget this value.</span></span>

    <span data-ttu-id="b4b32-182">b.</span><span class="sxs-lookup"><span data-stu-id="b4b32-182">b.</span></span> <span data-ttu-id="b4b32-183">Open Hallo metagegevensbestand met Hallo koppeling: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="b4b32-183">Open hello metadata file using hello following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="b4b32-184">c.</span><span class="sxs-lookup"><span data-stu-id="b4b32-184">c.</span></span> <span data-ttu-id="b4b32-185">Zoek Hallo **md:AssertionConsumerService** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="b4b32-185">Locate hello **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="b4b32-186">d.</span><span class="sxs-lookup"><span data-stu-id="b4b32-186">d.</span></span> <span data-ttu-id="b4b32-187">Kopieer de waarde Hallo Hallo **locatie** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="b4b32-187">Copy hello value of hello **Location** attribute.</span></span> 
   
    ![App-instellingen configureren][12]
   
    <span data-ttu-id="b4b32-189">e.</span><span class="sxs-lookup"><span data-stu-id="b4b32-189">e.</span></span> <span data-ttu-id="b4b32-190">In Hallo **aanmelding op URL** textbox voorbij Hallo-waarde die u hebt verkregen in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="b4b32-190">In hello **Sign On URL** textbox, past hello value you have obtained in hello previous step.</span></span>

4. <span data-ttu-id="b4b32-191">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b4b32-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="b4b32-193">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b4b32-193">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b4b32-195">tooconfigure eenmalige aanmelding op **O.C. Tan - AppreciateHub** zijde, moet u toosend Hallo gedownload **Metadata XML** te[O.C. Tan - ondersteuningsteam AppreciateHub](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="b4b32-195">tooconfigure single sign-on on **O.C. Tanner - AppreciateHub** side, you need toosend hello downloaded **Metadata XML** too[O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="b4b32-196">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="b4b32-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b4b32-197">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="b4b32-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b4b32-198">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b4b32-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b4b32-199">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b4b32-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="b4b32-200">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b4b32-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b4b32-202">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b4b32-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4b32-203">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b4b32-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b4b32-205">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b4b32-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b4b32-207">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="b4b32-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b4b32-209">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b4b32-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b4b32-211">a.</span><span class="sxs-lookup"><span data-stu-id="b4b32-211">a.</span></span> <span data-ttu-id="b4b32-212">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b4b32-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b4b32-213">b.</span><span class="sxs-lookup"><span data-stu-id="b4b32-213">b.</span></span> <span data-ttu-id="b4b32-214">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b4b32-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b4b32-215">c.</span><span class="sxs-lookup"><span data-stu-id="b4b32-215">c.</span></span> <span data-ttu-id="b4b32-216">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b4b32-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b4b32-217">d.</span><span class="sxs-lookup"><span data-stu-id="b4b32-217">d.</span></span> <span data-ttu-id="b4b32-218">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b4b32-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="b4b32-219">Maken van een O.C.</span><span class="sxs-lookup"><span data-stu-id="b4b32-219">Creating a O.C.</span></span> <span data-ttu-id="b4b32-220">Tan - AppreciateHub testgebruiker</span><span class="sxs-lookup"><span data-stu-id="b4b32-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="b4b32-221">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in O.C. van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="b4b32-221">hello objective of this section is toocreate a user called Britta Simon in O.C.</span></span> <span data-ttu-id="b4b32-222">Tan - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="b4b32-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="b4b32-223">**toocreate een gebruiker is aangeroepen terwijl Britta Simon O.C. Tan - AppreciateHub, Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="b4b32-223">**toocreate a user called Britta Simon in O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

<span data-ttu-id="b4b32-224">Vraag uw [O.C. Tan - ondersteuningsteam AppreciateHub](mailto:sso@octanner.com) toocreate een gebruiker die heeft als nameID kenmerk Hallo dezelfde als de gebruikersnaam Hallo van Britta Simon in Azure AD waarde.</span><span class="sxs-lookup"><span data-stu-id="b4b32-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) toocreate a user that has as nameID attribute hello same value as hello user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b4b32-225">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4b32-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b4b32-226">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooO.C toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="b4b32-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooO.C.</span></span> <span data-ttu-id="b4b32-227">Tan - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="b4b32-227">Tanner - AppreciateHub.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b4b32-229">**tooassign Britta Simon tooO.C. Tan - AppreciateHub, Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="b4b32-229">**tooassign Britta Simon tooO.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4b32-230">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b4b32-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b4b32-232">Selecteer in de lijst met de toepassingen van Hallo **O.C. Tan - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="b4b32-232">In hello applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="b4b32-234">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b4b32-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b4b32-236">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b4b32-236">Click **Add** button.</span></span> <span data-ttu-id="b4b32-237">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b4b32-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b4b32-239">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="b4b32-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b4b32-240">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b4b32-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b4b32-241">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b4b32-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b4b32-242">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b4b32-242">Testing single sign-on</span></span>

<span data-ttu-id="b4b32-243">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="b4b32-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="b4b32-244">Wanneer u klikt op Hallo O.C.</span><span class="sxs-lookup"><span data-stu-id="b4b32-244">When you click hello O.C.</span></span> <span data-ttu-id="b4b32-245">Tan - tegel in AppreciateHub Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour O.C.</span><span class="sxs-lookup"><span data-stu-id="b4b32-245">Tanner - AppreciateHub tile in hello Access Panel, you should get automatically signed-on tooyour O.C.</span></span> <span data-ttu-id="b4b32-246">Tan - AppreciateHub toepassing.</span><span class="sxs-lookup"><span data-stu-id="b4b32-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b4b32-247">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b4b32-247">Additional resources</span></span>

* [<span data-ttu-id="b4b32-248">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4b32-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b4b32-249">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b4b32-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

