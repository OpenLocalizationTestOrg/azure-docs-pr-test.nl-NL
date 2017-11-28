---
title: 'Zelfstudie: Azure Active Directory-integratie met BC in Hallo Cloud | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en BC in Hallo Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7dc40d2c-6349-40cb-b304-b098bd03a66c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/1/2017
ms.author: jeedes
ms.openlocfilehash: e81ffb522b2c96c7e9b2919abd8d3b199c295eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bc-in-hello-cloud"></a><span data-ttu-id="1c1df-103">Zelfstudie: Azure Active Directory-integratie met BC in Hallo Cloud</span><span class="sxs-lookup"><span data-stu-id="1c1df-103">Tutorial: Azure Active Directory integration with BC in hello Cloud</span></span>

<span data-ttu-id="1c1df-104">In deze zelfstudie leert u hoe toointegrate BC in Hallo Cloud met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1c1df-104">In this tutorial, you learn how toointegrate BC in hello Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c1df-105">BC integreren in Hallo Cloud met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1c1df-105">Integrating BC in hello Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1c1df-106">U kunt beheren in Azure AD die toegang tooBC in Hallo Cloud heeft</span><span class="sxs-lookup"><span data-stu-id="1c1df-106">You can control in Azure AD who has access tooBC in hello Cloud</span></span>
- <span data-ttu-id="1c1df-107">U kunt uw gebruikers tooautomatically get aangemelde tooBC in Hallo Cloud (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="1c1df-107">You can enable your users tooautomatically get signed-on tooBC in hello Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1c1df-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1c1df-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1c1df-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1c1df-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c1df-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1c1df-110">Prerequisites</span></span>

<span data-ttu-id="1c1df-111">Azure AD-integratie met BC in Hallo Cloud tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="1c1df-111">tooconfigure Azure AD integration with BC in hello Cloud, you need hello following items:</span></span>

- <span data-ttu-id="1c1df-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1c1df-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c1df-113">Een BC in Hallo Cloud eenmalige aanmelding voor ingeschakelde abonnement</span><span class="sxs-lookup"><span data-stu-id="1c1df-113">A BC in hello Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c1df-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1c1df-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c1df-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1c1df-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c1df-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1c1df-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1c1df-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c1df-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c1df-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1c1df-118">Scenario description</span></span>
<span data-ttu-id="1c1df-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1c1df-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c1df-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1c1df-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c1df-121">BC toe te voegen in de Cloud uit de galerie Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="1c1df-121">Adding BC in hello Cloud from hello gallery</span></span>
2. <span data-ttu-id="1c1df-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1c1df-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bc-in-hello-cloud-from-hello-gallery"></a><span data-ttu-id="1c1df-123">BC toe te voegen in de Cloud uit de galerie Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="1c1df-123">Adding BC in hello Cloud from hello gallery</span></span>
<span data-ttu-id="1c1df-124">tooconfigure hello integratie van BC in Hallo Cloud met Azure AD, moet u tooadd BC in Hallo Cloud uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1c1df-124">tooconfigure hello integration of BC in hello Cloud into Azure AD, you need tooadd BC in hello Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1c1df-125">**tooadd BC in de Cloud via Hallo gallery Hallo uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1c1df-125">**tooadd BC in hello Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c1df-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1c1df-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1c1df-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1c1df-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1c1df-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1c1df-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1c1df-131">de nieuwe toepassing tooadd, klikt u op **toevoegen** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c1df-131">tooadd new application, click **Add** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1c1df-133">Typ in het zoekvak Hallo **BC in Hallo Cloud**.</span><span class="sxs-lookup"><span data-stu-id="1c1df-133">In hello search box, type **BC in hello Cloud**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_search.png)

5. <span data-ttu-id="1c1df-135">Selecteer in het deelvenster resultaten hello, **BC in Hallo Cloud**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1c1df-135">In hello results panel, select **BC in hello Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1c1df-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1c1df-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1c1df-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met BC in de Cloud op basis van een testgebruiker genaamd 'Britta Simon.' Hallo</span><span class="sxs-lookup"><span data-stu-id="1c1df-138">In this section, you configure and test Azure AD single sign-on with BC in hello Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1c1df-139">Voor één aanmelding toowork Azure AD moet tooknow welke Hallo equivalent in BC in Hallo Cloud is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c1df-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BC in hello Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="1c1df-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in BC in Hallo Cloud toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="1c1df-140">In other words, a link relationship between an Azure AD user and hello related user in BC in hello Cloud needs toobe established.</span></span>

<span data-ttu-id="1c1df-141">In BC in Hallo Cloud toewijzen Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="1c1df-141">In BC in hello Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1c1df-142">tooconfigure en eenmalige aanmelding Azure AD-test met BC in Hallo Cloud, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1c1df-142">tooconfigure and test Azure AD single sign-on with BC in hello Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1c1df-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="1c1df-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1c1df-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c1df-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1c1df-145">**[Maken van een BC in Hallo Cloud testgebruiker](#creating-a-bc-in-the-cloud-test-user)**  -toohave een equivalent van Britta Simon in BC in Hallo Cloud die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1c1df-145">**[Creating a BC in hello Cloud test user](#creating-a-bc-in-the-cloud-test-user)** - toohave a counterpart of Britta Simon in BC in hello Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1c1df-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1c1df-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1c1df-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1c1df-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1c1df-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1c1df-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1c1df-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw BC in de Cloud-toepassing hello configureren.</span><span class="sxs-lookup"><span data-stu-id="1c1df-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BC in hello Cloud application.</span></span>

<span data-ttu-id="1c1df-150">**Voer tooconfigure Azure AD eenmalige aanmelding met BC in Hallo Cloud, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1c1df-150">**tooconfigure Azure AD single sign-on with BC in hello Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c1df-151">In de Azure-portal op Hallo Hallo **BC in Hallo Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1c1df-151">In hello Azure portal, on hello **BC in hello Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1c1df-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1c1df-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_samlbase.png)

3. <span data-ttu-id="1c1df-155">Op Hallo **BC in Hallo Cloud-domein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1c1df-155">On hello **BC in hello Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_url.png)

    <span data-ttu-id="1c1df-157">a.</span><span class="sxs-lookup"><span data-stu-id="1c1df-157">a.</span></span> <span data-ttu-id="1c1df-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span><span class="sxs-lookup"><span data-stu-id="1c1df-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span></span>

    <span data-ttu-id="1c1df-159">b.</span><span class="sxs-lookup"><span data-stu-id="1c1df-159">b.</span></span> <span data-ttu-id="1c1df-160">In Hallo **id** textbox, typ een URL als:`https://app.bcinthecloud.com`</span><span class="sxs-lookup"><span data-stu-id="1c1df-160">In hello **Identifier** textbox, type a URL as: `https://app.bcinthecloud.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1c1df-161">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="1c1df-161">This value is not real.</span></span> <span data-ttu-id="1c1df-162">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="1c1df-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="1c1df-163">Neem contact op met [BC in Hallo Cloud Client ondersteuningsteam](https://www.bcinthecloud.com/supportcenter/) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="1c1df-163">Contact [BC in hello Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) tooget this value.</span></span> 
 
4. <span data-ttu-id="1c1df-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1c1df-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_certificate.png) 

5. <span data-ttu-id="1c1df-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1c1df-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1c1df-168">tooconfigure eenmalige aanmelding op **BC in Hallo Cloud** zijde, moet u toosend Hallo gedownload **Metadata XML** te[BC in Hallo Cloud ondersteuningsteam](https://www.bcinthecloud.com/supportcenter/).</span><span class="sxs-lookup"><span data-stu-id="1c1df-168">tooconfigure single sign-on on **BC in hello Cloud** side, you need toosend hello downloaded **Metadata XML** too[BC in hello Cloud support team](https://www.bcinthecloud.com/supportcenter/).</span></span>

> [!TIP]
> <span data-ttu-id="1c1df-169">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="1c1df-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1c1df-170">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="1c1df-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1c1df-171">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1c1df-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1c1df-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1c1df-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="1c1df-173">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1c1df-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1c1df-175">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1c1df-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c1df-176">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1c1df-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1c1df-178">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1c1df-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1c1df-180">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="1c1df-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1c1df-182">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1c1df-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1c1df-184">a.</span><span class="sxs-lookup"><span data-stu-id="1c1df-184">a.</span></span> <span data-ttu-id="1c1df-185">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1c1df-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1c1df-186">b.</span><span class="sxs-lookup"><span data-stu-id="1c1df-186">b.</span></span> <span data-ttu-id="1c1df-187">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1c1df-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1c1df-188">c.</span><span class="sxs-lookup"><span data-stu-id="1c1df-188">c.</span></span> <span data-ttu-id="1c1df-189">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1c1df-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1c1df-190">d.</span><span class="sxs-lookup"><span data-stu-id="1c1df-190">d.</span></span> <span data-ttu-id="1c1df-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1c1df-191">Click **Create**.</span></span>
 
### <a name="creating-a-bc-in-hello-cloud-test-user"></a><span data-ttu-id="1c1df-192">Maken van een BC in Hallo Cloud testgebruiker</span><span class="sxs-lookup"><span data-stu-id="1c1df-192">Creating a BC in hello Cloud test user</span></span>

<span data-ttu-id="1c1df-193">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in BC in Hallo Cloud maken.</span><span class="sxs-lookup"><span data-stu-id="1c1df-193">In this section, you create a user called Britta Simon in BC in hello Cloud.</span></span> <span data-ttu-id="1c1df-194">Werken met [BC in Hallo Cloud Client ondersteuningsteam](https://www.bcinthecloud.com/supportcenter/) Hallo gebruikers toevoegen in Hallo BC in Hallo Cloud-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1c1df-194">Work with [BC in hello Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to add hello users in hello BC in hello Cloud application.</span></span> <span data-ttu-id="1c1df-195">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1c1df-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1c1df-196">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c1df-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1c1df-197">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooBC in Hallo Cloud.</span><span class="sxs-lookup"><span data-stu-id="1c1df-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBC in hello Cloud.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1c1df-199">**tooassign Britta Simon tooBC in Hallo Cloud, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1c1df-199">**tooassign Britta Simon tooBC in hello Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c1df-200">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1c1df-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1c1df-202">Selecteer in de lijst met de toepassingen van Hallo **BC in Hallo Cloud**.</span><span class="sxs-lookup"><span data-stu-id="1c1df-202">In hello applications list, select **BC in hello Cloud**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_app.png) 

3. <span data-ttu-id="1c1df-204">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1c1df-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1c1df-206">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1c1df-206">Click **Add** button.</span></span> <span data-ttu-id="1c1df-207">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c1df-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1c1df-209">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="1c1df-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1c1df-210">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c1df-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1c1df-211">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c1df-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1c1df-212">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1c1df-212">Testing single sign-on</span></span>

<span data-ttu-id="1c1df-213">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="1c1df-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

 <span data-ttu-id="1c1df-214">Als u op Hallo BC in Hallo Cloud-tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour BC in Hallo Cloud-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1c1df-214">When you click hello BC in hello Cloud tile in hello Access Panel, you should get automatically signed-on tooyour BC in hello Cloud application.</span></span> <span data-ttu-id="1c1df-215">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1c1df-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1c1df-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1c1df-216">Additional resources</span></span>

* [<span data-ttu-id="1c1df-217">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c1df-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c1df-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1c1df-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_203.png

